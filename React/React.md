Important notes : 
- [[State with events and forms]]
- [[Rendering lists]]
- [[General information]]
- [[Advanced state management - The context API]]
- [[React Router]]
- [[css modules]]

# State

```jsx
import { useEffect, useState } from "react"

export default function App() {
  const [advice, setAdvice] = useState("Hello world !")
  const [count, setCount] = useState(0)

  async function getAdvice() {
    const res = await fetch("https://api.adviceslip.com/advice")
    const data = await res.json()
    
    setAdvice(data.slip.advice)
    setCount((c) => c + 1)
  }

  useEffect(function () {
    getAdvice()
  }, [])

  return (
    <div>
      <h1>{advice}</h1>

      <button onClick={getAdvice}>Get advice </button>

      <Message count={count} />
    </div>
  )
}

function Message(props) {
  return (
    <p>
      you have read <em>{props.count}</em> pieces of advice.
    </p>
  )
}

```

As a first look, `React` keeps the data in sync with UI with something called state.

> [!NOTE] React
> React is an extremely popular library which is : 
> - **component based**.
> - **declarative** 

# Working with components, props and JSX

Each component can only return one element.

```javascript
function App() {
  return (
    <div>
      <h1>Hello world !</h1>
      <Pizza />
      <Pizza />
      <Pizza />
    </div>
  )
}

function Pizza() {
  return (
    <div>
      <img src="pizzas/spinaci.jpg" alt="pizza spinaci" />
      <h2>Pizza</h2>
      <p>Tomato, mozarella, spinach, and ricotta cheese</p>
    </div>
  )
}

// React version 18

const root = ReactDOM.createRoot(document.getElementById("root"))

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)

```


> [!NOTE] JSX
> - Declarative syntax to describe what components look like and how they work based on their logic and data.
> - Components must return a block of JSX.
> - Extension of javascript that allows us to combine javascript, css and react components into html.
> - Each JSX element is converted to a `React.createElement` function call with the help of Babel which is provided when creating a react app with CRA.
> - We could use React without JSX.

# Imperative vs declarative 

**Imperative :** How to do things, we tell the browser how to do things step by step until we get to the desired UI.  Manuel DOM element selections and DOM traversing, also step by step DOM mutations until we reach the desired UI.

**Declarative :** Describe what UI should look like using JSX, based on current state, data, props and more. No `querySelectors` or `addEventlisteners`. It gets what we want to see in the screen, we think of the UI as a reflection to data.


> [!IMPORTANT] Strict mode
> In strict mode components are rendered twice.


> [!NOTE] Important 
> React does separation concerns, one component per file. Not one technology per file.

# Props 

 Props stands for property, it's a mechanism to link between parent-child components.

