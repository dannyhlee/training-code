

# Week 1
## Day 1  
  
#### What is Git?  
  
Git is an actively maintained, open-source distributed version control system (VCS) that tracks source code changes originally developed by the Linus Torvalds, the creator of Linux.  Recently acquired by Microsoft, its the most popular and well-known source code management (SCM) tools. It tracks a running history of a code base and stores changes, prevents conflicts when merging multiple contributions in parallel branchs from multiple authors.  
  
#### What about GitHub? How are they related?  
  
GitHub is a source code repository, along with storing the actual source code and Git histories, it provides extended
 functionality through desktop clients and plugins, search functions, issue tracking and an organized way to track and commit source code change suggestions (through pull requests). It also provides GitHub Actions which can be used to build continuous integration and continuous deployment by providing pipelines for testing, releasing and deploying software automatically. .  
  
#### What command moves changes from GitHub to our local repo?  
  
`git add .` will move changed files from the CWD (current working directory) to the staging area (aka index). It will not move files that match the filespecs contained in the .gitignore file.  
  
`git commit -m "message"` will take a snapshot of the repositories changes, including files added to the staging area.  
  
#### What command moves changes from our local repo to GitHub?  
  
`git push` will upload the changes from the local repository to GitHub (aka the remote repository)  
  
#### What two commands are used in sequence to save changes to our local repo?  
  
```  
git add .  
git commit -m "some fancy commit message"  
```  
  
#### What is BASH?  
  
BASH (or Bourne Again Shell) is a command line interface (or CLI) originally built for the for Unix/Linux based operating systems, but now available on macOs and windows computers.  Bash has scripting functionality and improved upon the sh CLI by adding command line editing, unlimited command history, job control and aliases and shell functions.
  
#### What does the PATH environment variable do?  
  
The PATH environment variable on Windows and Unix/Linux operating systems is a list of directories that containg commands. When the user enters a command the OS checks this list of directories for the entered command. If its found, the cmd is executed.  The PATH environment can be edited to add new commands or remove deleted/deprecated commands. After editing its important to refresh the environment so the new values can be used.
  
#### What is the JDK and what does it let us do?  
  
The JDK (or Java Development Kit) is a collection software development tools developed by Oracle such as compilers (javac), disassemblers (javap), debugger (jdb), archiver (jar) and a bunch of other tools for programming.  It also contains the JRE, which contains an JVM and libraries.  There is a free and open source JDK named OpenJDK.

#### What is the JRE and what does it let us do?  
  
The Java Runtime Environment (or JRE) runs on top of the computer operating system and provides class libraries and other resources Java apps need. It combines the compiled code created by the JDK with libraries to run the program. The JRE is made up of the ClassLoader, Bytecode verifier and Interpreter. A more complete list is available here: https://www.ibm.com/cloud/learn/jre  
  
#### What's the name for the code written in .class files?  
  
The .class files are created by the javac Java compiler and contains Java bytecode that can be loaded and run on the JVM.  
  
#### How does Scala relate to Java?  
  
Scala compiles into Java bytecode, the low-level language understood and executed on the JVM. Scala provides "language
 interoperability" with Java, meaning code libraries can be shared. Scala is Object Oriented like Java, but is built for functional programming rather than Object Oriented programming.  
  
#### What is sbt (high level)?  
  
sbt is a software tool for building Scala and Java projects. It helps organize and efficiently compile, debug and deploy projects. It helps manage dependencies and tracks libraries.  
  
#### How does Scala relate to the JRE and JVM?  
  
Scala programs translates into Java bytecode which is loaded into the JRE along with the classes and libraries it
 requires. The JVM is installed along witht he JRE and the JVM interprets the bytecode. The JVM does the heavy lifting when it comes with interacting with different operating systems and computers. A useful illustration is available at https://getkt.com/blog/difference-between-jdk-jre-and-jvm-explained-java/  
  
---  

## Day 2  
  
#### Is Scala statically or dynamically typed?  
  
Scala is statically typed. Every piece of data is an object, every object has a type. Static typing means the type is checked at compilation. Using the wrong type in an expression will cause a compilation (rather than runtime error). This results in more robust and trustworthy code.  
  
#### Do we need to declare type for our variables in Scala? always?  
  
Scala provides type inference, which means that Scala will try and guess the type of the data your are assigning to your variable. 
  
#### What are integer types in Scala?  
  
The integer types available in Scala are:  
  
