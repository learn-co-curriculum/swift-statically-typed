# Swift — Statically-Typed

## Objectives

1. Learn about various type systems and approaches to type safety in computer programming.
2. Understand what it means for Swift to be a statically-typed language.
3. Use type annotation to explicitly type an instance.
4. Recognize type matching errors and how to solve them.
5. Convert data types to other data types by using their built-in initializer methods.

## Static & Strong

So what does it mean for Swift to be a "statically-typed" or "strongly-typed" language? It refers to the way the language's compiler tracks the information on what kind of information each instance holds. The polarized terms "static" versus "dynamic" and "strong" versus "weak" are loose industry terms which refer to whether the language's [type system](https://en.wikipedia.org/wiki/Type_system) performs checks either at compile time (static/strong) or at run time (dynamic/weak).

>Swift is a *type-safe* language, which means the language helps you to be clear about the types of values your code can work with. If part of your code expects a `String`, type safety prevents you from passing it an `Int` by mistake. Likewise, type safety prevents you from accidentally passing an optional `String` to a piece of code that expects a nonoptional `String`. Type safety helps you catch and fix errors as early as possible in the development process.
>—[*The Swift Programming Language - The Basics*](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-ID309), Apple, Inc.

This static/strong typing nature of Swift means that type-mismatching usually raises errors that prevent the scheme from building, instead of waiting for run-time crashes to print a stack trace to report on what went wrong.

## Type Annotations (Explicit Syntax)

While Swift handles implicit typing rather well, there are times when we want to explicitly tell the compiler which type we want an instance to be defined as. This may be when we want the type to differ from the implicit type, when we're declaring a property without an associated value that will be set within an initializer, or when we just want to improve the readability of our code for the sake of ourselves and other developers.

To explicitly declare an instance as a particular type, we can use what's called a "type annotation". This syntax simply requires that the instance's name be followed with a colon (`:`) and the type name, such as `Int`, `Double`, or `String`.

```swift
let fortyTwo: Int = 42
let pi: Double = 3.14159
let welcome: String = "Welcome!"
```
This should already feel familiar from having declared the types of function parameters:

```swift
func heyListenGroup(group: String, speaker: String, minutes: Int) -> String {
    return "Heyyy, \(group)! Come listen to \(speaker) give a talk for \(minutes) minutes."
}
```
Further details on Type Annotations and [Type Safety](https://en.wikipedia.org/wiki/Type_safety) can be found in [The Basics chapter](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html#//apple_ref/doc/uid/TP40014097-CH5-ID309
) of Apple's *The Swift Programming Language*

## Type Mismatching

Type mismatches in your code will interrupt the compile phase and keep the scheme from building. Mismatches occur when an instance of one type is assigned a value or variable of a different type:

```swift
let pi: Int = 3.14159    // error
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-statically-typed/type_mismatch_pi_Int.png)

This occurs when assigning from other instances as well as from values:

```swift
let pi: Double = 3.14159
let piInt: Int = pi      // error
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-statically-typed/type_mismatch_piInt_pi.png)

Since function & method parameters are typed as well, type mismatching can occur in a function or method call when a parameter is passed a value that does not match its type:

```swift
let pi: Double = 3.14159

func heyListenGroup(group: String, speaker: String, minutes: Int) -> String {
    return "Heyyy, \(group)! Come listen to \(speaker) give a talk for \(minutes) minutes."
}

heyListenGroup("iOS", speaker: "Orta", minutes: pi) // error
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-statically-typed/type_mismatch_function_parameter.png)

**Top-tip:** *Apple recommends using* `Int` *for general use, even when the instance represents a non-negative value. Their reasoning is that this improves interoperability between different units of code.*

## Converting Data Types

One use case for specifically needing a `UInt32` type is when submitting an argument to the `arc4random_uniform()` C function. If we attempt to submit a value of type `Int` to this function, the Swift compiler will complain about a mismatch:

```swift
let die: Int = 20
let random = arc4random_uniform(die)  // error
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-statically-typed/type_mistmatch_arc4random_uniform.png)

However, if we use `UInt32()` to initialize a `UInt32` instance from our `Int` instance, we can silence the compiler error:

```swift
let die: Int = 20
let random = arc4random_uniform(UInt32(die))
```
![](https://curriculum-content.s3.amazonaws.com/swift/swift-statically-typed/type_casting_UInt32_for_arc4random_uniform.png)

You can initialize a new instance of a different data type by using the new data type's name suffixed with a parenthesis containing the value or instance to convert to the new type. This is a Swift shorthand for calling an initializer, and the data types have a series of initializers for translating themselves from other similar types, such as the `Int` and `UInt` families. The following instance declarations are all equivalent:

```swift
// equivalent instance declarations

let twenty = Int.init(20)    // long form initializer method call
let twenty = Int.init(20.0)  // uses initializer from Double type
let twenty = Int(20)         // shorthand for initializer method
let twenty = Int(UInt(20))   // uses the initializer from UInt type
let twenty: Int = 20         // type annotation syntax
let twenty = 20              // inferred type syntax
```


<p data-visibility='hidden'>View <a href='https://learn.co/lessons/swift-statically-typed' title='Swift Statically Typed'>Swift Statically Typed</a> on Learn.co and start learning to code for free.</p>
