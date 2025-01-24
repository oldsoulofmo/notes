## Type conversion 

For a computer to perform arithmetic conversion the operands must usually be of the same size _(same number of bits)_ and be stored in the same way. So, a computer might add two 16-bits integers directly but not 32-bits with a 16-bits integer or a 32-bits integer with a 32-bits floating point number. 

C allows to combine different types and sizes into one expression, the C compiler then might have to generate instructions that convert some operands to different types so that the hardware might be able to evaluate the expression. Since the compiler is taking care of these conversions then it's called *implicit conversion*.

> C allows the programmer to perform explicit conversion using the cast operator.

Implicit conversions happen when : 

- The operands in an expression do not have the same type *(usual arithmetic conversions)*.
- The type of the expression on the right side of an assignment does not match the type of the variable on the left. `int x = 1.2;`
- The type of an argument in a function call doesn't match the type of the corresponding parameter.
- When the type of the expression in a return statement doesn't match the function's return type.

### The usual arithmetic conversions 

Let's start by an example :

```c
int x = 1;
float y =2.5;
```

The safest thing is to convert x to float because an int can always be a float, the worst that can happen is a minor loss of precision. 

> A conversion of y to int would cost us the fractional part of the number. 

The strategy behind the usual arithmetic conversions is to convert operands to the narrowest type that will safely accommodate both values.

> One type in narrower than the other if it requires fewer bytes to store.

Promotion : Converting the operand of the narrower type to the type of the other operand, this can be used also to match the types of the operands.

Among the most known promotions are the integral promotions which converts a character or short integer to an integer or an unsigned integer in some cases.

- The type of either operand is a floating type : 
- Neither operand's type is a floating type : First we perform integral promotion on both operands *(to guarantee that neither operand will be a character or a short integer)* 


> [!note] Special case 
> When we have a long integer and an unsigned int that share the same length then both of them are converted to unsigned long integer 

There is an interesting thing here happening, check this code. 

```c
int main () {
	signed int i = -10; 
	unsigned int u = 10;
	printf("%d\n",i<u); // output is 0 .. not what i have expected
}
```

So when a signed operand is combined with an unsigned operand the signed operand is converted to an unsigned operand, the conversion involves adding or subtracting a multiple of $n+1$, where $n$ is the largest representable value of the unsigned type. This rule causes a lot of obscure programming errors. 

What happened in the previous code is that the integer i was converted to an unsigned integer and to do that we can't leave it equal to -10 but instead the value 4,294,967,296 was added *(assuming that 4,294,967,295 is the largest unsigned int value)* giving a converted value of 4,294,967,286. The comparison $i<u$ will produce $0$. 

> Some compilers produce a warning message such as comparison between signed and unsigned, because of traps like this, it is best to use unsigned integers as little as possible and never mixed them with signed integers.


### Implicit conversions in C99 

> The rules of implicit conversions in C99 are different from the ones in C89 primarily because of new data types in C99 such as _Bool, long long types, extended integer types and complex types. 

To define conversion rules, C99 gives each integer types an *integer conversion rank*.

>In place of C89's integral promotions, C99 has integer promotions, which involve converting any type whose rank below int and unsigned int to int (provided that all value of the type can be represented using int) or else to unsigned int. 


The C99 rules for performing the usual arithmetic conversions can be divided into two parts : 
- __The type of either operand is a floating type :__ As long as neither operand has a complex type, then the rules are the same as before. 
- __Neither operand is a floating type :__ First, perform integer promotion on both operands, If the type of the two operands match then the process ends otherwise there are more options. *(check type conversion page 171-172)*

### Casting 

```C
float f,frac_part; 
frac_part = f - (int) f; 
```

> Cast expressions enable us to document conversions that will happen anyways. 

`(type-name)` is a unary operator, so it has higher precedence over binary operators. 

```C
(float) a/b; 
//is exactly 
((float) a)/b;
```

> casts are sometimes necessary to avoid overflows.

```C
long int i;
int j = 100;
i = j*j; 
// int * int = int, so j*j is too large to store on an int, 
// causing an overflow.
i = (long) j*j;
// first j will be long, forces the second one to be long too 
i= (long) (j*j); 
// wrong because the overflow would already happen by the time of 
// the cast 
```







  
  












## Type definitions 

Type definitions are a great way to define types and use them based on the definition we gave them, instead of trying to call the same type over and over or just to avoid changing a type in the whole program _(which is very tiring if the program is very long)_. 
Instead we could use _type definitions_. 
```C
typedef int Age;

Age x = 10; // equivalent to int x = 10;
Age y = 20; // equivalent to int y = 20;
```

## Structure variables 

> The elements of a structure _(members in C parlance)_ are not required to have the same type, the members of a structure have names, to select a particular member we specify it's name and not it's position _(like in arrays)._


> [!NOTE] Tip
> When we need to store a collection of related data items, a structure is a logical choice.

## Pointers 

> In most modern computers, the main memory is divided into bytes where each byte can store up to 8 bits. 
> >Each byte has a unique address.

> p The argument shall be a pointer to void. The value of the pointer is converted to a sequence of printing characters, in an implementation-defined manner.
>  > _(Shall come back to it later ...)_

```C
printf("The address of %d is %p \n", x, (void*)&x);
```

## Basic Types 
### Floating typess 

`double` has more precision than `float`. 
`%lf` for doubles, `%Lf` for long doubles.

### Character types 

> C treats chars as small integers. 

> Char constants have int type rather than char type.

