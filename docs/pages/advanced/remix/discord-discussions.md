# Discord Discussions

## Remix Catch boundary

```tsx
import type { LoaderFunction } from 'remix'

export const loader: LoaderFunction = function () {
  throw new Response(null, { status: 404 })
}

export function CatchBoundary() {
  return <h1>404 Not Found</h1>
}

export default function () {}
```

## Preload Images with remix

- so what I do is in Remix I import those hero images in different sizes, all are webp images compressed, then I set them as CSS variables using inline styles, and image-set let the browser pick what image to use based on the device pixel density 

```css
#hero {
  background-image: var(--hero-image-4x);
  background-image: image-set(
    var(--hero-image-1x) 1x,
    var(--hero-image-2x) 2x,
    var(--hero-image-3x) 3x,
    var(--hero-image-4x) 4x
  );
  background-image: -webkit-image-set(
    var(--hero-image-1x) 1x,
    var(--hero-image-2x) 2x,
    var(--hero-image-3x) 3x,
    var(--hero-image-4x) 4x
  );
}
```

- and I have a LinksFunction,. rendering a preload link which will also preload the image

```tsx
{
  rel: "preload",
  as: "image",
  href: heroBg4x,
  imagesrcset: `${heroBg} 1x, ${heroBg2x} 2x, ${heroBg3x} 3x, ${heroBg4x} 4x`,
}
```

- this is the preload for the hero image using imagesrcset the browser will also use that srcset to choose the correct image which will match the image the CSS will ask for.

> Sure, the image-set is fine. But you run into the issue that the browser needs to parse your CSS first to get the image.

- **the preload tag solves that image is preloaded before the CSS is even loaded**

> the JS object? it's from a LinksFunction ?

- something like that, but with more links :

```tsx
// it preload heroBg4x image from header

export let links: LinksFunction = () => {
  return [
    {
      rel: "preload",
      as: "image",
      href: heroBg4x,
      imagesrcset: `${heroBg} 1x, ${heroBg2x} 2x, ${heroBg3x} 3x, ${heroBg4x} 4x`,
    }
  ]
}
```

[Don't fight the browser preload scanner](https://web.dev/preload-scanner/)



- I have been testing this a lot for like a week to make that page load fast and don't have issues with the image not loading immediately

> Preload only works if you know *exactly* which of the images you need to preload, which in the case of a srcset or image set, defeats the purpose

- preload has a imagesrcset to let you preload based on an srcset. 
  
  the browser only preload the same image from the srcset the CSS or img tag is gonna use later
  
  

[Preloading responsive images](https://web.dev/preload-responsive-images/)



>  ok, so you use the link preloader, then the CSS uses whichever one fits. That all seems to work out well in my head

- yeah, so the image is preloaded while CSS is also being downloaded, once CSS loads and is parsed it will chose and image which will be the same image the browser preloaded before if internet is slow it can still happen that the hero takes a while to show up but at least it doesn't need to wait for CSS to start loading.

- most of the work is exporting each variant of the image and ensuring its compressed what would be cool is to have a resource route where I could render `<Image src="/path/to/the/file" />` and get the picture tag with multiple sources asking for different pixel densities

```html
<picture>
  <source
    srcSet={`${mockupDesktop} 1x, ${mockupDesktop2x} 2x, ${mockupDesktop3x} 3x, ${mockupDesktop4x} 4x`}
    media="(min-width: 768px)"
  />
  <source
    srcSet={`${mockupMobile} 1x, ${mockupMobile2x} 2x, ${mockupMobile3x} 3x, ${mockupMobile4x} 4x`}
    media="(max-width: 767px)"
  />
  <img
    src={mockupDesktop4x}
    srcSet={`${mockupDesktop} 1x, ${mockupDesktop2x} 2x, ${mockupDesktop3x} 3x, ${mockupDesktop4x} 4x`}
    height={589.82}
    width={298.38}
    alt=""
    className="max-w-48 md:max-w-72"
    decoding="async"
  />
</picture>
```

> for more dynamic Image, yes you need some service to optimize the images

- you need the image component to send the URL to an API the optimization needs to happen at runtime but the response needs to have a cache-control header and the API needs to be behind a CDN so you only really do it once per image

- Cloudflare has an image optimization service that works this way [Cloudflare Image Optimization · Cloudflare Image Optimization docs](https://developers.cloudflare.com/images "https://developers.cloudflare.com/images")
  
  Next.js Image component does that too, you could use Cloudinary for that too but this one becomes expensive and they charge the bandwidth too


