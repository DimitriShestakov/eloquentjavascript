- [Data Structures: Objects and Arrays](#data-structures-objects-and-arrays)
  - [Properties](#properties)
  - [Methods](#methods)
  - [Objects](#objects)
  - [Mutability](#mutability)
  - [Array loops](#array-loops)
  - [Further arrayology](#further-arrayology)
  - [Strings and their properties](#strings-and-their-properties)
  - [Rest parameters](#rest-parameters)
  - [The Math object](#the-math-object)
  - [Destructuring](#destructuring)
  - [JSON](#json)
- [Summary](#summary)

# Data Structures: Objects and Arrays

>On two occasions I have been asked, ‘Pray, Mr. Babbage, if you put into the machine wrong figures, will the right answers come out?’ [...] I am not able rightly to apprehend the kind of confusion of ideas that could provoke such a question.

-- Charles Babbage, Passages from the Life of a Philosopher (1864)

>Numbers, Booleans, and strings are the atoms that data structures are built from. Many types of information require more than one atom, though. Objects allow us to group values—including other objects—to build more complex structures.

```
let listOfNumbers = [2, 3, 5, 7, 11];
console.log(listOfNumbers[2]);
// → 5
```
## Properties
What objects in JS don't have properties?
>null and undefined 

How to access a property of an object? 2 ways
>The two main ways to access properties in JavaScript are with a dot and with square brackets. Both value.x and value[x] access a property on value—but not necessarily the same property. 

What's the difference?
>When using a dot, the word after the dot is the literal name of the property. When using square brackets, the expression between the brackets is **evaluated** to get the property name. Whereas value.x fetches the property of value named “x”, value[x] tries to evaluate the expression x and uses the result, converted to a string, as the property name.

What are possible property names?
>Property names are strings. They can be any string, but the dot notation works only with names that look like valid binding names. So if you want to access a property named 2 or John Doe, you must use square brackets: value[2] or value["John Doe"]. The elements in an array are stored as the array’s properties, using numbers as property names.

## Methods
What are methods?
>Both string and array values contain, in addition to the length property, a number of properties that hold function values.
>Properties that contain functions are generally called methods of the value they belong to, as in “toUpperCase is a method of a string”.

## Objects
What are objects?
>Values of the type **object** are arbitrary collections of **properties**. One way to create an object is by using braces as an expression.
```
let day1 = {
  squirrel: false,
  events: ["work", "touched tree", "pizza", "running"],
  "touched tree": "Touched a tree"

};
console.log(day1.squirrel);
// → false
console.log(day1.wolf);
// → undefined
day1.wolf = false;
console.log(day1.wolf);
// → false
```
What is the use of a **delete** and **in** operators?
>The delete operator cuts off a tentacle from such an octopus. It is a unary operator that, when applied to an object property, will remove the named property from the object. This is not a common thing to do, but it is possible.
```
let anObject = {left: 1, right: 2};
console.log(anObject.left);
// → 1
delete anObject.left;
console.log(anObject.left);
// → undefined
console.log("left" in anObject);
// → false
console.log("right" in anObject);
// → true
```
>The difference between setting a property to undefined and actually deleting it is that, in the first case, the object still has the property (it just doesn’t have a very interesting value), whereas in the second case the property is no longer present and in will return false.

How to find what properties an object has?
```
console.log(Object.keys({x: 0, y: 0, z: 2}));
// → ["x", "y", "z"]
```

How to copy all properties from one object into another?
```
let objectA = {a: 1, b: 2};
Object.assign(objectA, {b: 3, c: 4});
console.log(objectA);
// → {a: 1, b: 3, c: 4}
```

## Mutability
What is identity of an object?
>With objects, there is a difference between having two references to the same object and having two different objects that contain the same properties. Consider the following code:

let object1 = {value: 10};
let object2 = object1;
let object3 = {value: 10};

```
console.log(object1 == object2);
// → true
console.log(object1 == object3);
// → false

object1.value = 15;
console.log(object2.value);
// → 15
console.log(object3.value);
// → 10
```
>The object1 and object2 bindings grasp the same object, which is why changing object1 also changes the value of object2. They are said to have the same **identity**. The binding object3 points to a different object, which initially contains the same properties as object1 but lives a separate life.

## Array loops
A very common action for an array
```
for (let i = 0; i < JOURNAL.length; i++) {
  let entry = JOURNAL[i];
  // Do something with entry
}
```
Can be simplified with newer syntax
```
for (let entry of JOURNAL) {
  console.log(`${entry.events.length} events.`);
}
```
>When a for loop looks like this, with the word of after a variable definition, it will loop over the elements of the value given after of. This works not only for arrays but also for strings and some other data structures.

## Further arrayology
>We saw **push** and **pop**, which add and remove elements at the end of an array, earlier in this chapter. The corresponding methods for adding and removing things at the start of an array are called **unshift** and **shift**.
>To search for a specific value, arrays provide an **indexOf** method. To search from the end instead of the start, there’s a similar method called **lastIndexOf**.
>Another fundamental array method is **slice**, which takes start and end indices and returns an array that has only the elements between them. The start index is inclusive, the end index exclusive. When the end index is not given, slice will take all of the elements after the start index. You can also omit the start index to copy the entire array.
>The **concat** method can be used to glue arrays together to create a new array, similar to what the + operator does for strings.

How to write a function that removes a specific element in an array using slice and concat?
```
function remove(array, index) {
  return array.slice(0, index)
    .concat(array.slice(index + 1));
}
console.log(remove(["a", "b", "c", "d", "e"], 2));
// → ["a", "b", "d", "e"]
```
## Strings and their properties
>We can read properties like length and toUpperCase from string values. But if you try to add a new property, it doesn’t stick.
```
let kim = "Kim";
kim.age = 88;
console.log(kim.age);
// → undefined
```
>Values of type string, number, and Boolean are not objects, and though the language doesn’t complain if you try to set new properties on them, it doesn’t actually store those properties. As mentioned earlier, such values are immutable and cannot be changed.

Methods of string values.
>But these types do have built-in properties. Every string value has a number of methods. Some very useful ones are **slice** and **indexOf**, which resemble the array methods of the same name.
>The **trim** method removes whitespace (spaces, newlines, tabs, and similar characters) from the start and end of a string.
>You can split a string on every occurrence of another string with **split** and join it again with **join**.
```
let sentence = "Secretarybirds specialize in stomping";
let words = sentence.split(" ");
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join(". "));
// → Secretarybirds. specialize. in. stomping
```
>A string can be repeated with the **repeat** method, which creates a new string containing multiple copies of the original string, glued together.
 
## Rest parameters
>It can be useful for a function to accept any number of arguments. For example, Math.max computes the maximum of all the arguments it is given. To write such a function, you put three dots before the function’s last parameter, like this:
```
function max(...numbers) {
  let result = -Infinity;
  for (let number of numbers) {
    if (number > result) result = number;
  }
  return result;
}
console.log(max(4, 1, 9, -2));
// → 9
```
>When such a function is called, the rest parameter is bound to an array containing all further arguments. 

How to spread an array into its members?
>You can use a similar three-dot notation to call a function with an array of arguments.
```
let numbers = [5, 1, 7];
console.log(max(...numbers));
// → 7
```
>This “spreads” out the array into the function call, passing its elements as separate arguments. It is possible to include an array like that along with other arguments, as in max(9, ...numbers, 2).

How to spread an array into a new array with additional members?
```
let words = ["never", "fully"];
console.log(["will", ...words, "understand"]);
// → ["will", "never", "fully", "understand"]
```

## The Math object
What is its value? What is a namespace?
>It provides a namespace so that all math functions like max, min, sqrt and values do not have to be global bindings. Having too many global bindings “pollutes” the **namespace**. The more names have been taken, the more likely you are to accidentally overwrite the value of some existing binding.

How does JS prevent us from using bindings that are already in use?
>Many languages will stop you, or at least warn you, when you are defining a binding with a name that is already taken. JavaScript does this for bindings you declared with let or const but—perversely—not for standard bindings nor for bindings declared with var or function.

How to get a random number from 0 to 9 in Java?
```
console.log(Math.floor(Math.random() * 10));
// → 2
```

## Destructuring
>Let’s go back to the phi function for a moment.
```
function phi(table) {
  return (table[3] * table[0] - table[2] * table[1]) /
    Math.sqrt((table[2] + table[3]) *
              (table[0] + table[1]) *
              (table[1] + table[3]) *
              (table[0] + table[2]));
}
```
>One of the reasons this function is awkward to read is that we have a binding pointing at our array, but we’d much prefer to have bindings for the elements of the array, that is, let n00 = table[0] and so on. Fortunately, there is a succinct way to do this in JavaScript.
```
function phi([n00, n01, n10, n11]) {
  return (n11 * n00 - n10 * n01) /
    Math.sqrt((n10 + n11) * (n00 + n01) *
              (n01 + n11) * (n00 + n10));
}
```
Where can it be used?
>This also works for bindings created with let, var, or const. If you know the value you are binding is an array, you can use square brackets to “look inside” of the value, binding its contents.
```
let {name} = {name: "Faraji", age: 23};
console.log(name);
// → Faraji
```
>Note that if you try to destructure null or undefined, you get an error, much as you would if you directly try to access a property of those values.

## JSON
What do objects actually contain?
>Because properties only grasp their value, rather than contain it, objects and arrays are stored in the computer’s memory as sequences of bits holding the addresses—the place in memory—of their contents.
>So an array with another array inside of it consists of (at least) one memory region for the inner array, and another for the outer array, containing (among other things) a binary number that represents the position of the inner array.

How do we send this data over to another device? What is JSON?
>If you want to save data in a file for later or send it to another computer over the network, you have to somehow convert these tangles of memory addresses to a description that can be stored or sent.
>What we can do is serialize the data. That means it is converted into a flat description. A popular serialization format is called JSON (pronounced “Jason”), which stands for JavaScript Object Notation. It is widely used as a data storage and communication format on the Web, even in languages other than JavaScript.

What is the difference between JSON and a normal JS object?
>JSON looks similar to JavaScript’s way of writing arrays and objects, with a few restrictions. All property names have to be surrounded by double quotes, and only simple data expressions are allowed—no function calls, bindings, or anything that involves actual computation. Comments are not allowed in JSON.
```
{
  "squirrel": false,
  "events": ["work", "touched tree", "pizza", "running"]
}
```

How to we use JSON.stringify and JSON.parse methods?
>JavaScript gives us the functions JSON.stringify and JSON.parse to convert data to and from this format. The first takes a JavaScript value and returns a JSON-encoded string. The second takes such a string and converts it to the value it encodes.
```
let string = JSON.stringify({squirrel: false,
                             events: ["weekend"]});
console.log(string);
// → {"squirrel":false,"events":["weekend"]}
console.log(JSON.parse(string).events);
// → ["weekend"]
```

# Summary
>Objects and arrays (which are a specific kind of object) provide ways to group several values into a single value. Conceptually, this allows us to put a bunch of related things in a bag and run around with the bag, instead of wrapping our arms around all of the individual things and trying to hold on to them separately.

>Most values in JavaScript have properties, the exceptions being null and undefined. Properties are accessed using value.prop or value["prop"]. Objects tend to use names for their properties and store more or less a fixed set of them. Arrays, on the other hand, usually contain varying amounts of conceptually identical values and use numbers (starting from 0) as the names of their properties.

>There are some named properties in arrays, such as length and a number of methods. Methods are functions that live in properties and (usually) act on the value they are a property of.

>You can iterate over arrays using a special kind of for loop—for (let element of array).








