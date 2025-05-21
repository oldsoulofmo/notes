[[]]

```java
try {  
    PrintWriter writer = 
    new PrintWriter("/Users/mohammedchaouki/documents/file.txt");  
    writer.println("This file was generated for some purposes ...");  
    writer.println("Fuck off, bye !");  
    writer.close();  
} catch (FileNotFoundException e) {  
    throw new RuntimeException(e);  
}
```

The constructor of the `PrintWriter` class might throw an exception that must be either handled or thrown and that is the responsibility of the calling method. 

```java
public class Storer {

    public void writeToFile(String fileName, String text) throws Exception {
        PrintWriter writer = new PrintWriter(fileName);
        writer.println(text);
        writer.close();
    }
}
```

The possible exception that the constructor throws has to be handled with a `try-catch` block or the handling responsibility has to be transferred elsewhere.

In the `writeToFile` method, the responsibility to handle the exception is placed on the method that calls `writeToFile`, and the method that calls it is the `main` method.

```java
public class Main {  
    public static void main(String[] args) throws Exception {  
  
	  Storer storer = new Storer();
      storer.writeToFile("/Users/mohammedchaouki/documents/file.txt"
      ,"hello mfs");  
    }  
}
```

There is nothing that forces the `main` method to to handle the exception and it too can throw an exception. 


> [!NOTE] FileWriter
> Using the `writeToFile` method on the same file will cause the file to be written from the beginning, to add more content to the file I better use the `FileWriter` class.

