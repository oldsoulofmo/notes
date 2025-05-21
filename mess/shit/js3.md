## Working with strings [1]

### methods

string.length - string.indexOf - string.lastIndexOf - string.slice

`string.slice(i,j)` slice from i to j-1, {i,j-1} are included but {j} is not included !

All string methods return primitives even if called on string objects.

### Working with strings [2]

### methods

string.toLowerCase() - string.toUpperCase() - string.trim() - string.replace()

`string.trim()` trim the string if it has any spaces !

`string.replace(/word/g,'by what to change')` /word/g means targetting every occurence of word and change it 'by what to change'

**methods that return booleans:**

string.includes() - string.startsWith() - string.endsWith()

### Working with strings [3]

### methods

.split() - .join() => split a string from a desired place, join it from a desired place.

.padStart() - .padEnd() => create some padding in a string with the {length,character} desired.

.repeat(n) => repeat a string n times.
