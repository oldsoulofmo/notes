They are a key-value pairs. 

```python
dict = {'name': 'mohammed', 'age': 24}
```

To delete permanently :

```python 
del dict['name']
```

Looping through keys is the default behavior when looping through a dictionary. 

To loop in a desired order we might do : 

```python
for name in sorted(names.keys()) : 
	print(name)
```

Looping through all values : 

```python 
for lang in langs.values() : 
	print(lang)
```


> [!NOTE] Nesting
> Just like in JavaScript, nesting a list in a dictionary or a dictionary in a list or dictionary in a dictionary is very doable and possible. 

```python
alien_0 = {'color': 'green', 'points': 5}
alien_1 = {'color': 'yellow', 'points': 10}
alien_2 = {'color': 'red', 'points': 15}

aliens = [alien_0, alien_1, alien_2]
```

```python
dict = {'name': 'hola', 'age': '22', 'list': ['s', 'ss'], 'dddd': {
'a': '0',
'b': '1'
}}

listo = [{
'name' : 'mo'
}]
```

