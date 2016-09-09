# Language Questions

Q. What is the difference between a Java future and a Scala future?

> The main inconvenience of Java Future is that you can't get the inside value without blocking
> Maybe it would be more precise to say that Scala has a more convenient api to interact such with pending Futures and callback.
> But the `CompletableFuture` in Java 8 supports similar functionality as i know.

Q. What is the difference between a **trait** and an **abstract class**?

> I can think of 3 differences.
> First, classes can inherit multiple traits but only one abstract class.
> Second, abstract classes can have constructor parameters as well as type parameters while Traits can have only type parameters.
> Last, abstract classes are fully interoperable with Java code without any wrappers. But traits are only interoperable only they do noy contain any implementation 

Q. What is the difference between the following terms and types in Scala: `Nil`, `Null`, `None`, `Nothing`?

> Nothing is a trait. It is a subtype of everything but not superclass of anything so that some people call it as the bottom type. 
There are no instance of Nothing. If you are retuning Nothing, it means that it will never return
The reason Scala has a bottom type is tied to its ability to express variance in type parameter.
Nothing is useful for expressing the empty type of covariant containers such as `List` and `Option`  
> `object None extends Option[Nothing]`
> `object Nil extends List[Nothing`  
> Null is a trait but it is different from Nothing in that it has instance, lowercase `null` which is similar to Java `null`   
> 
> I would like to explain a little more.  
> - Any is supertype of AnyRef and AnyVal on the top of the type system hierarchy
> - AnyRef is the supertype of all the reference classes like String, List
> - AnyVal is the supertype of all the primitive values such as Float, Double, Char

Q. What is `Unit`?

> Unit is a type that has exactly one value `()` and 
retuning `Unit` is analogous to `void` of Java so that `Unit` is not represented at runtime. 

Q. What is Referential Transparency?

> Referential Transparency, in terms of functional programming, is that given a function and inputs you will always get the same output 
> If we use global variable instead of local variables, we can not get the same result due to effect of external world.  
> **A referentially transparent function is one which only depends on its input** 

Q. What is the difference between a **call-by-value** and **call-by-name** parameter?

> - call-by-value arguments are evaluated eagerly
> - call-by-name arguments are not evaluated until they are used directly

```scala
@ def something(): Int = { println("something"); 1 }
defined function something
@ def callByName(x: => Int) { println(s"x1= ${x}"); println(s"x2= ${x}") }
defined function callByName
@ def callByValue(x: Int) { println(s"x1= ${x}"); println(s"x2= ${x}") }
defined function callByValue

@ callByValue(something())
something
x1= 1
x2= 1

@ callByName(something())
something
x1= 1
something
x2= 1
```

Q. Explain the `implicit` keyword 

> Implicits in Scala refers to either a value that can be passed automatically or an automatic conversion from one type to another type.
> The first thing is called implicit parameters while the later one is called implicit conversion.    
> in Scala, implicit parameters used to inject runtime environment such as `ExecutionContext` required to running futures

```
// View Bound
def f[A <% B](a: A) = a.bMethod
def f[A](a: A)(implicit ev: A => B) = a.bMethod

// Context Bound
def g[A : B](a: A) = h(a)
def g[A](a: A)(implicit ev: B[A]) = h(a)
```

Q. How does `yield` work?

> for-comprehension is a syntax sugar for combining `map`, `flatMap` and `withFilter`
> Generally, a for expression is of the form  
> `for ( seq ) yield expr`  
> Seq is a sequence of generators, definitions and filters  
>
```scala
for {
  p <- persons           // a generator
  n = p.name             // a definition
  if (n startsWith "To") // a filter
} yield n
```  
> 
```scala
for (x <- expr1 if expr2) yield expr3
expr1 withFilter (x => expr2) map (x => expr3)
```
```
for (x <- expr1; y <- expr2) yield expr3
expr1.flatMap(x => for (y <- expr2) yield expr3)
expor1.flatMap(x => expr2.map(y => expr3))
```  

Q. What is tail recursion?

```scala
def factorial(n: BigInt): BigInt = 
  if (n == 0) 1 
  else n * factorial(n - 1) 
  
@tailrec
def tailFactorial(n: BigInt, current: BigInt): BigInt =
  if (n == 0) current
  else factorial(n - 1, n * current)
```

> Unlikely the common recursion, we perform calculation first and then execute recursive call.
> The consequence of this is, we don't need to avoid new stackframe since we already did required computation so that we can avoid stackoverflow
> In other words, we can replace tail recursive code to the simple while loop  
> in Scala, we need `tailrec` annotation which is not supported at JVM level


