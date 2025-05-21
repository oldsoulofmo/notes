```java
package org.example;  
  
import java.util.ArrayList;  
import java.util.Scanner;  
  
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
        ArrayList<Book> books = new ArrayList<>();  
  
        while (true) {  
            System.out.println("Enter an ame, empty will stop");  
            String name = scanner.nextLine();  
  
            if (name.isEmpty()) break;  
            System.out.println("Who's the author");  
            String author = scanner.nextLine();  
  
            books.add(new Book(name, author));  
        }  
  
        System.out.println("What do you want to print ?");  
        String output = scanner.nextLine();  
  
        for (Book book : books) {  
            if (output.equals("everything")) {  
                System.out.println(book);  
            }  
  
            if (output.equals("title")) {  
                System.out.println(book.getName());  
            }  
        }  
  
  
    }  
}
```


```java
package org.example;  
  
import java.time.LocalDateTime;  
  
public class Book {  
    private String name;  
    private String author;  
    private LocalDateTime addedOn;  
  
    public Book(String name, String author) {  
        this.name = name;  
        this.author = author;  
        this.addedOn = LocalDateTime.now();  
    }  
  
    public LocalDateTime getDate() {  
        return this.addedOn;  
    }  
  
    public void setDate(LocalDateTime addedOn) {  
        this.addedOn = addedOn;  
    }  
  
    @Override  
    public String toString() {  
        return this.name + " ," + this.author + " ," + this.addedOn;  
    }  
  
    public String getName() {  
        return name;  
    }  
  
    public void setName(String name) {  
        this.name = name;  
    }  
  
    public String getAuthor() {  
        return author;  
    }  
  
    public void setAuthor(String author) {  
        this.author = author;  
    }  
}
```