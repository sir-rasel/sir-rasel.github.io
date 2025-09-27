---
title: "Java Crash Course - Part 2 (Fundamental Basics)"
description: "Let's learn writing program with Java"
date: 2025-09-27
tags: ["programming", "language", "java", "crash-course"]
draft: false
showtoc: false
tocOpen: false
hidemeta: false
comments: true
disableHLJS: false
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowCodeCopyButtons: true
cover:
    image: "img/blogs/30-java-language.webp"
    caption: "Java"
    alt: "Java"
    relative: true
    hidden: true
---

---
### Other Parts of This Series:
- **Part 1:** [Java Crash Course - Part 1 (Before Start)]({{< ref "blogs/30-java-part-1-before-start.md" >}})
---

{{< figure
    src="/img/blogs/30-java-language.webp"
    caption="Java Programming Language (Photo Credit: Orient Software)"
    align=center
>}}

***N.B:*** Please read the following concepts for better understanding before continue reading this article.

☛ [Programming & Fundamental Concepts of Programming]({{< ref "blogs/1-lets-feel-programming-part-1.md" >}})

☛ [Data Types, Variable, Operator]({{< ref "blogs/2-lets-feel-programming-part-2-variable-operator.md" >}})

☛ [Condition & Looping]({{< ref "blogs/3-lets-feel-programming-part-3-condition-loop.md" >}})

☛ [Function, Pointer, Scope]({{< ref "blogs/4-lets-feel-programming-part-4-function-pointer.md" >}})

