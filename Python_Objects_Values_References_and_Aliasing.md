# Python Objects, Values, References, and Aliasing

Objects are a piece of data that has a value, type, and unique location in our computer's memory (Rossom, 2001). Therefore, objects are not values, but they have values. This concept can be a bit confusing, which is why it's best to illustrate with examples.

Let's say I want to create a grocery list for myself. I create a Python list where each element is a string that represents the item I need to buy. I create a variable called *my_grocery_list* and assign my list to that variable. 

```python
>>> my_grocery_list = ['eggs', 'milk', 'ice cream', 'bread']
```

So, I have created an object that has a list type, has a value of a list with 5 string elements of 'eggs', 'milk', 'ice cream', and 'bread', in that order, and Python has assigned some memory location to my list that I am unaware of.

Now let's say my mom needs to go shopping and she asks me to make her a list too. She gives me the items she needs, which just so happens to be the same items that I need. So I go through the same process as before, and I assign my new list to a different variable called *mom_grocery_list.*

```python
>>> mom_grocery_list = ['eggs', 'milk', 'ice cream', 'bread']
```

This time, I have also created a new object. This new object has the same type and value as the list assigned to *my_grocery_list*, but now there is one key difference - Python has assigned this list a different memory location than my first list. So my two lists are equivalent, meaning they have the same exact value (Downey, 2015, ch 10.10); in other words, they are the same type (which is a list), both lists have the same number of elements, all of their elements are the same, and the elements are listed in the same order. But, they are not identical because they are not actually the same object (Downey, 2015, ch 10.10). We can validate this by comparing them using the *is* operator:

```python
>>> print(my_grocery_list is mom_grocery_list)
False
```

While this behavior might not seem intuitive, these objects work similarly to objects in real life. If this scenario happened without the help of a computer, I would write down my grocery list on a piece of paper. Then, I would write another list for my mother on a different piece of paper, and her list would happen to have the same items as mine. The final result would be that I have two pieces of paper that look exactly the same, but we know that they are still two different objects. The same goes for objects in Python. They might look exactly the same, but they are two different objects that occupy different physical locations in memory.

Python does a good job of remembering where it stores objects in memory, but humans are not very good at remembering things like that, which is why variables are important to help us distinguish between different objects. When we assign an object to a variable, we are creating a reference to that object (Downey, 2015, ch 10.11). We can use this variable, or reference, to *refer back* to our object whenever we need it. We have already been doing this quite a bit. 

You might be wondering, why do we even need to care about objects vs values vs references, etc? One answer is that oftentimes we need to do manipulations or calculations on objects, but we want to keep the original list just in case. Think about any paper or assignment that you have worked on. It's always a safe bet to make a copy of your work, just in case something goes wrong and you need to revert back to the original.

 In Python, there are actions that seem like we are making a copy of our object, but we are actually creating a second reference to it; when an object has more than one variable that refers to it, it is known as aliasing (Downey, 2015, ch 10.11). 

For example, let's redo the first scenario with grocery lists. I quickly create a Python list and assign it to variable *grocery_list*, and then, thinking I'll save some time, I go ahead and assign *grocery_list* to the variable *grocery_list2.* 

```python
>>> grocery_list = ['eggs', 'milk', 'ice cream', 'bread']
>>> grocery_list2 = grocery_list 
```

I think I saved myself some time from having to write the same list twice. I tell my mom what her variable name is so she can refer to it when she needs it. Now I go to the store and start crossing things off my list.

```python
>>> grocery_list.remove('eggs')
>>> grocery_list
['milk', 'ice cream', 'bread']
>>> grocery_list.remove('milk')
>>> grocery_list
['ice cream', 'bread']
>>> grocery_list.remove('ice cream')
>>> grocery_list
['bread']
```

I can't find any bread, so I leave the store with only one thing left on my list. But now my mom arrives at the store, and goes to check what's on her list, and is extremely surprised to see that there is only bread.

```python
>>> grocery_list2
['bread']
```

Instead of creating a copy of my list, I aliased it by giving it a second name (variable). So the object assigned to *grocery_list* and the object assigned to *grocery_list2* are both equivalent (same value) and identical (they are the same object). Again, we can verify this by using the *is* operator.

```python
>>> print(grocery_list is grocery_list2)
True
```

Now, when we create functions that have parameters, similar behavior occurs: the parameter will become an additional reference for whatever object we pass as the argument (Downey, 2015, ch 10.12).

For example, let's create a function to delete objects off my grocery list instead of doing it manually each time. The function *deleteGroceryItem* has a parameter *groceries* that should be a list and another parameter *item* that should be a string item that is in the *groceries* list. 

```python
>>> def deleteGroceryItem(groceries, item):
...     groceries.remove(item)
...
```

Whenever I call this function, the function will alias the argument object by assigning the parameter variable name *groceries* to it and using the parameter to refer to the same object.

So, when we pass a list to the function *deleteGroceryItem*, the function alters the original list. We can see this in the example below:

```python
>>> grocery_items = ['eggs', 'milk', 'ice cream', 'bread']
>>> deleteGroceryItem(grocery_items, 'eggs')
>>> grocery_items
['milk', 'ice cream', 'bread']
>>>
```

If we want to avoid aliasing our original list, we can create a copy of our list inside of our function and do all of our manipulations on the copy. Then, we can return the copy.

```python
>>> def deleteItemV2(groceries, item):
...     copy_groceries = groceries[:]
...     copy_groceries.remove(item)
...     return copy_groceries
...
>>> grocery_items = ['eggs', 'milk', 'ice cream', 'bread']
>>> after_shopping_list = deleteItemV2(grocery_items, 'ice cream')
>>> grocery_items
['eggs', 'milk', 'ice cream', 'bread']
>>> after_shopping_list
['eggs', 'milk', 'bread']
```

## References

Downey, A. (2015). Think Python, How to think like a computer scientist. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0)

Rossom, G. V. (2001, June 22). Python Reference Manual. Retrieved from [https://docs.python.org/2.0/ref/ref.html](https://docs.python.org/2.0/ref/ref.html)