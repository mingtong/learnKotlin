# Learn Kotlin

- Differences from Java/C#.
- Tricky

## Basic

- Kotlin can run without a class (only a main function).
- No ?: operator
- Support nullable: Int?

## Data types
```kotlin
```
is
!is 
as


## Defining variables
var for variable
val for constant variable
```kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
```

## Defining string
```kotlin
var a = 1
val s1 = "a is $a" 
val s2 = "${s1.replace("is", "was")}, but now is $a"
```

## Logical control
```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```
like foreach
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (item in items) {
    println(item)
}
```
get index
```kotlin
val items = listOf("apple", "banana", "kiwifruit")
for (index in items.indices) {
    println("item at $index is ${items[index]}")
}
```
while is same as C#/Java

when
```kotlin
fun describe(obj: Any): String =
    when (obj) {
        1          -> "One"
        "Hello"    -> "Greeting"
        is Long    -> "Long"
        !is String -> "Not a string"
        else       -> "Unknown"
    }
```

## Range
```kotlin
for (x in 1..5) {
    print(x)
}
```
step
```kotlin
for (x in 1..10 step 2) {
    print(x)
}
println()
for (x in 9 downTo 0 step 3) {
    print(x)
}
```

## Defining function
```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```
```kotlin
fun sum(a: Int, b: Int) = a + b
```


## Defining class

## Data class
create DTO with getter/setter/equals/hashCode etc. automaticlly.
```kotlin
data class Customer(val name: String, val email: String)
```
