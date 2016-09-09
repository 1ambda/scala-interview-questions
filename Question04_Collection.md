# Collection Questions

Q. What are the basic interfaces of Java Collections Framework?

> Collection interface is the root of the collection hierarchy
> Set is a collection that cannot contain duplicated elements
> List is an ordered collection and can contain duplicate elements. List is more like array with dynamic size
> A Map is an object that maps keys to values.


Q. Why Map interface does not extend Collection interface?

> Map contains key-value pairs and it provides methods to retrieve list of keys or values
> but it doesn't fit into **group of elements** paradigm


Q. What is difference between Enumeration and Iterator interface?

> Iterator allow the caller to remove elements from the underlying collection that is not possible in Enumeration 

Q. What do you understand by iterator fail-fast property?

> Fail-fast iterator checks for any modification in the underlying collection every we try to get the next element.
> If there are any modification found, it throws `ConcurrentModificationException`

Q. How to avoid ConcurrentModificationException while iterating a collection?

> We can use Concurrent collection classes to avoid it such as CopyOnWriteArrayList, ConcurrentHashMap

Q. What is difference between fail-fast and fail-safe?

> Fail-safe iterators work with the clone of the underlying collection, hence it is not affected by any modification
> By design, all the collection classes in `java.util` package are fail-fast whereas collection classes in `java.util.concurrent` are fail-safe

Q. What is difference between HashMap and Hashtable?

> HashTable is synchronized while HashMap is not
> The iterator of HashMap is fail-fast

Q. How to decide between HashMap and TreeMap?

> TreeMap provides ordered key traversing since it implements SortedMap

Q. What is difference between Array and ArrayList? When will you use Array over ArrayList?

> Array can contain both primitives and objects whereas ArrayList can only contain objects
> Also, Array is fixed size while ArrayList is dynamic size

Q. What is difference between ArrayList and LinkedList?

> ArrayList provides random access hile LinkedList doesn't
