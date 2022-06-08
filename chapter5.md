
- [Higher-Order Functions](#higher-order-functions)
  - [Abstraction](#abstraction)
  - [Abstracting repetition](#abstracting-repetition)
  - [Higher-order functions](#higher-order-functions-1)
  - [Filtering arrays](#filtering-arrays)
  - [Transforming with map](#transforming-with-map)
  - [Summarizing with reduce](#summarizing-with-reduce)
  - [Composability](#composability)
  - [Strings and character codes](#strings-and-character-codes)
  - [Recognizing text](#recognizing-text)
  - [Summary](#summary)

# Higher-Order Functions
>Tzu-li and Tzu-ssu were boasting about the size of their latest programs. ‘Two-hundred thousand lines,’ said Tzu-li, ‘not counting comments!’ Tzu-ssu responded, ‘Pssh, mine is almost a million lines already.’ Master Yuan-Ma said, ‘My best program has five hundred lines.’ Hearing this, Tzu-li and Tzu-ssu were enlightened.

--Master Yuan-Ma, The Book of Programming

>There are two ways of constructing a software design: One way is to make it so simple that there are obviously no deficiencies, and the other way is to make it so complicated that there are no obvious deficiencies.

--C.A.R. Hoare, 1980 ACM Turing Award Lecture
  
>A large program is a costly program, and not just because of the time it takes to build. Size almost always involves complexity, and complexity confuses programmers. Confused programmers, in turn, introduce mistakes (bugs) into programs. A large program then provides a lot of space for these bugs to hide, making them hard to find.

Same functionality
```
let total = 0, count = 1;
while (count <= 10) {
  total += count;
  count += 1;
}
console.log(total);
```
```
console.log(sum(range(1, 10)));
```
>The definitions of this vocabulary (the functions sum and range) will still involve loops, counters, and other incidental details. But because they are expressing simpler concepts than the program as a whole, they are easier to get right.


## Abstraction
>In the context of programming, these kinds of vocabularies are usually called **abstractions**. Abstractions hide details and give us the ability to talk about problems at a higher (or more abstract) level.

As an analogy, compare these two recipes for pea soup. The first one goes like this:
>Put 1 cup of dried peas per person into a container. Add water until the peas are well covered. Leave the peas in water for at least 12 hours. Take the peas out of the water and put them in a cooking pan. Add 4 cups of water per person. Cover the pan and keep the peas simmering for two hours. Take half an onion per person. Cut it into pieces with a knife. Add it to the peas. Take a stalk of celery per person. Cut it into pieces with a knife. Add it to the peas. Take a carrot per person. Cut it into pieces. With a knife! Add it to the peas. Cook for 10 more minutes.
And this is the second recipe:
>Per person: 1 cup dried split peas, half a chopped onion, a stalk of celery, and a carrot. Soak peas for 12 hours. Simmer for 2 hours in 4 cups of water (per person). Chop and add vegetables. Cook for 10 more minutes.
>The second is shorter and easier to interpret. But you do need to understand a few more cooking-related words such as soak, simmer, chop, and, I guess, vegetable.

## Abstracting repetition
>Since “doing something” can be represented as a function and functions are just values, we can pass our action as a function value.
```
function repeat(n, action) {
  for (let i = 0; i < n; i++) {
    action(i);
  }
}
repeat(3, console.log);
// → 0
// → 1
// → 2
```
>We don’t have to pass a predefined function to repeat. Often, it is easier to create a function value on the spot instead.
```
let labels = [];
repeat(5, i => {
  labels.push(`Unit ${i + 1}`);
});
console.log(labels);
// → ["Unit 1", "Unit 2", "Unit 3", "Unit 4", "Unit 5"]
```

## Higher-order functions
>Functions that operate on other functions, either by taking them as arguments or by returning them, are called higher-order functions. Since we have already seen that functions are regular values, there is nothing particularly remarkable about the fact that such functions exist. 
What is a factory function?
```
function greaterThan(n) {
  return m => m > n;
}
let greaterThan10 = greaterThan(10);
console.log(greaterThan10(11));
// → true
```

How to change another function using a higher-order function?
```
function noisy(f) {
  return (...args) => {
    console.log("calling with", args);
    let result = f(...args);
    console.log("called with", args, ", returned", result);
    return result;
  };
}
noisy(Math.min)(3, 2, 1);
// → calling with [3, 2, 1]
// → called with [3, 2, 1] , returned 1
```

## Filtering arrays
>To find the scripts in the data set that are still in use, the following function might be helpful. It filters out the elements in an array that don’t pass a test.
```
function filter(array, test) {
  let passed = [];
  for (let element of array) {
    if (test(element)) {
      passed.push(element);
    }
  }
  return passed;
}

console.log(filter(SCRIPTS, script => script.living));
// → [{name: "Adlam", …}, …]
```
>Note how the filter function, rather than deleting elements from the existing array, builds up a new array with only the elements that pass the test. This function is pure. It does not modify the array it is given.

## Transforming with map
>The map method transforms an array by applying a function to all of its elements and building a new array from the returned values. The new array will have the same length as the input array, but its content will have been mapped to a new form by the function.
```
function map(array, transform) {
  let mapped = [];
  for (let element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}

let rtlScripts = SCRIPTS.filter(s => s.direction == "rtl");
console.log(map(rtlScripts, s => s.name));
// → ["Adlam", "Arabic", "Imperial Aramaic", …]
```

## Summarizing with reduce
>Another common thing to do with arrays is to compute a single value from them. Our recurring example, summing a collection of numbers, is an instance of this. Another example is finding the script with the most characters. The higher-order operation that represents this pattern is called reduce (sometimes also called fold). It builds a value by repeatedly taking a single element from the array and combining it with the current value. When summing numbers, you’d start with the number zero and, for each element, add that to the sum.

```
function reduce(array, combine, start) {
  let current = start;
  for (let element of array) {
    current = combine(current, element);
  }
  return current;
}

console.log(reduce([1, 2, 3, 4], (a, b) => a + b, 0));
// → 10
```

## Composability
>Higher-order functions start to shine when you need to compose operations. As an example, let’s write code that finds the average year of origin for living and dead scripts in the data set.
```
function average(array) {
  return array.reduce((a, b) => a + b) / array.length;
}

console.log(Math.round(average(
  SCRIPTS.filter(s => s.living).map(s => s.year))));
// → 1165
console.log(Math.round(average(
  SCRIPTS.filter(s => !s.living).map(s => s.year))));
// → 204
```
How does abstraction affect program's performance?
>You can usually afford the readable approach, but if you’re processing huge arrays, and doing so many times, the less abstract style might be worth the extra speed.

## Strings and character codes
What is UTF-16?
>In Chapter 1 I mentioned that JavaScript strings are encoded as a sequence of 16-bit numbers. These are called code units. A Unicode character code was initially supposed to fit within such a unit (which gives you a little over 65,000 characters). When it became clear that wasn’t going to be enough, many people balked at the need to use more memory per character. To address these concerns, **UTF-16**, the format used by JavaScript strings, was invented. It describes most common characters using a single 16-bit code unit but uses a pair of two such units for others.
>UTF-16 is generally considered a bad idea today. It seems almost intentionally designed to invite mistakes. It’s easy to write programs that pretend code units and characters are the same thing. And if your language doesn’t use two-unit characters, that will appear to work just fine. 

## Recognizing text
Difference between indexOf() and findIndex() array methods.
>It uses another array method—findIndex. This method is somewhat like indexOf, but instead of looking for a specific value, it finds the first value for which the given function returns true. Like indexOf, it returns -1 when no such element is found.

```
function countBy(items, groupName) {
  let counts = [];
  for (let item of items) {
    let name = groupName(item);
    let known = counts.findIndex(c => c.name == name);
    if (known == -1) {
      counts.push({name, count: 1});
    } else {
      counts[known].count++;
    }
  }
  return counts;
}

console.log(countBy([1, 2, 3, 4, 5], n => n > 2));
// → [{name: false, count: 2}, {name: true, count: 3}]
```
## Summary
>Being able to pass function values to other functions is a deeply useful aspect of JavaScript. It allows us to write functions that model computations with “gaps” in them. The code that calls these functions can fill in the gaps by providing function values.

>Arrays provide a number of useful higher-order methods. You can use forEach to loop over the elements in an array. The filter method returns a new array containing only the elements that pass the predicate function. Transforming an array by putting each element through a function is done with map. You can use reduce to combine all the elements in an array into a single value. The some method tests whether any element matches a given predicate function. And findIndex finds the position of the first element that matches a predicate.