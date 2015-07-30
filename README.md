# Learn Swift

While reading the docs mentioned below, try typing out the examples in an Xcode "Playground" (from Xcode, click File -> New -> Playground). 

Read the Swift language documentation on [Declaring Constants and Variables](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-ID310). 

### Question 1
*What's the difference between the keywords `let` and `var`?*

Read the docs on [Functions](
https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID158).

Skim through the docs on [Strings](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#//apple_ref/doc/uid/TP40014097-CH7-ID285). After skimming quickly, 
read the [part on how to concatenate strings](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/StringsAndCharacters.html#//apple_ref/doc/uid/TP40014097-CH7-ID291) (a fancy word for add together).


## Exercise 1

Still in a Playground, implement a function named `lengthOfJoinedStrings` which takes two Strings as arguments and returns the length of both Strings added together. The length of a String is the number of characters in it. 

You can use the `count` function to get the length of a String. For example `count("hi")` prints `2`. Don't worry about where `count` from.

If you implemented the function correctly then `lengthOfJoinedStrings("hello", "world")`, for example, should print `10` since "helloworld" has 10 characters.

## Exercise 1.1

Implement a function named `add` which takes two `Int`s as arguments and returns the sum of the two numbers.

```swift
add(1, 1) //should print 2
```

## Exercise 1.2

Implement a function named `mult` which takes two `Int`s as arguments and returns the product of the two numbers.

```swift
mult(2, 2) //should print 4
```

## Exercise 1.3

Every Swift function takes the form of:

```swift
func swiftFunction(arg1: Type1, arg2: Type2, ...) -> ReturnType {...}
```

`arg1: Type1` says that one of the parameters of `swiftFunction` is named `arg1` and its type is `Type1`. `Type1` could be `Int` or `String` or whatever. To refer to the argument in the body of the function, you use its name. 

Example:

```swift
func sayHello(person: String) -> String {
    return "hello, " + person
} 
```

The ` -> ReturnType` part says that the function named swiftFunction *returns a __ReturnType__*. This just means that the result of calling the function with the correct arguments is a `ReturnType`.

Example: 

```swift
func fizzle(a: Int, b: String) -> String {...}
```

The return type of `fizzle` is String.

```swift
func dizzle(x: Int) -> Int {...}
```

The return type of `dizzle` is Int.

Review/read the Function docs on [Function Types as Parameter Types](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID174) *You may need to scroll down a bit to see that section*

When you write a function, every argument or "parameter" has a *type*. 

In the function:

```swift
func foo(x: Int) -> String { ... }
```

The `x` parameter has type `Int`. 

In the function:

```swift
func bar(y: String) -> Int {...}
```

the `y` parameter has type `String`. 

### Question 2
What is the type of `f` in the following function?

```swift
func buzz(f: (Int, String) -> String) -> String {...}
```

If you've read the section linked to above, you know that just like a function can take, say, an Int or a String, as an argument, it can also take a function as an argument. Functions that take other functions as arguments are called **higher-order functions**. 

## Exercise 1.4

Implement a function named `calculate` as follows: 

1. This function should have three arguments. The first two should be `Int`s. Name them `x` and `y`
2. The third and final argument should be a **function** that takes two `Int`s as arguments and returns an `Int`. Name this argument `operation`. 
3. The return type of `calculate` should be an `Int`. 
4. Implement the `calculate` function so that it uses the third argument (the function which takes two `Int`s and returns an `Int`) to produce an `Int`. You should use the `x` and `y` arguments of the `calculate` function as arguments to the `operation` function. 


### Question 3
You've already written two functions which can be passed as the third argument to `calculate`. What are they?

## Exercise 1.5
Use the calculate function to get the product of 2 X 2. When calling `calculate`, the argument you pass to it must be a function you've already written. 

```swift
calculate(2, 2, ???) //fill in the ???
```

## Exercise 1.6

Use the calculate function to get the sum of 1 + 1. When calling `calculate`, the argument you pass to it must be a function you've already written. 

```swift
calculate(1, 1, ???) //fill in the ???
```

## Exerise 1.7

Same as the previous two exercises, but this time, you should pass as the third argument to `calculate` a function which is built in to Swift. **Hint**: both of these functions have names which are a single symbol. **Another hint**: read [this section from the "Basic Operators" documentation](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/BasicOperators.html#//apple_ref/doc/uid/TP40014097-CH6-ID63).

## Exercise 1.8 

Read the section in the "Functions" documentation on [Function Types as Return Types](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID174)

Read the section in the "Expressions" documentation on [Closure Expression](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Expressions.html)

The upshot is that the same way function types are perfectly valid parameters/arguments to functions 	so too they are valid return types. 

Here's a function that returns a function:

```swift
func plus(x: Int) -> Int -> Int {
    let myFunction = {
        (y: Int) -> Int in
        return x + y
    }
    return myFunction
}
```

`plus` is a function that takes a single `Int` argument and returns a function which takes an `Int` and returns an `Int`. In this function, we create a function and name it `myFunction`. This function takes an `Int` and adds it to the `x` passed to `plus`. The return value of `plus` is the function `myFunction`. 

Here's how you use `plus`

```swift
let increment = plus(1)
increment(1) //prints 2

let add22 = plus(22)
add22(1) // prints 23
```

The first line declares a constant named `increment`. The value of `increment` is a function which will take an `Int` and add 1 to it. The `increment` constant can now be used like any other function, e.g. `increment(100)`. 

From now on when we have a function that takes just one argument, we will refer to it as "a function from X to Y". For example, `func length(x: String) -> Int` can be referred to as a "function from String to Int", which means it takes a `String` as an argument and returns an `Int`. 

Implement a function which takes a String and returns a function from String to String. The function should have the following signature. 

```swift
func join(x: String) -> String -> String { ... }
```

It should behave like this:

```swift
let joinWithHello = join("hello")
joinWithHello(" world") //prints "hello world"

let joinWithWhy = join("why")
joinWithWhy(" not") //prints "why not"
```



	





