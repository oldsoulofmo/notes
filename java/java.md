#### The continue statement 

In it's simplest form, will stop executing the current iteration of a block of code in a loop and start a new iteration. 

#### Local variables and scope 

In the switch block we can access a local variable defined in the previous case, assign it another value or whatever .. 

#### Reading input 

Reading an input using `System.console()` which is disabled in IDE'S, a workaround this is to run the program from terminal `java src/Main.java`

#### Exception handling and Introduction to scanner 

```java
import java.util.Scanner;  
  
public class Main {  
    public static void main(String[] args) {  
//        Scanner scanner = new Scanner(System.in);  
//  
//        // String name = System.console().readLine("Enter your name ");  
//  
//        System.out.println("What's your name ?");  
//        String name = scanner.nextLine();  
//        System.out.println(name);  
//  
//        //String age = System.console().readLine("Enter you age ");  
//  
//        System.out.println("and your age ?mo");  
//        String age = scanner.nextLine();  
//        System.out.println(2023 - Integer.parseInt(age));  
  
        Scanner scanner = new Scanner(System.in);  
  
        int counter = 1;  
        int sum = 0;  
  
        do {  
            System.out.println("Enter numeber #" + counter + " :");  
            String nexNumber = scanner.nextLine();  
            try {  
                int number = Integer.parseInt(nexNumber);  
                counter++;  
                sum += number;  
            } catch (NumberFormatException nfe) {  
                System.out.println("Invalid Number1");  
            }  
  
        } while (counter <= 5);  
        System.out.println(sum);  
    }  
}
```

### OOP - PART 1 : INHERITANCE 

State is stored in fields, which can be called variables or attributes.

If a field is static, there's only one copy in memory and this value is associated with the class itself. If the field is not static then it is an instance field and each object (instance) may have different value stored for this field.

> A static method cannot be dependent on any one object's state, so it cannot reference any instance members. 
> > Any method that operates on instances fields, needs to be non-static. 


> [!NOTE] Special keyword "null"
> null means that a variable or attribute has a type but no reference to an object. Which means 
> that no instance or object is assigned to the variable (field). 
>  > Field with primitive data types are never null.
>  

#### Getters 

 A way to protect data and retrieve it from a private field.

#### Setters 

A way to set the value of a field 

> Check `documents/JAVA/OOP/challenge` 

#### Constructors part-1 

If a class contains no constructor declaration then a default one is implicitly declared, the constructor has no parameters and is often called the no-arguments constructor.

> If a class contains any other constructor declarations, then a default constructor is NOT implicitly declared.

> If the name of the parameters is the same as the name of the fields then the `this` keyword must be used.

> [!NOTE] Constructor overloading
> Declaring multiple constructors with different formal parameters, if the number of parameters is the same then the type or order must differ.

#### Reference vs Object vs Instance vs Class



#### The text block and other formatting options 

Some common escape sequences : 

- `\t` Insert a tab character.
- `\n` Insert a new line character.
- `\"` Insert a double quote character.
- `\\` Insert a backslash character.

To format `Strings` we get to work in a lot of ways, using format specifiers like `%d %f %6d %.2f` or use text block which is like `String shit = """ strings go here """`. 
We also may use `String shit = String.format("hi %d",age)` and also there's a method on string `String shit = "Your age %d".formatted(age)`.

```java
string1.equals(string2);
string1.equalsIgnoreCase(string2);
string1.contentEquals(string2); 
// able to compare string builders value too, not supported by equals. 


```

### The StringBuilder class




### Arrays 


> [!NOTE] Note
> Declarations are on the left of the equal sign.

An array is not resizable, we cannot add or delete elements, we can only assign values.

##### The array initializer 
easy way to initialize a small array. 

```java
int numbers = new int[]{1,2,3,4,5};
```

this way length can be determined, so we do not need to specify the size ourselves.

###### A simpler way to do it 

Java lets us drop `new int`.

```java
int[] numbers = {1,2,3,4,5};
// this is called an anonymous array.
```


> [!NOTE] Note
> Array initializer can only be used in declaration assignments or method arguments.
> ```java
> // do not do this  
// int[] anArray;  
// anArray = {1,2,3}  
// instead fix it by this  
// anArray = new int[] {1,2,3} 
> ```

