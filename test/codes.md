---
sort: 3
---

# Code Blocks

`Some inline code ^^ 500000`

[`inline code inside link`](./)

```
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```

**Highlight:**

```scss
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```




```js
function HighlightSomeText(highlight) {
  if (highlight) {
    // highlight-next-line
    return 'This text is highlighted!';
  }

  return 'Nothing highlighted';
}

function HighlightMoreText(highlight) {
  // highlight-start
  if (highlight) {
    return 'This range is highlighted!';
  }
  // highlight-end

  // code-block-error-line
  return 'Nothing highlighted';
}
```

```jsx {1,4-6,11} showLineNumbers
import React from 'react';

function MyComponent(props) {
  if (props.isBar) {
    return <div>Bar</div>;
  }

  return <div>Foo</div>;
}

export default MyComponent;
```

```jsx live
function Clock(props) {
  const [date, setDate] = useState(new Date());
  useEffect(() => {
    const timerID = setInterval(() => tick(), 1000);

    return function cleanup() {
      clearInterval(timerID);
    };
  });

  function tick() {
    setDate(new Date());
  }

  return (
    <div>
      <h2>It is {date.toLocaleTimeString()}.</h2>
    </div>
  );
}
```