- Byte (8 bits) (-2^7 to 2^7-1, inclusive)  
- Short (16 bits) (-2^15 to 2^15-1, inclusive)  
- Int (32 bits) (-2^31 to 2^31-1, inclusive) _default_  
- Long (64 bits) (-2^63 to 2^63-1, inclusive)  
- BigInt  
  
#### Decimal types?  
  
The decimal types available in Scala are:  
  
- Float (32 bits) (IEEE 754 single-precision float) 
- Double (64 bits) (IEEE 754 double-precision float)  _default_  
- BigDecimal  
  
#### What is the size of an Int? a Double? (the default integer and decimal types)
 
 - Int (32 bits) (-2^31 to 2^31-1, inclusive) _default_  
 - Double (32 bits) (IEEE 754 single-precision float) _default_  
  
#### What is the difference between val and var?  
  
A variable initialized with the `val` keyword will be _immutable_. A variable with `var` will be _mutable_.  
  
#### Why do we make use of programming paradigms like Functional Programming and Object Oriented Programming?  
  
We use these programming paradigms to organize a code base that grows larger over time, and has many people working on it. It creates a consistent way to build software. It helps to manage complexity in a large body of code.  
  
#### What are the 4 pillars of OOP: Abstraction, Encapsulation, Inheritance, Polymorphism? (a bit on each)  
  
Abstraction is the act of hiding complexity from the end-user, by providing a front-end interface for the user to interact with the object or program, without having to know the details of what is going behind the scenes.  
  
Encapsulation is the principle that Objects should take care of their own data. This means that the object projects its state (values) through the use of getters and setters so that they cannot be directly manipulated.  
  
Inheritance is the strategy of using inherited Classes (the Superclass) to reuse code. In this way a child class can inherit the attributes and methods of its parent class.  
  
Polymorphism or multiple forms, allows an object to take on different characteristics and respond in different ways depending on the parameters it is provided (method overloading/static polymorphism/compile-time). A different signature (set of parameters) will trigger different methods (ex: animal class, that is a parent to dog and cat subclasses. Depending on child class, speak() will output different strings.) Another form of polymorphism is runtime polymorphism (dynamic polymorphism) which involves multiple classes where methods will be different but have the same name and signature (set of parameters).  
  
#### What are classes? Objects?  
  
A class is user-defined blueprint to create an object. A class can contain fields and methods and is identified with a name (identifier). An object is an instance of class, when it is created a place in memory is referenced for it and the class constructor is called.  
  
#### What is the significance of the Object class in Scala?  
  
Everything in Scala is an object. There are no primitives, numbers are objects. Functions are objects.  
  
#### What does it mean that functions are first class citizens in Scala?  
  
This means that functions will support all operations available to other entities (like variables). They can be assigned to a variable, passing them as arguments (parameters) and return them from functions. An example is _map_ which takes a list and function as an argument and returns a list after applying the function.  
  
#### What is a pure function?  
  
A pure function does not cause any side effects. It does not access external objects, for example changing variables or data, print, or output to disk, it simply returns a value consistently. Given the same input, it will always return the same output. Pure functions will not break anything outside the function, guarantees order of execution, makes unit testing easier, making caching easer, makes the code self-contained and easier to understand, with no unexpected side-effects.  
  
#### What is a side effect?  
  
A side effect is a change in the state of variables, printing or outputting to display or filesystem, or has another observable effect besides returning a value to the invoker of the function.  
  
#### What's the difference between an expression and a statement?  
  
An expression is a unit of code that returns a value. A statement is a unit of code that doesn't return a value. Multiple expressions can be combined with curly braces to create an _expression block_. A common statement is println() and value and variable definitions. A good reference available at https://www.oreilly.com/library/view/learning-scala/9781449368814/ch03.html  
  
#### Is if-else an expression or a statement in Scala?  
  
The if-else construct is an expression in Scala because it always returns a result.  
  
#### What's the difference between a while loop and a do-while loop?  
  
The while loop will only execute if the a condition is met, where a do-while loop is guaranteed to execute at least once even if ithe condition is false.  
  
#### How does String interpolation work in Scala?  
  
Strings can be interpolated so that variable references can be put inside the quotes of string literals and processed inline. There are three prepended symbols that provide different interpolation methods. They are `s`, `f` and `raw`. `s` is the String interpolator and when it is used:  
  
