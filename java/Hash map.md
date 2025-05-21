[[Hash Map - Java Programming]]

```java
HashMap<String,String> postalCodes = new HashMap<>();  
postalCodes.put("01","azemmour");  
postalCodes.put("02","el jadida");  
  
System.out.println(postalCodes.get("01"));
```

If the hash map does not contain the key desired to search for, the `get` method will return a `null` reference. 

In the hash map, if there was already a key associated to value, using the same key to for a new value will cause the first value to vanish. 

## A reference type variable as a Hash Map value

```java
Book book1 = new Book("Notes from underground",1920,"...");  
Bshook book2 = new Book("The stranger",1940,"...");  
  
HashMap<String,Book> directory = new HashMap<>();  
  
directory.put(book1.getName(),book1);  
directory.put(book2.getName(),book2);  
  
Book book = directory.get("Notes from underground");  
Book anotherBook = directory.get("The adolescent");  
  
System.out.println(book);  
System.out.println(anotherBook); // null
```

> The hash map is implemented in a way that searching by a key is very fast.

## When should Hash Maps be used ?

The hash map generates a hash value from the key. 

>A hash value is a piece of code used to store the value of a specific location.

When a key is used to retrieve information from a hash map, the hash code identifies the location where the value associated with the key is stored. In practice, It's not necessary to go through all the key-value pairs in the hash map when searching for a key, check [[Hash tables]] where I will look deeper into the implementation using Data structures.

If we take performance into consideration them we should look into the worst case scenarios in using a list first. In a list, order is important as it marks the order of which item was added to the list. For example, searching for books in a list can be tricky because the way the list is ordered has an effect, if the book that we're looking for was first on the list then the program would be faster. But, if the book was not on the list then the program would have to go through all the books in the list before It determines that such book does not exist and that is bad for performance when the number of books is millions for example. On the other hand we can use hash maps in this scenario because in a hash map it is not necessary to check all the books, the key determines the location of a given book in a hash map.

This does not mean I must always use hash maps, they work well when we know what we are looking for but if I wanted to identify books whose title contains a particular string then the hash map would be useless. 

> The hash maps have no internal order, I cannot search based on indexes and order.


> [!NOTE] Important
> Typically hash maps and lists are used together, the hash map provides a quick access to a specific key or multiple keys, while the list is used to maintain order.

`System.nanoTime()` for checking how much time the program took to execute, back for this when it matters !

## Hash Map as an instance variable 

- trim.
- toLowerCase.

Code explains itself.

```java
public void addBook(Book book) {  
    String name = sanitizedString(book.getName());  
  
    if (this.directory.containsKey(name)) {  
        System.out.println("Book already exists !");  
    } else {  
        this.directory.put(name, book);  
    }  
}  
  
public Book getBook(String bookTitle) {  
    bookTitle = sanitizedString(bookTitle);  
    return this.directory.get(bookTitle);  
}  
  
public void removeBook(String bookTitle) {  
    bookTitle = sanitizedString(bookTitle);  
  
    if (this.directory.containsKey(bookTitle)) {  
        this.directory.remove(bookTitle);  
    } else {  
        System.out.println("Book not found");  
    }  
}  
  
public static String sanitizedString(String string) {  
    if (string == null) return "";  
    string = string.toLowerCase();  
    return string.trim();  
}
```


## Going through a Hash Map's keys

The get method in the hash map searches by key, using it for searching for a book by a part of it's title is not possible. 

To accomplish this we can go through the values of a hash map by using a for-each loop on the set returned by the `KeySet()` of the hash map.

```java
public ArrayList<Book> getBookByPart(String titlePart) {  
    titlePart = sanitizedString(titlePart);  
    ArrayList<Book> books = new ArrayList<>();  
  
    for (String bookTitle : this.directory.keySet()) {  
        if (!bookTitle.contains(titlePart)) {  
            continue;  
        }  
  
        books.add(this.directory.get(bookTitle));  
    }  
  
    return books;  
  
}
```

This way we lose the speed advantage that comes with the hash map.

The hash map is implemented in such a way that searching by a single key is extremely fast. The example above goes through all the book titles when looking for the existence of a single book using a particular key. 

## Primitive variables in Hash Maps 

> A hash map expects that only reference variables are added to it (in the same way that `ArrayList` does).

Java converts primitive variables to their corresponding reference types when using java's built in data structures such as `ArrayList` and `HashMap`.  

A hash map's key and the object to be stored are always reference type variables. If I ever want to use a primitive variable as a key or value, there exists a reference type conversion for each one. 

- `int` -> `Integer`
- `double` -> `Double`
- `char` -> `Character`

This conversion happens automatically as primitives are added to a hash map or an `ArrayLits`. 

> This automatic conversion is called auto-boxing.

The auto-boxing is also possible in the other way. 

```java
int key = 2;
HashMap<Integer, Integer> hashmap = new HashMap<>();
hashmap.put(key, 10);
int value = hashmap.get(key);
System.out.println(value);
```

The key is an integer and is going to be converted to Integer reference type, while value inside the hash map is a reference type and will be converted to integer type _(primitive)_ when stored in the value variable. 

```java
public class registerSightingCounter {
    private HashMap<String, Integer> allSightings;

    public registerSightingCounter() {
        this.allSightings = new HashMap<>();
    }

    public void addSighting(String sighted) {
        if (!this.allSightings.containsKey(sighted)) {
            this.allSightings.put(sighted, 0);
        }

        int timesSighted = this.allSightings.get(sighted);
        timesSighted++;
        this.allSightings.put(sighted, timesSighted);
    }

    public int timesSighted(String sighted) {
        return this.allSightings.get(sighted);
    }
}
```

In this example we might have a `InvocationTargetException` that can occur in the `timeSighted` method if the `allSightings` hash map does not contain the value we are looking for, then it would return a `null` reference and the auto boxing would fail. 

When performing auto boxing we should ensure that the value being converted is not null. 

```java
public int timesSighted(String sighted) {
    return this.allSightings.getOrDefault(sighted, 0);
}
```

The `getOrDefault` method takes two arguments, the first one is to be searched but it does not exist then the method would return the second parameter. 

The one liner could be like this also :

```java
public int timesSighted(String sighted) {
    if (this.allSightings.containsKey(sighted)) {
        return this.allSightings.get(sighted);
    }

    return 0;
}
```

 