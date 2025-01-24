---
title: "Rendering Lists – React"
source: "https://react.dev/learn/rendering-lists"
author:
  - "[[@reactjs]]"
published:
created: 2025-01-24
description: "The library for web and native user interfaces"
tags:
  - "clippings"
---
What do you do when each item needs to render not one, but several DOM nodes?

The short [`<>...</>` Fragment](https://react.dev/reference/react/Fragment) syntax won’t let you pass a key, so you need to either group them into a single `<div>`, or use the slightly longer and [more explicit `<Fragment>` syntax:](https://react.dev/reference/react/Fragment#rendering-a-list-of-fragments)

```js
import { Fragment } from 'react';

// ...

const listItems = people.map(person =>
  <Fragment key={person.id}>
    <h1>{person.name}</h1>
    <p>{person.bio}</p>
  </Fragment>
);
```

Fragments disappear from the DOM, so this will produce a flat list of `<h1>`, `<p>`, `<h1>`, `<p>`, and so on.