```java
package org.example;  
  
import java.nio.file.Paths;  
import java.util.ArrayList;  
import java.util.Scanner;  
  
public class Main {  
    public static void main(String[] args) {  
        ArrayList<String> names = new ArrayList<>();  
        System.out.println("What file do you wanna read ?");  
        Scanner scanner = new Scanner(System.in);  
        String file = scanner.nextLine();  
        try (Scanner reader = new Scanner(Paths.get(file))) {  
            while (reader.hasNextLine()) {  
                String name = reader.nextLine();  
                names.add(name);  
            }  
  
            while (true) {  
                System.out.println("searching for ?");  
                String input = scanner.nextLine();  
  
                if (input.isEmpty()) {  
                    System.out.println("Thank you !");  
                    break;  
                }  
  
                if (names.contains(input)) {  
                    System.out.println("Found");  
                } else {  
                    System.out.println("Not found");  
                }  
            }  
  
  
        } catch (Exception e) {  
            System.out.println("Reading the file " + file + " failed");  
        }  
    }  
}  
  
class ListNode {  
    int value; // Node value  
    ListNode next;  
  
    ListNode(int x) {  
        value = x;  
    }  
}
```