# Fetching in react

- **1) Fetch-On-Render** : UseEffect with useFetch hook (contained data, isLoading, error states) with an Abort controller (See Ryan Florence tip: doc in progress).
  
  > **ISSUE :** it doesn't start fetching until after the component was render on screen -> Lead problem to **waterfall** loading (component wait the previous, one per one)
  
  

- **2) Fetch-Then-Render** : with Relay, React-query, Swr, Redux RTK Query : kick off Fetching early as possible (put fetch hook from parent)
  
  > **ISSUE :** it solve waterfall but all component render wait that all was fetched
  
  

- **3) Render-As-You-Fetch** : With **Concurrent/Suspense** (react 17-18.1).
  
  > **NO MORE ISSUE:** Here we dont wait to the response to come back before we start rendering. But it need to work with React 18 new render.
  
  

- **4) React Router 6.4** (doc in progress) : combine concurrent/Suspense and Remix Router



- **5)** Use **SWR** with concurrent/suspense actived (react 18). [Exemple - samselikoff](https://github.com/samselikoff/2022-01-04-suspend-after-initial-render)



- **6) React Concurrent Futur (>18.1) :** combine 3 **(Render-As-You-Fetch)** with **`react-fetch`**  : [What changes are planned for Suspense in React 18 ?](https://github.com/reactwg/react-18/discussions/47) / [The Journey of SWR and Suspense · GitHub](https://gist.github.com/shuding/6ef6a85c4c8ee57d9926e705adef88e3) / [Example with the new react-fetch/suspence](https://codesandbox.io/s/sad-banach-tcnim?file=/src/App.js:47-71)
  
  > react-fetch is experimental, in progress, not ready for prod
  
  

## 2) 'Fetch-Then-Render' with legacy mode

- Create **Fetch functions** : `fetchUser`, `FetchPosts` ... which return a fetch Promise

```js
const fetchUser = () => {
    console.log('Fetching user');
    return fetch('your-url-user-fetch')
        .then( response => response.json())
        .then( data => data)
        .catch( error => console.error(error))
}
```

- Create a **Wrap Promise** function :

```js
const wrapPromise = (promise) => { // promise is the fetch return
    let status = 'pending';
    let result;
    // it execute the promise
    let suspender = promise.then(
        response => {
            status = 'success';
            result = response;
        },
        error => {
            status = 'error';
            result = error;
        }
    );
    return {        // return an object with read function
        read() {
            switch (status) {
                case 'pending'
                    throw suspender; // it run the fetch
                break;
                case 'success'
                    throw result; // store the data
                break;
                case 'error'
                    throw result; // return the error
                break;
                default:
                    throw new Error('Forbidden call');
            }
        }
    }
}
```

- Create a **FetchData** function which call `fetchUser`, `FetchPosts` functions in a const and return them wraped in the **Wrap Promise** function :

```js
export const fetchData = () => {
    const userPromise = fetchUser();
    const postsPromise = fetchPosts();
    return {
        user: wrapPromise(userPromise),
        posts: wrapPromise(postsPromise)
    }
}
```

- Call the component in this way:

```js
const resource = fetchData();

export ProfilDetail = () => {
    const user = resource.user.read();
    return <div>
            <p> username : {user.name} </p>
            <p> usercity : {user.city} </p>
           </div>
}
```

- From the app call the component:

```js
const App = () => (
    <div>
        <React.Suspense fallback={<h4>Loading user ...</h4>}>
            <ProfilDetail />
        </React.Suspense>
    </div>
);
```

[Github project example](https://github.com/ovieokeh/suspense-data-fetching)

## 3) 'Fetch-Then-Render' with *'Suspend'*

[GitHub - pmndrs/suspend-react: 🚥 Async/await for React components](https://github.com/pmndrs/suspend-react)

```js
import { Suspense } from 'react'
import { suspend } from 'suspend-react'

function Post({ id, version }) {
  const data = suspend(async () => {
    const res = await fetch(`https://hacker-news.firebaseio.com/${version}/item/${id}.json`)
    return await res.json()    
  }, [id, version])
  return (
    <div>
      {data.title} by {data.by}
    </div>
  )
}

