Important notes : 

- [[Rendering Lists – React]].
- [[Rendering Lists – React 1]].
- [[Rendering Lists – React 2]].

```jsx
<ul className="pizzas">

{pizzaData.map((pizza) => (
	<Pizza pizzaObj={pizza} key={pizza.name}
	// name={pizza.name}
	// photoName={pizza.photoName}
	// ingredients={pizza.ingredients}
	// price={pizza.price}
	/>
))}

</ul>
```

> JSX elements directly inside a `map()` call always need keys. 

> Keys tell React which array item each component corresponds to so that it can match them up later. 
 
> This is important if the array items start moving due to sorting or deletion for example, a well chosen key helps React infer what exactly has happened and make the correct updates to the DOM tree. 
 
> Keys should be included in the data.

