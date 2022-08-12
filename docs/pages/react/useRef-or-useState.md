# useRef or useState

- Counter App to see `useRef` does not rerender

If you create a simple counter app using useRef to store the state:

```js
import { useRef } from "react";

const App = () => {
  const count = useRef(0);

  return (
    <div>
      <h2>count: {count.current}</h2>
      <button
        onClick={() => {
            count.current = count.current + 1;
            console.log(count.current);
        }}
      >increase count
      </button>
    </div>
  );
};
```

If you click on the button,  `<h2>count: {count.current}</h2>` this value will not change because component is NOT RE-RENDERING. If you check the console `console.log(count.current)`, you will see that value is actually increasing but since the component is not rerendering, UI does not get updated.

If you set the state with `useState`, clicking on the button would rerender the component so UI would get updated.

- Prevent the unnecessary re-renderings while typing into `input`.

Rerendering is an expensive operation. In some cases you do not want to keep rerendering the app. For example, when you store the input value in state to create a controlled component. In this case for each keystroke you would rerender the app. If you use the `ref` to get a reference to the DOM element, with `useState` you would rerender the component only once:

```js
import { useState, useRef } from "react";
const App = () => {
  const [value, setValue] = useState("");
  const valueRef = useRef();

  const handleClick = () => {
    console.log(valueRef);
    setValue(valueRef.current.value);
  };
  return (
    <div>
      <h4>Input Value: {value}</h4>
      <input ref={valueRef} />
      <button onClick={handleClick}>click</button>
    </div>
  );
};
```

- Prevent the infinite loop inside `useEffect`

to create a simple flipping animation, we need to 2 state values. one is a boolean value to flip or not in an interval, another one is to clear the subscription when we leave the component:

```javascript
const [isFlipping, setIsFlipping] = useState(false);

  let flipInterval = useRef<ReturnType<typeof setInterval>>();
  useEffect(() => {
    startAnimation();
    return () => flipInterval.current && clearInterval(flipInterval.current);
  }, []);

  const startAnimation = () => {
    flipInterval.current = setInterval(() => {
      setIsFlipping((prevFlipping) => !prevFlipping);
    }, 10000);
  };
```

`setInterval` returns an id and we pass it to `clearInterval` to end the subscription when we leave the component. `flipInterval.current` is either null or this id. If we did not use `ref`here, everytime we switched from null to id or from id to null, this component would rerender and this would create an infinite loop.

- If you do not need to update UI, use `useRef` to store state variables.

Let's say in react native app, we set the sound for certain actions which have no effect on UI. For one state variable it might not be that much performance savings but If you play a game and you need to set different sound based on game status.

```javascript
const popSoundRef = useRef<Audio.Sound | null>(null);
const pop2SoundRef = useRef<Audio.Sound | null>(null);
const winSoundRef = useRef<Audio.Sound | null>(null);
const lossSoundRef = useRef<Audio.Sound | null>(null);
const drawSoundRef = useRef<Audio.Sound | null>(null);
```

If I used `useState`, I would keep rerendering every time I change a state value.
