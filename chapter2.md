- [Functions](#functions)
  - [Expressions and statements](#expressions-and-statements)
  - [Bindings](#bindings)
  - [Binding names](#binding-names)
  - [The environment](#the-environment)
  - [Functions](#functions-1)
  - [Return values](#return-values)
  - [Control flow](#control-flow)
  - [Indenting Code](#indenting-code)
  - [For loops](#for-loops)
  - [Switch statements](#switch-statements)
  - [Capitalization](#capitalization)
  - [Comments](#comments)
  - [Summary](#summary)

# Functions
>And my heart glows bright red under my filmy, translucent skin and they have to administer 10cc of JavaScript to get me to come back. (I respond well to toxins in the blood.) Man, that stuff will kick the peaches right out your gills!

--why, Why's (Poignant) Guide to Ruby

## Expressions and statements
What is an expression?
>A fragment of code that produces a value is called an expression. Every value that is written literally (such as 22 or "psychoanalysis") is an expression. An expression between parentheses is also an expression, as is a binary operator applied to two expressions or a unary operator applied to one.

>This shows part of the beauty of a language-based interface. Expressions can contain other expressions in a way similar to how subsentences in human languages are nested—a subsentence can contain its own subsentences, and so on.

What is a statement?
>If an expression corresponds to a sentence fragment, a JavaScript statement corresponds to a full sentence. A program is a list of statements. The simplest kind of statement is an expression with a semicolon after it. This is a program:
```
1;
!false;
```

When use semicolons? Always!
>In some cases, JavaScript allows you to omit the semicolon at the end of a statement. In other cases, it has to be there, or the next line will be treated as part of the same statement. The rules for when it can be safely omitted are somewhat complex and error-prone. So in this book, every statement that needs a semicolon will always get one.

## Bindings
What are bindings or variables?
>To catch and hold values, JavaScript provides a thing called a binding, or variable:
```
let caught = 5 * 5;
```

How to use bindings?
>After a binding has been defined, its name can be used as an expression. The value of such an expression is the value the binding currently holds. Here’s an example:
```
let ten = 10;
console.log(ten * ten);
// → 100
```

What is mutability of variables in JS?
>When a binding points at a value, that does not mean it is tied to that value forever. The = operator can be used at any time on existing bindings to disconnect them from their current value and have them point to a new one.
>You should imagine bindings as tentacles, rather than boxes. They do not contain values; they grasp them—two bindings can refer to the same value. A program can access only the values that it still has a reference to. When you need to remember something, you grow a tentacle to hold on to it or you reattach one of your existing tentacles to it.

What happens, when we don't assign a value to a new variable?
>When you define a binding without giving it a value, the tentacle has nothing to grasp, so it ends in thin air. If you ask for the value of an empty binding, you’ll get the value undefined.

Multiple bindings
>A single let statement may define multiple bindings. The definitions must be separated by commas.
```
let one = 1, two = 2;
console.log(one + two);
// → 3
```

var vs let vs const
>The words var and const can also be used to create bindings, in a way similar to let. The first, var (short for “variable”), is the way bindings were declared in pre-2015 JavaScript. The word const stands for constant. It defines a constant binding, which points at the same value for as long as it lives. This is useful for bindings that give a name to a value so that you can easily refer to it later.

## Binding names
What are the possible names for a binding?
>Binding names can be any word. Digits can be part of binding names—catch22 is a valid name, for example—but the name must not start with a digit. A binding name may include dollar signs ($) or underscores (_) but no other punctuation or special characters.
>Words with a special meaning, such as let, are keywords, and they may not be used as binding names. There are also a number of words that are “reserved for use” in future versions of JavaScript, which also can’t be used as binding names. The full list of keywords and reserved words is rather long.

>break case catch class const continue debugger default
delete do else enum export extends false finally for
function if implements import interface in instanceof let
new package private protected public return static super
switch this throw true try typeof var void while with yield


## The environment
What is an environment?
>The collection of bindings and their values that exist at a given time is called the environment. When a program starts up, this environment is not empty. It always contains bindings that are part of the language standard, and most of the time, it also has bindings that provide ways to interact with the surrounding system. For example, in a browser, there are functions to interact with the currently loaded website and to read mouse and keyboard input.


## Functions
What is a function in JS?
>A function is a piece of program wrapped in a value. Such values can be applied in order to run the wrapped program. For example, in a browser environment, the binding prompt holds a function that shows a little dialog box asking for user input. Executing a function is called **invoking**, **calling**, or **applying** it. Values given to functions are called **arguments**.


## Return values
What is a return value?
>When a function produces a value, it is said to **return** that value. Anything that produces a value is an **expression** in JavaScript, which means function calls can be used within larger expressions.

## Control flow
What are conditional statements?
>Conditional execution is created with the if keyword in JavaScript. The statement after the if is wrapped in *braces* ({ and }) in this example. The braces can be used to group any number of statements into a single statement, called a **block**. If you have more than two paths to choose from, you can “chain” multiple if/else pairs together. 

Why do we need looping?
>If we needed all even numbers less than 1,000, printing them manually one by one would be unworkable. What we need is a way to run a piece of code multiple times. This form of control flow is called a **loop**. Looping control flow allows us to go back to some point in the program where we were before and repeat it with our current program state.

What are while/do loops?
>A statement starting with the keyword while creates a loop. The word while is followed by an expression in parentheses and then a statement, much like if.
```
let result = 1;
let counter = 0;
while (counter < 10) {
  result = result * 2;
  counter = counter + 1;
}
console.log(result);
// → 1024
```
>A do loop is a control structure similar to a while loop. It differs only on one point: a do loop always executes its body at least once, and it starts testing whether it should stop only after that first execution. To reflect this, the test appears after the body of the loop.
```
let yourName;
do {
  yourName = prompt("Who are you?");
} while (!yourName);
console.log(yourName);
```

## Indenting Code
What is code indentation?
>In code where new blocks are opened inside other blocks, it can become hard to see where one block ends and another begins. With proper indentation, the visual shape of a program corresponds to the shape of the blocks inside it. I like to use two spaces for every open block, but tastes differ—some people use four spaces, and some people use tab characters. The important thing is that each new block adds the same amount of space.
```
if (false != true) {
  console.log("That makes sense.");
  if (1 < 2) {
    console.log("No surprise there.");
  }
}
```

## For loops
How to write for loops in JS? What are the break/continue keywords?
```
for (let number = 0; number <= 12; number = number + 2) {
  console.log(number);
}
// → 0
// → 2
//   … etcetera
```
>There is a special statement called break that has the effect of immediately jumping out of the enclosing loop.
```
for (let current = 20; ; current = current + 1) {
  if (current % 7 == 0) {
    console.log(current);
    break;
  }
}
// → 21
```
>The for construct in the example does not have a part that checks for the end of the loop. This means that the loop will never stop unless the break statement inside is executed.
>The continue keyword is similar to break, in that it influences the progress of a loop. When continue is encountered in a loop body, control jumps out of the body and continues with the loop’s next iteration.

## Switch statements

>It is not uncommon for code to look like this:
```
if (x == "value1") action1();
else if (x == "value2") action2();
else if (x == "value3") action3();
else defaultAction();
```
>Here the switch version of it
```
switch (prompt("What is the weather like?")) {
  case "rainy":
    console.log("Remember to bring an umbrella.");
    break;
  case "sunny":
    console.log("Dress lightly.");
  case "cloudy":
    console.log("Go outside.");
    break;
  default:
    console.log("Unknown weather type!");
    break;
}
```

## Capitalization 
>Binding names may not contain spaces, yet it is often helpful to use multiple words to clearly describe what the binding represents.
```
fuzzylittleturtle
fuzzy_little_turtle
FuzzyLittleTurtle
fuzzyLittleTurtle
```
>The standard JavaScript functions, and most JavaScript programmers, follow the bottom style—they capitalize every word except the first. It is not hard to get used to little things like that, and code with mixed naming styles can be jarring to read, so we follow this convention.

## Comments
>A comment is a piece of text that is part of a program but is completely ignored by the computer. JavaScript has two ways of writing comments. To write a single-line comment, you can use two slash characters (//) and then the comment text after it.
>A section of text between /* and */ will be ignored in its entirety, regardless of whether it contains line breaks. This is useful for adding blocks of information about a file or a chunk of program.

## Summary
>You now know that a program is built out of statements, which themselves sometimes contain more statements. Statements tend to contain expressions, which themselves can be built out of smaller expressions.
>Putting statements after one another gives you a program that is executed from top to bottom. You can introduce disturbances in the flow of control by using conditional (if, else, and switch) and looping (while, do, and for) statements.

>Bindings can be used to file pieces of data under a name, and they are useful for tracking state in your program. The environment is the set of bindings that are defined. JavaScript systems always put a number of useful standard bindings into your environment.

>Functions are special values that encapsulate a piece of program. You can invoke them by writing functionName(argument1, argument2). Such a function call is an expression and may produce a value.