function App() {
  return (
    <Suspense fallback={<div>loading...</div>}>
      <Post id={1000} version="v0" />
    </Suspense>
  )
}
```

[suspend-react hackernews - CodeSandbox](https://codesandbox.io/s/yb62q)

[Revalidate Live Queries – No cache management, no manual refetches! - YouTube](https://www.youtube.com/watch?v=agS8EZgeUd8)

## 5) Coding 'Fetch-Then-Render' with *'SWR'*

[GitHub - vercel/swr: React Hooks for Data Fetching](https://github.com/vercel/swr)

- The `Coin.jsx` component :

```js
import useSWR from 'swr';
const fetcher = (...args) => fetch(...args)
    .then((response) => response.json());

export default function Coins() {
    const { data } = useSWR(
        "https://api2.binance.com/api/v3/ticker/24hr",
        fetcher,
        {suspence : true}
    );

    return (
        <div className="App">
            {data?.map( (coin) => {
                return <h1> {coin.lastprice} </h1>
            })}
        </div>
    );
}
```

- The `App.jsx` :

```js
import Coins from './Coins';
import { Suspense } from 'react';

export default function App() {
    return (
        <div className='App'>
            <h1>Coin List</h1>
            <Suspense fallback={<h1>Loading ...</h1>}>
                <Coins />
            </Suspense>
        </div>
    );
}
```

[swr/examples at main · GitHub](https://github.com/vercel/swr/tree/main/examples)

## Adding error-boundary

[Use react-error-boundary to handle errors in React](https://kentcdodds.com/blog/use-react-error-boundary-to-handle-errors-in-react)

### with 'react-error-boundary'

```js
import * as React from 'react'
import ReactDOM from 'react-dom'
import {ErrorBoundary} from 'react-error-boundary'

function ErrorFallback({error}) {
  return (
    <div role="alert">
      <p>Something went wrong:</p>
      <pre style={{color: 'red'}}>{error.message}</pre>
    </div>
  )
}

function Greeting({subject}) {
  return <div>Hello {subject.toUpperCase()}</div>
}

function Farewell({subject}) {
  return <div>Goodbye {subject.toUpperCase()}</div>
}

function App() {
  return (
    <div>
      <ErrorBoundary FallbackComponent={ErrorFallback}>
        <Greeting />
        <Farewell />
      </ErrorBoundary>
    </div>
  )
}
```

### Built-in with React error boundaries

[React doc](https://reactjs.org/docs/error-boundaries.html)

- Create a component class error :

```js
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state so the next render will show the fallback UI.
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // You can also log the error to an error reporting service
    logErrorToMyService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
  }
}
```

- then use it with :

```js
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

 [Exemple](https://codepen.io/gaearon/pen/wqvxGa?editors=0010)

## Transition API

[React Transition official Doc](https://reactjs.org/docs/hooks-reference.html#usetransition)

- Create the transition
  
  ```js
    const [isPending, startTransition] = useTransition();
  ```

- use it for exemple a fetching and setData :
  
  ```js
  return (
    <>
      <button
        disabled={isPending}
        onClick={() => {
          startTransition(() => {
            const nextUserId = getNextId(resource.userId);
            setResource(fetchProfileData(nextUserId));
          });
        }}
      >
        Next
      </button>
      {isPending ? " Loading..." : null}
      <ProfilePage resource={resource} />
    </>
  );
  ```

**[Try it on CodeSandbox](https://codesandbox.io/s/serverless-fast-isjkvt)**

[Discussion more on Transition](https://github.com/reactwg/react-18/discussions/41)

- Another exemple code :
  
  ```js
  const [isPending, startTransition] = useTransition();
  
  function handleClick() {
    startTransition(() => {
      setTab('comments');
    });
  }
  
  <Suspense fallback={<Spinner />}>
    <!-- dim the content while update is being worked on  -->
    <div style={{opacity: isPending ? 0.8 : 1 }}>
      {tab === 'photos' ? <Photos /> : <Comments />}
    </div>
  </Suspense>
  ```
