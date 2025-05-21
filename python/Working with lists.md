> Check [[List]].

Making a list using `range`  function : 

```python
numbers = list(range(1,6))
```

Using a step : 

```python
numbers = list(range(0,10,2))
```

> `min, max, sum` functions do exist in python.

```python
# 2^2 : 2 ** 2 in python
x = 2 ** 2 
```

## List comprehensions 

```python
list = [value**2 for value in range(1,10)]
```

List comprehensions allow to combine an expression `value ** 2` and a loop `for value in range(1,10)` into one line. 

- slice : `list[0:3]`.
- start of the list : `list[:3]`.
- end of the list : `list[3:]`.

Slicing the last three values :

```python
list = [1,2,3,4,5,6,7,8,9,10]

for i in list:
    print(i)

print(list[-3:])

```

> A third value in the brackets can be added to tell how many items to skip between items in the specified range.

We can also loop through a slice : 

```python
numbers = list(range(1,11))

for n in numbers[:5] :
	print(n)
```

## Copying a list 

A way to copy a list is to make a slice from the beginning to the end of it. 

```python 
x = [1,2,3]
y = x[:]
```

Here I have created a new list, so we have two different lists.


