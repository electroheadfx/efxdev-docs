# The fundamentals in CSS

## CSS Calculation

```css title="CSS Calc function"
div {

width: calc(100% + 50px);

}

div {

width: calc(100% * 2);

}
```

## CSS Variables

### for unit variable (size, width...)

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

### for color variable

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