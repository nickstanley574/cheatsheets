# Concepts of Programming Languages (CSC447), Spring, 2019

# Lecture Notes 

## Overview 

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

## C: STATEMENTS VERSUS EXPRESSIONS, STRICT VERSUS NONSTRICT AND UNDEFINED BEHAVIOR

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

## SCHEME (LISP AND SCHEME)
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

Bookmark-lecture

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
##Chapter 4: Classes and Objects

## 4.1 CLASSES, FIELDS, AND METHODS
A class is a blueprint for objects. Once you define a class, you can create objects from the class blueprint with the keyword new.
Inside a class definition, you place fields and methods, which are collectively called **members**.

Fields are also known **asinstance variables**, because every instance gets its own set of the variables.

The way you make members public in Scala is by not explicitly specifying any access modifier. Put another way, where you'd say "public" in Java, you simply say nothing in Scala. **Public is Scala's default access level.**

## 4.2 SEMICOLON INFERENCE

In a Scala program, a semicolon at the end of a statement is usually optional. You can type one if you want but you don't have to if the statement appears by itself on a single line. On the other hand, a semicolon is required if you write multiple statements on a single line.

### THE RULES OF SEMICOLON INFERENCE
In short, aline ending is treated as a semicolon unless one of the following conditions is true:
1. The line in question ends in a word that would not be legal as the end of a statement, such as a period or an infix operator.
2. The next line begins with a word that cannot start a statement.
3. The line ends while inside parentheses (...) or brackets [...], because these cannot contain multiple statements anyway.

## 4.3 SINGLETON OBJECTS
Scala has singleton objects. A singleton object definition looks like a class definition, except instead of the keyword `class` you use the keyword `object` .When a singleton object shares the same name with a class, it is called that class's **companion object.**
`object ChecksumAccumulator {` 

If you are a Java programmer, one way to think of singleton objects is as the home for any static methods you might have written in Java.

A singleton object that does not share the same name with a companion class is called **astandalone object.** 

## 4.4 A SCALA APPLICATION

Instead, you'll need to actually compile these files with the Scala compiler, then run the resulting class files. One way to do this is to use `scalac`, which is the basic Scala compiler, like this: `$ scalac ChecksumAccumulator.scala Summer.scala`

This compiles your source files, but there may be a perceptible delay before the compilation finishes. The reason is that every time the compiler starts up, it spends time scanning the contents of jar files and doing other initial work before it even looks at the fresh source files you submit to it. For this reason, the Scala distribution also includes a Scala compilerdaemon called fsc (for fast Scala compiler). You use it like this: `$ fsc ChecksumAccumulator.scala Summer.scala`

The first time you run fsc, it will create a local server daemon attached to a port on your computer. It will then send the list of files to compile to the daemon via the port, and the daemon will compile the files. The next time you run fsc, the daemon will already be running, so fsc will simply send the file list to the daemon, which will immediately compile the files.

## 4.5 THE APP TRAIT
To use the trait, you first write "extends App" after the name of your singleton object. Then instead of writing a main method, you place the code you would have put in the main method directly between the curly braces of the singleton object. You can access command-line arguments via an array of strings named args. That's it. You can compile and run this application just like any other.

Bookmark-PS

____

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







Bookmark-CLP