```  
var month = "October"  
var date = 1  
println(s"Today is $month $date") // Today is October 1  
```  
  
The variables will be output as Strings.  
  
The `f` Interpolator variables must be referenced with a printf-style variable type reference. It is typesafe. The `raw` interpolator will output the literal string without escaping any literals (ex: \n)  
  
#### How do operators work in Scala? Where is "+" defined?  
  
Operators are methods that are connected to objects. They are overriden from the base class and have specific functionality depending on the class of the object its attached to. The "+" operator is a method defined by the Int type.  
  
#### What are the ways we could provide default values for a field?  
  
We can define them in the primary Class constructor:  
  
```  
class Car(var color: String = "white", var doors: Int = 4)  
```  
  
We can also define them in auxillary class constructors:  
  
```  
class Car(var color: String, var doors: Int) {  
 def this(color: String) = { this(color, 4)  // accepts color parameter and sets doors to default of "4" } def this(doors: Int) = { this("white", doors) } def this() = { this("white", 4) // sets both default parameters. }}  
  
```  
  
#### How do we define an auxiliary constructor?  
  
An auxillary constructor takes care of cases where a function is not provided with all of the arguments (parameters) it requires to initialize. Auxillary constructors can be made for different cases where certain parameters are left out, or for all-other cases so that the object can be initialized even if it doesn't receive all the values it requires.  
  
#### What is an enumeration?  
  
An enumeration defines a finite set of constant values.   Scala's Enumeration class is extended to create enumerations, whose values are defined as vals, and wgucg are iterable and immutable.
  
#### What is a REPL?  
  
REPL (Read-Evaluate-Print-Loop) is a CLI used to execute Scala code. To enter the Scala REPL, use the command `scala` or open a Scala worksheet in Intellij. You will be able to write a Scala expression and the REPL will evaluate its value. The REPL automatically assign variables for the output of expressions. Use :help for list of commands, :quit to exit.  
  
#### How does the Scala REPL store the results of evaluated expressions?  
  
If the user doesn't define a variable name, the REPL will automatically store them in the form "res0, res1, res2...res-n)
  
---  

## Day 3  
  
#### What is a higher order function?  
  
A higher order function is a function that either takes a function as an argument or returns a function.  
  
#### What is function composition?  

Function composition the building of complex function with simple functions.  Readibility and facility of reuse is improved by factoring (breaking apart) complex function.  The result of one function is passed into the next, and so on, until the final result, which is the result of the whole, is achieved.  
  
#### Why might we want to write an application using pure functions instead of impure functions?  
  
Pure functions are predictible and easy to test, while impure functions can be unpredictible and have unexpected side effects. Impure functions also are harder to test because state may have been changed outside of the context of the function.  Pure functions, with no side effects, can be run in parallel without the concern of creating race conditions that affect outside values.
  
#### Why might we want mutable state (OOP) in our application? Why might we want immutable state (FP)?  
  - This question is open-ended, don't focus on finding the "right" answer  
    Having immutable state (FP) will allow us to more easily run applications in parallel.  Starting up and stopping services becomes easier when we dont have to retrieve or store a particular state that is shared. 
    Mutable state is useful, though more difficult to manage, in cases where customization or "distinct identity" is used. Rather than create new instances of an object everytime a change is made (like we do in FP), keeping the same object and modifying the attributes may be more efficient.  
    
#### What are some examples of side effects?  
  
Some examples of side effects are: outputting to screen or filesystem (I/O operations), modifying a mutable variable or data structure, throwing exceptions or errors.  
  
#### What is a Lambda?  
  
A Lambda (or lambda function, lambda expression, anonymous function, or closure) is a nameless function written inline. Its an expression which can be used in place of a variable/value.  Its useful in writing code in place and improves readiblity of code, and decreases the need to track down functions to understand what a program is doing.
  
#### How can we write Lambdas in Scala?  
  
One parameter: val mySum = (x: Int) => x + x    
Two parameters (using type inference): val myName = (first: String, last: String) => first + " " + last  
Two paraemters (w/o type inference): val myName: (String, String) => String = (first: String, last: String) => first + " " + last  
  
#### What does map do?  
  
The Map method takes an iterable data structure and a callback function, and returns an iterable made up of the result of applying the callback to each element. An alternative to map is foreach, that works similarly, can be used to cause side effects, without a returned iterable (returns Unit instead).  

  
#### What does filter do?  
  