☛ Setting up the environment: [Read this link and follow the instruction](https://www.geeksforgeeks.org/setting-environment-java/?ref=lbp)

---

## Basic Syntax of Java
I try to keep the things simple enough as much as possible. Without any outside discussion I only mention the main focus point. So lets start..

### Skeleton:
```java
import java.io.*; // 0

class Simple{ // 1
    public static void main(String args[]){  // 2
        System.out.println("Hello Java");  // 3
    }  
}
```
As java is a object oriented programming language so everything here is considered as a combination of class and object. In the above code snippet we can see the basic skeleton of a java program. Here in -
- Mark (0) - This is the importing of package or library.
- Mark (1) - This is the starter point of the program.
- Mark (2) - This is main function and the entry point of program execution.
- Mark (3) - A basic statement which print Hello Java in console.

*** Java 25 don't need the whole class and static void main() method as starting point. We can just write the statement and Java consider them as part of main() ***
```java
System.out.println("Hello Java 25!");
```

### Comments:
Like other programming language java also supports single line and multi line comments.

Single line comments starts with "//" and multi line comments "/* comments */".

Example:
```java
// Single line comment

/*
Multi line
something in between
comments
*/
```

### Data Type
{{< figure
    src="/img/blogs/31-java-data-type.png"
    caption="Java Programming Language (Photo Credit: javaTpoint)"
    align=center
>}}

There are two types of data types in Java:
1. **Primitive data types**: The primitive data types include boolean, char, byte, short, int, long, float and double.
2. **Non-primitive data types**: The non-primitive data types include classes, interfaces and arrays.

### Variable: 
In programming variable is like a container which can holds data of different types. As java is a strongly typed language so we need to specify the type when declare a variable.

Example:
```java
import java.io.*;

class Sample {
	public static void main(String args[])
	{
		char a = 'G';
		int i = 89;
		byte b = 4;
		short s = 56;
		double d = 4.355453532;
		float f = 4.7333434f;
		long l = 12121;

		System.out.println("char: " + a);
		System.out.println("integer: " + i);
		System.out.println("byte: " + b);
		System.out.println("short: " + s);
		System.out.println("float: " + f);
		System.out.println("double: " + d);
		System.out.println("long: " + l);
	}
}
```

### Operators:
There are many types of operators in Java which are given below:
- Unary Operator, (++, --)
- Arithmetic Operator, (+, -, *, /, %)
- Shift Operator, (>>, <<)
- Relational Operator, (<, >, <=, >=, !=, ==)
- Bitwise Operator, (|, &, ^)
- Logical Operator, (||, &&)
- Ternary Operator and (? :)
- Assignment Operator. (=)

Example:
```java
import java.io.*;

class Operators {
	public static void main(String[] args)
	{
		int a = 10, b = 20;
        int c = a + b;
        int d = a ^ b;
        bool isSame = a == b;

		System.out.println(a);
		System.out.println(b);
		System.out.println(c);
        System.out.println(d);
        System.out.println(isSame);
	}
}
```
---
### Let's Practice:
The best way of practicing programing is solving programming problem. Lets solve the problem [LeetCode 371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/) by using the knowledge that we learn till now.

Problem says that given two integer a and b, calculate their sum.

Solution:
```java
class Solution {
    public int getSum(int a, int b) {
        int sum = a + b;
        return sum;
    }
}
```
---
### Condition (if-else and if-else if-else):
Java if-else and and if-else if-else or if-else ladder syntax is similar to C++/C#.

Example:
```java
import java.io.*;

public class IfElseExample { 
    public static void main(String[] args) {  
        int age = 20;  
    
        if(age>18){  
            System.out.print("Age is greater than 18");  
        }
        else {
            System.out.print("Age is not greater than 18");
        }
    }  
}
```

Please note: infinite level of nesting of if else or else if ladder is support by the java program.

Example:
```java
import java.io.*;

public class ElseIfLadderExample { 
    public static void main(String[] args) {  
        int age = 20;  
    
        if(age>18){  
            System.out.print("Age is greater than 18");
            
            if(age > 20) {
                System.out.print("Age is greater than 20");
            } 
            else {
                System.out.print("Age is greater than 18 but less than 20");
            }
        }
        else if(age == i8){
            System.out.print("Age is equal to 18");
        }
        else {
            System.out.print("Age is not greater than 18");
        }
    }  
} 
```

### Condition (switch case):
Java switch case syntax is also similar to C++. The difference between if else and switch condition is, if condition can check the all relational condition but, switch can only check equal with case value. You can write the nested switch statements also.

Example:
```java
import java.io.*;
 
class Sample {
    public static void main (String[] args) {
        int num=20;
        switch(num){
          case 5 :  System.out.println("It is 5");
                    break;
          case 10 : System.out.println("It is 10");
                    break;
          case 15 : System.out.println("It is 15");
                    break;
          case 20 : System.out.println("It is 20");
                    break;
          default:  System.out.println("Not present");
        }
    }
};
```

Java support ***switch expression*** in its latest release.

Example:
```java
import java.io.*;
 
class Sample {
    public static void main (String[] args) {
        Day day = Day.WEDNESDAY;
        int numLetters = switch (day) {
            case MONDAY, FRIDAY, SUNDAY -> 6;
            case TUESDAY -> 7;
            case THURSDAY, SATURDAY -> 8;
            case WEDNESDAY -> 9;
        };
    }
};
```

**Break statements**: The switch case example has break statements. Like its name suggests, a break statement breaks an execution block so that the below code of that block will be ignored. So if the program encounters a break statement, then it immediately breaks that block.

### Array:
Arrays are non-primitive data types in Java. An array is nothing but a collection of similar types of data. That means when we need more than one similar and related data, then we should use the array. Arrays are being declared using [ ]. Also, it can be one-dimensional and multi-dimensional. Arrays can be declared in 3 ways.

Example:
```java
class Sample {
	public static void main(String[] args)
	{
		int[] arr1; // type 1 declaration
        int arr2[]; // type 2 declaration
        int []arr3; // type 3 declaration

        // multi dimensional array declaration
        int marr1[][]; // type 1 declaration
        int[][] marr2; // type 2 declaration
        int [][]marr3; // type 3 declaration
	}
}
```

### Loop:
Java supports generally 4 types of loop. They are:

1. While loop

Example:
```java
import java.io.*;

class whileLoopDemo {
	public static void main(String args[])
	{
		int i = 1;

		while (i < 6) {
			System.out.println("Hello World");
			i++;
		}
	}
}
```

2. Do...While loop

Example:
```java
import java.io.*;

class DoWhileDemo {
	public static void main(String[] args)
	{
		int i = 0;
		do {
			System.out.println("Print statement");
			i++;
		} while (i < 0);
	}
}
```

3. For loop

Example:
```java
import java.io.*;

class forLoopDemo {
	public static void main(String args[])
	{
		for (int i = 1; i <= 5; i++){
            if(i == 3) continue;
			System.out.println("Hello World");
        }
	}
}
```

4. For...Each loop

Example:
```java
import java.io.*;

class ForEachDemo	
{
	public static void main(String[] arg)
	{
		{
			int[] marks = { 125, 132, 95, 116, 110 };
			
            for (int num : marks){
  			    System.out.println(num);
            }
  		}
  	}
}
```

**Continue statements**: Continue also to ignore the execution of the existing below code of a block, but unlike break, continue its executions for the next iterations.

### Function or Method:
A Java function, also known as a method, is a block of code or a collection of statements or a set of code grouped together to perform a certain task or operation. It is used to achieve the reusability of code. The declaration signature of a method is as below:

```java
Access_Modifier Return_type Method_Name (Parameter_List) {
   Method_body (collection of statements)
   
   return return_value; // when void type it do not return anything
}
```

Lets write a method for finding maximum value from a array.

Example:
```java
import java.io.*;

class FunctionDemo	
{
	public static void main(String[] arg)
	{
		{
			int[] marks = { 125, 132, 95, 116, 110 };
			
            // call the maximum function to get highest marks
			int highest_marks = maximum(marks);

			System.out.println("The highest score is " + highest_marks);
		}
	}

    // This is our maximum finding method
	public static int maximum(int[] numbers)
	{
		int maxSoFar = numbers[0];
		
		for (int num : numbers)
		{
			if (num > maxSoFar)
			{
				maxSoFar = num;
			}
		}
	    return maxSoFar;
	}
}
```
---
### Lets Practice:
The best way of practicing programing is solving programming problem. Lets solve the problem [LeetCode 1704. Determine if String Halves Are Alike](https://leetcode.com/problems/determine-if-string-halves-are-alike/) by using the knowledge that we learn till now.

Here problem says, return true if first half and the second half of the string contains equal number of vowel otherwise return false.

Solution:
```java
class Solution {
    public boolean halvesAreAlike(String s) {
        int len = s.length();
        return countVowel(s, 0, len/2) == countVowel(s, len/2, len);
    }


    public int countVowel(String s, int start, int end){
        int count = 0;

        for(int i=start;i<end;i++){
            if(isVowel(s.charAt(i))) 
                count++;
        }

        return count; 
    }


    public boolean isVowel(char toCheckValue){
        char arr[] = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'};
        for (char element : arr) {
            if (element == toCheckValue) {
                    return true;
            }
        }
        return false;
    }
}
```
---

*Insha Allah, in the upcoming part, I will try to share the Object Oriented Programming of Java. Until than, may Allah keep you healthy and happy.*