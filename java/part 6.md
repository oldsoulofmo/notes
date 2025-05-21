To return an object form a method : 

```java
public Person getTallest() {
    // return a null reference if there's no one on the ride
    if (this.riding.isEmpty()) {
        return null;
    }

    // create an object reference for the object to be returned
    // its first value is the first object on the list
    Person returnObject = this.riding.get(0);

    // go through the list
    for (Person prs: this.riding) {
        // compare each object on the list
        // to the returnObject -- we compare heights
        // since we're searching for the tallest,

        if (returnObject.getHeight() < prs.getHeight()) {
            // if we find a taller person in the comparison,
            // we assign it as the value of the returnObject
            returnObject = prs;
        }
    }

    // finally, the object reference describing the
    // return object is returned
    return returnObject;
}
```

Now finding the tallest person is easy, just comparing the height of each person to the first person we assigned to that return Object. 

WordSet -> Interface -> Main 

WordSet provides to the Interface some methods and it encapsulates the ArrayList words. 

Changes made to the WordSet class won't affect the Interface because we only use methods provided from it. 

The `UserInterface` uses the `WordSet` class's public methods to interact with it, but it doesn't directly modify or access the internal details of `WordSet`.

