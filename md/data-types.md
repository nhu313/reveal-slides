## What's the answer?

## 65 + 3

-
## The answer

##<p class="fragment fade-in-then-semi-out">Is it 68?</p>

##<p class="fragment fade-in-then-semi-out">Is it 653?</p>

##<p class="fragment fade-in-then-semi-out">Is it D?</p>

<p class="fragment fade-in-then-semi-out">It depends on what the data type is.</p>

-

## Integer

## 65 + 3 => 68

-
## String

## "65" + "3" => "653"

-
## Character

## 65 + 3 => 'D'

## 'A' + 3 => 'D'

-
-

## Data type

Java is a strongly-typed language, and every variable must have a declared type.

-

## Primitive Data Types

There are eight primitive types in Java:

1. byte
2. short
3. int
4. long
5. float
6. double
7. char
8. boolean

-

## Integer Types

Negative and positive numbers without fractions

| Type  | Storage requirements | Range (Inclusive)                                       |
| ----- |:------------------- | :------------------------------------------------------ |
| byte  | 1 byte              | -128 to 127                                             |
| short | 2 bytes             | –32,768 to 32,767                                       |
| int   | 4 bytes             | –2,147,483,648 to 2,147,483, 647 (just over 2 billion)  |
| long  | 8 bytes             | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

-
## What is a byte?

Think of a byte as one tiny box of memory. A short needs boxes to store the number. An int needs 4 boxes.

Each of the box holds 8 bits. A bit can hold a value of 0 or 1.

1 MB ~ 1 million bytes
1 GB ~ 1 trillion bytes

-
## Variables


```
byte b = 127;
short s = 30000;
short s1 = -32_000;
```

Most common:

```
int i = 20;

//long
long l = 100;
long l1 = 100L;
long l2 = 100l;
```

-
## Casting

Java can automatically convert from one smaller type into a bigger type.

```
byte b = 127;
int i = b;
```

-
## Integer data types

| Type  | Storage requirements | Range (Inclusive)                                       |
| ----- |:------------------- | :------------------------------------------------------ |
| byte  | 1 byte              | -128 to 127                                             |
| short | 2 bytes             | –32,768 to 32,767                                       |
| int   | 4 bytes             | –2,147,483,648 to 2,147,483,647 (just over 2 billion)  |
| long  | 8 bytes             | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

-
## Casting and integer overflow

To cast a larger type into a smaller type, you have to write the type you want it to.

```
int i = 129;
byte b = (byte)i; // casting from 4 bytes into 1 byte
System.out.println(b); // => -127
```

If the number is out of its bound, then it will reset back from the lowest number.

-

## Floating-Point Types

Numbers with fractional parts

| Type   | Storage requirements | Range (Inclusive)                                              |
| ------ |:------------------- | :------------------------------------------------------------- |
| float  | 4 bytes             | Approximately ±3.40282347E+38F (6–7 significant decimal digits) |
| double | 8 bytes             | Approximately ±1.79769313486231570E+308 (15 significant decimal digits)|

-

## Casting

Java can automatically cast integers into float/double.

```
int i = 2000;
float f = i;
```

-
## Casting

To cast from a decimal number into an integer, you have to explicitly say so.

```
float f = 3.14f;
int i = (int)f;
System.out.println(i);
```

It will prints out:
<p class="fragment fade-in-then-semi-out">3</p>

-

## The char Type

The char type is a single character represented by a value enclosed in single quotes. It takes up 2 bytes.

```
char a = 'a';
char capA = 'A';
char semi = ';';
char num = '8';
char numChar = 65; // 'A'
```

Note `'8'` is NOT the same as the number `8` without quotes. One is a char, the other an int.

-

###The boolean Type

The boolean type has two values: <span style="color: red">false</span> and <span style="color:green">true</span>.

```
boolean a = 1 > 0; // true
boolean b = 1 > 5; // false
boolean c = 1 == 1; // true
boolean d = 1 >= 5; // false
boolean e = 1 <= 5; // true
```

-
-
## Resources
- Core Java Chapter 3.3
- [Data types - Oracle](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)
- [Understanding Binary](https://www.youtube.com/watch?v=Xpk67YzOn5w)

## The end

<img src="https://weneedfun.com/wp-content/uploads/2015/10/Cute-puppy-Pictures-29.jpg">