Filter takes in an iterable ds and a callback function that evaluates each element in the collection and returns a boolean. It returns only the elements from the original collection that evaluate to **true**.  
  
#### What does reduce do?  
  
Reduce takes in an iterable and a callback function that takes 2 parameters and applies the function to the pair.  It then takes that value and uses it as one of the parameters for the next iteration.  The other parameter comes from the iterable we passed in.  Its next element is the other parameter. It continues this until it goes through each element of the collection.  
  
#### What does it mean that a function returns Unit in Scala?  
  
This means that the function is not expected to have a return value. These kinds of functions are run for their side effects.  
  
#### What is recursion?  
  
Recursion is the defining of something in terms of itself. In programming recursive functions are functions which calls itself as a subfunction repeatedly. It is useful in solving problems whose solutions are smaller versions of itself, so by breaking the problem down into smaller and smaller pieces and then combining the results. Also called the divide-and-conquer method.  
  
#### What do we need to include in any effective recursive function?  
  
To prevent a recursive function from calling itself infinitely there needs to be a base case (smallest division of the problem). The base case is the point at which the problem can no longer be divided and whose solution can be returned directly.  
  
#### What is parameterized typing?  
  
Parameterized typing is where we say Array[Int] to make an int array or Array[String] to make a string array. Parameterized typing just means that the type is accepted as a parameter. (samuel owens)  
  
---  

## Day 4  
  
#### What is the Stack? What is stored on the Stack?  
  
