# CSS bases

#### CSS Selector

📑 Le lien vers la doc [Sélecteurs CSS - Apprendre le développement web | MDN](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Selectors)

#### FlexBox

📑 Le lien vers la doc [A Complete Guide to Flexbox | CSS-Tricks - CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

#### Grid

📑 Le lien vers la doc [A Complete Guide to Grid | CSS-Tricks - CSS-Tricks](https://css-tricks.com/snippets/css/complete-guide-grid/)

# CSS Fondamentals

#### CSS Calc function

```css
div {
    width: calc(100% + 50px);
}
div {
    width: calc(100% * 2);
}
```

---

#### CSS Units

###### px (absolute)

*Pretty self explanatory absolute lenght in pixel*

> **Avoid using `pixel` for font-sizes. Use mostly for small details like border and shadow.**
> 
> - Fixed in size
> 
> - Not responsive
> 
> - Overrides user's browser preference

---

###### % (relative)

*Relative to the value of parent element. 100% is the width of the parent element*

> **I recommend using percentages for layouts and width/height. For example, laying out links on navbar, placing images inside a div ...**
> 
> - Size is defined as percentage of another value (mostly parent element)
> 
> - Sometimes size is defined as percentage of the element itself

---

###### em (relative)

*Relative to the font-size of the parent element.*

> **You can use `em` for font-size and margin/padding. Use `em` when you want to adjust margin/padding based on that element's font-size** *(if you font-sized is big, you maybe want bigger spacing)*
> 
> - Changes behavior based on property
> 
> - 1 em = parent font-size
> 
> - if parent doesn't have a size, defaults to 16 px (body)

---

###### rem (relative)

*Relative to the font-size of the root element*

> **You can also use `rem` for font-size and margin/padding.** *`rem`is easier to work than `em` because its more consistent.*
> 
> - Relative to the root HTML, no matter what (default is 16px)
> 
> - You can change the root HTML size. For exemple if you change it to 20px,
>   1 rem will always 20 px.

---

###### vw / vh (relative)

*Equal to 1% of the height of the browser window size*

> ****vh/vh are relative to the width/height of the browser window. 100vw means full width of the screen. Use vw/vh for bigger layouts, like background.**
> 
> - Useful for responsive website because everything scales.

###### dvh / lvh / svh (relative)

*For mobile screen height*

<img title="" src="mobile.jpeg" alt="mobile.jpeg" width="435">

---

#### CSS Variables

> for unit variable (size, width...)

```css
:root {
    --unit: 16px;
}

header {
    padding: var(--unit);
}

h1 {
    margin-bottom: var(--unit);
}
```

> for color variable

```css
:root {
    --primary-color: #333;
}

div {
    background-color: var(--primary-color);
}

.test {
    color: var(--primarycolor);
}
```
