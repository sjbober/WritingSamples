# Using Tuples with Lists and Dictionaries in Python

Tuples are useful because we can use them to iterate over two or more lists (or other sequences) at the same time using a *for* loop and the *zip()* function (Downey, 2015, ch 12.5). 

For example, let's say we are a teacher and we have a project for our class to complete. We want to assign each student a partner in the class and assign each pair of students a topic for the project. 

```python
half_class1 = ['Sarah','Jesse','Rachel','Sam','Michael',]
half_class2 = ['Jimmy','Jessica','Tom','Debbie','Alex']
topics = ['lists','dictionaries','strings','functions','tuples']

groups = []
for each_tuple in zip(half_class1,half_class2, topics):
    groups.append(each_tuple)

print(groups)
```

First, we create two lists of students, where each list has half of our students and a list of topics. Then we create an empty list, which will be used to store our pairs of students and their assigned topic. Then, we iterate over the zip object created by calling the zip function on the three lists. The zip function will create an iterator object, or an object that we can iterate over, which contains a set of tuples where each tuple contains one element from each list in the order that they appear (Ramos, 2019). During each iteration, we append each tuple to our *groups* list and then print the final list. 

```python
# Output
C:\Users\sjbober\Documents\UoPeople\CS1101\unit7>df7.py
[('Sarah', 'Jimmy', 'lists'), ('Jesse', 'Jessica', 'dictionaries'), ('Rachel', 'Tom', 'strings'), ('Sam', 'Debbie', 'functions'), ('Michael', 'Alex', 'tuples')]
```

Another good use for tuples when looping over lists is to use the *enumerate()* function to easily iterate over the list elements and their indices. The *enumerate()* function creates an iterable object of tuples, where each tuple contains an index of the sequence and its corresponding element (Downey, 2015, ch 12.5).

For example, let's say we want to print out our student groupings in our *groups* list along with the index of each pair, to show our students who their partner is, what their topic is, and what their group number is. 

```python
for index, group in enumerate(groups):
    print(index,group)
```

```python
# Output:
C:\Users\sjbober\Documents\UoPeople\CS1101\unit7>df7.py
0 ('Sarah', 'Jimmy', 'lists')
1 ('Jesse', 'Jessica', 'dictionaries')
2 ('Rachel', 'Tom', 'strings')
3 ('Sam', 'Debbie', 'functions')
4 ('Michael', 'Alex', 'tuples')
```

The enumerate() function is also handy if we want to create a dictionary from a sequence and use the index as the key in the dictionary. We can create a dictionary of our student groups using this method:

```python
dictPairings = dict(enumerate(groups))
print(dictPairings)
```

```python
# Output:
C:\Users\sjbober\Documents\UoPeople\CS1101\unit7>df7.py
{0: ('Sarah', 'Jimmy', 'lists'), 1: ('Jesse', 'Jessica', 'dictionaries'), 2: ('Rachel', 'Tom', 'strings'), 3: ('Sam', 'Debbie', 'functions'), 4: ('Michael', 'Alex', 'tuples')}
```

Finally, tuples are also useful if we want to iterate over each key-value pair in a dictionary. Dictionaries have a built-in method called *items()* which creates an iterable object of tuples where each tuple contains a key-value pair from the dictionary (Downy, 2015, ch 12.6).

So, we can iterate over each tuple in our dictionary of student groupings and print them out. 

```python
for each_tuple in dictPairings.items():
    print(each_tuple)
```

```python
# Output:
C:\Users\sjbober\Documents\UoPeople\CS1101\unit7>df7.py
(0, ('Sarah', 'Jimmy', 'lists'))
(1, ('Jesse', 'Jessica', 'dictionaries'))
(2, ('Rachel', 'Tom', 'strings'))
(3, ('Sam', 'Debbie', 'functions'))
(4, ('Michael', 'Alex', 'tuples'))
```


## References

Downey, A. (2015). Think Python, How to think like a computer scientist. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0)

Ramos, L. P. (2019, October 2). Using the Python zip() function for parallel iteration. Retrieved from [https://realpython.com/python-zip-function/](https://realpython.com/python-zip-function/)