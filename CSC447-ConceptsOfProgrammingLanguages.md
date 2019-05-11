# Concepts of Programming Languages (CSC447), Spring, 2019

# Lecture Notes 

## Topic -- Overview 

Programming languages come and go... You will have to keep learning new languages

### LEARNING GOALS
- Learn PLs more easily by recognizing concepts
- Deeper understanding of PL concepts / paradigms
- Impact of PL on program development, modularity, correctness, runtime efficiency, etc.
- Programming paradigms and styles: mutability vs immutability -- functional vs object-oriented -- iteration vs recursion -- pattern matching vs visitor design pattern
- Runtime Storage: lexical and dynamic scope; stack layout; object and vtable layout to support inheritance and dynamic dispatch; nested structures (functions or objects); garbage collection
- Static analysis: dynamic vs static type checking; subtyping; parametric polymorphism

### MACHINES AND PROGRAMS

**Machine:** responds to inputs and generates outputs; Batch computing: input at beginning, output at end.

**Program:** tells machine how to respond to input and outputs

## Topic -- C: STATEMENTS VERSUS EXPRESSIONS, STRICT VERSUS NONSTRICT AND UNDEFINED BEHAVIOR

Statements: executed for their side-effects
- Expression statements (including assignment)
- Return statements
- Selection statements (if-then-else; switch-case)
- Iteration statements (while; do-while; for)

