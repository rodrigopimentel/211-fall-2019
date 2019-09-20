# Lab 03: Number Systems and Branching (Conditionals)

Welcome to CSC 211 Lab 03. Yor goal for this lab will be to gain a better understanding of branching, and how to handle programming problems with multiple conditionals. **Be sure to read and follow all instructions unless otherwise specified.** Some of the language used here has been adopted from the *OpenDSA Data Structures and Algorithms Modules Collection Chapter 8 Algorithm Analysis* text.

The table of contents for this lab is found below.

<ol>
1. Number System Conversions[50 minutes]
1.1 Examples
1.2. Problem Set
2. Branching (Conditionals) [50 minutes]
2.1. Syntax Review
1.2. Problem Set

</ol>

# Part 1. Number System Conversions [50 minutes]

## Number Systems Overview

For each number system, the right-most value starts at 1. Each position moving left is 2x the value on the right.

Examples:

Encoding in groups of 3 (Octal) we get a maximum value of 7 representable by a single digit. 
[4 2 1] = 111, they are all "on".

Encoding in groups of 4 (Hexadecimal) we get a maximum value of 15 representable by a single digit. 
[8 4 2 1] = 1111, they are all "on".

## Binary (Base 2)
Allowed Digits: [0, 1]

Groups of 1: 0 or 1

With each digit known as a bit, Binary is the number system used by computers to process information. Binary is difficult for us to read because expressing anything meaningful takes far too many bits. All programs get converted into this number system by your computer. Binary digits are limited in use by themselves, but when placed into groups of multiple bits, we can start to form other number systems to represent more complex numbers.

Examples:

0 stands for "false", or "off".

1 stands for "true" or "on".

## Octal (Base 8)

Allowed Digits - [0, 1, 2, 3, 4, 5, 6, 7]

Groups of 3: 

| Decimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Octal | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |

Octal is an older method of abbreviating binary where bits are grouped in 3s.
Once upon a time, CPUs were 26 or 36 bits and processed information in Octal. Now that we have 32/64-bit processors, we use Hexadecimal (base 16) as they are both more efficiently divisible by 16.

Example:

Unix file permissions are written in 3 Octal digits, as each bit stands for 1 of 3 permissions (read, write, execute), and there are 3 categories (user, group, others.) 
rwxr-xr-- translates to 111101100, and would allow the user to read, write, and execute a file, members of a specific group to read and execute the file, and all others to only read the file.


## Decimal (Base 10)