```java
public class Main {  
    public static void main(String[] args) {  
        int[] myArray = new int[10];  
        myArray[5] = 50;  
  
        double[] myOtherArray = new double[10];  
        myOtherArray[5] = 60.5;  
  
        System.out.println(myArray[5]);  
        System.out.println(myOtherArray[5]);  
  
        int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};  
        int length = numbers.length;  
  
        System.out.println(numbers[length - 1]);  
        System.out.println("length = " + length);  
  
        // do not do this  
        // int[] anArray;
        // anArray = {1,2,3}
        // instead fix it by this
        //anArray = new int[] {1,2,3}  
        
        System.out.print("=> elements of the array are ");  
        
        for (int i = 0; i < length; i++) {  
            System.out.print(numbers[i] + " ");  
        }  
    }}
```


An array is a special class, it also inherits from `java.lang.Object`.
Default element values, primitive values set to 0, boolean to false and for any class type to null.

###### Populate an array using the for loop 

```java
int[] numArray;  
numArray = new int[5];  
  
for (int i = 0; i < numArray.length; i++) {  
    numArray[i] = numArray.length - i;  
}  
  
System.out.print("=> elements of the array are ");  

for (int i = 0; i < numArray.length; i++) {  
    System.out.print(numArray[i] + " ");  
}
```

###### Enhanced for loop 

Called the `forEach` loop.

```java
for (int element : numArray) {  
    System.out.print(element + " ");  
}
```

```java
  System.out.println(numArray); // [I@4f023edb
  ```  

> This means that the array class doesn't print the elements out neatly for us, as we might hope. In other words, it doesn't override the toString method, so it uses java.lang.Object's toString method. And this gives us the left square bracket with a capital I, which means it's a primitive integer array, and then it's followed by the hexadecimal representation, of the hash code.

An array is actually an object, therefore we can assign an array to an object instance. We also use the helper class `java.util.Arrays` which has many functionalities, these are static methods on Arrays, so they are class methods, not instance methods.  

```java
System.out.println(Arrays.toString(numArray));  
  
Object objectVariable = numArray;  
if (objectVariable instanceof int[]) {  
    System.out.println("objectVariable is really an int array.");  
}  
  
Object[] objectArray = new Object[3];  
objectArray[0] = "Hello";  
objectArray[1] = new StringBuilder("World");  
objectArray[2] = numArray;
```

  
> [!NOTE] Note
> For primitives, the values get copied.
> For objects, the object references get copied.

###### Some important methods 

```java
import java.util.Arrays;  
import java.util.Random;  
  
public class Main {  
    public static void main(String[] args) {  
        int[] firstArray = getRandom(10);  
        System.out.println(Arrays.toString(firstArray));  
  
        //sort an array  
        Arrays.sort(firstArray);  
        System.out.println(Arrays.toString(firstArray));  
  
        // fill out an array  
        int[] secondArray = new int[10];  
        System.out.println(Arrays.toString(secondArray));  
        Arrays.fill(secondArray, 5);  
        System.out.println(Arrays.toString(secondArray));  
  
        // copy an array  
        int[] thirdArray = getRandom(5);  
        System.out.println(Arrays.toString(thirdArray));  
  
        int[] fourthArray = Arrays.copyOf(thirdArray, thirdArray.length);  
        System.out.println(Arrays.toString(fourthArray));  
  
        Arrays.sort(fourthArray);  
        System.out.println(Arrays.toString(thirdArray));  
        System.out.println(Arrays.toString(fourthArray));  
        // only the fourth array will be sorted, third won't be sorted even if              it is  
        // the array we copied values from, copyOf creates a new instance of                array.  
        // exceeding the size will result in zeros in additional indexes, and               using a smaller size will result in taking the first indexes
        // only = size (length).  
    }  
  
    private static int[] getRandom(int length) {  
        Random random = new Random();  
        int[] newArray = new int[length];  
        for (int i = 0; i < length; i++) {  
            newArray[i] = random.nextInt(100); // it will generate from 0-99 ... 
        }  
  
        return newArray;  
  
    }  
}
```

### Binary search 

```java
Arrays.binarySearch(byteArr, byteKey);
```

### Composition 

Inheritance defines a IS a relationship, while composition defines a HAS a relationship.

