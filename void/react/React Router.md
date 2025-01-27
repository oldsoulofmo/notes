`Building single page applications (SPA).`

With routing we match different URLS to different UI views (components), the matchings are called *routes*.  We can then navigate between different applications screen using the URL. 

It helps : 

- Keeping the UI in sync with the current URL. 
-  Allows us to build SPAs. 

> Note that here we are talking about client-side routing which is done with help of third party libraries like react-router. 

> [!NOTE] SPA
> SPA is an app entirely executed on the client, javscript (react) is used to update the DOM and the page is never reloaded. 

Cycle meaning : 

- User clicks on router link.
- URL is changed by react-router.
- DOM is updated, the component matches the URL active. 

An example that explains itself : 

```javascript
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import About from "./pages/About";
import PageNotFound from "./pages/PageNotFound";

function App() {
  return (
    <div>
      <h2>Hello world</h2>
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="About" element={<About />} />
          <Route path="*" element={<PageNotFound />} />
        </Routes>
      </BrowserRouter>
    </div>
  );
}

export default App;
```

> react-router-dom comes handy with some components (BrowserRouter, Routes, Route etc). 

### Navigation 

React router provides two important components (Link and NavLink) to help create a navigation link, they serve the same main purpose but there is an important feature that comes with NavLink which is to provide an active class to the page (URL) we're in in the meantime. (It's important to style things later on)

> The assets are to be directly imported into our javascript code.

### Nested routes 

Nested routes give us the ability to show a part of the UI based on a part of the URL.

```jsx
  <BrowserRouter>
        <Routes>
          <Route index element={<Homepage />} />
          <Route path="pricing" element={<Pricing />} />
          <Route path="product" element={<Product />} />
          <Route path="app" element={<AppLayout />}>
            <Route index element={<p>Cities</p>} />
            <Route path="cities" element={<p>cities</p>} />
            <Route path="countries" element={<p>countries</p>} />
            <Route path="form" element={<p>form</p>} />
          </Route>
          <Route path="login" element={<Login />} />
          <Route path="*" element={<PageNotFound />} />
        </Routes>
      </BrowserRouter>
```

the `index` means that the default route to be shown if not other routes are active is the one with an `index` attribute. 

To show these nested routes we use the outlet component inside the component we want to host these nested routes.

```jsx
 <Outlet />
```

### Store state in the URL 

Perfect for UI state.
Examples : 

- open/closed panels
- currently selected list item
- list sorting order
- applied list filters 

Pros: 

- Store state in a global place
- Pass data from one to the next one
- Gives the ability to bookmark and share a page with it's exact UI it had at the time of bookmarking

Example : `www.example.com/app/cities/lisbon?lat=38&lng=-9` 
Here we have param and a query string in that order.

Too straight forward details so it is better to check the worldWise project and look for these things : 

- Created a new route `<Route path="cities/:id" element={<City />} />` 
  Here the id can be anything, literally anything .. for example here we might use city rather than id. This means that we have to de-structure whatever passed after the / in path when receiving the return value from the useParam hook.
- In the CityItem component I have added a Link `<Link className={styles.cityItem} to={`/${id}`\>` 
  Here the id is de-structured from `const { cityName, emoji, date,id } = city;`  
- Finally I just had to retrieve the id in the City component to render it afterwards 
  ` const { id } = useParams();`


### Programmatic navigation with useNavigate

> Move to a new URL without having the user to click on any link.

A typical use would be after the submission of a form where we want users to be redirected to another link automatically. 




 