Allowed Digits - [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

Groups of 1: each digit represents itself; we use multiple digits to represent larger numbers.

Human-readable numbers. This is the system humans are most comfortable with, and (hopefully) the one you are familiar with.

Example:

We'll operate on the assumption no example is needed for the Decimal number system.

## Hexadecimal (Base 16) 

Allowed Digits - [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F]

Groups of 4:

| Decimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |
| Hexadecimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B| C | D | E | F |


Hexadecimal is the modern method of abbreviating binary where bits are grouped in sets of 4.
With modern processors being either 32/64 bit, they are both most efficiently divided by 16. The Hexadecimal number system is used to define locations in memory, colors on a web page, MAC addresses, error messages, etc.

Example:

Web page colors are frequently written in Hexadecimal. Why? Easy to read, we can encode many colors into a few digits! With 4 Hexadecimal digits (FFFF) we can encode 65,535 unique values, that’s a lot of colors!

### Summary

The digits used to represent a value will vary in both quantity, and legibility, depending on the number system being used; each number system is best suited for a particular task.

Reminder: For each number system, the right-most value starts at 1. Each position moving left is 2x the value on the right.

Let's look at the maximum value of each system using 2 digits

#### 2 Binary Digits:[2 1]

| Binary | [0 0] | [0 1] | [1 0] | [1 1] |
| --- | --- | --- | --- | --- |
| Decimal | 0 | 1 | 2 | 3 |

4 unique values can be represented. Max # = 3

#### 2 Octal Digits: [32 16 8 4 2 1]

| Octal | [000 000] | [000 001] | ... | [111 110] | [111 111] |
| --- | --- | --- | --- | --- | --- |
| Decimal | 0 | 1 | ... | 62 | 63 |

64 unique values can be represented. Max # = 63

#### 2 Decimal Digits:

| Decimal | 0 | 1 | ... | 98 | 99 |
| --- | --- | --- | --- | --- | --- |

100 unique values can be represented. Max # = 99

#### 2 Hexadecimal Digits: [128 64 32 16 8 4 2 1]

| Hexadecimal | 00 | 01 | ... | FE | FF |
| --- | --- | --- | --- | --- | --- |
| Binary | [0000 0000] | [0000 0001] | ... | [1111 1110] | [1111 1111] |
| Decimal | 0 | 1 | ... | 254 | 255 |

256 unique values can be represented. Max # = 255

## Number System Conversions

How do we convert between number systems? We use a different algorithm based on the base we are converting from and the base we are converting to.

### Binary Conversion

#### Binary to Octal

1.	Group the digits into sets of 3 from the right, padding left with 0s if necessary.
2.	Read right to left, treating each group separately from the others and calculate the correct digit conversion.
..*	A table can help for this, as demonstrated below.

|Binary | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Octal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

Example: 

Convert 1101 in Binary to Octal

1. Group the digits into sets of 3 from the right, padding left with 0s if necessary.
- 1101 becomes 001 101
2. Read right to left, treating each group separately from the others and calculate the correct digit conversion.	  
- 101 becomes 5
- 001 becomes 1

15 is the Octal representation of 1101 in Binary.

#### Binary to Hexadecimal
1. Group digits into sets of 4 from the right, padding left with 0s if necessary.
2. Read right to left, treating each group separately from the others and calculate the correct digit conversion.
- A table can help for this, as demonstrated below.

| Decimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |
| Hexadecimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B| C | D | E | F |

Convert 1101101 in Binary to Hexadecimal

1. Group digits into sets of 4 from the right, padding left with 0s if necessary.
- 1101101 becomes 0110 1101
2. Read right to left, treating each group separately from the others and calculate the correct digit conversion.
- 1101 becomes D
- 0110 becomes 6

6D is the Hexadecimal representation of 1101101 in Binary

#### Binary to Decimal

1.	Begin with your Decimal result set to 0.
2.	Remove the most significant binary digit (leftmost) and add to the result.
3.	If there are no more digits, stop.
4.	Otherwise, multiply your result by 2.
5.	Repeat starting at step 2.

Convert 1101 in Binary to Decimal

| Current Number | Remaining Bits After This Step | Decimal Result After Add | Decimal Result After Multiply |
| --- | --- | --- | --- |
| 1101 | 101 | 1 | 2 | 
| 101 | 01 | 3 | 6 |
| 01 | 1 | 6 | 12 |
| 1 | - | 13 | STOP |

### Decimal Conversion

The same algorithm works for converting Decimal to Binary, Octal, or Hexadecimal.
1. Divide the Decimal number by the target number system’s base.
2. Append the remainder as the next leftmost digit (most significant)
3. Repeat until you compute 0 as your quotient.

#### Convert 173 Decimal to Binary

| Number | Divisor | Quotient | Remainder | Binary Representation |
| --- | --- | --- | --- | --- |
| 173 | 2 | 86 | 1 | 1 |
| 86 | 2 | 43 | 0 | 01 | 
| 43 | 2 | 21 | 1 | 101 |
| 21 | 2 | 10 | 1 | 1101 |
| 10 | 2 | 5 | 0 | 01101 |
| 5 | 2 | 2 | 1 | 101101 |
| 2 | 2 | 1 | 0 | 0101101 |
| 1 | 2 | 0 | 1 | 10101101 |

173 Decimal is 10101101 Binary

#### Convert 173 Decimal to Octal

| Number | Divisor | Quotient | Remainder | Octal Representation |
| --- | --- | --- | --- | --- |
| 173 | 8 | 21 | 5 | 5 |
| 21 | 8 | 2 | 5 | 55 | 
| 2 | 8 | 0 | 2 | 255 |

173 Decimal is 255 Octal

#### Convert 173 Decimal to Hexadecimal

Hexadecimal has an extra step; you must convert any number > 9 to its letter representation.

Convert 173 to Hexadecimal

| Number | Divisor | Quotient | Remainder | Hexadecimal Representation |
| --- | --- | --- | --- | --- |
| 173 | 16 | 10 | 13 | D |
| 10 | 16 | 0 | 10 | AD |

173 Decimal is AD Hexadecimal

### Octal Conversion

#### Octal to Binary

Reverse the process of going from Binary to Octal.
Convert each digit in Octal to Binary, then drop the padding left 0s.

|Binary | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Octal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

Convert 15 Octal to Binary

1. 1 5
2. 001 101

15 Octal is 1101 Binary


#### Octal to Hexadecimal

The easiest way to do this is via a 2-step process.

1. Convert from Octal to Binary
2. Convert from Binary to Hexadecimal

| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Hexadecimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B| C | D | E | F |

15 Octal is 1101 Binary
1101 Binary is D

15 Octal is D Hexadecimal

#### Octal to Decimal

1.	Start with a result of 0
2.	Remove the leftmost digit (most significant) and add it to the result
3.	If there are no more digits, stop.
4.	Otherwise, multiply the result by 8
5.	Repeat from step 2.

Convert 15 Octal to Decimal

| Number | Extracted Digit | Decimal Representation After Addition | Decimal Representation After Multiplication |
| --- | --- | --- | --- |
| 15 | 1 | 1 | 8 |
| 5 | 5 | 13 | DONE |

15 Octal is 13 Decimal

### Hexadecimal Conversion

#### Hexadecimal to Binary

Similar to converting from Binary to Hexadecimal, take the groups of 4 bits and, from right to left, convert to the appropriate digit.

| Hexadecimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B| C | D | E | F |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |

Convert FADA Hexadecimal to Binary

1. F A D A
2. 1111 1010 1101 1010

FADA Hexadecimal is 1111101011011010 Binary

Sidenote: In Decimal, FADA is 64,218. Mentioning this here to showcase how a single number can take up a varying number of digits based on the number system it is being represented in.

#### Hexadecimal to Octal

The easiest way to perform this conversion is to first convert the Hexadecimal to Binary, then from Binary to Octal.

From the previous example we have the Binary representation of FADA Hexadecimal.

1111101011011010

Following the Binary to Octal algorithm:

|Binary | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Octal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

1.	Group the digits into sets of 3 from the right, padding left with 0s if necessary.
- 1111101011011010 -> 001 111 101 011 011 010
2.	Read right to left, treating each group separately from the others and calculate the correct digit conversion.
- 010 -> 2
- 011 -> 3
- 011 -> 3
- 101 -> 5
- 111 -> 7
- 001 -> 1

1111101011011010 Binary is 175332 Octal

#### Hexadecimal to Decimal

1. Convert the letters to their decimal counterparts.
2. From right to left, multiply each value by 16^n, where n is the distance from the right starting with 0.
3. Sum the values to get the Decimal representation of the original number.

Convert FADA to Decimal

1. Convert the letters to their decimal counterparts.
- FADA becomes 15 10 13 10
2. From right to left, multiply each value by 16^n, where n is the distance from the right starting with 0.
- (15 * 16^3) (10 * 16^2) (13 * 16^1) (10 * 16^0)
- 61,440 2,560 208 10
3. Sum the values to get the Decimal representation of the original number.
- 61,440 + 2,560 + 208 + 10 = 64,218

FADA Hexadecimal is 64,218 Decimal

## Number System Exercises

:white_check_mark: Question 1. For each of the number systems discussed, how many unique values can be represented by 4 digits from that system?
1. Binary
2. Octal
3. Decimal
4. Hexadecimal

:white_check_mark: Question 2. Convert 74F8E9DA Hexadecimal to Decimal.

:white_check_mark: Question 3. Convert 11011010101 Binary to Hexadecimal.

:white_check_mark: Question 4. Convert 726354 Octal to Hexadecimal.

:white_check_mark: Question 5. Convert 128,472,481 Decimal to Octal.

# Part 2. Conditionals [50 minutes]
Branching statements are among some of the core concepts available in almost every modern programming language. They come in varying forms depending on the language you work with. To focus on C++ syntax specifically, there are four main types of branching statements availble in C++, the `if` statement, the `if/else if/else` statement, the `in-line if`, and the `switch` statement. The following are examples of syntax for each of the above.

```c++
/** The if statement
 * The if statement is the simplest of branching options. It allows for the testing of 
 * a conditional within parentheses and executing a set of statements if the condtional
 * evaluates to true. It should also be noted that the curly braces are optional, 
 * though if omitted the if statement will execute the next line after it if the 
 * conditional was true.
 */
if(<condition>) {
    // statements to execute if condition is true
}
``` 

```c++
/** The if/else if/else statement
 * The if/else if/else statement is the logical next step in complexity. It allows for 
 * testing a series of conditionals and executing a set of statements based on which
 * conditional was true. Any number of else if blocks can follow the if, and any 
 * combination of the (if, else if, and else) are valid in C++.
 * The first conditional to evaluate as true is the only one 
 * that will execute, and if none of the ifs or else ifs are true, then the statements 
 * in the else section will execute. 
 */
if(<condition>) {
    // statements to execute if condition is true
}
else if(<condition2>) {
    // statements to execute if condition2 is true
}
else {
    // statements to execute if neither condition nor condition2 is true
}
``` 

```c++
/** The switch statement 
* The switch statement is particularly useful when you have a large amount of possible 
* values to test, and executing statements based on which was true. Switches are unique
* as as soon as a case evaluates to true all cases that follow it will also execute  
* their statements unless a break is included.
*/
switch(<value>) {
    case <desired value>: 
        // statements to be executed if value == desired value
        break;
    case <desired value2>: 
        // statements to be executed if value == desired value2
        break;
    case <desired value3>: 
        // statements to be executed if value == desired value3
        break;
    default: 
        // statements to execute if none of the above cases were true
}
```

```c++
/** The in-line if
 * The in-line if is a statement that allows the functionality of an if statement
 * to be written on a single line.
 */
(<condition>) ? <statement if condition is true> : <statement if condition is false>;
```

## 2.1. Debugging
With the introduction of branching we are also introducing your first opportunity to make semantic errors in your code, that is to say bugs. Debugging is a vital step of programming and being able to identify errors as you make them can help to prevent hours of searching later. The following examples of code will all contain errors in some capacity, do your best to determine what that error is, what it will cause the code to do, and how to fix it.

:white_check_mark: Question 1.
```c++
#inclde <iostream>
int main() {
    int test = 0;

    if(test = 10) {
        std::cout << "Hello World" << std::endl;
    }
    else {
        std::cout << "foo bar" << std::endl;
    }
    return 0;
}
```

:white_check_mark: Question 2.
```c++
#inclde <iostream>
int main() {
    int test = 0;

    if test == 10 {
        std::cout << "Hello World" << std::endl;
    }
    else {
        std::cout << "foo bar" << std::endl;
    }
    return 0;
}
```

:white_check_mark: Question 3.
```c++
#inclde <iostream>
int main() {
    int test = 0;

    if (test == 0) 
        std::cout << "Hello World" << std::endl;
        std::cout << "Hello World2" << std::endl;
    else {
        std::cout << "foo bar" << std::endl;
    }
    return 0;
}
```

## 2.2. Programming Portion
<!--- simple branching / switch problem --->
:white_check_mark: Question 4. Implement an algorithm using C++ that outputs the letter grade to a number grade. You can use a typical grade scheme found [here](https://pages.collegeboard.org/how-to-convert-gpa-4.0-scale).

<!--- forced if/elif/else --->
:white_check_mark: Question 5. Implement an algorithm using C++ to detect a speeding car, given that the speed limit is 50 mph. This algorithm should have three possible outputs, "Safe" for any speed below the limit, "Pushing your luck" for any speed in the range [50-55]mph, and "Speeding" for any speed greater than 55. 

<!--- simple branching --->
:white_check_mark: Question 6. Implement an algorithm using C++ to determine if a number is prime. This algorithm should have two possible outputs, "Prime" if a number is prime, "Not Prime" otherwise.

<!--- branching with chars --->
:white_check_mark: Question 7. Implement an algorithm using C++ to determine if a given letter is capitalized or not. This algorithm should have two possible outputs, "Upper Case" if a letter is capital, "Lower Case" otherwise.

<!--- when to not use if/elif/else --->
:white_check_mark: Question 8. Implement an algorithm using C++ to implement the following rules. Note that a single entry can trigger multiple rules.
* Output 1 if the number is even.
* Output 2 if the number is odd.
* Output 3 if the number is evenly divisible by 2.
* Output 4 if the number is evenly divisible by 3.

Examples: 
* If 6 is entered, the program would output "134"
* If 9 is entered, the program would output "24"

<!--- Different conditional tests (!=, && ||) --->
:white_check_mark: Question 9. Implement an algorithm in C++ to test if a number is within a range given by the user, using a single if statement. This should take three values from the user those being (in order) the lower bound on the range, the upper bound on the range, and then the number to be tested.
```c++
std::cin >> low >> high >> test;
// implement a test for [low <= test <= high]
```

:white_check_mark: Question 10. Implement an algorithm in C++ to print the maximum of three given numbers. This should take three values from the user (in any order) and print out the largest of the three.

# Part 5. Submission [5 minutes]

Each group will submit a text file named `lab-03.txt` and all of your.cpp files containing all your answers and programs to the lab problems in a lab03.zip on [Gradescope](http://gradescope.com). Instructions to download your `lab-03.txt` file can be found in the IDE introduction page that you read earlier in the lab. For your convenience, that page is relinked [here](https://cs50.readthedocs.io/ide/online/).
