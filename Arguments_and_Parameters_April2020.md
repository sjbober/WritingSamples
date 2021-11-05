# Arguments and Parameters

*Example 1: Define a function that takes an argument. Call the function. Identify what code is the argument and what code is the parameter.*

A parameter is essentially a variable that acts as a placeholder in a function; when someone calls the function, they can pass whatever arguments they want, and each occurrence of the parameter will be substituted by the given argument (Downey, 2015, ch 3.7). Parameters are useful because we can make our functions dynamic and make actions or return results that vary based on the arguments given, resulting in functions that are more interesting and more useful. 

In my first function, the parameter is called *param*. The function converts the argument into a string, and then concatenates that value with the string "Your argument is ". When I called the function, I used the value integer 2 as the argument.

```python
>>> # Defining the function:
...** def my_function(param):
...     print("Your argument is " + str(param))
...
>>> # Calling the function:
... my_function(2)
Your argument is 2
```

*Example 2: Call your function from Example 1 three times with different kinds of arguments: a value, a variable, and an expression. Identify which kind of argument is which.*

A value is a piece of data that serves as one of the basic building blocks in programming (Downey, 2015, ch 1.5). In this first example, I called the function using a value which is the string "hi".

```python
>>> # Calling the function with a value:
... my_function("hi")
Your argument is hi
```

Whenever we need to use a specific value multiple times, we can assign that value a name which is known as a variable (Downey, 2015, p. 9). Creating variables saves us time because if we need to change a value, we only have to modify our program in one place. In this second example, I assigned the variable *arg* to the value of string "bamboozled". Then I called the function using the variable *arg* as the argument.

```python
>>> # Calling the function with a variable:
... arg = "bamboozled"
>>> my_function(arg)
Your argument is bamboozled
```

In the third example, I needed to use an expression, which is, "a combination of values, variables, and operators" (Downey, 2015, ch 2.3). I created an expression by combining a string, an addition operator, a string, a multiplication operator, and an integer. When evaluated, the expression has a value of a string: "part 1 of expression. ha ha ha ha ha ". The result of calling this function with this expression as the argument gives the following result:

```python
>>> # Calling the function with an expression:
... my_function("part 1 of expression. " + "ha " * 4)
Your argument is part 1 of expression. ha ha ha ha
```

*Example 3: Create a function with a local variable. Show what happens when you try to use that variable outside the function. Explain the results.*

A local variable is a variable that has been declared inside of a function; these variables cannot be referred to outside of the definition of the function (Downey, 2015, ch 3.8).

For this example, I created a function that calculates and displays the area of a triangle. My parameters are *height* and *base*, and I created a local variable called *area* to store the area value before printing it. I called the function with arguments 12 and 3, and the value of 18.0 was displayed. Finally, I tried to print out the local variable called area, but as expected I was given an error because this variable is only defined inside the function and essentially does not exist to the interpreter outside of the function.

```python
>>> # Defining a function with a local variable called area:
... def triangle_area(base, height):
...     area = .5 * base * height
...     print(area)
...

>>> # Calling the function with arguments 12 and 3:
... triangle_area(12,3)
18.0

>>> # Attempting to print the local variable called area
... print(area)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'area' is not defined
```

*Example 4: Create a function that takes an argument. Give the function parameter a unique name. Show what happens when you try to use that parameter name outside the function. Explain the results.*

In this example, I created a function that uses a parameter called *total* to calculate and print the value of a 20% tip for a restaurant bill (here in the US, a 20% tip is typical for good service). Then I called the function, passing it a value of integer 25 as the argument. After calling the function, I attempted to print the parameter variable *total* but was given an error. Parameters are also local variables, which means that they essentially do not exist outside of the function definition and execution (Downey, 2015, ch 3.8).

```python
>>> # Define a function that calculates a 20% tip
... def calculate_tip(total):
...     tip = total * .2
...     print(tip)
...

>>> calculate_tip(25)
5.0

>>> print(total)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'total' is not defined
```

*Example 5: Show what happens when a variable defined outside a function has the same name as a local variable inside a function. Explain what happens to the value of each variable as the program runs.*

First, I assigned the string value "hello" to the variable *greeting*. Then I created a function called *say_hello* which has one parameter called *name*. Inside the function, a local variable called *greeting* is also created and assigned the expression which concatenates the string "greetings ", the parameter, and the string "!". Finally, the local variable *greeting* is displayed. 

After defining the function and again after calling the function, I tried printing the variable *greeting* to see which value gets displayed. As expected, the variable defined outside of the function is the value that gets displayed because the local variable inside of the function is ignored outside of the function.

```python
>>> greeting = "hello"
>>> def say_hello(name):
...     greeting = "greetings " + name + "!"
...     print(greeting)
...
>>> greeting
'hello'
>>> say_hello("Sarah")
greetings Sarah!
>>> greeting
'hello'
```

We can also use a stack diagram to see the value of all the variables during the execution of the program and which functions (if any) they belong to, as well as the order in which functions were called (Downey, 2015, ch 3.9). Below is a stack diagram for the above code:

![Stack diagram for greeting execution](/images/argspar_stackdiagram.png)

The variable *greeting* is assigned to the frame called __main__ because it was defined outside of any function. When the *say_hello* function is called, we can see that the local variable *name* is assigned to the value of string "Sarah", and the local variable *greeting* is assigned to the value "greetings Sarah!". These local variables do not have any effect on variables defined outside of its function, which explains why even after calling the function, the non-local variable *greeting* does not change.

## Reference

Downey, A. (2015). Think Python: How to think like a computer scientist. Green Tea Press. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0).