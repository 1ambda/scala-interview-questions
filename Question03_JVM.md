# JVM Questions

- equals, hashcode

A. Java is always **pass-by-value** But everything is a reference in Java, we are actually passing reference.

Q. What is **overloading** and **overriding** in java?

> They are quite different concepts.
> - Method overloading is a feature that a class have two ore more methods having same name
if their argument lists are different.
> - Method overriding enable us to re-defining methods on subclasses 

Q. What is the difference between `==` and `equals()` method in Java?

> `==` operator used to check two object references are identical 
> `equals()` method used to identify two object are equal 

Q. What are `equals` and `hashcode` keywords in Java?

> These methods are related to object comparison in Java
> - `equals` used to compare to object is equal
> - `hashCode`, on the other hand, is used to bucketing in **Hash** implementation like `HsahMap`, `HashTable`, `HashSet`  

Q. What is difference between Heap and Stack Memory?

> The basic difference between stack and heap is the life cycle of the values they contain
> - Stack values only exist within the scope of the function where they are created.
Currently, Java only stores primitives values into stack
> - Heap values however exist even after the function returns where they are created in  
> Also, heap differs from stack in that heap can be shared between threads while stack is owned by each thread

Q. What is Garbage Collection? 

> Garbage collection is a process of reclaiming the unused objects for memory management at runtime

Q. What is structure of Java Heap ? What is Perm Gen space in Heap ?

> Heap memory can be divided into 3 areas.  
> **Young Generation** is the place where newly created objects are located. If garbage collection is occurred in this area, we called it as **minor GC**.
> **Old Generation** is the location where survived objects are stored from minor GC  
> **Permanent Generation** maintain class meta and string pool. (remove from Java 8)   
> we can adjust heap area size by specifying JVM options `-Xmx`, `-XX:MaxNewSize`, `-XX:MaxPerSize`

Q. What GC collectors are available?

> **Serial GC**: uses single thread with mark-sweep-compact algorithm
> **Parallel GC**: use multi threads with mark-sweep-compact algorithm
> **Concurrent Mark Sweep GC**:
- initial mark (stop), concurrent mark (running), remark (stop), concurrent sweep (running)
- low GC pause
- requires more memory and CPU
- no compaction step
> **G1 GC**
>
> GC collector should be chosen based on the application characteristics. (real-time, batch, heap size..) 

Q. What is the difference between Process and Thread?

> Both process and thread are independent path of execution but one process can have multiple threads. 
> Thread has its own stack and share heap with other threads.
> Also, threads in the same process can communicate via `wait`, `notify` in Java and this is much simpler than IPC

Q. What is difference between user Thread and daemon Thread?

> Daemon thread can't prevent JVM from exiting. In other words, JVM will exit when only daemon threads remain.
> Daemon threads are used for background tasks interacting with normal user threads.

Q. What is context-switching in multi-threading? 

> It refers to switching between threads or processes 
> since each thread has its own state such as registers, context-switching takes time  

Q. How does thread communicate with each other?

> We can use synchronized collections such as BlockingQueue or lock object.

Q. What is volatile keyword in Java

> Declaring a volatile Java variable means that
> - this variable will never be cached thread-locally. 
> - all reads and writes will go straight to main memory
> - accessing to this variable acts as though it is enclosed in a synchronized block

Q. What is ThreadLocal?

> ThreadLocal is a storage that can be allocated per thread. 
> `SimpleDateFormat` stores intermediate results in instance fields, we have to use `ThreadLocal` to avoid invalid result between threads 
