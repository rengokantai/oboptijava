# oboptijava
## Chapter 11. Java language performance techniques
### Optimizing Collections
sequential and associative
- Sequential containers store objects at a particular position, denoted by a numerical index.
- Associative containers use the object itself to determine where the object should be stored inside the Collection.

### Optimization Considerations for Lists

#### ArrayList
An ```ArrayList``` has a default size of 10, 
but we can override this by passing our preferred value into the constructor or by using the ```ensureCapacity()``` method
- (although the latter choice will still create an array of default size first, so is slightly more wasteful) 
- __Preferring a correctly sized ArrayList is always preferable when possible.__
```
//better.
@Benchmark
public List<String> properlySizedArrayList() {	
  List<String> list = new ArrayList<>(1_000_000);	
  for(int i=0; i < 1_000_000; i++) {		
    list.add(item);	
  }	
  return list;
}
@Benchmarkpublic List<String> resizingArrayList() {	
  List<String> list = new ArrayList<>();
  for(int i=0; i < 1_000_000; i++) {		
    list.add(item);	
  }	
  return list;
}
```
#### LinkedList
Insertion to the __end of a list__ in both ArrayList and LinkedList 
is a constant time operation (after amortizing the resize operations in the case of ArrayList).

#### Optimization Considerations for Maps
When considering the performance of a HashMap two important variables are used 
```initialCapacity``` and ```loadFactor```

#### TreeMap
The TreeMap provides log(n) performance for get, put, containsKey and remove operations.

### Optimization Considerations for Sets
A TreeSet guarantees log(n) for insertion, removal and contains operations and maintains the ordering of elements.

### Domain Objects
(tbc)

### Avoid Finalization
when an object is created, it takes ownership of some resource,
and the object’s ownership of that resource persists for the lifetime of the object. 

Once the object has been registered as needing finalization, then instead of being immediately reclaimed during the garbage collection cycle, 
the object follows this extended lifecycle:
- Finalizable objects are moved to a queue.
- After application threads restart, separate finalization threads will drain the queue and run the finalize() method on each object.
- Once the finalize() method terminates, the object will be ready for actual collection in the next cycle.  

#### Try-with-resources
tbc