The Stack is an allocated portion of memory that is created for each thread of a program.  During runtime, functions are added to the Stack in a LIFO (Last In First Out) order.  Each time a new function is called from within a function, a new stack frame is pushed on to the stack.  In addition, local variables (available only within the stack, aand references to objects that are being stored in the heap (which are available too all threads/stacks.  When there are no more functions being called, the last function in is "popped" off the stack and it is
    evaluated, and its value returned (if any).  Then the stack frame will be discarded, its local variables and
     references discarded and the space made available for future stack frames. If a thread tries to add a new stack
      frame, but there is no space, a StackOverFlowError error will be thrown.
  
#### What is the Heap? What is stored on the Heap?  
  
In the Java memory model, the heap is the area of memory where Objects are stored.  It is not organized and objects
 in memory are referenced from the stack by references stored in each stack frame.  The objects can be accessed by
  different threads and so there can be more than one thread pointing to the same objects in memory.  Once all
   references to an object are removed (by execution) the object is ready for garbage collection.  If there's not
    enough space to allocate an object and the garbage collector cannot make space, and the heap cannot be expanded
    , an OutOfMemoryError will be thrown.
  
#### What is garbage collection?  
  
In the Java memory model, Garbage collection is an automatic process in which the JVM's GC (Garbage collector) will mark
 objects stored in the heap that have no references to them.  The GC will scan all objects to see if they are "live
 " or unreferenced.  After scanning all objects (which can be very time-consuming depending on how many objects are
  in the heap), the GC will delete the marked objects.  GC can also compact the remaining referenced ("live") objects
   to move them closer together to make memory allocation easier and faster.  JVM Generations provides a way to
    prioritize stored objects into Young Generation, Old Generation and Permenant generations.  New objects go in the
     YG, YG objects that survive GC may be moved to the OG.  When YG is cleaned up it is a minor garbage colelction
     .  When the OG is cleaned up it is a major garbage collection.  These events are both "Stop the world" events
     , meaning that application threads are put on hold until they finish.  The PG contains data that is needed by
      JVM and will be populated at runtime.  Java SE library classes and methods are stored here.  They may be
       removed if there is a need for space and they are not used by the program.  
  
#### When is an object on the Heap eligible for garbage collection?  
  
When there are no longer references to an object from any of the  it is marked for collection.    Garbage collection
 occurs when the heap becomes full.
  
#### How do methods executing on the stack interact with objects on the heap?  

Methods in the stack contain reference variables that point  to objects in the heap.

#### Know the basics of the following Scala Collections: (mutable? indexed? when to use it?)  Performance table: https://www.lihaoyi.com/post/BenchmarkingScalaCollections.html#lists-vs-vectors

  - List: a list is a singly linked list that is an immutable, collection of elements of the same type that preserves order and can contain duplicates.  It is unindexed and access to the head is very fast. The head is the first item, the tail is everything else.   
  
  - Set: have no duplicates, generally do not preserve order and are not indexed, but they are iterable.  Some have guaranteed order, some do not.  Can be thought of as a map without values.
  
  - Map - Are hashtables under the hood, key-value pairs that provide constant time lookups.  Mutable and immutable versions are available.  
  
  - ArrayBuffer  - Index, sequential, mutable, appending elements is fast.  Can contain duplicates.
  
  - Vector - indexed, immutable, sequences, effectively Constant time
    
#### What is a generic?  
  - the phrase "compile time type safety" is useful in this answer  
  Generics is the same as templating. Essentially you can write a function or object that treats any class you give it the exact same way. For example, List[T]. It doesn't matter which data type or class you give it, the List just knows that it needs to keep track of some number of some class. (Rheomyr)
  
  
#### What is an Option?  

An option is a collection of one item that consists of either Some or None.  Some contains the value, while None is equivalent to null, without throwing the Null Pointer Exception.  

#### What is found inside an empty Option?  

An empty Option returns a None singleton, which is a reference that has no value.

#### How do we write an Option that contains a value?  

val myName: Option[String] = Some("Danny Lee")

#### What are Exceptions?

  In programming, exceptions are unexpected behavior or abnormal conditions in a program.  In Scala, when this happen an Exception object will be thrown and the programs execution is interrupted until the exception is caught and handled.  Sometimes this is due to using the Scala language improperly, othertimes we want to throw Exceptions intentionally when something exceptional happens.
  
#### What are Errors?

   Errors are thrown when more serious problems are indicated.  Errors can't or generally shouldn't be caught and/or recovered from.
  
#### What is Throwable?

Throwable is the superclass to Exceptions and Errors, and only it and its subclasses can be thrown by the JVM or by the Java throw statement.  It also takes a snapshot of the execution stack of its thread and can contain other information to investigate what caused the program to abort execution.
  
#### How would we write code that handles a thrown Exception?
```
  try {
    // some code here
  } catch {
    case red: RedException => handleRedException(red)
    case e: BlueException => System.err.println(e.getMessage)
    case _: Throwable => println("Other type of exception") 
  } finally {
    // code to clean up before exiting
  }
```
  
  
#### How do we write code to throw an Exception?  
  
  try {
    throw new Exception("Whee!")
  } catch {
    case _: Throwable => println("Thrown exception")
  }
  
---  

## Day 5  
  
#### What does the src folder contain in an sbt project?  

    The /src/main/scala holds our classes, traits, objects and packages.
    The /src/main/java holds our Java classes
    The /src/main/resources folder holds configuration files
    The src/test folder holds tests with a similar structure to src/main

#### the target folder?  

    The src/target folder holds compiled version of Scala files.
    
#### What is a Trait?  

    Traits share methods and fields between classes, and are similar to Java's interfaces.  They can have abstract (undefined) methods and concrete (defined) methods.  Traits can be extended by a class and the methods implemented.  To add multiple traits we can use:
  ```
  trait Tailwagger {}
  
  class Dog extends Tailwagger with Runner with Speaker {
  }
  
  or 
  
  val d = new Dog("Snoop") with Tailwagger with Runner
  // methods in traits must be defined!
  ```
    
    Concrete (defined) methods can be overridden using the `override` keyword.
    

#### What is a case class?

  A case class is like a class but with some extra built in functionality.  The export their constructor parameters and allow the class constructor to be pattern matched. One feature is the .apply syntactic sugar that enables instantiation without using the keyword `new`.  Also, the case classes constrcutor parameters are promoted to members and are accessible as `caseClass.memberName`.  
  
  Also, members are compared by values rather than identity.

#### What methods get generated when we declare a case class?  
    apply - no need for `new` keyword
    unapply - useful for match expressions
    accessor methods for each constructor parameter
    copy - clone object and change a field/member
    equals - for comparing instances
    hashCode - for use in collections
    toString - Creates a string with the identity


#### What does the apply method do?  

The apply method provides syntactic sugar for creating new object instances without the New keyword.  It lets us use a functional style notation instead of the more traditional way of instantiating a new object with the New keyword. (ex: val john = new Person("john") is changed to val john = Person("john")) 


#### What is a Thread?  

A thread is a single, independent path of instruction execution within a program.  When a program is started the **main thread** is started up.  New threads (java.lang.Thread) can be created and run concurrently (either async or sync).


#### In what situations might we want to use multiple threads? (just some)  

Some examples of situations we would use this is we are getting or putting data to a database, file system (I/O events) or accessing network resources.  Running code in parallel or to different entities and awaiting their return, even though we are not sure when (or even if) they will return a value.  And we don't those values could return at different times. 


#### What is a Future?  

Futures provide a way to perform a computation asynchronously so they do not stop our program to wait for a result.  By using this nonblocking strategy we can make a request, try and perform an operation or run tasks in   parallel, and have a place to store the result, which is going to arrive in the future. A future is placeholder object that receives that result and it accepts a callback function to execute once the request has resolved.

#### How can we do something with the result of a Future?  

When we create a Future we provide a callback function, when the Future resolves, that callback function will be executed.  Wwe can also check on the Future's value later in our code, after some reasonable time has passed.  

#### How does a Future return a value or exception? 

Upon completion, the future either returns a Success or Failure object.  A Success includes the computed value.  A Failure returns an exception, whose message can be accessed through the getMessage() method.
 
#### How does the onComplete callback function work?

The onComplete function returns nothing (Unit) and lets us apply a provided callback function to the resolved Future.  In the case of Success, there will be a value and in the case of Failure there will be an exception.  The Future's resolution happens **eventually**. 

The callback function is of type `Try[T] => U` which is a monad simliar to `Option[T]` which holds a value (Some[T]) or (None).  Try[T] holds a value as Success[T] or an exception as Failure[T].  Another option is to use a `foreach` callback, which will only be called in case of Success. Care must be taken if applying multiple callbacks to a future, because the order of the execution is not guaranteed by the order they are written in code, nor are they affected by exceptions thrown by other callbacks.


---

## QC Week 1

#### What are some methods that come with the object class in Scala?  

clone, equals, getClass, toString, hashcode

#### What are some features of Scala?

- Type inference: data type is inferred, function type by last expression in function
- Singleton object: no static var or methods.  Singleton holds class vars and methods
- Immutability: immutable by default, helps manage concurrency control
- Lazy computation: Evaluate expressions only when required, lazy variables can be declared.
- Case classes and Pattern matching: Case classes immutable and decomposable through pattern matching.
- Concurrency control: Scala provides standard library which includes the actor model. You can write concurrency code by using actor. Scala provides one more platform and tool to deal with concurrency known as Akka. Akka is a separate open source framework that provides actor-based concurrency. Akka actors may be distributed or combined with software transactional memory.
- String interpolation
- Higher order function
- Traits
- Rich collection set
- concise, readble and expressive syntax
- compiles to .class and run on JVM
- can use thousands of Java libraries
- pure OOP language, every variable is an object, every operator a method
- built for FP, functions are variables and can be passed.
- You can use either, or combine them hybrid style

#### How do for loops work in Scala?

Sample for loop:
```
for( var x <- Range ){
   statement(s);
}
```
The range can be set with 1 to 5 or 1 until 5.  Left arrow operator is called a `generator`, which generates individual values from a range.

Two dimensional:
```
for( a <- 1 to 3; b <- 1 to 3){
         println( "Value of a: " + a );
         println( "Value of b: " + b );
      }
```

Collection:
```
for( var x <- List ){
   statement(s);
}
```

With filters:
```
for( a <- numList
     if a != 3; if a < 8 ){
   println( "Value of a: " + a );
}
```

With yield, returns value through a function:
var retVal = for{ var x <- List
   if condition1; if condition2...
}
yield x

---

# Week 2

## Day 2

#### What are the benefits of SQL vs NoSQL?

Scaling: NoSql scales out.  SQL scales up. If you need more quickly, NOSQL is the way to go.

Structure: SQL is good for highly structured data.  Complex queries and reports and ACID compliance.  Don't anticipates lot of changes and growth.  High transaction rate, because SQL is more stable and has better data integrity.

Speed: When data consistency and 100%d data integrity is not as import, NoSQL adapts quickly to changes in structure, with a highly flexible schema design.

Data Types: Lots of data types, and lkots of data is stored easily in NoSQL. No need to devise structures and strategies to work with data.

You can also use both.

#### What is standalone mode for a database?

Mostly used for testing and development.  Another option is a **Single node replica set**, which has additional meta information (oplog).  MongoDB in production was designed with a replica set deployment in mind, for:

- High availability in the face of node failures
- Rolling maintenance/upgrades with no downtime
- Possibility to scale-out reads
- Possibility to have a replica of data in a special-purpose node that is not part of the high availability nodes