> [!NOTE] Important
> State is internal data that can be updated by the component logic, while props is data coming from the outside and can only be updated by the parent component.
> - Props are read-only, they are immutable ! (One of React's strict rules)
> - If you need to mutate props then you actually need state.
> 
> Props are immutable because they're an object and changing them will affect the parent component too.
> 
> Changing an object outside a function causes side-effects (not pure), in React components must be pure in terms of props and state because : 
> - It allows React to optimize apps.
> - Avoid bugs.
> - Make apps predictable.
> 
> In general, we should never write a component that mutate data outside it's function scope.



> [!NOTE] Rules of JSX
> - Statements are not allowed (if / else, switch statements etc).
> - JSX produces a javascript expression : 
  > > - We can place other pieces of JSX inside `{}`.
  >- We can write JSX anywhere inside a component (inside if / else, assign to variables, pass it to functions).
> - A piece of JSX can only have one root element, if we need more then use `<React.Fragment>` or short for `<>`.




# Conditional rendering with &&

 React does not render `true` or `false`. 

 This makes it clear to when rendering with `&&` then i should base the condition on a `false` or `true` value not a number of `0` etc.


```javascript
//conditional rendering with ternaries
expression ? value1 : value2 ; 
```

# De-structuring props

```javascript
// Setting classes and text conditionally 
<li className={`pizza ${pizzaObj.soldOut ? "sold-out" : ""}`}>
```

# More thoughts about state and state guidelines 

For data that should not trigger component re-renders, don't use state. Use a regular variable instead. This is a common beginner mistake.

# Forms and handling forms


>[!REMINDER] CHECK
> Check TRAVEL-LIST project's code.

# Controlled elements 

Make REACT take control of the form's elements state by attaching event handlers to these elements.

# State vs Props 


> [!NOTE] Important
> Receiving new PROPS causes component to re-render, usually when the parent's state is updated.
>  > Props are used by parent to configure child components ("settings").
>  > Props are external data while State is internal data.
>  > Props are read-only.
>  > State can be updated by component itself.
>  


# Thinking in react 
# Fundamentalists of state management 

> [!NOTE] State management 
> Deciding when to create pieces of state, what types of state are necessary, where to place each piece of state and how data flows through the app.
> 

# Types of state

> [!NOTE] Local state
> State needed only by one or few components.
> 
> State that is defined in a component and only that component and child components have access to it by passing via props.
> 
> We should always start with local state.


> [!NOTE] Global state
> State that many components might need.
> 
> Shared state that is accessible to every component in the app.
> 
> To manage global state we might use context API or REDUX.

# Thinking about state and lifting up state

React is about immutability, we can't mutate an array by using the `push` method.

What I have done in the travel-list project is to lift up state because many other siblings needed that piece of state, therefore I lifted up state to the very first common parent component which is the `App` component.

# More child to parent communication

```javascript
<button onClick={() => onDelete(item.id)}>&times;</button>
```

Here we don't need to pass in the event to the function, instead we need to pass in the `item.id` therefore we have to use another function to call the `onDelete` while passing `item.id` as it's parameter, using only `onDelete` will return an even object which we have to deal with if we want to respond to that event specifically. 

```javascript
export default function App() {
  const [items, setItems] = useState([])

  function addItems(item) {
    setItems((items) => [...items, item])
  }

  function handleDeleteItems(id) {
    setItems((items) => items.filter((item) => item.id !== id))
  }

  return (
    <>
      <Header />;
      <Form onAddItems={addItems} />
      <PackingList items={items} onDelete={handleDeleteItems} key={items.id} />
    </>
  )
}

function PackingList({ items, onDelete }) {
  return (
    <div className="list">
      <ul>
        {items.map((item) => (
          <Item item={item} onDelete={onDelete} key={item.key} />
        ))}
      </ul>
    </div>
  )
}

function Item({ item, onDelete }) {
  return (
    <li>
      <span style={item.packed ? { textDecoration: "line-through" } : {}}>
        {item.quantity} {item.description}
      </span>

      <button onClick={() => onDelete(item.id)}>&times;</button>
    </li>
  )
}

```

In this code, `handleDeleteItems` is passed to `<PackingList />` then passed again to 
`<Item />` because `<Item />` is in `<PackingList />` and that is the only way to go through it.

# Derived state 


> [!NOTE] Derived state
> State that is computed from an existing piece of state or from props.

Creating a number $n$ of states that are linked together is very bad because : 

- They depend on each other.
- Need to keep them in sync (updated all together).
- $n$ state updates will re-render the component $n$ times.

Therefore derived state comes into place, just regular variables and no more `useState`. 

- The most general state is the only one that should exist as a single source of truth for other related data.
- Works fine because re-rendering the component once will lead to recalculations automatically.

> For more derived state code, check my-travel-list project !

# Sorting items

Also using controlled elements, which is like this : 

```javascript
function PackingList({ items, onDelete, onToggle }) {
  const [sortBy, setSortBy] = useState("input")

  let sortedItems

  if (sortBy === "input") sortedItems = items

  if (sortBy === "description")
    sortedItems = items
    .slice()
    .sort((a, b) => a.description.localeCompare(b.description))

  if (sortBy === "packed")
    sortedItems = items
      .slice()
      .sort((a, b) => Number(a.packed) - Number(b.packed))

  return (
    <div className="list">
      <ul>
        {sortedItems.map((item) => (
          <Item
            item={item}
            onDelete={onDelete}
            onToggle={onToggle}
            key={item.id}
          />
        ))}
      </ul>

      <div className="actions">
        <select value={sortBy} onChange={(e) => setSortBy(e.target.value)}>
          <option value="input">Sort by input order</option>

          <option value="description">Sort by description</option>

          <option value="packed">Sort by packed status</option>
        </select>
      </div>
    </div>
  )
}
```



# Thinking in React : Components, Composition and Reusability

## How to split a UI into components 

### Component size matters 
Check hand taken notes.

### The criteria of splitting a UI 
- Logical separation of content/UI.
- Reusability.
- Responsibilities/Complexity. 
- Personal coding style.
  
  ### Components categories 
  ##### Stateless components/Presentational
  - No state.
  - Can receive props and simply present received data or other content.
  - Usually small and reusable.

##### Stateful components 
- Have state.
- Can still be reusable.

##### Structural components 
- Pages, layouts or screens of the app.
- Result of composition.
- Can be huge and non-reusable (but don't have to).

### Prop drilling 

Passing the state down the tree, it gets bad when we have a lot of child components .. we can go on forever to pass that state down the tree until it's final destination. 

### Component composition 



## Effects and data fetching 

### useEffect 

Running a side effect on mount, when the initial render is triggered. 

```javascript
useEffect(function () {
fetch(`http://www.omdbapi.com/?apikey=${KEY}&s=interstellar`)
.then((res) => res.json())
.then((data) => setMovies(data.Search));
}, []);
```

The second argument is designated for a dependency list, for now we are using an empty array that indicates that we are running this side effect on mount. 

The function body, registering a side effect. Meaning it will only run after the component is painted onto the screen. 

> [!NOTE] Side effect
> It's an interaction that happens between the component and the world outside the component. A side is a code that does something, like data fetching, setting up subscriptions, setting up timers, manually accessing the DOM ... 
> 

useEffect allow us to write code that will run at different moments, mount, re-render or un-mount. 

> We need side effects all the time, they make our applications do something. Not in render logic. 

### React 18 strict mode 

Effects will be called twice, therefore we will have two outputs if we log something out.
This only happens in development and not production. 

> Setting state is asynchronous. 

```javascript
useEffect(function () {
  console.log("After initial render")
}, [])

