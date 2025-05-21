Grep is a command to search for patterns in files or text in general.

```bash
grep "fuck" book.txt
```

Grep is case-sensitive, to make it case-insensitive : 

```bash
grep -i "Fuck" book.txt
```

#### Word search 

To search for words instead of fragments inside words. 

```bash
grep -w "fuck" book.txt
```

#### Recursive search 

Searching recursively means to perform a search for a pattern in the whole directory going deeply inside it if it has to ! 

```bash
inside the current directory
grep -ri "fuck"

inside documents directory
grep -ri "fuck" documents/
```

If we want to perform a search and we are not sure about the spelling, we can search for spellings at once ! 

```bash
grep -ri "f[ua]ck"
```

This will perform : 

```bash 
grep -ri "fuck"

and also 

grep -ri "fack"
```

#### Grep options 

```bash
To check how many a word occured as a pattern 
grep "I" fuck.txt -cw (as a word) 
grep "I" fuck.txt -c  

To add lines before of after the pattern 
grep "shit" fuck.txt -B1
grep "shit" fuck.txt -A1

To add lines before and after the matched pattern at once 
grep "shit" fuck.txt -C1 (this will add 1 line before and after the match).

To get the line number 
grep "shit" fuck.txt -nC1 (will give line numbers).

To specify the number of matches to show 
grep "shit" fuck.txt -m2 (show the first two macthes).
```


#### Grep and regular expressions 

#### Grep extended regex 

#### Piping to grep 


