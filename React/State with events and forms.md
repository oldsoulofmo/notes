# Handling events the react way 

Pass in the `onClick={ callback function }`, a pattern very well known in react is to use : 

```javascript
function handleStuff() {
	// Do shit 
}

function App() {
return <div onClick={handleStuff}></div>
}
```

# State 

> [!NOTE] Important
> When we update a piece of state in a component, React re-render the component in the UI. 
> 
> When a single component is rendered we call that a view, a component view.
> > All views together make a UI.
> 

State allow developers to :

- Update the component's view (by re-rendering it).
- persist local variables between renders.

> State is a tool, mastering it will unlock the power of react development.

# Creating a state with `useState`

Everything  that starts with a `use` keyword is called a react hook, hooks are declared on the top level of the component. 

> [!NOTE] Don't set state manually
> We do not set state manually, instead we set it accordingly to the setter function. 
> We use the tools react is providing for us, `setState`.

# The mechanics of state

> [!NOTE] Mechanics of react
> - We don't do direct DOM manipulations, because react is declarative.
> - In react a view is updated by re-rendering the component.
> - A component is re-rendered when it's state is updated.
> - So to update a view we update state.

> We can also set the state as an object.

# Updating state based on current state

It's always better to use a callback function to update the state based on the current state. 
