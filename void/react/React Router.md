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




