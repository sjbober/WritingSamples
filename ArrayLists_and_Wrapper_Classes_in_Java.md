# ArrayLists and Wrapper Classes in Java

An array is a numbered sequence of elements, where each element is a variable. These variables can contain primitive values, or they can be reference variables that refer to objects (Eck, 2019, ch. 3.8.1). For example, the following array *ages* refers to an array with 12 variables that are ready to be assigned to *int* values.

```java
int[] ages = new int[12];
```

Arrays are extremely useful, but one of their limitations is that the size of the array (the number of variables it contains) can never change after the array object has been created. For the array created above, it will only ever be able to hold 12 variables, no more, no less. If we need to adjust the size of the array, we would have to create a whole new array with a larger size and copy the values of the variables into the new array. For example, we could use an assignment statement to make our array variable refer to a new array created by the function *copyOf.* This function takes an array we want to copy, and the number of elements we want the new array to contain, and returns a new array object:

```java
greetings = Arrays.copyOf(greetings, 13);
```

Java provides an easier way to work with Arrays that need to change size by providing another built-in data structure called ArrayList. ArrayList and Arrays are very similar in that they both are numbered sequences of variables, but ArrayList differs in two ways. First, ArrayLists can change in size. We can add and remove elements without keeping track of the size of the array and creating new array objects when capacity is full. Second, ArrayLists can only contain reference variables, meaning it cannot contain variables that store primitive values (Eck, 2019, ch. 7.3.1).

Fortunately, Java provides **wrapper classes** for all of the primitive types. A wrapper class is a class that allows us to treat primitive values like objects; we can "wrap" a primitive value in an object belonging to a wrapper class (Eck, 2019, ch. 7.3.2). The following chart lists all of the primitive types and their corresponding wrapper class:

|Primitive Data Type | Wrapper Class| 
|--------------|-----------|
| byte    | Byte      |
| short   | Short     | 
| int     | Integer   |      
| long    | Long      |    
| float   | Float     |   
| double  | Double    |    
| boolean | Boolean   |    
| char    | Character |  


Since wrapper classes allow us to treat primitives as objects, we can create an ArrayList of primitive values by using the corresponding wrapper class. For example, if we want to create an ArrayList of *ints*, we can create an ArrayList of *Integer*:

```java
ArrayList<Integer> ages = new ArrayList<Integer>();
```

We can construct new Integer objects to put in the ArrayList *ages* by using the Integer constructor or by calling the class method *valueOf* to convert a primitive. Both options take a primitive and return the corresponding wrapper object:

```java
ages.add(new Integer(22));  
ages.add(Integer.valueOf(22));              
```

Converting primitives to their corresponding wrapper objects constantly could get pretty tedious. Fortunately, Java comes with built-in conversion between the two. 

**Autoboxing** is when a primitive value is automatically converted to an object of the wrapper class (Eck, 2019, ch. 7.3.2). For example, we can add a primitive *int* directly to the *ages* ArrayList, and Java will know it needs to convert the value to an Integer object:

```java
ages.add(22);               // auto-boxed version
```

**Unboxing** is when Java automatically converts an object of a wrapper class to a primitive value (Eck, 2019, ch. 7.3.2). For example, if we want to loop through the *ages* ArrayList and print out each value using a for-each loop, we can still use an *int* to represent each element in the array. Java will know to automatically convert each Integer object to its *int* value.

```java
for ( int age : ages) {
   System.out.println(age);
}
```


## Reference

Eck, D. J. (2019). Introduction to programming using Java, version 8.1. [http://math.hws.edu/javanotes](http://math.hws.edu/javanotes)
