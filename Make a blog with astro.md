The `<slot />` allows to inject child components written between any `<Component>` and `</Component>` to any `Component.astro` file.

To keep the styling of the `About` page I had to move the style tags inside the component's body and to style the page title  `<h1>`, I had to put the `is:global` before the `define:vars`, this will ensure that every component inside the page will have those styles I defined.
