# Introduction

This outline serves as an quick start to Haskell for those new to programming in general, but with some understanding of JavaScript, Ruby or Python.In this outline we will refer to JavaScript, Ruby and Python as Common Programming Languages
There will be links to various books and videos in each section. Make sure to also watch the videos to further strengthen your memory of the topic.

## Installing Haskell

Follow the steps outlined in [GHCup Getting Started](https://www.haskell.org/ghcup/install/) to install `ghc`, `runghc`, and `ghci`.

- `ghc` is a Haskell compiler that "compiles" or translates your source into a binary language computers can understand
- `runghc` is a shortcut to compile your code and then run it
- `ghci` allows you to run Haskell code interactively, similar to Python or Ruby repl

## What is Haskell

Haskell is a statically-typed, purely functional programming language with type inference and lazy evaluation.
Let's break that down:

### Statically Typed

Static Typing means that the compiler (program that translates source code into machine code) knows what are that types of all your variables and functions are during compile time. In a common programming language (JavaScript, Ruby, Python), the source code is dynamically typed, meaning that the interpreter only knows the types of your variables once they are evaluated (ran).

Example dynamically typed (JavaScript):

```javascript
// We define a new variable as empty string
let myDate = "";
// We try to create a new Date
let newDate = new Date(myDate); // Error: Invalid Date
```

A new `Date` could not be created from an empty string, the error happened when `new Date(myDate)` was evaluated.

Example statically typed (Haskell):

```haskell
-- We define a new variable as empty string
myDate :: String -- We tell Haskell that `myDate` is a String
myDate = ""
-- we try to create a new Date
newDate = UTCTime myDate -- Error: Couldn't match expected type ‘time-1.9.3:Data.Time.Calendar.Days.Day’ with actual type ‘String’
```

A new `UTCTime` could not be created from a string, this error happens at compile time, when ghc tries to translate your source code into machine code

### Immutable Data

Immutable data means that when we create a variable we can no longer change it, for example:
In JavaScript:

```js
// We define a variable
let myAge = 10;
// We change the variable
myAge = 20;
```

We can mutate (change) `myAge` as many times as we would like, since JavaScript allows mutable variables.
When we try to do the same in Haskell:

```haskell
myAge :: Int
myAge = 10
myAge = 20 -- This is not allowed `myAge` can only be defined once, and we cannot change it
```

### Declarative

Declarative means we tell the computer **what** we want to achieve, not **how** to achieve it.

Example Imperative:

```js
let p = document.createElement("p");
p.textContent = "Hello";
document.body.append(p);
```

This is an imperative way of programming, we create a `<p>` tag, and insert some text, then append it to the document body

Example Declarative:

```html
<body>
  <p>Hello</p>
</body>
```

This is an declarative way of programming, we don't specify how to create a body tag, or p tag

### Purely Functional

Pure means doing one thing, and one thing only, example: `1 + 1`, the `+` function is pure, it adds two numbers together and does nothing else.

In common programming languages we can can mix pure and impure functions together:

Example JavaScript:

```js
function addImpure(number1, number2) {
  let day = new Date().getDay();
  console.log("Todays Day Is: ", day);
  return number1 + number2;
}
// The `addImpure` function is not pure, it will add two numbers together, but also print todays Day to the console.

function addPure(number1, number2) {
  return number1 + number2;
}
// The `addPure` function is pure, it will add two numbers together and do nothing else.
```

Haskell is purely functional, you cannot have impure functions such as:

```haskell
-- We create a function `addImpure` that receives `number1` which is of type `Int`, a `number2` also `Int` type, and then returns a value that is also `Int` type.
addImpure :: Int -> Int -> Int
addImpure number1 number2 =
    print "Hello" -- We cannot do this, the compiler will fail with an error
    number1 + number2
```

We can only create pure functions:

```haskell
-- We create a Pure Function named `addPure`
addPure :: Int -> Int -> Int
addPure number1 number2 =
    number1 + number2
```

## Type Inference

Type inference is very useful when writing lots of functions and variables, if allows the compiler to figure out what is the Type of functions and values

Let's revisit the function defined above:

```haskell
addPure :: Int -> Int -> Int
addPure number1 number2 =
    number1 + number2
```

We specified that `addPure` has a type of `Int -> Int -> Int`.

However we did not have to do that, Haskell can figure it out for us:

```haskell
addPure number1 number2 =
    -- Haskell figured out that `number1` and `number2` are both of type `Int`, so we can add them together
    number1 + number2
```

## Lazy Evaluation

Haskell is lazy, just like many programmers, it will not do things unless it needs to

In common programming languages, when we define variables they are immediately evaluated.

Example JavaScript:

```js
let something = console.log("Hello from here");
let one = 1;
let two = 2;
console.log(one + two);
// Output Is:
// Hello from here
// 3
```

In the example above, the variable `something` is evaluated, even though we did not use it anywhere in the code.

Example Haskell:

```haskell
something = print "Hello from here"
one = 1
two = 2

main =
  print (1 + 2)

-- Output Is:
-- 3
```

In the example above, the variable `something` is not evaluated, Haskell figured out that we did not use it anywhere.

### Once again, What is Haskell?

We can now see how statically-typed, purely functional, type inference and lazy evaluation work together:

```haskell
-- This wont be evaluated, because we don't use it anywhere else in the code
something = print "Lazy"

-- `addNumbers` is pure, it does nothing other than add two numbers
addNumbers :: Int -> Int -> Int
addNumbers number1 number2 =
  number1 + number2

-- We don't need to specify the type for everything, haskell can figure it out.
addStrings string1 string2 =
  string1 ++ string2

-- This will fail, `addNumbers` function can only accept numbers not strings
result = addNumbers 1 "2"
```