useEffect(function () {
  console.log("After every render")
})

useEffect(
  function () {
    console.log("After the state of query changes.")
  },
  [query]
)

console.log("during render")

```


### useEffect Clean up function 

- Function that we can return from an effect (optional).
- Runs on two different occasions : 
	 - Before the effected is executed again.
	 - After a component has unmounted. 

Component renders : Execute effect if dependency array includes updated data.
Component unmounts : Execute cleanup function.

### When do we need a cleanup function ? 

Whenever a side effect keeps happening after the component re-renders or unmounts.  For example, if we trigger the component to re-render while the first time there was an http request sent, the second time also another http request will be sent therefore we will have a race condition bug. Therefore we should cleanup the http request .. 
other cases are like API subscription, cancel it (Potential cleanup).
Start timer, stop timer (Pot. cleanup).
Add evenList., stop evenList. (Pot. cleanup).

> Each effect should do only one thing, Use one effect hook for one side effect. It makes cleanup easier. 


> [!NOTE] Closure
> After cleaning up, the function will close up on any variable that was set before destroying the state. Meaning, because of closure we can know the value of that variable even after cleaning up.

### A recipe to clean up requests after a re-render. 

```javascript
useEffect(
  function () {
    const controller = new AbortController()
    
    async function fetchMovies() {
      try {
        setIsLoading(true)
        setError("")

        const res = await fetch(
          `http://www.omdbapi.com/?apikey=${KEY}&s=${query}`,
          { signal: controller.signal }
        )

        if (!res.ok) throw new Error("Something went wrong !")

        const data = await res.json()
        
        if (data.Response === "False") throw new Error("Movie not found")

        setMovies(data.Search)
        setError("")
      } catch (err) {
        console.error(err.message)
        if (err.message !== "AbortError") setError(err.message)
      } finally {
        setIsLoading(false)
      }
    }

    if (query.length < 3) {
      setMovies([])
      setError("")
      return
    }
    fetchMovies()
    return function () {
      controller.abort()
    }
  },
  [query]
)
```

### useReducer hook 

A complex way of managing state, it works with a pure function called the reducer function. 

The `useReducer` hook takes the reducer function and also the initial state. 

The reducer function takes state and action, the action we pass it into the dispatch function, the dispatch is one of the things useReducer returns, then we dispatch actions like the following one : 

```javascript
  const inc = function () {
    dispatch({type : "inc"});
  };
```

The convention is to dispatch actions with a type and optionally a payload with the goal to pass in som value into the reducer. 

```javascript
function reducer(state, action) {
  console.log(state, action);
  if (action.type === "inc") return state + 1;
  if(action.type === "dec") return state - 1;
  if(action.type === "setCount") return action.payload;
}
```

The reducer takes all the information that is contained in the action in order to compute the next state.

#### Managing related pieces of state 


#### Managing state with useReducer 

`useState` is not enough sometimes : 
- when components have a lot of state variables and states updates, spread across many event handlers all over the component. 
- when multiple state updates need to happen  at the same time (as a reaction to the same event, like starting a game).
- when updating one piece of state depends on one or multiple other pieces.

> Ideal for complex state and related pieces of state. 


- stores related pieces of state in a state object.
- needs a reducer function that contains all the logic to update state, decouples state logic from component.
- the reducer is a pure function with no side effects, it takes current state and action then returns the next state.
- action is an object that describes how to update state.
- dispatch is a function to trigger state updates by sending actions from event handlers to the reducer. 


> [!NOTE] Important
> React reducers accumulates all actions into one single state over time.

> one file per component, more real world.


#### useState vs useReducer 

`useState` : 
- Ideal for single, independent pieces of state (nums, strings, single arrays, etc.)
- Logic to update state is placed directly in event handlers or effect, spread all over one or multiple components.
- Imperative state updates.

`useReducer` : 
- Ideal for multiple related pieces of state and complex state (object with many values and nested objects or arrays)
- Logic to update state lives in one central place, decoupled from components : _the reducer_.
- State is updated by dispatching an action to a reducer.
- Declarative state updates  : complex state transitions are mapped to actions 
```javascript 
  dispatch({type: 'startGame' });
```


