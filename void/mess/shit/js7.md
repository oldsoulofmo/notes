# Working with arrays

### Simple array methods

---

> arrays are objects and they have built-in methods.

```javascript
	// slice

	let arr = ['a','b','c','d','e']
	arr.slice(2)  [2 => end]
	arr.slice(2,4)  [2 => d]
	arr.slice(-2) [d,e]
	arr.slice(1,-2) [b,c]
	arr.slice() [copy of arr]

	// splice

	arr.splice(-1) [e]
	arr will be [a => d] splice delete a part from the original array,
	we can say splice mutates the og array.
	arr.splice(1,2) start from a splice 2 chars [b,c]
	arr [a,d]

	// reverse

	arr.reverse() [e,d,c,b,a] and it mutates the og array.

	// concat

	const arr2=[f,g,h,i,j,k]
	const letters=arr.concat(arr2)	[a,b,c,d,e,f,g,h,i,j,k]

	[...arr1,...arr2] [a => k] does not mutate the both arrays

	// join

	letters.join(' - ') a - b -c -d - ... - k
```

### The new at method

---

```javascript
	const arr = [1,2,3,4,5];

	// get last array element
	arr[arr.length-1];
	arr.slice(-1)[0];
	arr.at(-1);

	// at method also works for strings
```

### forEach method (looping through arrays)

---

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
for (const x of y);

// forEach is a higher order fucntion

// for each iteration we call the callback function passed-in

numbers.forEach(function (n) {
  if (n < 5) {
    console.log(n);
  } else {
    console.log(n);
  }
});
```

> forEach cannot be broken, no break statement works in forEach loop !
> order matters in the args of forEach loop !

### forEach with maps & sets

---

3 vars for maps, 2 identiques for sets and + one ;

### Data transformation: map,filter,reduce

---

> create new arrays based on transforming data from other
> arrays.

**map** : returns a new array containing  
the results of calling a callback function on all original array els.

**filter** : returns a new array containing the array els
that passed a specified test condition.

**reduce** : reduces all array els down to one single value.

### map method

---

```javascript
const arr = [1, 2, 3, 4, 5];

const multibytwo = arr.map((x) => x * 2);

// multibytwo = [1,4,..,10]
```

> map can accept more than one method (try it asap).

```javascript
const arr = ["mohammed", "salma", "manal", "hassan", "mina"];

const fam = arr.map((name, i) => {
  return `${i} : ${name}`;
});

console.log(fam);

// ["0 : mohammed","1 : salma","2 : manal","3 : hassan","4 : mina"]
```

.split(' ') split an array from spaces.  
forEach doesn't return an array, .map() does.

### The filter method

---

we filter an array for a condition using a callback function.  
it returns an array.

```javascript
const nums = [1, 2, 3, 44, -5, -55, 5, -22];
const positive = nums.filter((n) => n > 0);
```

### The reduce method

---

it reduces the array to one single value.  
the reduced value can be anything we want, sum, max  
it's callback function accepts 4 args: {acc,cur,i,arr}.

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
nums.reduce((acc, cur, i, arr) => {
  return acc + cur;
}, 0);

// 0 is the initial value of the accumulator.
// acc: previous value.
// cur: current value.
// i  : index.
// arr: array.
```

### The magic of chaining methods

---

```javascript
const nums = [-5, -4, -3, -2, -1, 1, 2, 3, 4, 5];
const sumofopsitivenums = nums
  .filter((num) => x > 0)
  .reduce((acc, curr) => {
    return acc + curr;
  }, 0);
```

### The find method

---

It returns the first element / value that satisfies a certain condition, this condition  
can be a callback function.

```javascript
const nums = [1, 2, 3, 4, 5];
const first_value_bigger_than_one = nums.find((x) => x > 0);

// first value is 2.
```

> `e.preventDefault()` prevents the default behaviour from happening, as refreshing the
> page when clicking a submit button in a form.

### The findIndex method

---

It return the first index of the first element that satisfies a certain condition  
that might be a callback function, three args can be passed the callbackFn  
(el , i , arr).

```javascript
const nums = [1, 2, 3, 4, 5];
const index = nums.findIndex((n) => n > 2);
// it will return 1.
```

### Some & every methods

---

##### Some :

It returns a boolean based on a condition.

> check if there are anything that satisfies the passed condition.
>
> > includes method returns a boolean based on equality.

```javascript
const nums = [-4, -3, -2, -1, 1, 2, 3, 4, 5];
nums.some((n) => n > 3);
// it returns true.
```

##### Every :

It returns a boolean if all the elements satisfy the passed condition.

```javascript
const nums = [-4, -3, -2, 2, 1, 3, 4];
nums.every((n) => n > 0);
// it will return false, not all numbers are positive :> clear sh!t.
```

> we might want to define the callback function by it's own  
> so we don't repeat ourselves once we need it again.

### flat & flatMap methods

---

##### flat :

It creates a new-array with all all sub-array elements concatenated  
into it up to the specified depth.

> the default depth is 1.
>
> > `array.flat(level)` for more depth levels.
> >
> > > a common operation is to map the array then flatten it.

##### flatMap :

To combine map & flat methods we use flatMap.

```javascript
const arr = [[1, 2], 3];
arr.flatMap();
```

> flatMap goes only one level deeper !

### Sorting arrays

---

It sorts arrays in an ascending order by default, it converts elements  
to strings then compares their sequences of UTF-16 code units values.

**CompareFn**

1. return > 0 : sort b before a ( b , a )
2. return < 0 : sort a before a ( a , b )

```javascript
const arr = [4, 6, 2, 4, 32, -9, 4, -55, -10];
arr.sort((a, b) => {
  if (a > b) return 1; // [b,a]
  if (a < b) return -1; // [a.b]
});
// Improving this code mathematically
arr.sort((a, b) => a - b);
// if a > b => a - b > 0 => [b,a]
// if a < b => a - b < 0 => [a,b]
```

### More ways of creating and filling arrays

---

> This part is for creating and filling arrays more programatically.

#### new Array

```javascript
// creating an empty array with a length of 10.
const arr = new Array(10);
// arr = [empty * 10].
// we can only call one method on it, the fill method.
arr.fill(v, s, e);
// v = value , s = startingIndex , e = endingIndex.
```

#### Array.from

```javascript
// create an array that contains numbers from 1 to 7.
const nums = Array.from({ length: 7 }, (cur, i) => i + 1);
// nums = [1,2,3,4,5,6,7]
```

> NodeList objects are collections of nodes, usually returned  
> by properties such as Node.childNodes and methods  
> such as document.querySelectorAll().
>
> > Although NodeList is not an Array, it is possible to iterate  
> > over it with forEach(). It can also be converted to  
> > a real Array using Array.from().

```javascript
// Create an array based on a property of DOM Elements
const images = document.querySelectorAll("img");
const sources = Array.from(images, (image) => image.src);
```

We can actually create arrays from different iterabls such as :

1.  maps
2.  sets
3.  strings
4.  node-list