Expressions: executed for their value (and side-effects)
- Literals (boolean, character, integer, string
- Operators (arithmetic, bitwise, logical)
- Function calls

### SIDE EFFECTS
- In mathematical function takes arguments and gives results An expression is pure if that's all it does Anything else us a side effect. 
- Assignment, Change of control (goto), I/O (console, network)

### STRICT AND NON-STRICT OPERATORS
An operator is strict if it evaluates all of its operands before it runs:

#### strict constructs in C
- Arithmetic operators: `+`, `-`, `*`, `/`, ...
- Comparison operators: `<`, `<=`, `==`, `!=`, `>`, `>=`
- Bitwise operators: `|`, `&`, `~`, `^`
- Function calls

#### non-strict constructs in C
- ????

Function calls are strict BUT Macro calls are non-strict

A **macro** is a fragment of code which has been given a name. Whenever the name is used, it is replaced by the contents of the macro. There are two kinds of macros. They differ mostly in what they look like when they are used. Object-like macros resemble data objects when used, function-like macros resemble function calls.

In computer programming, **undefined behavior** is the result of executing computer code whose behavior is not prescribed by the language specification to which the code adheres, for the current state of the program.

## Topic -- SCHEME (LISP AND SCHEME)
- Influential programming language from the 1950s
- Pioneered many PL concepts:
    - automatic garbage collection
    - first-class, higher-order, nested functions
    - read-eval-print loop including runtime compilation with "eval"
    - sophisticated macro system
    - multiple dispatch / multi-methods
- Dialects: Common Lisp, Scheme, Clojure, Racket
- We will use Scheme
```
; This (recursive) function calculates the length of a linked list.
(define (length l) 
  (if (equal? l ()) 
    0 
    (+ 1 (length (cdr l)))))
```

### LITERALS IN SCHEME
- Number `5`
- String `"hello world"`
- symbol `'helloworld`

### ARITHMETIC IN SCHEME
Arithmetic expressions use prefix notation. Prefix notation, is a mathematical notation in which operators precede their operands
```
; (1 + 2) * 3 would be written in Scheme as follows
(* (+ 1 2) 3)
```

### OPERATOR TERMINOLOGY
- **Prefix notation:** operator *before* arguments `+ 1 2`
- **Infix notation:** operator *between* arguments `1 + 2`
- **Postfix notation:** operator *after* arguments ` 1 2 +`

### FUNCTIONS
- Define a function `square` with parameter `n`: `(define (square n) (* n n))`
- Invoke the `square` function: `(square 5)`
- Invoke the square function twice: `(square (square 5))`

### DEFINING FUNCTIONS:
```
(define (f param_1 param_2 ... param_m) 
  e_1 e_2 ... e_n)
```
- Body of function is a sequence of expressions
- e_n is evaluated and its result is returned
- No return keyword, no statements, just expressions

### BOOLEANS AND CONDITIONALS
- `=` operator tests number equality `(define (zero n) (= n 0))`
- Boolean values are `#t` and `#f`
- `if` is a non-strict special form

### RECURSIVE FUNCTIONS

- Recursive functions are common in Scheme
```
; Factorial using conditional expression
(define (fact n) 
  (if (<= n 1) 
      1 
      (* n (fact (- n 1)))))
```

### CONS CELLS
- A **cons cell** is a pair of two pieces of data
- Pair of numbers `(cons 1 2)`, Pair of strings `(cons "hello" "world")`, Pair of a number and a string `(cons 1 "world")`
- `car` and `cdr` functions extract components: 
- `(car (cons 1 "world")) (cdr (cons 1 "world"))`
- Cons cells (pairs) are used to represent linked lists
- `car` position for elements
- `cdr` position for next cons cell

### CONS CELLS FOR LINKED LISTS
- Linked lists built up using () and cons
- Empty list `()`
- Singleton list containing 3 only `(cons 3 ())`
- List containing 1, 2, 3 `(cons 1 (cons 2 (cons 3 ())))`

### SYNTACTIC SUGAR FOR LISTS
- `quote` special form prevents evaluation `(quote (3))`
- `'` is shorthand for quote `'(3)`
- `list` function evaluates args, puts results in a list `(list 1 2 (+ 1 2))`

### EQUALITY TESTING FOR LISTS
- `eqv?` for pointer equality: `(eq? (cons 1 (cons 2 (cons 3 ()))) '(1 2 3))`
    - Pointer equality compares two pointers
- `equal?` for structural equality `(equal? (cons 1 (cons 2 (cons 3 ()))) '(1 2 3))` 
    - Structural equality traverses two structures
- in computer science, a **pointer** is a programming language object that stores the memory address of another value located in computer memory.

### DYNAMIC TYPES
- Dynamic: Types checked on the fly, during execution. 
```
(symbol? 'x)
(number? 1)
(boolean? #t)
(string? "x")
(procedure? (lambda (x) (+ x 1)))
```
- List only has one structure type: the pair. `(pair? '(1 . 2))`

### READ-EVAL-PRINT LOOP (REPL)
- Quoting delays evaluation
- `eval` function evaluates an expression
- `read` function reads an expression

## Topic -- TYPES

Types used to describe when operations allowed: Java: `+` allowed on strings and numeric types  Conversion to strings using `toString`

### DYNAMIC TYPE CHECKING: 
- Tracks and stores type of data at **runtime**
- Checks types before applying an operation

EXAMPLE: SCHEME / DYNAMIC: 
Dynamic type checking detects a failure: 
```
#;> (- 5 "hello") 
Error in -: expected type number, got '"hello"'.
```
Type checker invoked before execution starts?
```
#;> (define (f) (- 5 "hello")) // compiles just fine
#;> (f) // but when it runs ... it fail! 
Error in -: expected type number, got '"hello"'.
```
Failure is when `f` run! Conclusion: no type checking before execution. 

### STATIC TYPE CHECKING
- Compiler analyzes code for type errors
- Reports (rejects) programs with incorrect usage
- Found in C, Java, Scala, Haskell, Rust, Coq, etc.

EXAMPLE: JAVA / STATIC: 

```
class Typing01 {
  void f () {
    int a = 5;
    String b = "hello";
    System.out.println ("Result = " + (a - b));
  }
}
```

```
$ javac Typing01.java 
Typing01.java:5: error: bad operand types for binary operator '-'
    System.out.println ("Result = " + (a - b));
                                         ^
  first type:  int
  second type: Strin
  ```
errors out BEFORE runtime ! 
  
### UNSAFE ACCESS (SHAPE ERRORS)
- Memory location contains data written at a given type (such as character array)
- The same memory location is read and interpreted at an incompatible type (such as int).
- This is known as an **unchecked runtime type error** For brevity, I will call this an **unsafe access** 
- Scheme prevents shape errors by _throwing an exception and denying access_

### STRONG VS WEAK
- **Strong** typing **guarantees** no UNSAFE ACCESS
- **Weak** typing may **permit** UNSAFE ACCESS
- UNSAFE ACCESS = data used contrary to type 
    - E.g., a floating point number used as an integer
- **Strong, static:** Java, C#, Scala, Rust, etc. early warning, strong guarantees
- **Weak, static:** C early warning, weak guarantees
- **Strong, dynamic:** Scheme, Python, Ruby, etc. problem detected at runtime, but before unsafe access occurs!

IS JAVA STRONG? - Yes, error is detected before memory is accessed
IS JAVA DYNAMIC? - Java's type checking is mostly static

### DYNAMIC CHECKS IN JAVA
- Arrays
    - Reading always safe, Writing potentially dangerous
    - Bounds checking prevents C-like indexing errors
- Casting
    - Upcasting always safe, Downcasting potentially dangerous
- Garbage collection and restricted use of pointers
    
### TRADEOFFS

| Dynamic                                     | Static                                        |
|---------------------------------------------|-----------------------------------------------|
| more flexible                               | compile-time detection of errors              |
| usually conceptually simpler                | no unit tests for type checking               |
| faster compilation                          | automatic documentation                       |
| easier runtime code generation/modification | faster runtime (dynamic checks, optimization) |
|                                             | less memory consumption at runtime            |
 
 ## Topic -- SCALA INTRODUCTION

 Scala = Scalable Component Abstractions
 
- Functional and object-oriented PL
- ML + Java + more
- Compiles to JVM: Interop: Scala calls Java; Java calls Scala
- Scala has a REPL like Scheme, ML, Python, etc. 
- Access to Java libraries
- For real programs and homeworks, use sbt to run tests
- You can use :console/:quit to get a REPL within sbt
- Scala performs static type checking
- DISASSEMBLY To see what scala is doing, you can disassemble in the REPL: `scala> :javap -p -c -filter C`
- Scala performs **static type checking**: `def f () { 5 - "hello" }  // rejected by type checker`

### IMMUTABLE VARIABLES
```
** Java **
final int x = 10;  // declare and initialize x
x = 11;            // assignment to x fails
Final.java:4: error: cannot assign a value to final variable x

** C **
const int x = 10;  // declare and initialize x
x = 11;            // assignment to x fails
final.c:6:3: error: assignment of read-only variable ‘x’

** Scala ** 
val x = 10         // declare and initialize x
x = 11             // assignment to x fails
final.scala:3: error: reassignment to val
```

### MUTABLE VARIABLES
```
** Java **
int x = 10;        // declare and initialize x
x = 11;            // assignment to x OK

** C **
int x = 10;        // declare and initialize x
x = 11;            // assignment to x OK

** Scala ** 
var x = 10         // declare and initialize x
x = 11             // assignment to x OK
```


### EXPRESSION ORIENTED

**Scala is expression oriented; no statements like Scheme, ML, etc. unlike C, Java, etc.**

- C comma expressions `(e_1, e_2, ..., e_n)`
- Scheme begin expressions `(begin e_1 e_2 ... e_n)`
- Scala compound expressions `{e_1; e_2; ...; e_n}`

### METHODS

- Parameters require type annotations: `def plus (x:Int, y:Int) : Int = x + y`
- Return types can often be inferred but are required for recursive method
- Body is an expression; its value is returned

#### METHODS VERSUS FIELDS
- `def` can be used as non-parameterized methods: `def y = 1`
- `val` and `def` differ in when initializer is executed.
- `val` is strict; `def` is non-strict

### EVERYTHING IS AN OBJECT

- `5:Int` is an object with methods: `5.toDouble`
- Methods can have symbolic names: `5.+ (6)`
- `e1.f(e2)` can be written as `e1 f e2`: `5 + 6` , `5 max 6`

### IMMUTABLE TUPLES

**Fixed number of heterogeneous items**

```
** Scala **
val p : (Int, String) = (5, "hello")
val x : Int = p._1

** Java ** 
public class Pair<X,Y> {
  final X x;
  final Y y;
  public Pair (X x, Y y) { this.x = x; this.y = y; }

  static void f () {
    Pair<Integer, String> p = new Pair<Integer, String> (5, "hello");
    Pair<Integer, String> q = new Pair<> (5, "hello"); // infer type params
    int x = p.x;
  }
}
```

### IMMUTABLE LINKED LISTS

**Varying number of homogeneous items**

```
** Scheme** 
(car (cons 1 (cons 2 (cons 3 (cons 4 ()))))) -> 1 
(cdr (cons 1 (cons 2 (cons 3 (cons 4 ()))))) -> 2,3,4

** Scala **
(1 :: (2 :: (3 :: (4 :: Nil)))).head -> 1
(1 :: (2 :: (3 :: (4 :: Nil)))).tail -> 2,3,4

** Scheme **
'(1 2 3)

** Scala **
List (1, 2, 3)
```

### PATTERN MATCHING

```
val p : (Int, String) = p match {
  case (x, y) => "Int is %d".format (x)
}

val xs : List[Int] = // ...
xs match {
  case Nil   => "List is empty"
  case y::ys => "List is non-empty, head is %d".format (y)
}
```

#### Implement isEmpty, head, tail by pattern matching

```
def isEmpty [X] (xs:List[X]) : Boolean = xs match {
  case Nil   => true
  case y::ys => false
}
def head [X] (xs:List[X]) : X = xs match {
  case Nil   => throw new NoSuchElementException ()
  case y::ys => y
}
def tail [X] (xs:List[X]) : List[X] = xs match {
  case Nil   => throw new NoSuchElementException ()
  case y::ys => ys
}
```
**Parametric polymorphism: X is type parameter**

### RECURSIVE METHODS

- Imperative programming typically has: iteration using while loops, mutable programming
- Functional programming typically has: iteration using recursion, immutable programming

```
//Length of a linked list recursively
def length (xs:List[Int]) : Int = xs match {
  case Nil   => 0
  case y::ys => 1 + length (ys)
}

//With parametric polymorphism
def length [X] (xs:List[X]) : Int = xs match {
  case Nil   => 0
  case y::ys => 1 + length (ys)
}

/Ignore head of list with wildcard _
def length [X] (xs:List[X]) : Int = xs match {
  case Nil   => 0
  case _::ys => 1 + length (ys)
}

```

#### Evaluate step-by-step: 

```
def length (xs:List[Int]) : Int = xs match {
  case Nil   => 0
  case y::ys => 1 + length (ys)
}

length (List (1, 2, 3))
--> length (1::(2::(3::Nil)))
--> 1 + length (2::(3::Nil))      // y = 1, ys = 2::(3::Nil)
--> 1 + (1 + length (3::Nil))     // y = 2, ys = 3::Nil
--> 1 + (1 + (1 + length (Nil)))  // y = 3, ys = Nil
--> 1 + (1 + (1 + 0))
--> 1 + (1 + 1)
--> 1 + 2
--> 3

```

### APPENDING LISTS

`::` Run is constant time b/c connects lists to reference of list. 

List class has builtin method `:::`

```
scala> ((1 to 5).toList) ::: ((10 to 15).toList)
res1: List[Int] = List(1, 2, 3, 4, 5, 10, 11, 12, 13, 14, 15)
```

#### NOTE: 4/17/2019 1HR HW1 Review.

## Functional Programming 

Type( X => Unit) - argument => return type


` forEach (xs, x:Int) => { println(x)}` 
` for each (xs, println(_))`

Anonymous function: using underscore: 

`val sum1 = (x:Int, y:Int) => x+y`
`val sum2 = (_:Int) + (_:Int)`
`val sum2 : (Int, Int) => Int = _ + _`

### Tansforming Elements 

- Create a new list from an old list

## Map on lists
```
def map [X, Y] (xs:List[X], f:X=>Y) : List[Y] = {
  xs match {
    case Nil  => Nil 
    case y::ys => f(y) :: map (ys,f)
  }
}
```
Abstract building a new list, `f` function param, for each element `y` of old list builds an element `f(y)` of new list  

### IDENTITY AND MAP PROPERTIES 

- one cons cell in input => one cons cell in output 
- input list length = output list length 

```
identity (1::(2::(3::Nil)))
--> 1::(identity (2::(3::Nil)))
--> 1::(2::(identity (3::Nil)))
--> 1::(2::(3::(identity (Nil))))
--> 1::(2::(3::(Nil))

map (1::(2::(3::Nil)), f)
--> f(1)::(map (2::(3::Nil), f))
--> f(1)::(f(2)::(map (3::Nil, f)))
--> f(1)::(f(2)::(f(3)::(map (Nil, f))))
--> f(1)::(f(2)::(f(3)::(Nil)))
```

### FILTER 
```
def filter [X] (xs:List[X], f:X=>Boolean) : List[X] = {
  xs match {
    case Nil            => Nil
    case y::ys if f (y) => y :: filter (ys, f)
    case _::ys          => filter (ys, f)
  }
}
```
### SUM TO FOLDLEFT

Using tail recursion (computing forward)
```
def sum (xs:List[Int], z:Int = 0) : Int =  xs match {
  case Nil   => z
  case y::ys => sum (ys, z + y)
}
val xs = List(11,21,31)
sum (xs)

----

    sum(List(11,21,31),0)     // Fod/Reducation 
--> sum(List(21,31),11)
--> sum(List(31), 32)
--> sum(List(), 63)
--> 63

```
### SUM TO FOLDRIGHT
Using non-tail recursion (computing backward)

### LEFT V RIGHT
```
def foldLeft [Z,X] (xs:List[X], z:Z, f:((Z,X)=>Z)) : Z =  xs match {
  case Nil   => z
  case y::ys => foldLeft (ys, f(z,y), f)
}
def foldRight [X,Z] (xs:List[X], z:Z, f:((X,Z)=>Z)) : Z =  xs match {
  case Nil   => z
  case y::ys => f (y, foldRight (ys, z, f))
}
``` 

- **foldLeft** is tail recursive: each iteration applies f to the next value and the accumulated result; recursive call is the result
- **foldRight** is recursive into an argument: each iteration applies f to the next value and the result of recursively folding the rest of the list

```
foldLeft (xs, z, f) === f( f( f( f(z, a), b), c)) === (z /: xs)(f)
foldRight(xs, z, f) === f(a, f(b, f(c, z)))       === (xs :\ z)(f) 


                    (z /: xs)(f)           (xs :\ z)(f)
                      f                       f
                     / \                     / \
                    f   c                   a   f
                   / \                         / \
                  f   b                       b   f
                 / \                             / \
                z   a                           c   z

```





## FOR EXPRESSIONS

### SET/LIST Comprehensions 

- set comprehensions `{ (m, n) | m ∈ { 0, ..., 10 } ∧ n ∈ { 0, ..., 10 } ∧ m ≤ n }` 

#### Java foreach statement:
```
int[] a = new int[]{1,2,3};
int sum = 0;
for (int x : xs) sum = sum + x;
```
#### Scala foreach expression:
```
val xs : List[Int] = List(1,2,3)
var sum = 0
for (x <- xs) sum = sum + x // for x drawn-from (<-) xs 
```
#### Scala infers type: If xs:List[T] then x:T
```
for (x <- xs) e   ===   xs.foreach ((x)=>e)
```
#### SCALA: FOR EXPRESSIONS AS MAP
```
val xs : List[Int] = List(1,2,3)
for (x <- xs) yield x*10

for (x <- xs) yield e   ===   xs.map ((x)=>e)
```

- yield -- don't use a `forEach` use a Map: ` xs . map (x => x+10)`
`for (x <- xs) yield e   ===   xs.map ((x)=>e)`

### FLATTEN 
```
val xss = List(List(1,2,3),List(4,5,6,7),List(8,9),List(10))
flatten (xss) == (1 to 10).toList
xss.flatten == (1 to 10).toList // builtin method
```

And with for expressions using nested iterations:
```
(for (xs <- xss; x <- xs) yield x) == (1 to 10).toList
```



 


[//]: # (endof lecture notes)

# Programming in Scala: A Comprehensive Step-by-step Guide by Odersky (PS)

## Chapter 1: A Scalable Language

The name Scala stands for "scalable language." The language is so named because it was designed to grow with the demands of its users.

It runs on the standard Java platform and interoperates seamlessly with all Java libraries. It's quite a good language for writing scripts that pull together Java components.

Technically, Scala is a blend of object-oriented and functional programming concepts in a statically typed language.

### 1.1 A LANGUAGE THAT GROWS ON YOU

**Associative maps** are very useful because they help keep programs legible and concise, but sometimes you might not agree with their "one size fits all" philosophy because you need to control the properties of the maps you use in your program in a more fine-grained way.

#### Growing new types

Eric Raymond introduced the cathedral and bazaar as two metaphors of software development.[3] The cathedral is a near-perfect building that takes a long time to build. Once built, it stays unchanged for a long time. The bazaar, by contrast, is adapted and extended each day by the people working in it. In Raymond's work the bazaar is a metaphor for open-source software development.

Instead of providing all constructs you might ever need in one "perfectly complete" language, Scala puts the tools for building such constructs into your hands.

#### Growing new control constructs

Unfortunately, creating dependable multi-threaded applications has proven challenging in practice. Java's threading model is built around shared memory and locking, a model that is often difficult to reason about, especially as systems scale up in size and complexity. It is hard to be sure you don't have a race condition or deadlock lurking—something that didn't show up during testing, but might just show up in production.

Java comes with a rich, thread-based concurrency library. Scala programs can use it like any other Java API. However, Akka is an additional Scala library that implements an actor model similar to Erlang's.

Actors are concurrency abstractions that can be implemented on top of threads.

### 1.2 WHAT MAKES SCALA SCALABLE?

In principle, the motivation for object-oriented programming is very simple: all but the most trivial programs need some sort of structure. The most straightforward way to do this is to put data and operations into some form of containers. The great idea of object-oriented programming is to make these containers fully general, so that they can contain operations as well as data, and that they are themselves values that can be stored in other containers, or passed as parameters to operations. Such containers are called objects.

By contrast, Scala is an object-oriented language in pure form: every value is an object and every operation is a method call. For example, when you say 1 + 2 in Scala, you are actually invoking a method named + defined in class Int. You can define methods with operator-like names that clients of your API can then use in operator notation.

#### Scala is functional

In addition to being a pure object-oriented language, Scala is also a full-blown functional language. The ideas of functional programming are older than (electronic) computers. Their foundation was lai in Alonzo Church's lambda calculus, which he developed in the 1930s. The first functional programming language was Lisp, which dates from the late 50s.

Functional programming is guided by two main ideas. The first idea is that functions are first-class values. In a functional language, a function is a value of the same status as, say, an integer or a string. You can pass functions as arguments to other functions, return them as results from functions, or store them in variables. You can also define a function inside another function, just as you can define an integer value inside a function. And you can define functions without giving them a name, sprinkling your code with function literals as easily as you might write integer literals like 42.

In most traditional languages, by contrast, functions are not values. Languages that do have function values often relegate them to second-class status.

###  1.3 WHY SCALA?

#### Scala is compatible

Scala doesn't require you to leap backwards off the Java platform to step forward from the Java language. It allows you to add value to existing code—to build on what you already have—because it was designed for seamless interoperability with Java.

#### Scala is concise

Scala programs tend to be short. Scala programmers have reported reductions in number of lines of up to a factor of ten compared to Java.

Scala's syntax avoids some of the boilerplate that burdens Java programs. For instance, semicolons are optional in Scala and are usually left out.

```
// this is Java

class MyClass {
    private int index;
    private String name;
}
public MyClass(int index, String name) {
    this.index = index;
    this.name = name;
}
```
In Scala, you would likely write this instead:
`class MyClass(index: Int, name: String)`

#### Scala is high-level

Scala helps you manage complexity by letting you raise the level of abstraction in the interfaces you design and use.

prior to Java 8, you might have written a loop, like this:
```
boolean nameHasUpperCase = false; // this is Java
for (int i = 0; i < name.length(); ++i) {
    if (Character.isUpperCase(name.charAt(i))) {
        nameHasUpperCase = true;
        break;
    }
}
```
Whereas in Scala, you could write this:
`val nameHasUpperCase = name.exists(_.isUpper)` 

The Java code treats strings as low-level entities that are stepped through character by character in a loop. The Scala code treats the same strings as higher-level sequences of characters that can be queried with predicates. The predicate `_.isUpper` is an example of a function literal in Scala.

Java 8 introduced support for lambdas and streams, which enable you to perform a similar operation in Java. Here's what it might look like:
```
// This is Java 8
boolean nameHasUpperCase = name.chars().anyMatch( (int ch) -> Character.isUpperCase((char) ch) );
``` 
Although a great improvement over earlier versions of Java, the Java 8 code is still more verbose than the equivalent Scala code.

#### Scala is statically typed

A static type system classifies variables and expressions according to the kinds of values they hold and compute. Scala stands out as a language with a very advanced static type system.

If you like dynamic languages, such as Perl, Python, Ruby, or Groovy, you might find it a bit strange that Scala's static type system is listed as one of its strong points. After all, the absence of a static type system has been cited by some as a major advantage of dynamic languages.

- **Verifiable properties.** Static type systems can prove the absence of certain run-time errors. For instance, they can prove properties like: Booleans are never added to integers; private variables are not accessed from outside their class; functions are applied to the right number of arguments; only strings are ever added to a set of strings.
- **Safe refactorings.** A static type system provides a safety net that lets you make changes to a codebase with a high degree of confidence.
- **Documentation.** Static types are program documentation that is checked by the compiler for correctness. Unlike a normal comment, a type annotation can never be out of date (at least not if the source file that contains it has recently passed a compiler). Furthermore, compilers and integrated development environments (IDEs) can make use of type annotations to provide better context help.

## Chapter 2 First Steps in Scala

The best way to start learning Scala is to program in it.

### STEP 1. LEARN TO USE THE SCALA INTERPRETER
Packages in Scala are similar to packages in Java: They partition the global namespace and provide a mechanism for information hiding.

### STEP 2. DEFINE SOME VARIABLES
Scala has two kinds of variables, `vals` and `vars`. A `val` is similar to a final variable in Java. Once initialized, a `val` can never be reassigned. A `var`, by contrast, is similar to a non-final variable in Java. A `var` can be reassigned throughout its lifetime.

### STEP 3. DEFINE SOME FUNCTIONS
Function definitions start with `def`. The function's name, in this case max, is followed by a comma-separated list of parameters in parentheses. A type annotation must follow every function parameter, preceded by a colon, because the Scala compiler (and interpreter, but from now on we'll just say compiler) does not infer function parameter types.
```
scala> def max(x: Int, y: Int): Int = {
    if (x > y) x
    else y
    }
max: (x: Int, y: Int)Int
```
#### STEP 4. WRITE SOME SCALA SCRIPTS
A script is just a sequence of statements in a file that will be executed sequentially.

Command line arguments to a Scala script are available via a Scala array named args. In Scala, arrays are zero based, and you access an element by specifying an index in parentheses. `println("Hello, " + args(0) + "!")` 

#### STEP 5. LOOP WITH WHILE; DECIDE WITH IF
Note that in Scala, as in Java, you must put the boolean expression for a while or an if in parentheses. (In other words, you can't say in Scala things like `if i < 10` as you can in a language such as Ruby. You must say `if (i < 10)` in Scala.)

## Chapter 3 Next Steps in Scala  

#### STEP 7. PARAMETERIZE ARRAYS WITH TYPES
In Scala, you can instantiate objects, or class instances, using new. When you instantiate an object in Scala, you can parameterize it with values and types. Parameterization means "configuring" an instance when you create it.You parameterize an instance with values by passing objects to a constructor in parentheses. For example, the following Scala code instantiates a new `java.math.BigInteger` and parameterizes it with the value "12345": `val big = new java.math.BigInteger("12345")`

When you apply parentheses surrounding one or more values to a variable, Scala will transform the code into an invocation of a method named apply on that variable.

Scala doesn't technically have operator overloading, because it doesn't actually have operators in the traditional sense. Instead, characters such as +, -, *, and / can be used in method names. Thus, when you typed 1 + 2 into the Scala interpreter in Step 1, you were actually invoking a method named + on the Int object 1, passing in 2 as a parameter.

#### STEP 8. USE LISTS

For example,List has a method named `:::` for listconcatenation. Here's how you use it:
```
val oneTwo = List(1, 2)
val threeFour = List(3, 4)val oneTwoThreeFour = oneTwo ::: threeFour
println(oneTwo + " and " + threeFour + " were not mutated.")
println("Thus, " + oneTwoThreeFour + " is a new list.")
```
If you run this script, you'll see:
```
List(1, 2) and List(3, 4) were not mutated.
Thus, List(1, 2, 3, 4) is a new list.
```

Perhaps the most common operator you'll use with lists is `::`, which is pronounced "cons."Cons prepends a new element to the beginning of an existing list and returns the resulting list. For example: if you run this script:
```
val twoThree = List(2, 3)
val oneTwoThree = 1 :: twoThree
println(oneTwoThree)
```
You'll see:
`List(1, 2, 3)`

**WHY NOT APPEND TO LISTS?** - Class List does offer an "append" operation—it's written :+ and is explained in Chapter 24—but this operation is rarely used, because the time it takes to append to a list grows linearly with the size of the list, whereas prepending with :: takes constant time.

#### STEP 9. USE TUPLES
Another useful container object is the **tuple**. Like lists, tuples are immutable, but unlike lists, tuples can contain different types of elements. Whereas a list might be a `List[Int]` or `aList[String]`, a tuple could contain both an integer and a string at the same time. Tuples are very useful, for example, if you need to return multiple objects from a method.
```
val pair = (99, "Luftballons")
println(pair._1)
println(pair._2)
```

#### STEP 11. LEARN TO RECOGNIZE THE FUNCTIONAL STYLE
Every useful program is likely to have side effects of some form; otherwise, it wouldn't be able to provide value to the outside world. Preferring methods without side effects encourages you to design programs where side-effecting code is minimized. One benefit of this approach is that it can help make your programs easier to test.

#### STEP 12. READ LINES FROM A FILE
```
import scala.io.Source

if (args.length > 0) {
    for (line <- Source.fromFile(args(0)).getLines())
    println(line.length + " " + line)
}
else
    Console.err.println("Please enter filename")
```
## Chapter 4: Classes and Objects

### 4.1 CLASSES, FIELDS, AND METHODS
A class is a blueprint for objects. Once you define a class, you can create objects from the class blueprint with the keyword new.
Inside a class definition, you place fields and methods, which are collectively called **members**.

Fields are also known **asinstance variables**, because every instance gets its own set of the variables.

The way you make members public in Scala is by not explicitly specifying any access modifier. Put another way, where you'd say "public" in Java, you simply say nothing in Scala. **Public is Scala's default access level.**

### 4.2 SEMICOLON INFERENCE

In a Scala program, a semicolon at the end of a statement is usually optional. You can type one if you want but you don't have to if the statement appears by itself on a single line. On the other hand, a semicolon is required if you write multiple statements on a single line.

#### THE RULES OF SEMICOLON INFERENCE
In short, aline ending is treated as a semicolon unless one of the following conditions is true:
1. The line in question ends in a word that would not be legal as the end of a statement, such as a period or an infix operator.
2. The next line begins with a word that cannot start a statement.
3. The line ends while inside parentheses (...) or brackets [...], because these cannot contain multiple statements anyway.

### 4.3 SINGLETON OBJECTS
Scala has singleton objects. A singleton object definition looks like a class definition, except instead of the keyword `class` you use the keyword `object` .When a singleton object shares the same name with a class, it is called that class's **companion object.**
`object ChecksumAccumulator {` 

If you are a Java programmer, one way to think of singleton objects is as the home for any static methods you might have written in Java.

A singleton object that does not share the same name with a companion class is called **astandalone object.** 

### 4.4 A SCALA APPLICATION

Instead, you'll need to actually compile these files with the Scala compiler, then run the resulting class files. One way to do this is to use `scalac`, which is the basic Scala compiler, like this: `$ scalac ChecksumAccumulator.scala Summer.scala`

This compiles your source files, but there may be a perceptible delay before the compilation finishes. The reason is that every time the compiler starts up, it spends time scanning the contents of jar files and doing other initial work before it even looks at the fresh source files you submit to it. For this reason, the Scala distribution also includes a Scala compilerdaemon called fsc (for fast Scala compiler). You use it like this: `$ fsc ChecksumAccumulator.scala Summer.scala`

The first time you run fsc, it will create a local server daemon attached to a port on your computer. It will then send the list of files to compile to the daemon via the port, and the daemon will compile the files. The next time you run fsc, the daemon will already be running, so fsc will simply send the file list to the daemon, which will immediately compile the files.

### 4.5 THE APP TRAIT
To use the trait, you first write "extends App" after the name of your singleton object. Then instead of writing a main method, you place the code you would have put in the main method directly between the curly braces of the singleton object. You can access command-line arguments via an array of strings named args. That's it. You can compile and run this application just like any other.

## Chapter 5 Basic Types and Operations

If you're familiar with Java, you'll be glad to find that Java's basic types and operators have the same meaning in Scala.

### 5.1 SOME BASIC TYPES

| Basic type | Range | 
| --- | -- | 
| Byte | 8-bit signed two's complement integer (-27 to 27 - 1, inclusive) |
| Short | 16-bit signed two's complement integer (-215 to 215 - 1, inclusive) |
| Int | 32-bit signed two's complement integer (-231 to 231 - 1, inclusive) | 
| Long | 64-bit signed two's complement integer (-263 to 263 - 1, inclusive) | 
| Char | 16-bit unsigned Unicode character (0 to 216 - 1, inclusive) | 
| String | a sequence of Chars | 
| Float | 32-bit IEEE 754 single-precision float | 
| Double | 64-bit IEEE 754 double-precision float | 
| Boolean | true or false | 

#### Two's complement Review 
It basically says,

for zero, use all 0's.
for positive integers, start counting up, with a maximum of 2(number of bits - 1)-1.
for negative integers, do exactly the same thing, but switch the role of 0's and 1's (so instead of starting with 0000, start with 1111 - that's the "complement" part).

```
0000 - zero
0001 - one
0010 - two
0011 - three
0100 to 0111 - four to seven

1111 - negative one
1110 - negative two
1101 - negative three
1100 to 1000 - negative four to negative eight
```
Doing this, the first bit gets the role of the "sign" bit, as it can be used to distinguish between positive and negative decimal values. If the most significant bit is 1, then the binary can be said to be negative, where as if the most significant bit (the leftmost) is 0, you can say discern the decimal value is positive.
https://stackoverflow.com/questions/1049722/what-is-2s-complement

### 5.2 LITERALS

#### FAST TRACK FOR JAVA PROGRAMMERS

The syntax of most literals shown in this section are exactly the same as in Java, so if you're a Java master, you can safely skip much of this section.

#### Integer literals

Integer literals for the types Int, Long, Short, and Byte come in two forms: decimal and hexadecimal. The way an integer literal begins indicates the base of the number. If the number begins with
a 0x or 0X, it is hexadecimal (base 16), and may contain 0 through 9 as well as upper or lowercase digits A through F. Some examples are:
```
scala> val hex = 0x5
hex: Int = 5
scala> val hex2 = 0x00FF
hex2: Int = 255
scala> val magic = 0xcafebabe
magic: Int = -889275714
 ```
 
 If an integer literal ends in an L or l, it is a Long; otherwise it is an Int. 
 
If an Int literal is assigned to a variable of type Short or Byte, the literal is treated as if it were aShort or Byte type so long as the literal value is within the valid range for that type. For example:
```
scala> val little: Short = 367
little: Short = 367
scala> val littler: Byte = 38
ittler: Byte = 38
```

#### Floating point literals

Floating point literals are made up of decimal digits, optionally containing a decimal point, and optionally followed by an E or e and an exponent. Some examples of floating-point literals are:
```
scala> val big = 1.2345
big: Double = 1.2345
scala> val bigger = 1.2345e1
bigger: Double = 12.345
scala> val biggerStill = 123E45
biggerStill: Double = 1.23E47
```

Note that the exponent portion means the power of 10 by which the other portion is multiplied. Thus, 1.2345e1 is 1.2345 times 101, which is 12.345. If a floating-point literal ends in an F or f, it is a Float; otherwise it is a Double.

#### Character literals

Character literals are composed of any Unicode character between single quotes, such as:

```
scala> val a = 'A'
a: Char = A
```

In addition to providing an explicit character between the single quotes, you can identify a character using its Unicode code point. To do so, write \u followed by four hex digits with the code point, like this:
```
scala> val d = '\u0041'
d: Char = A
```

Finally, there are also a few character literals represented by special escape sequences, shown in Table: 
| Literal | Meaning | 
| --- | --- | 
| `\n` | line feed (\u000A) | 
| `\b` | backspace (\u0008) |
| `\t` | tab (\u0009) | 
| `\f` |form feed (\u000C) | 
| `\r` | carriage return (\u000D) \" double quote (\u0022) |
| `\'` | single quote (\u0027) |
| `\\` | backslash (\u005C) | 

#### Symbol literals

A symbol literal is written 'ident, where ident can be any alphanumeric identifier. Such literals are mapped to instances of the predefined class scala.Symbol. 

#### Boolean literals

```
scala> val bool = true
bool: Boolean = true
scala> val fool = false
fool: Boolean = false
```

### 5.3 STRING INTERPOLATION

```
Here's an example:
val name = "reader"
println(s"Hello, $name!")
```

### 5.4 OPERATORS ARE METHODS

Operators are actually just a nice syntax for ordinary method calls. For example, `1 + 2` really means the same thing as `1.+(2)`.

```
scala> val sum = 1 + 2    // Scala invokes 1.+(2)
sum: Int = 3
```

#### ANY METHOD CAN BE AN OPERATOR

In Scala operators are not special language syntax; any method can be an operator. What makes a method an operator is how you use it. When you write `s.indexOf('o')`,indexOf is not an operator. But when you write `s indexOf 'o'`, indexOf is an operator, because you're using it in operator notation.
`  scala> -2.0                  // Scala invokes (2.0).unary_-` 

### 5.5 ARITHMETIC OPERATIONS

You can invoke arithmetic methods via infix operator notation for addition (+), subtraction (-), multiplication (\*), division (/), and remainder (%) on any numeric type. 

### 5.6 RELATIONAL AND LOGICAL OPERATIONS

You can compare numeric types with relational methods greater than (>), less than (<), greater than or equal to (>=), and less than or equal to (<=), which yield a Boolean result. 

Logical methods, logical-and (&& and &) and logical-or (|| and |), take Boolean operands in infix notation and yield a Boolean result.

### 5.7 BITWISE OPERATIONS

Scala enables you to perform operations on individual bits of integer types with several bitwise methods. The bitwise methods are: bitwise-and (&), bitwise-or (|), and bitwise-xor (^).[5] The unary bitwise complement operator (~, the method unary_~) inverts each bit in its operand. 

Scala integer types also offer three shift methods: shift left (<<), shift right (>>), and unsigned shift right (>>>). The shift methods, when used in infix operator notation, shift the integer value on the left of the operator by the amount specified by the integer value on the right. Shift left and unsigned shift right fill with zeroes as they shift. Shift right fills with the highest bit (the sign bit) of the left-hand value as it shifts. 

### 5.8 OBJECT EQUALITY

If you want to compare two objects for equality, you can use either == or its inverse !=. These operations actually apply to all objects, not just basic types. For example, you can use== to compare lists. You can even compare against null, or against things that might be null. No exception will be thrown. 

### 5.9 OPERATOR PRECEDENCE AND ASSOCIATIVITY

For example, the expression 2 + 2 * 7 evaluates to 16, not 28, because the * operator has a higher precedence than the + operator. Thus the multiplication part of the expression is evaluated before the addition part. You can of course use parentheses in expressions to clarify evaluation order or to override precedence. For example, if you really wanted the result of the expression above to be 28, you could write the expression like this: (2 + 2) * 7

#### Operator precedence: 

- (all other special characters) 
- * / %
- +-
- :
-  =! <> &
- ^
- |
- (all letters)
- (all assignment operators)

## Chapter 6 Functional Objects

### 6.1 A SPECIFICATION FOR CLASS RATIONAL
A rational number is a number that can be expressed as a ratio n/d, where n and d are integers, except that d cannot be zero. n is called the numerator and d the denominator. Examples of rational numbers are 1/2, 2/3, 112/239, and 2/1

### 6.2 CONSTRUCTING A RATIONAL

#### IMMUTABLE OBJECT TRADE-OFFS 

Immutable objects offer several advantages over mutable objects, and one potential disadvantage. First, immutable objects are often easier to reason about than mutable ones, because they do not have complex state spaces that change over time. Second, you can pass immutable objects around quite freely, whereas you may need to make defensive copies of mutable objects before passing them to other code. Third, there is no way for two threads concurrently accessing an immutable to corrupt its state once it has been properly constructed, because no thread can change the state of an immutable. Fourth, immutable objects make safe hash table keys. If a mutable object is mutated after it is placed into a HashSet, for example, that object may not be found the next time you look into the HashSet

The main disadvantage of immutable objects is that they sometimes require that a large object graph be copied, whereas an update could be done in its place. In some cases this can be awkward to express and might also cause a performance bottleneck. 

### 6.3 REIMPLEMENTING THE TOSTRING METHOD

The result of toString is primarily intended to help programmers by providing information that can be used in debug print statements, log messages, test failure reports, and interpreter and debugger output. 

### 6.4 CHECKING PRECONDITIONS
One of the benefits of object-oriented programming is that it allows you to encapsulate data inside objects so that you can ensure the data is valid throughout its lifetime. In the case of an immutable  object such as Rational, this means that you should ensure the data is valid when the object is constructed. 

### 6.7 AUXILIARY CONSTRUCTORS

Sometimes you need multiple constructors in a class. In Scala, constructors other than the primary constructor are called auxiliary constructors.

Auxiliary constructors in Scala start with def this(...). The body of Rational's auxiliary constructor merely invokes the primary constructor, passing along its lone argument, n, as the numerator and 1 as the denominator. 

```
class Rational(n: Int, d: Int) {

  require(d != 0)

  val numer: Int = n
  val denom: Int = d

  def this(n: Int) = this(n, 1) // auxiliary constructor

  override def toString = numer + "/" + denom

  def add(that: Rational): Rational =
    new Rational(
      numer * that.denom + that.numer * denom,
      denom * that.denom
    )
 }
 ```

### 6.9 DEFINING OPERATORS

The current implementation of Rational addition is OK, but could be made more convenient to use. You
might ask yourself why you can write: `x + y` if x and y are integers or floating-point numbers, but you have to write: `x.add(y)` or at least: `x add y`

The first step is to replace add by the usual mathematical symbol.

```
def + (that: Rational): Rational =
  new Rational(
    numer * that.denom + that.numer * denom,
    denom * that.denom
 )
 ```
### 6.11 METHOD OVERLOADING

To make Rational even more convenient, we'll add new methods to the class that perform mixed addition and multiplication on rational numbers and integers. 

```
def + (i: Int): Rational =
 new Rational(numer + i * denom, denom)
```


## Chapter 7 Built-in Control Structures

The only control structures are `if`,`while`, `for`, `try`, `match`, and function calls. 

### 7.1 IF EXPRESSIONS

```
var filename = "default.txt"
if (!args.isEmpty)
    filename = args(0)

val filename =
    if (!args.isEmpty) args(0)
    else "default.txt"
```

### 7.2 WHILE LOOPS
```
var a = x
var b = y
while (a != 0) {
  val temp = a a=b%a
  b = temp
}
```

### 7.3 FOR EXPRESSIONS

#### Iteration through collections
```
val filesHere = (new java.io.File(".")).listFiles
for (file <- filesHere)
   println(file)
```
With the "file <- filesHere" syntax, which is called a generator, we iterate through the elements
of filesHere. In each iteration, a new val named file is initialized with an element value. 

You can create Ranges using syntax like "1 to 5" and can iterate through them with a for. Here is a simple example:
```
scala> for (i <- 1 to 4)
      println("Iteration " + i)
Iteration 1
Iteration 2
Iteration 3
Iteration 4
```

#### Filtering

For example, the code shown in Listing 7.6 lists only those files in the current directory whose names end with ".scala":
```
val filesHere = (new java.io.File(".")).listFiles
for (file <- filesHere if file.getName.endsWith(".scala"))
   println(file)
```

#### Nested iteration

If you add multiple <- clauses, you will get nested "loops."

The outer loop iterates through filesHere, and the inner loop iterates through fileLines(file) for any file that ends with .scala.

```
    def fileLines(file: java.io.File) =
      scala.io.Source.fromFile(file).getLines().toList
    def grep(pattern: String) =
      for (
        file <- filesHere
        if file.getName.endsWith(".scala");
        line <- fileLines(file)
        if line.trim.matches(pattern)
      ) println(file + ": " + line.trim)
    grep(".*gcd.*")
```

### 7.4 EXCEPTION HANDLING WITH TRY EXPRESSIONS

#### Throwing exceptions
`throw new IllegalArgumentException`

#### Catching exceptions

```
    import java.io.FileReader
    import java.io.FileNotFoundException
    import java.io.IOException
    try {
      val f = new FileReader("input.txt")
      // Use and close file
    } catch {
      case ex: FileNotFoundException => // Handle missing file
      case ex: IOException => // Handle other I/O error
}
```

#### The finally clause

You can wrap an expression with a finally clause if you want to cause some code to execute no matter how the expression terminates.

```
 import java.io.FileReader
    val file = new FileReader("input.txt")
    try {
      // Use the file
    } finally {
      file.close()  // Be sure to close the file
    }
```

### 7.7 VARIABLE SCOPE

If you're a Java programmer, you'll find that Scala's scoping rules are almost identical to Java's. One difference between Java and Scala is that Scala allows you to define variables of the same name in nested scopes. 

Once a variable is defined, you can't define a new variable with the same name in the same scope. For example, the following script with two variables named a in the same scope would not compile:
```
val a = 1
val a = 2 // Does not compile
println(a)
```
You can, on the other hand, define a variable in an inner scope that has the same name as a variable in an outer scope. The following script would compile and run:
```
val a = 1;
{
  val a = 2 // Compiles just fine
  println(a)
}
println(a)
```

## Chapter 8 Functions and Closures

### 8.1 METHODS

```
import scala.io.Source
object LongLines {
  def processFile(filename: String, width: Int) = {
    val source = Source.fromFile(filename)
    for (line <- source.getLines())
      processLine(filename, width, line)
  }
  private def processLine(filename: String,
    width: Int, line: String) = {
    if (line.length > width)
      println(filename + ": " + line.trim)
  }
}
```
This is very similar to what you would do in any object-oriented language. However, the concept of a function in Scala is more general than a method. Scala's other ways to express functions will be explained in the following sections.

### 8.2 LOCAL FUNCTIONS

Programs should be decomposed into many small functions that each do a well-defined task. Individual functions are often quite small. The advantage of
this style is that it gives a programmer many building blocks that can be flexibly composed to do more
difficult things. Each building block should be simple enough to be understood individually.

One problem with this approach is that all the helper function names can pollute the program namespace. In the interpreter this is not so much of a problem, but once functions are packaged in reusable classes and objects, it's desirable to hide the helper functions from clients of a class.In Java, your main tool for this purpose is the private method. This private-method approach works in
Scala as well.

### 8.3 FIRST-CLASS FUNCTIONS

Scala has **first-class** functions. Not only can you define functions and call them, but you can write down functions as unnamed literals and then pass them around as values. A function literal is compiled into a class that when instantiated at runtime is a **function value**.

Example of a function literal that adds one to a number: `(x: Int) => x + 1`. The `=>` designates that this function converts the thing on the left (any integer x) to the thing on the
right `(x + 1)`.

Function values are objects, so you can store them in variables if you like. yhey are functions, too, so you can invoke them using the usual parentheses function-call notation.

```
scala> var increase = (x: Int) => x + 1
increase: Int => Int = <function1>
scala> increase(10)
res0: Int = 11
```

### 8.4 SHORT FORMS OF FUNCTION LITERALS

```
scala> someNumbers.filter((x) => x > 0)
res5: List[Int] = List(5, 10)
```

The Scala compiler knows that x must be an integer, because it sees that you are immediately using the function to filter a list of integers (referred to by `someNumbers`). This is called **target typing** because the targeted usage of an expression (in this case, an argument `tosomeNumbers.filter()`) is allowed to influence the typing of that expression (in this case to determine the type of the x parameter).

### 8.5 PLACEHOLDER SYNTAX

To make a function literal even more concise, you can use **underscores** (`_`) as placeholders for one or more parameters, so long as each parameter appears only one time within the function literal. For example, `_ > 0` is very short notation for a function that checks whether a value is greater than zero: `scala> someNumbers.filter(_ > 0)`

Sometimes when you use underscores as placeholders for parameters, the compiler might not have enough information to infer missing parameter types. For example, suppose you write `_ + _` by itself In such cases, you can specify the types using a colon, like this: `scala> val f = (_: Int) + (_: Int)` 

### 8.6 PARTIALLY APPLIED FUNCTIONS

Although the previous examples substitute underscores in place of individual parameters, you can also replace an entire parameter list with an underscore. For example, rather than writing println(`_`), you could write `println _`. Here's an example: `someNumbers.foreach(println _)`  Scala treats this short form exactly as if you had written the following: `someNumbers.foreach(x => println(x))`. Thus, the underscore in this case is not a placeholder for a single parameter.

When you use an underscore in this way, you are writing a **partially applied function**. A partially applied function is an expression in which you don't supply all of the arguments needed by the function. Instead, you supply some, or none, of the needed arguments. 

```
scala> val a = sum _
a: (Int, Int, Int) => Int = <function3>
```

### 8.7 CLOSURES

```
scala> var more = 1
more: Int = 1

scala> val addMore = (x: Int) => x + more
addMore: Int => Int = <function1>

scala> addMore(10)
res16: Int = 11
```

A function literal with no free variables, such as `(x: Int) => x + 1`, is called a **closed term**, where a term is a bit of source code.

But any function literal with free variables, such as `(x: Int) => x + more`, is an **open term**. Therefore, any function value created at runtime from(x: Int) => x + more will, by definition, require that a binding for its free variable, more, be captured.

### 8.8 SPECIAL FUNCTION CALL FORMS

Scala supports repeated parameters, named arguments, and default arguments.

#### Repeated parameters

Scala allows you to indicate that the last parameter to a function may be repeated. This allows clients to pass variable length argument lists to the function. To denote a repeated parameter, place an asterisk after the type of the parameter. For example:
```
scala> def echo(args: String*) =
  for (arg <- args) println(arg)
echo: (args: String*)Unit
```
Defined this way, echo can be called with zero to many String arguments:
```
scala> echo()
scala> echo("one")
one
scala> echo("hello", "world!")
hello
world!
```

#### Named arguments
```
scala> def speed(distance: Float, time: Float): Float =
distance / time
speed: (distance: Float, time: Float)Float
scala> speed(100, 10)
res27: Float = 10.0
``` 
Named arguments allow you to pass arguments to a function in a different order. The syntax is simply ,that each argument is preceded by a parameter name and an equals sign. For example, the following call to speed is equivalent to speed(100,10):
```
scala> speed(time = 10, distance = 100)
res29: Float = 10.0
```

#### Default parameter values

Scala lets you specify default values for function parameters.
```
def printTime2(out: java.io.PrintStream = Console.out, divisor: Int = 1) = out.println("time = " + System.currentTimeMillis()/divisor)
```
### 8.9 TAIL RECURSION

A **tail-recursive** function will not build a new stack frame for each call; all calls will execute in a single frame. This may surprise a programmer inspecting a stack trace of a program that failed. For example, this function calls itself some number of times then throws an exception. 
```
def boom(x: Int): Int = 
  if (x == 0) throw new Exception("boom!") 
  else boom(x - 1) + 1
```
This function is not tail recursive, because it performs an increment operation after the recursive call. You'll get what you expect when you run it:
```
scala> boom(3)
java.lang.Exception: boom!
at .boom(<console>:5)
at .boom(<console>:6)
at .boom(<console>:6)
at .boom(<console>:6)
at .<init>(<console>:6)
```
If you now modify boom so that it does become tail recursive:
```
def bang(x: Int): Int =
  if (x == 0) throw new Exception("bang!")
  else bang(x - 1)

scala> bang(5)
java.lang.Exception: bang!
at .bang(<console>:5)
at .<init>(<console>:6) ...
```
This time, you see only a single stack frame for bang. You might think that bang crashed before it called itself, but this is not the case.

## Chapter 9: Control Abstraction

### 9.1 REDUCING CODE DUPLICATION

**Higher-order** functions—functions that take functions as parameters—give you extra opportunities to condense and simplify code. One benefit of higher-order functions is they enable you to create control abstractions that allow you to reduce code duplication.

### 9.2 SIMPLIFYING CLIENT CODE

Here's a method that uses this approach to determine whether a passedList contains a negative number:
```
def containsNeg(nums: List[Int]): Boolean = {
  var exists = false
  for (num <- nums)
    if (num < 0)
      exists = true
  exists
}

scala> containsNeg(List(1, 2, 3, 4))
res0: Boolean = false
scala> containsNeg(List(1, 2, -3, 4))
res1: Boolean = true
```
A more concise way to define the method, though, is by calling the higher-order functionexists on the passed List, like this:

```
def containsNeg(nums: List[Int]) = nums.exists(_ < 0)
```

### 9.3 CURRYING

A **curried function** is applied to multiple argument lists, instead of just one. Instead of one list of two Intparameters,
you apply this function to two lists of one Int parameter each. 

```
scala> def curriedSum(x: Int)(y: Int) = x + y
curriedSum: (x: Int)(y: Int)Int

scala> curriedSum(1)(2)
res5: Int = 3

```
What's happening here is that when you invoke curriedSum, you actually get two traditional function invocations back to back.

### 9.4 WRITING NEW CONTROL STRUCTURES

Any time you find a control pattern repeated in multiple parts of your code, you should think about implementing it as a new control structure.

## Chapter 10: Composition and Inheritance

### 10.3 DEFINING PARAMETERLESS METHODS

The recommended convention is to use a parameterless method whenever there are no parameters and the method accesses mutable state only by reading fields of the containing object (in particular, it does not change mutable state). This convention supports the uniform access principle,[1] which says that client code should not be affected by a decision to implement an attribute as a field or method.

### 10.4 EXTENDING CLASSES

Subtyping means that a value of the subclass can be used wherever a value of the superclass is required. For example:`val e: Element = new ArrayElement(Array("hello"))` Variable `e` is defined to be of type Element, so its initializing value should also be an Element. In fact, the initializing value's type is ArrayElement. This is OK, because class ArrayElement extends class Element, and as a result, the type ArrayElement is compatible with the type Element.

### 10.9 POLYMORPHISM AND DYNAMIC BINDING
You saw in Section 10.4 that a variable of type Element could refer to an object of typeArrayElement. The name for this phenomenon is polymorphism, which means "many shapes" or "many forms." In this case, Element objects can have many forms.[7]

**Dynamically bound**. This means that the actual method implementation invoked is determined at run time based on the class of the object, not the type of the variable or expression. 

### 10.13 DEFINING A FACTORY OBJECT
A factory object contains methods that construct other objects. Clients would then use these factory methods to construct objects, rather than constructing the objects directly with new. An advantage of this approach is that object creation can be centralized and the details of how objects are represented with classes can be hidden. This hiding will both make your library simpler for clients to understand, because less detail is exposed, and provide you with more opportunities to change your library's implementation later without breaking client code.

## Chapter 11 Scala's Hierarchy

In Scala, every class inherits from a common superclass named Any. Because every class is a subclass of Any, the methods defined in Any are "universal" methods: they may be invoked on any object. Scala also defines some interesting classes at the bottom of the hierarchy, Null and Nothing, which essentially act as common subclasses. 

### 11.1 SCALA'S CLASS HIERARCHY
The root class Any has two subclasses: AnyVal and AnyRef. AnyVal is the parent class of value classes in Scala. While you can define your own value classes (see Section 11.4), there are nine value classes built into Scala: Byte, Short, Char, Int, Long, Float, Double, Boolean, and Unit. The first eight of these correspond to Java's primitive types, and their values are represented at run time as Java's primitive values. The instances of these classes are all written as literals in Scala. For example, 42 is an instance of Int, 'x' is an instance of Char, and false an instance ofBoolean. You cannot create instances of these classes using new. This is enforced by the "trick" that value classes are all defined to be both abstract and final.

### 11.2 HOW PRIMITIVES ARE IMPLEMENTED

In fact, Scala stores integers in the same way as Java—as 32-bit words. This is important for efficiency on the JVM and also for interoperability with Java libraries. Class Null is the type of the null reference; it is a subclass of every reference class (i.e., every class that itself inherits from AnyRef). Null is not compatible with value types. 

### 11.3 BOTTOM TYPES

the two classes scala.Null andscala.Nothing. These are special types that handle some "corner cases" of Scala's object-oriented type system in a uniform way

## Chapter 15: Case Classes and Pattern Matching

A pattern match includes a sequence of alternatives, each starting with the keyword case. Each alternative includes a pattern and one or more expressions, which will be evaluated if the pattern matches. An arrow symbol => separates the pattern from the expressions.A match expression is evaluated by trying each of the patterns in the order they are written. The first pattern that matches is selected, and the part following the arrow is selected and executed.

Match expressions can be seen as a generalization of Java-style switches. However, there are three differences to keep in mind: 
- First, match is an expression in Scala (i.e., it always results in a value). 
- Second, Scala's alternative expressions never "fall through" into the next case. 
- Third, if none of the patterns match, an exception named MatchError is thrown. This means you always have to make sure that all cases are covered, even if it means adding a default case where there's nothing to do.

```
expr match {
  case BinOp(op, left, right) =>
    println(expr + " is a binary operation")
  case _ =>
}
```

### 15.2 KINDS OF PATTERNS
The ****wildcard** pattern (_) matches any object whatsoever. You have already seen it used as a default, catch-all alternative. Wildcards can also be used to ignore parts of an object that you do not care about.

A **constant** pattern matches only itself. Any literal may be used as a constant. Any val or singleton object can be used as a constant.

A **variable** pattern matches any object, just like a wildcard. But unlike a wildcard, Scala binds the variable to whatever the object is. You can then use this variable to act on the object further.

A **constructor** pattern looks like `BinOp("+", e, Number(0))`. It consists of a name (BinOp) and then a number of patterns within parentheses: "+", e, and Number(0). Assuming the name designates a case class, such a pattern means to first check that the object is a member of the named case class, and then to check that the constructor parameters of the object match the extra patterns supplied.

You can match against **sequence** types, like List or Array, just like you match against case classes. Use the same syntax, but now you can specify any number of elements within the pattern.

You can match against **tuples** too. A pattern like (a, b, c) matches an arbitrary 3-tuple.

You can use a **typed pattern** as a convenient replacement for type tests and type casts.

```
def generalSize(x: Any) = x match {
  case s: String => s.length
  case m: Map[_, _] => m.size
  case _ => -1
}
```

### 15.3 PATTERN GUARDS

A pattern guard comes after a pattern and starts with an if. The guard can be an arbitrary boolean expression, which typically refers to variables in the pattern. If a pattern guard is present, the match succeeds only if the guard evaluates to true.


## Chapter 16 Working with Lists  

Lists are quite similar to arrays, but there are two important differences. First, lists are immutable. That is, elements of a list cannot be changed by assignment. Second, lists have a recursive structure (i.e.,a linked list), whereas arrays are flat.

### 16.2 THE LIST TYPE

Like arrays, lists are homogeneous: the elements of a list all have the same type. The list type in Scala is covariant. This means that for each pair of types S and T, if S is a subtype of T, then List[S] is a subtype of List[T]. For instance, List[String] is a subtype ofList[Object]. This is natural because every list of strings can also be seen as a list of objects.

### 16.3 CONSTRUCTING LISTS

All lists are built from two fundamental building blocks, Nil and :: (pronounced "cons"). Nilrepresents the empty list. The infix operator, ::, expresses list extension at the front.

### 16.4 BASIC OPERATIONS ON LISTS

- `head` - returns the first element of a list
- `tail` - returns a list consisting of all elements except the first
- `isEmpty` -  returns true if the list is empty

### 16.5 LIST PATTERNS

Lists can also be taken apart using pattern matching. List patterns correspond one-by-one to list expressions.

### 16.6 FIRST-ORDER METHODS ON CLASS LIST

A method is *****first-order** if it does not take any functions as arguments.

An operation similar to `::` is list concatenation, written `:::`. Unlike `::`, `:::` takes two lists as operands. The result of `xs ::: ys` is a new list that contains all the elements of `xs`, followed by all the elements of `ys`.


**Reversing lists: reverse**
```
scala> abcde.reverse
res6: List[Char] = List(e, d, c, b, a)
```

## Chapter 17 Working with Other Collections

### 17.1 SEQUENCES
Sequence types let you work with groups of data lined up in order. Because the elements are ordered, you can ask for the first element, second element, 103rd element, and so on. 

#### List
Perhaps the most important sequence type to know about is class List, the immutable linked-list described in detail in the previous chapter. Lists support fast addition and removal of items to the beginning of the list, but they do not provide fast access to arbitrary indexes because the implementation must iterate through the list linearly.
` scala> val colors = List("red", "blue", "green")`

#### Arrays

Arrays allow you to hold a sequence of elements and efficiently access an element at an arbitrary position, either to get or update the element, with a zero-based index.
` scala> val fiveInts = new Array[Int](5)` 
` scala> val fiveToOne = Array(5, 4, 3, 2, 1)` 
Scala arrays are represented in the same way as Java arrays. So, you can seamlessly use existing Java methods that return arrays.

#### List buffers
A ListBuffer is a mutable object (contained in package scala.collection.mutable), which can help you build lists more efficiently when you need to append. ListBuffer provides constant time append and prepend operations. You append elements with the += operator, and prepend them with the+=: operator. When you're done building, you can obtain a List by invoking toList on theListBuffer. 

```
scala> val buf = new ListBuffer[Int]
scala> buf += 1
scala> buf += 2
res5: buf.type = ListBuffer(1, 2)
scala> 3 +=: buf
res7: buf.type = ListBuffer(3, 1, 2)
```
#### Array buffers
An ArrayBuffer is like an array, except that you can additionally add and remove elements from the beginning and end of the sequence. All Array operations are available, though they are a little slower due to a layer of wrapping in the implementation.

### 17.2 SETS AND MAPS
By default when you write "Set" or "Map" you get an immutable object. If you want the mutable variant, you need to do an explicit import. Scala gives you easier access to the immutable variants, as a gentle encouragement to prefer them over their mutable counterparts.

The key characteristic of sets is that they will ensure that at most one of each object, as determined by ==, will be contained in the set at any one time. 

## Chapter 19 Type Parameterization

Type parameterization allows you to write generic classes and traits. For example, sets are generic and take a type parameter: they are defined as Set[T]. As a result, any particular set instance might be
a Set[String], a Set[Int], etc., but it must be a set of something. Unlike Java, which allows raw
types, Scala requires that you specify type parameters. Variance defines inheritance relationships of parameterized types, such as whether a Set[String], for example, is a subtype of Set[AnyRef].

### 19.1 FUNCTIONAL QUEUES

A functional queue is a data structure with three operations:
1. head - returns the first element of the queue
2. tail - returns a queue without its first element
3. enqueue - returns a new queue with a given element appended at the end

Unlike a mutable queue, a functional queue does not change its contents when an element is appended. Instead, a new queue is returned that contains the element. 

```
scala> val q = Queue(1, 2, 3)
q: Queue[Int] = Queue(1, 2, 3)
scala> val q1 = q enqueue 4
q1: Queue[Int] = Queue(1, 2, 3, 4)
scala> q
res0: Queue[Int] = Queue(1, 2, 3)
```
Purely functional queues also have some similarity with lists. Both are so called fully persistent data structures, where old versions remain available even after extensions or modifications. Both support head and tail operations. But where a list is usually extended at the front, using a :: operation, a queue is extended at the end, using enqueue.

### 19.2 INFORMATION HIDING

#### Private constructors and factory methods

In Java, you can hide a constructor by making it private. In Scala, the primary constructor does not have an explicit definition; it is defined implicitly by the class parameters and body. Nevertheless, it is still possible to hide the primary constructor by adding a private modifier in front of the class parameter list: `class Queue[T] private (` The private modifier between the class name and its parameters indicates that the constructor of Queue is private: it can be accessed only from within the class itself and its companion object. 

### An alternative: private classes
Private constructors and private members are one way to hide the initialization and representation of a class. Another more radical way is to hide the class itself and only export a trait that reveals the public interface of the class. 

```
trait Queue[T] {
    def head: T
    def tail: Queue[T]
    def enqueue(x: T): Queue[T]
}
object Queue {
    def apply[T](xs: T*): Queue[T] =
        new QueueImpl[T](xs.toList, Nil)
    ...
    ...
 }
```
### 19.3 VARIANCE ANNOTATIONS

trait Queue enables you to specify parameterized types, such as Queue[String],Queue[Int], or Queue[AnyRef]: Thus, Queue is a trait and Queue[String] is a type. Queue is also called a type constructor because you can construct a type with it by specifying a type parameter. The type constructor Queue "generates" a family of types, which includes Queue[Int],Queue[String], and Queue[AnyRef].

You can also say that Queue is a generic trait. (Classes and traits that take type parameters are "generic," but the types they generate are "parameterized," not generic.) The term **"generic"** means that you are defining many specific types with one generically written class or trait.

` trait Queue[+T] { ... }` - Prefixing a formal type parameter with a `+` indicates that subtyping is covariant (flexible) in that parameter.

Besides `+`, there is also a prefix `-`, which indicates contravariant subtyping. `trait Queue[-T] { ... }`. Then if T is a subtype of type S, this would imply that Queue[S] is a subtype of Queue[T] (which in the case of queues would be rather surprising!). 

The `+` and `- `symbols you can place next to type parameters are called **variance annotations**.

#### Variance and arrays
Scala treats arrays as nonvariant (rigid), so an Array[String] is not considered to conform to an Array[Any]. However, sometimes it is necessary to interact with legacy methods in Java that use an Object array as a means to emulate a generic array. 

### 19.4 CHECKING VARIANCE ANNOTATIONS
#### THE FAST TRACK
The most important thing to understand is that the Scala compiler will check any variance annotations you place on type parameters. For example, if you try to declare a type parameter to be covariant (by adding a +), but that could lead to potential runtime errors, your program won't compile.

### 19.5 LOWER BOUNDS

You can generalize enqueue by making it polymorphic (i.e., giving the enqueue method itself a type parameter) and using a lower bound for its type
parameter. 

The new definition gives enqueue a type parameter U, and with the syntax, "U >: T", defines T as the lower bound for U. As a result, U is required to be a supertype of T.[1] The parameter toenqueue is now of type U instead of type T, and the return value of the method is now Queue[U]instead of Queue[T].

### 19.7 OBJECT PRIVATE DATA

OBject private members can be accessed only from within the object in which they are defined. It turns out that accesses to variables from the same object in which they are defined do not cause problems with variance.Scala's variance checking rules contain a special case for object private definitions. Such definitions are omitted when it is checked that a type parameter with either a + or -annotation occurs only in positions that have the same variance classification.

### 19.8 UPPER BOUNDS

An upper bound is specified similar to a lower bound, except instead of the `>:` symbol used for lower bounds, you use a `<:` symbol. With the "T <: Ordered[T]" syntax, you indicate that the type parameter, T, has an upper bound,Ordered[T]. This means that the element type of the list passed to orderedMergeSort must be a subtype of Ordered. 


## Chapter 23 For Expressions Revisited

### 23.1 FOR EXPRESSIONS
Generally, a for expression is of the form: `for ( seq ) yield expr`
An example is the for expression: `for (p <- persons; n = p.name; if (n startsWith "To")) yield n`

As mentioned inSection
7.3 here, you can also enclose the sequence in braces instead of parentheses. Then the semicolons
become optional:
```
for {
  p <- persons
  n = p.name
  if (n startsWith "To")
} yield n
```




[//]: # (endof PS )
---
---
---

# Concepts in Programming Languages by Mitchell (CPL)

## Chapter 1: Introduction

### 1.1 PROGRAMMING LANGUAGES

Programming languages are the medium of expression in the art of computer programming. An ideal programming language will make it easy for programmers to write programs succinctly and clearly.

There are many difficult trade-offs in programming language design. Some language features make it easy for us to write programs quickly, but may make it harder for us to design testing tools or methods. Some language constructs make it easier for a compiler to optimize programs, but may make programming cumbersome. Because different computing environments and applications require different program characteristics, different programming language designers have chosen different trade-offs.



### 1.2 GOALS

- To understand the design space of programming languages.
- To develop a better understanding of the languages we currently use by comparing them with other languages.
- To understand the programming techniques associated with various language features.-
- Computability: Some problems cannot be solved by computer
- Static analysis: There is a difference between compile time and run time. At compile time, the program is known but the input is not. At run time, the program and the input are both available to the run-time system.
- Expressiveness versus efficiency: There are many situations in which it would be convenient to have a programming language implementation do something automatically.

### 1.3 PROGRAMMING LANGUAGE HISTORY

The history of modern programming languages begins around 1958-1960 with the development of Algol, Cobol, Fortran, and Lisp.

## Chapter 3: Lisp-Functions, Recursion, and Lists

### 3.1 LISP HISTORY
The Lisp programming language was developed at MIT in the late 1950s for research in artificial intelligence (AI) and symbolic computation. The name Lisp is an acronym for the LISt Processor. Lists comprise the main data structure of Lisp.

### 3.2 GOOD LANGUAGE DESIGN
Most successful language design efforts share three important characteristics with the Lisp project:
- **Motivating Application:** The language was designed so that a specific kind of program could be written more easily.
- **Abstract Machine:** There is a simple and unambiguous program execution model.
- **Theoretical Foundations:** Theoretical understanding was the basis for including certain capabilities and omitting others.

### 3.3 BRIEF LANGUAGE OVERVIEW
Here are some examples of Lisp expressions, with corresponding infix form for comparison.
```
(+12345) (1 + 2 + 3 + 4 + 5)
(* (+23)(+45)) ((2 + 3) * (4 + 5))
(f x y) f(x, y)
```

#### Atoms

Lisp programs compute with atoms and cells. Atoms include integers, floating-point numbers, and symbolic atoms.
Symbolic atoms may have more than one letter.

#### S-Expressions and Lists

The basic data structures of Lisp are dotted pairs, which are pairs written with a dot between the two parts of the pair. Putting atoms or pairs together, we can write symbolic expressions in a form traditionally called S-expressions. 

#### Functions and Special Forms

The basic functions of Historical Lisp are the operations: `cons car cdr eq atom`

We also use numeric functions such as `+`, `−`, and `*`, writing these in the usual Lisp prefix notation. The function `cons` is used to combine two atoms or lists, and `car` and `cdr` take lists apart. The function eq is an equality test and atom tests
whether its argument is an atom.

The functions `cond`, `lambda`, `define` , and `quote` are technically called **special forms** since an expression beginning with one of these special functions is evaluated without evaluating all of the parts of the expression. The language summarized up to this point is called **pure Lisp**. A feature of pure Lisp is that expressions do not have
side effects.

#### Evaluation of Expressions

The basic structure of the Lisp interpreter or compiler is the read-eval-print loop. This means that the basic action of the interpreter is to read an expression, evaluate it, and print the value. If the expression defines the meaning of some symbol, then the association between the symbol and its value is saved so that the symbol can be used in expressions that are typed in later.

ere are some additional examples of Lisp expressions and their values:
```
(+ 4 5)             expression with value 9
(+ (+ 1 2)(+ 4 5))  first evaluate 1+2, then 4+5, then 3+9 to get value 12
(quote (+ 1 2))     evaluates to a list (+ 1 2)
'(+ 1 2)            same as (quote (+ 1 2))    
```

#### Static and Dynamic Scope 

Historically, Lisp was a dynamically scoped language. This means that a variable inside an expression could refer to a different value if it is passed to a function that declared this variable differently. When Scheme was introduced in 1978, it was a statically scoped variant of Lisp. The difference between static and dynamic scope is not covered in this chapter.

### 3.4 INNOVATIONS IN THE DESIGN OF LISP

#### 3.4.1 Statements and Expressions

Just as virtually all natural languages have certain basic parts of speech, such as nouns, verbs, and adjectives, there
are programming language parts of speech that occur in most languages. The most basic programming language parts of speech are expressions, statements, and declarations.

- Expression: a syntactic entity that may be evaluated to determine its value.
- Statement: a command that alters the state of the machine in some explicit way.
- Declaration: a syntactic entity that introduces a new identifier, often specifying one or more attributes.  

Lisp is an expression-based language, meaning that the basic constructs of the language are expressions, not statements. In fact, pure Lisp has no statements and no expressions with side effects.

#### 3.4.2 Conditional Expressions

The Lisp conditional expression `(cond (p1 e 1) ...(p n e n))` could be written as 
```
if p1 then e1
    else if p 2 then e2
    ...
        else if pn then en
       else no_value
```
Here are some example conditional expressions and their values:
```
(cond ((< 2 1) 2) ((< 1 2) 1))  has value 1
(cond ((< 2 1) 2) ((< 3 2) 3))  is undefined
(cond (diverge 1) (true 0))     is undefined, if diverge does not terminate
(cond (true 0) (diverge 1))     has value 0
```

#### Cons Cells

Cons cells (or dotted pairs) are the basic data structure of the Lisp abstract machine. Only the letters `a` and `d` remain in the acronyms `car` (for "contents of the address register") and `cdr` (for "contents of the decrement register").

Cons cells:
- provide a simple model of memory in the machine
- are efficiently implementable
- are not tightly linked to particular computer architecture

There are five basic functions on cons cells, which are evaluated as follows:
- `atom` - a function with one argument: If a value is an atom, then the word storing the value has a special bit pattern in its address part that flags the value as being an atom.
- `eq` , a function with two arguments: compares two arguments for equality by checking to see if they are stored in the same location.
- `cons` , a function with two arguments: The expression ( cons x y ) is evaluated as follows:
    1. Allocate new cell c .
    2. Set the address part of c to point to the value of x .
    3. Set the decrement part of c to point to the value of y .
    4. Return a pointer to c .
- `car` a function with one argument: If the argument is a cons cell c , then return the contents of the address register of c.
- `cdr` a function with one argument: If the argument is a cons cell c , then return the contents of the decrement register of c .

#### 3.4.4 Programs as Data
One feature that sets Lisp apart from many other languages is that it is possible for a program to build a data structure that represents an expression and then evaluates the expression as if it were written as part of the program. This is done with the function `eval` .

#### 3.4.6 Recursion

Lisp lambda makes it possible to write **anonymous functions**, which are functions that do not have a declared name.

#### 3.4.7 Higher-Order Functions

The phrase **higher-order function** means a function that either takes a function as an argument or returns a function asa result (or both). 

This use of higher-order comes from a convention that calls a function whose arguments and results are not functions a **first-order** function. A function that takes a first-order function as an argument is called a second-order function, functions on second-order functions are called third-order functions, and so on.

If `f` and `g` are mathematical functions, say functions on the integers, then their composition `f ? g` is the function such that for every integer `x`, we have `( f ? g)(x) = f (g(x))`. We can write composition as a Lisp function compose that takes two functions as arguments and returns their
composition:
```(define compose (lambda (f g) (lambda (x) (f (g x)))))```
The first lambda is used to identify the arguments to compose . The second lambda is used to define the return value of the function, which is a function.

#### 3.4.8 Garbage Collection

In computing, **garbage** refers to memory locations that are not accessible to a program.

Here is a simple example called **mark-and-sweep**. The name comes from the fact that the algorithm first marks all of the locations reachable from the
program, then "sweeps" up all the unmarked locations as garbage.

**Mark-and-Sweep Garbage Collection**
1. Set all tag bits to 0
2. Start from each location used directly in the program. Follow all links, changing the tag bit of each cell visited to 1.
3. Place all cells with tags still equal to 0 on the free list.

#### 3.4.9 Pure Lisp and Side Effects

Pure Lisp expressions do not have side effects, which are visible changes in the state of the machine as the result of evaluating an expression. However, for efficiency, even early Lisp had expressions with side effects.

### 3.5 CHAPTER SUMMARY: CONTRIBUTIONS OF LISP

Lisp is an elegant programming language designed around a few simple ideas. The language was intended for  symbolic computation, as opposed to the kind of numeric computation that was dominant in most programming moutside of artificial intelligence research in 1960.

Three important aspects of programming language design contributed to the success of Lisp: a specific motivation application, an unambiguous program execution model,and attention to theoretical considerations.

Lisp was designed with concern for the mathematical class of partial recursive functions. Lisp syntax for function expressions is based on lambda calculus.

The following contributions are some that are important to the field of programming languages:
- Reursive functions. Lisp programming is based cons functions and recursion instead of assignment and while loops.
- Lists. The basic data structure in early Lisp was the cons cell. The main use of cons cells in modern forms of Lisp is for building lists, and lists are used for everything.
- Programs as data. - In Lisp, a program can build the list representation of a function or other forms of expression and then use the eval function to evaluate the expression.
- Garbage collection - Lisp was the first language to manage memory for the programmer automatically.

## Chapter 5: The Algol Family and ML

The Algol-like programming languages evolved in parallel with the Lisp family of languages, beginning with Algol 58 and Algol 60 in the late 1950s. In this chapter, we look at some of the historically important languages from the Algol family, including Algol 60, Pascal, and C.

### 5.1 THE ALGOL FAMILY OF PROGRAMMING LANGUAGES

The main characteristics of the Algol family are the familiar colon-separated sequence of statements used in most languages today, block structure, functions and procedures, and static typing.

In Algol, the two-character sequence `:=` is used for assignment, and the single character `=` for test for equality. 

**Pass-by-Name.** Perhaps the strangest feature of Algol 60, in retrospect, is the use of pass-by-name. In pass-by-name, the result of a procedure call is the same as if the formal parameter were substituted into the body of the procedure. This rule for defining the result of a procedure call by copying the procedure and substituting for the formal parameters is called the Algol 60 copy rule. 

**BNF.** An important by-product of the Algol 60 design effort was the invention of Backus Normal Form (or BNF), which was used in the Algol 60 report to define the well-formed programs of the language. BNF, summarized in Subsection 4.1.2, remains the standard notation for describing the syntax of programming languages. Although Algol 60 was very influential and commonly used in academic circles and in Europe, it was not a commercial success in the United States.

#### 5.1.3 Pascal

Pascal was design in the 1970s by Niklaus Wirth, who used the data-structuring ideas advanced by C.A.R. (Tony) Hoare. Wirth first designed and implemented a language called Algol W and then refined the design of Algol W to produce Pascal.

Although the use of Pascal declined in the 1990s, Pascal was one of the most widely used programming languages over approximately a 20-year period. Pascal was very successful as a programming language for teaching, in part because it was designed explicitly for this purpose. Pascal was also used for a significant number of production programming projects, including operating systems and applications for the Apple Macintosh.

An important contribution of the Pascal type system is the rich set of data-structuring concepts. These include records (similar to C structs), variant records (a form of union type), and subranges.

### 5.2 THE DEVELOPMENT OF C

There are several reasons for the success of C. One reason, which is unrelated to the design of the language it self, is the popularity of the Unix operating system, which was written in C.

C was originally designed and implemented from 1969 to 1973, as part of the Unix operating system project at Bell Laboratories. C was designed by Dennis Ritchie, one of the original designers of Unix, so that he and Ken Thompson could build Unix in a language that they liked.

#### C Arrays and Pointers

In C, pointers and arrays are declared differently, as if pointers and arrays are different types of values. For example, the following code declares a pointer p to an integer location and an array A of integers:
```
int*p;
int A[5];
```
 In C, arrays are effectively treated as pointers. To quote Dennis Ritchie's 1975 C Reference Manual,
> Every time an identifier of array type appears in an expression, it is converted into a pointer to the first member of the array.... By definition, the subscript operator [] is interpreted in such a way that "E1[E2]" is identical to "*((E1)+(E2))." Because of the conversion rules which apply to +, if E1 is an array and E2 is an integer, then E1[E2] refers to the E2-th member of E1.
There is no other programming language in widespread use that allows pointer arithmetic in this way.

#### Critique
Most C programmers have eventually come to consider the weak type checking of many C compilers to be a disadvantage. In fact, one of the most commonly cited advantages of C++ over C is the fact that C++ provides better type checking.

### 5.3 THE LCF SYSTEM AND ML

The following list enumerates our main reasons for looking at ML in some detail:
- ML illustrates most of the important concepts of the Lisp/Algol families of languages.
- ype systems have been an important part of programming language design from 1960 to the present day, and the ML type system is often considered the cleanest and most expressive type system to date.
- Because most readers are familiar with C and many have not written a lot of programs in significantly different languages, it is useful to have a language other than C to use for examples in the following chapters.
- ML allows higher-order functions and other constructions that are discussed in the following chapters.

One distinguishing feature of ML is its type system, which extends the successful Pascal type system in a number of ways. Unlike C, which has numerous loopholes, the ML type system is sound in a precise mathematical sense.

ML was designed as the **Meta- Language** (hence its name) of the LCF System. Its original purpose was for writing programs that would attempt to construct mathematical proofs.

More specifically, because a tactic is a function from formulas to proofs, the type of a tactic would be a function type: `tactic : formula → proof`

From this inspiration, Milner developed the first type-safe exception mechanism, one of the accomplishments that led to his Turing Award in 1991. Allowing for the possibility of exceptions, a function f that maps A to B, written as: `f:A → B` IN ML, means that, for all x in A, if f (x) terminates normally without raising an exception, then f (x) is in B.

### 5.4 THE ML PROGRAMMING LANGUAGE

Most ML compilers are based on the same kind of read-eval-print loop as many Lisp implementations. The standard way of interacting with the ML system is to enter expressions and declarations one at a time. As each is entered, the source code is type checked, compiled, and executed.

#### Expressions
```
--- <expression>;
val it = <print_value> : <type>
```

where "-" is the prompt for user input and the line below is output from the ML compiler and run-time system. The preceding lines show that if you type in an expression, the compiler will compile the expression and evaluate it. The output is a bit cryptic: it is a special identifier bound to the value of the last expression entered, so it = <print_value> : <type> means that the value of the expression is <print_value> and this is a value of type <type>. It is probably easier to understand the idea from a few examples. Here are four lines of input and the resulting compiler output:
    
```
--- (5+3) -2;
val it = 6 : int
```

#### Declarations

```
--- val <identifier> = <expression>;
val <identifier> = <print_value> : <type>
```

The keyword val stands for value. When a declaration is given to the compiler, the value associated with the identifier is computed and bound to that identifier. Because the value of the expression used in a declaration has a name, the compiler output uses this name instead of it for the value of the expression. Here are some examples:

```
--- val x=7+2; 
val x = 9 : int
```

Functions can be declared with the keyword fun (which stands for function) instead of val. The general form of user input and compiler output is

```
--- fun <identifier> <arguments> = <expression>; 
val <identifier> = fn <arg_type> → <result_type>
```

This declares a function whose name is <identifier>. The argument type is determined by the form of <arguments> and the result type is determined by the form of <expression>.
    
```
--- fun f(x) = x + 5; 
val f = fn : int → int
```

This declaration binds a function value to the identifier f. The value of f is a function from integers to integers. 

#### Unit

`( ) : unit` 

Like void in C, unit is used as the result type for functions that are executed only for side effects. 

#### Bool

```
true : bool 
false : bool
```

There are also ML Boolean operations for and, or, not, and so on. These are similar to AND, OR, and NOT in Pascal or &&, ?, and ! in C, with some minor differences. Negation is written as not, conjunction (and) is written as andalso and disjunction (or) is written as orelse.

#### Integers

Many ML integer expressions are written in the usual way, with number constants and standard arithmetic operations:

#### Strings

Strings are written as a sequence of symbols between double quotes:

#### Real

The ML type for floating-point numbers is real. For reasons that will be easier to understand when we come to type inference, ML requires a decimal point in real constants. The arithmetic operators +, -, and * may be applied to either integers or real numbers. 

#### Tuples

A tuple may be a pair, triple, quadruple, and so on. In ML, tuples may be formed of any types of values. Tuple values are written with parentheses and tuple types are written with *. 

#### Records

Like Pascal records and C structs, ML records are similar to tuples, but with named components. Record values and record types are written with curly braces. 

#### Lists

ML lists can have any length, but all elements of a list must have the same type. We can write lists by listing their elements, separated by commas, between brackets.

#### Value Declarations

```
val <pattern> = <exp> ;
```
a pattern can be an identifier, a tuple pattern, a list cons pattern, a record pattern, or a declared data-type constructor pattern. A tuple pattern is a sequence of patterns between parentheses, a list cons pattern is two patterns separated by double colons, a record pattern is a recordlike expression with each field in the form of a pattern, and a constructor pattern is an identifier (a declared constructor) applied to the right number of pattern arguments. 


#### Function Declarations

```
fun f( <pattern> ) = <exp>
```

### 5.4.6 ML Summary

ML is a programming language that encourages programming with functions. It is easy to define functions with function arguments and function return results. ML has an expressive type system. There are basic types for many common kinds of computable values, such as Booleans, integers, strings, and reals. The ML type system is often called a strong type system, as every expression has a type and there are no mechanisms for subverting the type system.
ML has several forms that allow programmers to define their own types and type constructors. 


## Chapter 6: Type Systems and Type Inference

Because programming languages are designed to help programmers organize computational constructs and use them correctly, many programming languages organize data and computations into collections called types. In this chapter, we look at the reasons for using types in programming languages, methods for type checking, and some typing issues such as polymorphism, overloading, and type equality.

### 6.1 TYPES IN PROGRAMMING

A well-designed program uses concepts related to the problem being solved. For example, a banking program will be organized around concepts common to banks, such as accounts, customers, deposits, withdrawals, and transfers.

A type error occurs when a computational entity, such as a function or a data value, is used in a manner that is inconsistent with the concept it represents. For example, if an integer value is used as a function, this is a type error. 

The reason why many people find the concept of type error confusing is that type errors generally depend on the concepts defined in a program or programming language, not the way that programs are executed on the underlying hardware. To be specific, it is just as much of a type error to apply an integer operation to a floating-point argument as it is to apply a floating-point operation to an integer argument. It does not matter which causes a hardware interrupt on any particular computer.

### 6.2 TYPE SAFETY AND TYPE CHECKING

A programming language is type safe if no program is allowed to violate its type distinctions. Sometimes it is not completely clear what the type distinctions are in a specific programming language.

| Safety Example | languages | Explanation |
| --- | --- | --- |
| Not safe | C and C++ | Type casts, pointer arithmetic|
| Almost safe | Pascal | Type casts, pointer arithmetic|
| Safe | Lisp, ML, Smalltalk, Java | Explicit deallocation; dangling pointers Complete type checking| 

- **Type Casts.** Type casts allow a value of one type to be used as another type. 
- **Pointer Arithmetic.** C pointer arithmetic is not type safe. The expression *(p+i) has type A if p is defined to have type A*. Because the value stored in location p+i might have any type, an assignment like x = *(p+i) may store a value of one type into a variable of another type and therefore may cause a type error.
- **Explicit Deallocation and Dangling Pointers.** In Pascal, C, and some other languages, the location reached through a pointer may be deallocated (freed) by the programmer. This creates a dangling pointer, a pointer that points to a location that is not allocated to the program. If p is a pointer to an integer, for example, then after we deallocate the memory referenced by p, the program can allocate new memory to store another type of value. This new memory may be reachable through the old pointer p, as the storage allocation algorithm may reuse space that has been freed. The old pointer p allows us to treat the new memory as an integer value, as p still has type int. This violates type safety.

#### Compile-Time and Run-Time Checking

- **Run-Time Checking.** In programming languages with run-time type checking, the compiler generates code so that, when an operation is performed, the code checks to make sure that the operands have the correct type. 
- **Compile-Time Checking.** Many modern programming languages are designed so that it is possible to check expressions for potential type errors. In these languages, it is common to reject programs that do not pass the compile-time type checks. An advantage of compile-time type checking is that it catches errors earlier than run-time checking does: A program developer is warned about the error before the program is given to other users or shipped as a product.
- **Conservativity of Compile-Time Checking.** A property of compile-time type checking is that the compiler must be conservative. This mean that compile-time type checking will find all statements and expressions that produce run-time type errors, but also may flag statements or expressions as errors even if they do not produce run-time errors. 

| Form of Type Checking | Advantages | Disadvantages| 
| --- | --- | --- |
| Run-time |  Prevents type errors| Slows program execution |
| Compile-time | Prevents type errors, Eliminates run-time tests, Finds type errors before execution and run-time tests | May restrict programming because tests are conservative. | 

**Combining Compile-Time and Run-Time Checking.** Most programming languages actually use some combination of compile-time and run-time type checking.

### 6.3 TYPE INFERENCE

Type inference is the process of determining the types of expressions based on the known types of some symbols that appear in them. The difference between type inference and compile-time type checking is really a matter of degree. A type-checking algorithm goes through the program to check that the types declared by the programmer agree with the language requirements.

#### 6.3.2 Type-Inference Algorithm

The ML type-inference algorithm uses the following three steps:
1. A assign a type to the expression and each subexpression. 
2. Generates a set of constraints on types, using the parse tree of the expression. These constraints reflect the fact that if a function is applied to an argument. 
3. Solve these constraints by means of unification, which is a substitution-based algorithm for solving systems of equations. 

### 6.4 POLYMORPHISM AND OVERLOADING

Polymorphism, which literally means "having multiple forms," refers to constructs that can take on different types as needed. 

#### Parametric polymorphism
In which a function may be applied to any arguments whose types match a type expression involving type variables; The main characteristic of parametric polymorphism is that the set of types associated with a function or other value is given by a type expression that contains type variables. In parametric polymorphism, a function may have infinitely many types, as there are infinitely many ways of replacing type variables with actual types. The sort function, for example, may be used to sort lists of integers, lists of lists of integers, lists of lists of lists of integers, and so on.

Parametric polymorphism may be implicit or explicit. In explicit parametric polymorphism, the program text contains type variables that determine the way that a function or other value may be treated polymorphically. 

Parametric polymorphism can be contrasted with overloading. A symbol is overloaded if it has two (or more) meanings, distinguished by type, and resolved at compile time.
 
- **ad hoc polymorphism**, another term for overloading, in which two or more implementations with different types are referred to by the same name;
- **subtype polymorphism,** in which the subtype relation between types allows an expression to have many possible types.

## 6.5 TYPE DECLARATIONS AND TYPE EQUALITY

### 6.5.1 Transparent Type Declarations

- **transparent**, meaning an alternative name is given to a type that can also be expressed without this name. 
- **opaque**, meaning a new type is introduced into the program that is not equal to any other type.

## 6.6 CHAPTER SUMMARY

### Reasons for Using Types

- Naming and organizing concepts: Functions and data structures can be given types that reflect the way these computational constructs are used in a program.
- Making sure that bit sequences in computer memory are interpreted consistently: Type checking keeps operations from being applied to operands in incorrect ways.
- Providing information to the compiler about data manipulated by the program: In languages in which the compiler can determine the type of a data structure, for example, the type information can be used to determine the relative location of a part of this structure. 

### Type Inference

Type inference is the process of determining the types of expressions based on the known types of some of the symbols that appear in them.

The following steps are used for type inference:
1. Assign a type to the expression and each subexpression by using the known type of a symbol of a type variable.
2. Generate a set of constraints on types by using the parse tree of the expression.
3. Solve these constraints by using unification, which is a substitution-based algorithm for solving systems of equations.

### Polymorphism and Overloading

The difference between parametric polymorphism and overloading is that parametric polymorphism allows one algorithm to be given many types, whereas overloading involves different algorithms. For example, the function + is overloaded in many languages. In an expression adding two integers, the integer addition algorithm is used. In adding two floating-point numbers, a completely different algorithm is used for computing the sum.

### Type Declarations and Type Equality

We discussed opaque and transparent type declarations. In opaque type declarations, the type name stands for a distinct type different from all other types. In transparent type declarations, the declared name is a synonym for another type. Both forms are used in many programming languages.

## Chapter 7: Scope, Functions, and Storage Management

### 7.1 BLOCK-STRUCTURED LANGUAGES

A **block** is a region of program text, identified by begin and end markers, that may contain declarations local to this region.  A variable declared within a block is said to be **local** to that block. A variable declared in an enclosing block is said to be **global** to the block.

### 7.2 IN-LINE BLOCKS

#### 7.2.1 Activation Records and Local Variables

An activation record is also sometimes called a stack frame.

##### Scope and Lifetime

It is important to distinguish the scope of a declaration from the lifetime of a location:
- Scope: a region of text in which a declaration is visible.
- Lifetime: the duration, during a run of a program, during which a location is allocated as the result of a specific declaration.

#### 7.2.2 Global Variables and Control Links

Because different activation records have different sizes, operations that push and pop activation records from the run-time stack store a pointer in each activation record to the top of the preceding activation record. The pointer to the top of the previous activation record is called the control link, as it is the link that is followed when control returns to the instructions in the preceding block. 

### 7.3 FUNCTIONS AND PROCEDURES

The difference between a procedure and a function is that a function has a return value but a procedure does not. In most languages, functions and procedures may have side effects. However, a procedure has only side effects; a procedure call is a statement and not an expression. Because functions and procedures have many characteristics in common, we use the terms almost interchangeably in the rest of this chapter. 

#### 7.3.1 Activation Records for Functions

Because a procedure may be called from different call sites, it is also necessary to save the return address, which is the location of the next instruction to execute after the procedure terminates. For functions, the activation record must also contain the location that the calling routine expects to have filled with the return value of the function.

The activation record associated with a function (see Figure 7.4) must contain space for the following information:
- control link, pointing to the previous activation record on the stack,
- access link,
- return address, giving the address of the first instruction to execute when the function terminates,
- return-result address, the location in which to store the function return value,
- actual parameters of the function,
- local variables declared within the function,
- temporary storage for intermediate results computed with the function executes

#### 7.3.2 Parameter Passing

The parameter names used in a function declaration are called formal parameters. When a function is called, expressions called actual parameters are used to compute the parameter values for that call. 

The difference between pass-by-value and pass-by-reference is important to the programmer in several ways:
- Side Effects. Assignments inside the function body may have different effects under pass-by-value and pass-by-reference.
- Aliasing. Aliasing occurs when two names refer to the same object or location. Aliasing may occur when two parameters are passed by reference or one parameter passed by reference has the same location as the global variable of the procedure.
- Efficiency. Pass-by-value may be inefficient for large structures if the value of the large structure must be copied. Pass-by-reference may be less efficient than pass-by-value for small structures that would fit directly on stack, because when parameters are passed by reference we must dereference a pointer to get their value.

#### 7.3.3 Global Variables (First-Order Case)

There are two main rules for finding the declaration of a global identifier:
- Static Scope: A global identifier refers to the identifier with that name that is declared in the closest enclosing scope of the program text.
- Dynamic Scope: A global identifier refers to the identifier associated with the most recent activation record.

One important difference between static and dynamic scope is that finding a declaration under static scope uses the static(unchanging) relationship between blocks in the program text. In contrast, dynamic scope uses the actual sequence ofcalls that are executed in the dynamic (changing) execution of the program.

##### Access Links are Used to Maintain Static Scope
The access link of an activation record points to the activation record of the closest enclosing block in the program. In-line blocks do not need an access link, as the closest enclosing block will be the most recently entered block - for in-line blocks, the control link points to the closest enclosing block. 

To summarize, the control link is a link to the activation record of the previous(calling) block. The access link is a link to the activation record of the closest enclosing block in program text. The control link depends on the dynamic behavior of program whereas the access link depends on only the static form of the program text. Access links are used to find the location of global variables in statically scoped languages with nested blocks at run time.

### 7.4 Tail Recursion as Iteration

When a tail recursive function is compiled, it is possible to generate code that computes the function value by use of an iterative loop. When this optimization is used, tail recursive functions can be evaluated by only one activation record for a first call and all resulting recursive calls, not one additional activation record per recursive call. 

### 7.4 HIGHER-ORDER FUNCTIONS

#### 7.4.1 First-Class Functions

A language has first-class functions if functions can be
- declared within any scope,
- passed as arguments to other functions, and
- returned as results of functions.

#### 7.4.2 Passing Functions to Functions

#### Use of Closures 

The standard solution for maintaining static scope when functions are passed to functions or returned as results is to use a data structure called a closure. A closure is a pair consisting of a pointer to function code and a pointer to an mactivation record. Because each activation record contains an access link pointing to the record for the closest enclosing scope, a pointer to the scope in which a function is declared also provides links to activation records for enclosing blocks.

### 7.5 CHAPTER SUMMARY

A block is a region of program text, identified by begin and end markers, that may contain declarations local to this region. 

Parameters passed to functions and procedures are stored in the activation record, just like local variables. The activation record may contain the actual parameter value (in pass-by-value) or its address (in pass-by-reference). Tail calls may be optimized to avoid returning to the calling procedure. 

## Chapter 8: Control in Sequential Languages

### 8.1 STRUCTURED CONTROL

#### 8.1.2 Structured Control

In the 1960s, programmers began to understand that unstructured jumps could make it difficult to understand a program. In modern programming style, we group code in logical blocks, avoid explicit jumps except for function returns, and cannot jump into the middle of a block or function body. 

In 1960 and even 1970, there were many applications in which it was useful to save the cost of a test, even if it meant complicating the control structure of the program. Therefore, programmers considered it important to be able to jump out of the middle of a loop, avoiding another test at the top of the loop.

In the 1980s and 1990s, as computer speed increased, the number of applications in which a small change in efficiency would truly matter decreased significantly, to the point at which, in the 1990s, Java was introduced without any go to statement. 

Simple control structures such as if-then-else have now been in common use since the rise of Pascal in the late 1970s. 

### 8.2 EXCEPTIONS

Exceptions are a basic mechanism that can be used to achieve the following effects: jump out of a block or function invocation, pass data as part of the jump, return to a program point that was set up to continue the computation. Another term for raising an exception is throwing an exception; another term for handling an exception is catching an exception.

### 8.3 CONTINUATIONS

Continuations are a programming technique, based on higher-order functions, that may be used directly by a programmer or may be used in program transformations in an optimizing compiler. Programming with continuations is also related to the systems programming concepts of upcall or callback functions. 

The concept of continuation originated in denotational semantics in the treatments of jumps (goto) and various forms of loop exit and in systems programming in the notion of upcall discussed in Section 7.4. Continuations have found application in continuation-passing-style (CPS) compilers, beginning with the groundbreaking Rabbit compiler for Scheme. 

#### 8.3.2 Continuation-Passing Form and Tail Recursion

There is a program form called continuation-passing form in which each function or operation is passed a continuation. This allows each function or operation to terminate by calling a continuation. As a consequence, no function needs to return to the point from which it was called. This property of continuation-passing form may remind you of tail calls, discussed in Subsection 7.3.4, as a tail call need not return to the calling function.

### 8.4 FUNCTIONS AND EVALUATION ORDER

Exceptions and continuations are forms of jumps that are used in high-level programming languages. A final technique for manipulating the order of execution in programs is to use function definitions and calls. More specifically, if a calculation can be put off until later, it may be placed inside a function and passed to code that will eventually decide when to do the calculation. Delay and force are programming forms that can be used together to optimize program performance. Delay and Force are explicit program constructs in Scheme, but the main idea can be used in any language with functions and static scope. 

### 8.5 CHAPTER SUMMARY

Control and Go to. Because structured programming is commonly accepted and taught, we did not look at the entire historical controversy surrounding go to statements. 

Exceptions. Exceptions are a structured form of jump that may be used to exit a block or function call and pass a return value in the process. 

Continuations. Continuation is a programming technique based on higher-order functions that may be used directly in programming or in program transformations in an optimizing compiler. 

Delay and Force. Delay and Force may be used to delay a computation until it is needed. When the delayed computation is needed, Force is used. Delay and Force may be implemented in conventional programming languages by use of functions: 

