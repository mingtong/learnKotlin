# Learn Kotlin

- Differences from Java/C#.
- Tricky

## Tricky

- Kotlin can run without a class (only a main function).
- No ?: operator
- Support nullable: Int?
- Int? cast to Int
- parameters in fun are defined with val by default.
- 

## Data types
- Int 32 bit,
- Long 64 bit, var a = 30L
- Float 32 bit, var b = 4.5F
- Double 64 bit,
- Short 16 bit,
- Byte 8 bit,
- Boolean true/false

type conversions 

- toByte(): Byte
- toShort(): Short
- toInt(): Int
- toLong(): Long
- toFloat(): Float
- toDouble(): Double
- toChar(): Char

```kotlin
is
!is 
as
```



## Defining variables
var for variable
val for constant variable
```kotlin
val a: Int = 1  // immediate assignment
val b = 2   // `Int` type is inferred
```

### Lazy init
```kotlin
val p: String by lazy {
    // compute the string
}
```


## Defining string
```kotlin
var a = 1
val s1 = "a is $a" 
val s2 = "${s1.replace("is", "was")}, but now is $a"
```

## Logical control

### If not null and else shorthand
```kotlin
val files = File("Test").listFiles()
println(files?.size ?: "empty")
```
### Get first item of a possibly empty collection
```kotlin
val emails = ... // might be empty
val mainEmail = emails.firstOrNull() ?: ""
```
### Execute if not null
```kotlin
val value = ...
value?.let {
    ... // execute this block if not null
}
```
### if else
```kotlin
fun maxOf(a: Int, b: Int) = if (a > b) a else b
```
### if expression
```kotlin
fun foo(param: Int) {
    val result = if (param == 1) {
        "one"
    } else if (param == 2) {
        "two"
    } else {
        "three"
    }
}
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
for (i in 1..100) { ... }  // closed range: includes 100
for (i in 1 until 100) { ... } // half-open range: does not include 100
for (x in 2..10 step 2) { ... }
for (x in 10 downTo 1) { ... }
if (x in 1..10) { ... }
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
### local function (fun in fun)
```kotlin
fun dfs(graph: Graph) {
    fun dfs(current: Vertex, visited: Set<Vertex>) {
        if (!visited.add(current)) return
        for (v in current.neighbors)
            dfs(v, visited)
    }

    dfs(graph.vertices[0], HashSet())
}
```

### Tail recursive functions
```kotlin
val eps = 1E-10 // "good enough", could be 10^-15

tailrec fun findFixPoint(x: Double = 1.0): Double
        = if (Math.abs(x - Math.cos(x)) < eps) x else findFixPoint(Math.cos(x))
```

## Defining class
### primary constructor
```kotlin
class Person constructor(firstName: String) { ... }
class Person constructor(val firstName: String, val lastName: String, var age: Int) { ... }
```
### init function executed when new a object of the class
```kotlin
class InitOrderDemo(name: String) {
    val firstProperty = "First property: $name".also(::println)
    init {
        println("First initializer block that prints ${name}")
    }
```
### secondary constructor
If has primary constructor, each secondary constructor needs to delegate to the primary constructor.
```kotlin
class Person(val name: String) {
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
```

### open class for inheritance
```kotlin
open class Base(p: Int)
class Derived(p: Int) : Base(p)
```

### overriding Methods
```kotlin
open class Base {
    open fun v() { ... }
    fun nv() { ... }
}
class Derived() : Base() {
    override fun v() { ... }
}
```

### get/set
```kotlin
class Person constructor(val firstName: String, val lastName: String, var age: Int) {
    var counter = 0 // Note: the initializer assigns the backing field directly
        get() = 2
        set(value) {
            if (value >= 0) field = value
        }
}
```

### Extensions to class
```kotlin
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] // 'this' corresponds to the list
    this[index1] = this[index2]
    this[index2] = tmp
}
val l = mutableListOf(1, 2, 3)
l.swap(0, 2) // 'this' inside 'swap()' will hold the value of 'l'
```


## Defining Data class
create DTO with getter/setter/equals/hashCode etc. automaticlly.
```kotlin
data class Customer(val name: String, val email: String)
```

## Enum
```kotlin
enum class Direction {
    NORTH, 
    SOUTH, 
    WEST, 
    EAST
}

