- [Values, Types, and Operators](#values-types-and-operators)
  - [Precision and Arithmetic](#precision-and-arithmetic)
  - [Special numbers](#special-numbers)
  - [Strings](#strings)
  - [Summary](#summary)

# Values, Types, and Operators
 >Below the surface of the machine, the program moves. Without effort, it expands and contracts. In great harmony, electrons scatter and regroup. The forms on the monitor are but ripples on the water. The essence stays invisibly below.

 --Master Yuan-Ma, The Book of Programming

What is data?
>Inside the computer’s world, there is only data. You can read data, modify data, create new data—but that which isn’t data cannot be mentioned. All this data is stored as long sequences of bits and is thus fundamentally alike.

What are JS's limitations in dealing with data?
>JavaScript uses a fixed number of bits, 64 of them, to store a single number value. There are only so many patterns you can make with 64 bits, which means that the number of different numbers that can be represented is limited.

## Precision and Arithmetic 
How different are integers and fractions handled in JS?
>Calculations with whole numbers (also called integers) smaller than the aforementioned 9 quadrillion are guaranteed to always be precise. Unfortunately, calculations with fractional numbers are generally not. Just as π (pi) cannot be precisely expressed by a finite number of decimal digits, many numbers lose some precision when only 64 bits are available to store them.

What are operators and what's their precedence?
>Arithmetic operations such as addition or multiplication take two number values and produce a new number from them. For example 100 + 4 * 11. The + and * symbols are called **operators**. When operators appear together without parentheses, the order in which they are applied is determined by the **precedence** of the operators.

## Special numbers
What are some special numbers in JS
>The first two are **Infinity** and **-Infinity**, which represent the positive and negative infinities.
>**NaN** stands for “not a number”, even though it is a value of the number type. You’ll get this result when you, for example, try to calculate 0 / 0 (zero divided by zero), Infinity - Infinity, or any number of other numeric operations that don’t yield a meaningful result.

## Strings
What are strings in JS?
>Strings are used to represent text. They are written by enclosing their content in quotes. "Hello, world"

>You can use single quotes, double quotes, or backticks to mark strings, as long as the quotes at the start and the end of the string match.

>Almost anything can be put between quotes, and JavaScript will make a string value out of it. But a few characters are more difficult. You can imagine how putting quotes between quotes might be hard. Newlines (the characters you get when you press enter) can be included without escaping only when the string is quoted with backticks (`).

What is an escape symbol and what's it used for?
>To make it possible to include such characters in a string, the following notation is used: whenever a backslash (\) is found inside quoted text, it indicates that the character after it has a special meaning. This is called **escaping** the character.

What is concatenation?
>Strings cannot be divided, multiplied, or subtracted, but the + operator can be used on them. It does not add, but it **concatenates—it** glues two strings together. The following line will produce the string "concatenate":
```
"con" + "cat" + "e" + "nate"
```

>Strings written with single or double quotes behave very much the same—the only difference is in which type of quote you need to escape inside of them. Backtick-quoted strings, usually called template literals, can do a few more tricks. Apart from being able to span lines, they can also embed other values.When you write something inside ${} in a template literal, its result will be computed, converted to a string, and included at that position. The example produces “half of 100 is 50”.

```
`half of 100 is ${100 / 2}`
````

## Unary operators
What are unary operators?
>Not all operators are symbols. Some are written as words. One example is the typeof operator, which produces a string value naming the type of the value you give it.

```
console.log(typeof 4.5)
// → number
```

>The other operators shown all operated on two values, but typeof takes only one. Operators that use two values are called **binary** operators, while those that take one are called **unary** operators. The minus operator can be used both as a binary operator and as a unary operator.

## Boolean values

```
console.log(3 > 2)
// → true
```
How are strings compared?
>Strings can be compared in the same way.
The way strings are ordered is roughly alphabetic but not really what you’d expect to see in a dictionary: uppercase letters are always “less” than lowercase ones, so "Z" < "a", and nonalphabetic characters (!, -, and so on) are also included in the ordering. When comparing strings, JavaScript goes over the characters from left to right, comparing the Unicode codes one by one.

```
console.log("Aardvark" < "Zoroaster")
// → true
```
What is a value that is not equal to itself?
>There is only one value in JavaScript that is not equal to itself, and that is NaN (“not a number”).
NaN is supposed to denote the result of a nonsensical computation, and as such, it isn’t equal to the result of any other nonsensical computations.


```
console.log(NaN == NaN)
// → false

```

## Logical operators
Explain the || && ! operators.
>There are also some operations that can be applied to Boolean values themselves. JavaScript supports three logical operators: and, or, and not. These can be used to “reason” about Booleans.
>The && operator represents logical and. The || operator denotes logical or. Not is written as an exclamation mark (!) 
>In practice, you can usually get by with knowing that of the operators we have seen so far, || has the lowest precedence, then comes &&, then the comparison operators (>, ==, and so on), and then the rest.

What is a conditional operator?
>This one is called the conditional operator (or sometimes just the ternary operator since it is the only such operator in the language). The value on the left of the question mark “picks” which of the other two values will come out. When it is true, it chooses the middle value, and when it is false, it chooses the value on the right.

```
console.log(true ? 1 : 2);
// → 1
```

## Empty values
What are empty values?
>There are two special values, written null and undefined, that are used to denote the absence of a meaningful value. They are themselves values, but they carry no information.

>Many operations in the language that don’t produce a meaningful value (you’ll see some later) yield undefined simply because they have to yield some value.

>In most cases, it just tries to convert one of the values to the other value’s type. However, when null or undefined occurs on either side of the operator, it produces true only if both sides are one of null or undefined.

```
console.log(null == undefined);
// → true
console.log(null == 0);
// → false
```

How to check for a real value of an expression?
>That behavior is often useful. When you want to test whether a value has a real value instead of null or undefined, you can compare it to null with the == (or !=) operator.

>When you do not want any type conversions to happen, there are two additional operators: **===** and **!==.** The first tests whether a value is precisely equal to the other, and the second tests whether it is not precisely equal. So "" === false is false as expected.

## Short-circuiting of logical operators

>The || operator, for example, will return the value to its left when that can be converted to true and will return the value on its right otherwise. This has the expected effect when the values are Boolean and does something analogous for values of other types.

Explain default values and how they are implemented.
```
console.log(null || "user")
// → user
console.log("Agnes" || "user")
// → Agnes
```

>We can use this functionality as a way to fall back on a default value. If you have a value that might be empty, you can put || after it with a replacement value.

> The rules for converting strings and numbers to Boolean values state that 0, NaN, and the empty string ("") count as false, while all the other values count as true. So 0 || -1 produces -1, and "" || "!?" yields "!?".

>The && operator works similarly but the other way around. When the value to its left is something that converts to false, it returns that value, and otherwise it returns the value on its right.

>Another important property of these two operators is that the part to their right is evaluated only when necessary. In the case of true || X, no matter what X is—even if it’s a piece of program that does something terrible—the result will be true, and X is never evaluated. The same goes for false && X, which is false and will ignore X. This is called short-circuit evaluation.

## Summary
>We looked at four types of JavaScript values in this chapter: numbers, strings, Booleans, and undefined values.
>Such values are created by typing in their name (true, null) or value (13, "abc"). You can combine and transform values with operators. We saw binary operators for arithmetic (+, -, *, /, and %), string concatenation (+), comparison (==, !=, ===, !==, <, >, <=, >=), and logic (&&, ||), as well as several unary operators (- to negate a number, ! to negate logically, and typeof to find a value’s type) and a ternary operator (?:) to pick one of two values based on a third value.

