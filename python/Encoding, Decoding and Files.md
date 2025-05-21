Encoding is converting the string type to byte type, decoding is the opposite. 

> Always remember to close the file after reading it and writing to it. 

```python
file = open ('path','w',encoding='utf-8)
file.write('hello\n')
file.close()
```

The second parameter `w` means that I am overwriting the original file, to add at the end of the file then I must use `a` mode. 

There are many methods to use like : 

- `file.readlines()`
- `data.split()`
- `data.join(otherData)`




