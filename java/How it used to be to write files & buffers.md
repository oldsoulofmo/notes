## The java.io.File class

It's an old class that was replaced by two new classes in the newer `java.nio.file` package. 

This class represents the file and not the content, a `FILE` object is a _path name_ of a file or even a _directory_ rather than the content. 

> A very useful thing about a `FILE` object is that it offers a much safer way to represent a file than just using a String filename.

## Buffers 

### Writing to a text file

```java
public class Main {  
    public static void main(String[] args) throws IOException {  
  
        FileWriter fW = new FileWriter("/Users/mohammedchaouki/documents/file.txt");  
        BufferedWriter writer = new BufferedWriter(fW);  
  
        writer.write("Hello");  
        writer.flush();  
    }  
}
```

Buffers are super efficient, they give us a holding place (a cart) until the holder (the cart) is full.

When the buffer is full all Strings (example) inside the buffer will be written to the file, but in the example above I have used `flush` method to just pass everything to the file without waiting until the buffer is full.

### Reading from a text file 

w
