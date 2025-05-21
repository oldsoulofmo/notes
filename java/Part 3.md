# List

`ArrayList` is used to store many values of the same type.

```java
package org.example;  
  
import java.util.ArrayList;  
import java.util.Scanner;  
  
public class Main {  
    public static void main(String[] args) {  
  
        ArrayList<String> list = new ArrayList<>();  
  
  
    }  
  
  
}
```

The type of the `ArrayList` variable is ArrayList. 

The type of an ArrayList that stores strings is `ArrayList<String>`. 


> [!Important] Reminder
> Value type variables (primitive) such as `int` and `double` hold their actual values.
> 
> Reference type variables (reference type) such as `ArrayList`, contains  a reference to the location that contains the value related to the variable.
> 
> Primitives hold a very limited amount of information, references can store a near limitless amount of information.


> String is a reference type variable.

```java
list.remove("First");
list.remove(1);
list.remove(Integer.valueOf(15));
```


```java
if (list.contains("Second")) {
    System.out.println("Second can still be found");
}
```

```java
import java.util.ArrayList;  
import java.util.List;  
import java.util.Scanner;  
  
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
  
        ArrayList<Integer> list = new ArrayList<>();  
  
        list.add(1);  
        list.add(2);  
        list.add(3);  
  
        print(list);  
    }  
  
    public static void print(ArrayList<Integer> list) {  
        for (Integer number : list) {  
            System.out.println(number);  
        }  
    }  
}
```


Remove the last item on the list :

```java
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
  
        ArrayList<String> strings = new ArrayList<>();  
  
        strings.add("First");  
        strings.add("Second");  
        strings.add("Third");  
  
        System.out.println(strings);  
        removeLast(strings);  
        System.out.println(strings);  
        removeLast(strings);  
        System.out.println(strings);  
        removeLast(strings);  
        System.out.println(strings);  
  
  
    }  
  
    public static void removeLast(ArrayList<String> strings) {  
        if (strings.size() == 0) {  
            return;  
        }  
  
        strings.remove(strings.size() - 1);  
  
  
    }  
  
  
}
```


Checking for the existence of a value, provided the value to search for and then it returns a boolean. 

```java
ArrayList<String> list = new ArrayList<>();
boolean found = list.contains("hello world!");
```

# Arrays 

> The size of an ArrayList is unlimited.


```java
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
  
        int[] numbers = new int[4];  
  
        numbers[0] = 1;  
        numbers[1] = 2;  
        numbers[2] = 3;  
        numbers[3] = 4;  
  
        int index_1 = Integer.valueOf(scanner.nextLine());  
        int index_2 = Integer.valueOf(scanner.nextLine());  
  
        int holder = numbers[index_1];  
        numbers[index_1] = numbers[index_2];  
        numbers[index_2] = holder;  
  
        for (Integer i : numbers) {  
            System.out.println(i);  
        }  
  
  
    }  
}
```

> `Array.length` is not a method ! 

# Very interesting exercise 

The idea is to set a boolean checking the state of the number being found or no.

Question :

> The exercise template already has an array containing numbers. Complete the program so that it asks the user for a number to search in the array. If the array contains the given number, the program tells the index containing the number. If the array doesn't contain the given number, the program will advise that the number wasn't found.

```java
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
  
        int[] numbers = new int[4];  
  
        numbers[0] = 1;  
        numbers[1] = 2;  
        numbers[2] = 3;  
        numbers[3] = 4;  
  
        int number = Integer.valueOf(scanner.nextLine());  
  
        boolean found = false;  
  
        for (int i = 0; i < numbers.length; i++) {  
            if (number == numbers[i]) {  
                System.out.println(number + " found at " + i);  
                found = true;  
            }  
        }  
  
        if (!found) System.out.println(number + " not found ..");  
  
    }  
  
  
}
```


# Sum of array 

```java
public class Main {  
    public static void main(String[] args) {  
  
        int[] numbers = {5, 1, 3, 4, 2};  
        int sum = sumCalc(numbers);  
  
        System.out.println(sum);  
    }  
  
    public static int sumCalc(int[] numbers) {  
        int sum = 0;  
        for (Integer i : numbers) {  
            sum += i;  
        }  
  
        return sum;  
    }  
}
```



# Print stars 

```java
public class Main {  
    public static void main(String[] args) {  
  
        int[] numbers = {5, 1, 3, 4, 2};  
  
        sumCalc(numbers);  
  
  
    }  
  
    public static void sumCalc(int[] numbers) {  
        for (Integer n : numbers) {  
            for (int i = 0; i < n; i++) {  
                System.out.print("*");  
            }  
            System.out.println();  
        }  
    }  
  
}
```

# Shorter way to create an array

```java
int[] numbers = {100,1,21};
```

# Strings 

```java
public class Main {  
    public static void main(String[] args) {  
  
        Scanner scanner = new Scanner(System.in);  
  
        System.out.println("Input a text");  
  
        String input = scanner.nextLine();  
  
        if (!("true".equals(input))) {  
            System.out.println("try again");  
        } else {  
            System.out.println("you got it right !");  
        }  
  
    }  
}
```

# Halted

```java
public class Main {  
    public static void main(String[] args) {  
        /*  
        Write a program that reads strings        from the user. If the input is empty,         the program stops reading input and halts.          For each non-empty input it splits the string input by whitespaces           and prints each part of the string on a new line.         */  
        Scanner scanner = new Scanner(System.in);  
        String input = scanner.nextLine();  
        String[] words = input.split(" ");  
  
        if (input.equals("")) {  
            System.out.println("halted");  
        } else {  
            for (String word : words) {  
                System.out.println(word);  
            }  
        }  
  
  
    }  
}
```

# Age of the oldest 

```java
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
        int greater = 0;  
  
        while (true) {  
            String input = scanner.nextLine();  
            if (input.isEmpty()) break;  
            String[] arr = input.split(",");  
            if (Integer.parseInt(arr[1]) > greater) {  
                greater = Integer.parseInt(arr[1]);  
            }  
        }  
        System.out.println(greater);  
    }  
}
```
# Name of the oldest 

```java
public class Main {  
    public static void main(String[] args) {  
        Scanner scanner = new Scanner(System.in);  
        int greater = 0;  
        String name = "";  
  
        while (true) {  
            String input = scanner.nextLine();  
            if (input.isEmpty()) break;  
            String[] arr = input.split(",");  
            if (Integer.parseInt(arr[1]) > greater) {  
                name = arr[0];  
                greater = Integer.parseInt(arr[1]);  
            }  
        }  
        System.out.println(name);  
    }  
}
```

