# Function Postconditions and Preconditions

When we get an unexpected result from a function, there are three reasons why this could be occurring. The first reason is that a precondition for the function has not been met (Downey, 2015, ch. 6.9). A precondition is a requirement that the caller of the function must meet in order for the function to work properly; in other words, it is an expectation and assumption that the user of the function will supply the right number of arguments, in the right order, and using the appropriate types and values (Downey, 2015, ch 4.10). If the caller of a function supplies arguments that fail to meet the expectations of the function, then the function could produce unintended results or fail to run at all.

Let's look at a simple example where a precondition is not met. The following function called *concatenate_words* takes two string arguments and concatenates them together in the order in which the arguments are given.

```python
def concatenate_words(firstword, secondword):
    """Concatenates two string parameters in the order in which they are listed as arguments.
       Returns the resulting concatenation
    """
    newword = firstword + secondword
    return newword

name = input("Please enter your name: ") # Ask the user to provide a name
greeting = "Hello there, "               # Generic greeting string

print("\nCall the function when the preconditions are not met:")
print(concatenate_words(name, greeting))

print("\nCall the function when the preconditions are met:")
print(concatenate_words(greeting, name))
```

When we call this function, we must remember to put our arguments in the correct order according to our desired result. When we don't, we can see we get a string that doesn't make sense, as we can see in the first output below. In the second output, we put the arguments in the order in which we want them to be concatenated, and now our result makes sense.

```python
>>> 
= RESTART: C:/Users/sjbober/AppData/Local/Programs/Python/Python37-32/df4.py =
Please enter your name: sarah

Call the function when the preconditions are not met:
sarahHello there, 

Call the function when the preconditions are met:
Hello there, sarah
```

A second reason that a function may not be working is that a postcondition for the function has not been satisfied (Downey, 2015, ch 6.9). A postcondition is any expected result that a function has promised to have, which could be printing information, supplying a specific return value, or doing some other action (Downey, 2015, ch 4.10). If one of these promised results does not occur, then the function is not behaving as expected and has a bug.

The function *calcGrade* calculates and returns your grade as a percentage out of 100. It has a parameter *score* that is expected to be a float or integer representation of the score you received on an assignment or test, and the second parameter *total_points* is expected to be a float or integer representation of the total number of points you could have received.

```python
def calcGrade(score, total_points):
    """Takes a float or integer score and a float or integer total_points and 
       calculates the percentage grade out of 100.
    """
    return (total_points/score) * 100

score = float(input("What is your numerical score? \n"))
total = float(input("What was the total possible score? \n"))

print("Your score is: ", calcGrade(score, total))
```

The function looks alright, but if we test it we can see that it is not working properly. In the following example, we provide a score of 9 out of a possible 10. This is a great example to use to test the function because we know that a 9/10 would be a 90%. From the result, we see right away that the return value is wrong: not only is the return value not equal to 90%, but we should not receive a percentage over 100! In this case, the preconditions are not met because the function is not giving a proper return value. In order to fix this issue, the positions of *total_points* and *score* parameters should be switched in the return expression.

```python
>>> 
= RESTART: C:/Users/sjbober/AppData/Local/Programs/Python/Python37-32/df4.py =
What is your numerical score? 
9
What was the total possible score? 
10
Your score is:  111.11111111111111
```

A third reason that a function may not be working is that the function return value is being used incorrectly (Downey, 2015, ch 6.9). In the following function *printHappyBirthday*, the Happy Birthday song gets printed with the string parameter *birthday_person* included as the name of the person being sung to. 

```python
def printHappyBirthday(birthday_person):
    """Takes a string birthday_person and prints out the Happy birthday song
       with that string as the name being sung to
    """
    print("Happy birthday to you, happy birthday to you, happy birthday dear "
             + birthday_person + 
             ", happy birthday to you!")

name = input("What is your name? ")
song = printHappyBirthday(name)

print(song)
```

It is important to be aware of what, if any, values are returned from a function. With this script, the person calling the function assumed that the function returned a string value of the birthday song, so they called the function and assigned it to the variable *song.* But, this function has no return value, and hence the special value None is assigned the variable *song*. When we run this script, the special value None gets printed out unexpectedly.

```python
>>> 
= RESTART: C:/Users/sjbober/AppData/Local/Programs/Python/Python37-32/df4.py =
What is your name? sarah
Happy birthday to you, happy birthday to you, happy birthday dear sarah, happy birthday to you!
None
```

## Reference

Downey, A. (2015). Think Python, How to think like a computer scientist. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0)