# Context API 

> It's a system to pass data throughout the app without passing props down the tree.

- The provider gives all child components access to value.
- The value is the data that we want to make available (usually state and functions).
- The consumers are all the components that read the provided context value.

whenever the context value is updated $=>$ the component is re-rendered. 
which means that the consumers are re-rendered.

```javascript
const PostContext = createContext();

function App() {
return (
	<PostContext.Provider value = {object}>
	// bla bla
	</PostContext.Provider>
);
}
```

To consume context :

```javascript
const {post} = useContext(PostContext);
```

this way we fix prop drilling, components are more independent. 

#### advanced pattern : a custom provider and a hook 

```javascript
  const router = createBrowserRouter([
  {
    element: <AppLayout />, // this is called the route layout 
    children: [
      {
        path: "/",
        element: <Home />,
      },
      {
        path: "/menu",
        element: <Menu />,
      },
      {
        path: "/cart",
        element: <Cart />,
      },
      {
        path: "/order/new",
        element: <CreateOrder />,
      },
      {
        path: "/order/:orderId",
        element: <Order />,
      },
    ],
  },
])
```

