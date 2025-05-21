First thing to have in mind is that passing props down the component tree can be a hassle and will surely at some point cause _props drilling_ which can be solved with component composition but some complex scenarios are better dealt with using the context API. 

> [!NOTE] What is the context API ?
> It's a system to pass data throughout the app without passing props down the tree.

> Allows us to broadcast global state to the entire app.

- The provider gives all child components access to value.
	 Better place at the top, in the _App_ for example.
- The value is the data that we want to make available (usually state and functions).
- The consumers are all the components that read the provided context value.

> Whenever the value is updated, all the consumers are re-rendered.

```jsx
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

This way we fix prop drilling and components are more independent. 
# Advanced pattern : a custom provider and hook

```jsx
import { Children, createContext, useState } from "react";
import { faker } from "@faker-js/faker";

function createRandomPost() {
  return {
    title: `${faker.hacker.adjective()} ${faker.hacker.noun()}`,
    body: faker.hacker.phrase(),
  };
}

// 1- create a new context
const PostContext = createContext();

function PostProvider({children}) {
  const [posts, setPosts] = useState(() =>
    Array.from({ length: 30 }, () => createRandomPost())
  );
  const [searchQuery, setSearchQuery] = useState("");
  const [isFakeDark, setIsFakeDark] = useState(false);

  // Derived state. These are the posts that will actually be displayed
  const searchedPosts =
    searchQuery.length > 0
      ? posts.filter((post) =>
          `${post.title} ${post.body}`
            .toLowerCase()
            .includes(searchQuery.toLowerCase())
        )
      : posts;

  function handleAddPost(post) {
    setPosts((posts) => [post, ...posts]);
  }

  function handleClearPosts() {
    setPosts([]);
  }

  return (
    <PostContext.Provider
      value={{
        posts: searchedPosts,
        onAddPost: handleAddPost,
        onClearPosts: handleClearPosts,
        // what would be cleaner is to create post context for it's own and query context for it's own
        searchQuery,
        setSearchQuery,
      }}>{children}</PostContext.Provider>
  );
}

export { PostProvider, PostContext };
```

What I did here by steps : 
- Create a new context.
- Create a custom context provider `PostProvider` which contains the whole state logic and state updating logic.
- Provide value to child components by accepting them as props on the context provider then wrapping these children by the `PostProvider` component. 
	```jsx
	 <PostProvider>
        <Header />
        <Main />
        <Archive />
        <Footer />
	 </PostProvider>
```

Now let's see why I need a custom hook. 

> Whenever I want to consume a custom hook I must use the `useContext` hook and pass in an object which is the return value of the context itself. 

Instead of using the `useContext(PostContext)` where I might not always which context I must consume then I can just wrap each call to consume the desired context inside a custom hook : 

```jsx

function usePosts() {
  const context = useContext(PostContext);
  if (context === undefined)
    throw new Error("PostContext was used outside of the PostProvider");
  return context;
}

export { PostProvider, usePosts };
```

# Advanced state management 

Include the slides here later on.

> In the worldWise project, we are doing things like we would do in real web applications. (Check how are fetching data in the `city` component) 


# advanced pattern : a custom provider and a hook 

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


