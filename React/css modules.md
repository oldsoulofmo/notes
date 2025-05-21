One external file per component. 


There will be some cases where we want to style something globally and with css modules we cannot for examples style the active class that is given to some of our links because css modules will be allocating a unique id to that active class, therefore we can use the global function.

```css
.nav :global(.active) {
    background-color: green;
}
```

It is even better to just style the active link for example in a global css file rather using the global function but here is it as a tip anyways. 