enum class ProtocolState {
    WAITING {
        override fun signal() = TALKING
    },
    TALKING {
        override fun signal() = WAITING
    };
    abstract fun signal(): ProtocolState
}
```

## Collection
```kotlin
//list
val list = listOf("a", "b", "c")  //Read-only list
println("Third element: ${list.get(2)}")
println("Fourth element: ${list[3]}")
println("Index of element \"two\" ${list.indexOf("two")}")

//map
val map = mapOf("a" to 1, "b" to 2, "c" to 3)  //Read-only map
println(map["key"]);  //Accessing a map
map["key"] = value;  //set a map
```

### Common operations
- Transformations
    - Mapping
    - Zipping
    - Association
    - Flattening
    - joinToString
    - joinTo
- Filtering
    - by predicate
    - Partitioning
    - Testing predicates
- plus and minus operators
- Grouping
- Retrieving collection parts
    - Slice
    - Take and drop
    - Chunked
    - Windowed
- Retrieving single elements
    - by position
    - by condition
    - Random element
    - Checking existence
- Ordering
    - Natural order
    - Custom orders
    - Reverse order
    - Random order
- Aggregate operations
    - min, max
    - average
    - sum() 
    - count()
    - Fold and reduce

### Adding/Removing elements
```kotlin
val numbers = mutableListOf(1, 2, 3, 4)
numbers.add(5)
numbers.remove(3) 
```
### List Specific Operations
- Retrieving elements by index
    - elementAt(), first(), last()
    - getOrElse()
    - getOrNull()
- Retrieving list parts:  numbers.subList(3, 6)
- Finding element positions: numbers.indexOf(2)
- Binary search in sorted lists: numbers.binarySearch("two")
- Sorting

### Set Specific Operations
- union()
- intersect()
- subtract()

### Map Specific Operations
- Retrieving keys and values: [key]
- Filtering
- plus and minus operators
- add element: put(key, value)
- Removing entries: remove("one"), remove("one", 4)

## Traversing a map
```kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
```

## Singleton
Creating a singleton
```kotlin
object Resource {
    fun f1(){
    }
    val name = "Name"
}
```

### Companion Objects (object in class)
```kotlin
class MyClass {
    companion object Factory {
        fun create(): MyClass = MyClass()
    }
}
```

## Delegated Properties

## Swapping two variables
```kotlin
var a = 1
var b = 2
a = b.also { b = a }
```
## Equality check
- Structural equality: "=="
    - a?.equals(b) ?: (b === null)
- Referential equality (two references point to the same object): "==="
- Floating point numbers equality

## Elvis Operator
```kotlin
val l: Int = if (b != null) b.length else -1
```
can be
```kotlin
val l = b?.length ?: -1
```

## The !! Operator
```kotlin
val l = b!!.length
```
this will return a non-null value of b (e.g., a String in our example) or throw an NPE if b is null

## Annotations
Annotations are means of attaching metadata to code. To declare an annotation:
```kotlin
annotation class Fancy
```
## Scope Functions
execute a block of code within the context of an object. 

- let, can be used to invoke one or more functions on results of call chains. "::"
```kotlin
Person("Alice", 20, "Amsterdam").let {
    println(it)
    it.moveTo("London")
    it.incrementAge()
    println(it)
}
```
- run, useful when your lambda contains both the object initialization and the computation of the return value.
```kotlin
val service = MultiportService("https://example.kotlinlang.org", 80)
val result = service.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}
```
- with, alling functions on the context object without providing the lambda result. In the code, with can be read as “with this object, do the following.”
```kotlin
val numbers = mutableListOf("one", "two", "three")
with(numbers) {
    println("'with' is called with argument $this")
    println("It contains $size elements")
}
```
- apply, common case for apply is the object configuration. Such calls can be read as “apply the following assignments to the object.”
```kotlin
val adam = Person("Adam").apply {
    age = 32
    city = "London"        
}
```
- also,  is good for performing some actions that take the context object as an argument. Use also for additional actions that don't alter the object, such as logging or printing debug information. Usually, you can remove the calls of also from the call chain without breaking the program logic.
When you see also in the code, you can read it as “and also do the following”.
```kotlin
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
```

- takeIf
- takeUnless

### Return value
- apply and also return the context object.
- let, run, with return the lambda result.
