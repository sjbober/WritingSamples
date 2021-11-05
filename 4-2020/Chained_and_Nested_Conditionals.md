# Chained and Nested Conditionals

We can use a chained conditional in our program if we want to check for more than 2 possible conditions (known as branches) and execute unique portions of code when one of those conditions is met (Downey, 2015, ch 5.6). For example, imagine we will print out a different message based on what the soup of the day is at our favorite restaurant. There are many more than 2 possible soup flavors, so a chained conditional is a good option to use here:

```python
def soup_of_the_day(flavor):
    if flavor == "Chicken noodle":
        print("Sure, I love chicken noodle soup!")
    elif flavor == "Cheddar Broccoli":
        print("Sure, that sounds good.")
    elif flavor == "Italian Wedding":
        print("No thanks.")
    else:
        print("Hmmmm...too risky. Maybe next time")
```

When a single branch also has multiple options and can be broken into multiple branches, we can create a nested conditional by putting a conditional inside of a conditional branch (Downey, 2015, ch 5.7). A branch in a simple conditional or a branch in a chained conditional can be a nested conditional. Additionally, a nested conditional can be a simple conditional or it can be a chained conditional.

For one example, let's rewrite the *soup_of_the_day* function to also include a parameter called *price*. Maybe we like Cheddar Broccoli and Chicken Noodle soup but will not buy them if the *price* is too high. 

```python
def soup_of_the_day(flavor, price):
    if flavor == "Chicken noodle":
        if price > 10:
            print("Too expensive, no thanks")
        else:
            print("Sure, I love chicken noodle soup!")
    elif flavor == "Cheddar Broccoli":
        if price >= 7:
            print("Too expensive, no thanks")
        else:
            print("Sure, that sounds good.")
    elif flavor == "Italian Wedding":
        print("No thanks.")
    else:
        print("Hmmmm...too risky. Maybe next time")
```

Nested conditionals can get messy quickly, so one way to avoid them is to use logical operators (Downey, 2015, ch 5.7). Let's write a function that determines and prints if someone can buy beer. In the US, the legal drinking age is 21, so we should check to make sure the age is equal to or greater than 21. We should also make sure the person has enough money to buy the beer. In this function, there are three parameters: *age* (which is the age of the person), *money* (how much money they have), and *price* (the price of the beer). 

In this function, we first check to see if the person is 21 or older. If they are, then we check if they have more money than the price. If they do, we print that they can buy beer, and if they don't, we print that they don't have enough money. If the person is not 21 or older, we print out that they can't buy beer because they aren't old enough.

```python
def can_buy_beer(age, money, price):
    if age >= 21:
        if money > price:
            print("You can buy beer")
        else:
            print("You cannot buy beer because you don't have enough money")
    else:
        print("You cannot buy beer because you are not old enough")
```

Now, we can rewrite this function by using the logical operator *and* to avoid using a nested conditional. In the first conditional statement, we check if they are 21 and older and if they have enough money. In the second conditional statement, we only check if they are at least 21. If they are, it means that they don't have enough money (because if they did, the first conditional statement would have been true). Finally, if neither of these statements is true, we can assume that the person is not old enough.

```python
def can_buy_beer_version2(age, money, price):
    if age >= 21 and money > price:
        print("You can buy beer")
    elif age >= 21:
            print("You cannot buy beer because you don't have enough money")
    else:
        print("You cannot buy beer because you are not old enough")
```

## Reference

Downey, A. (2015). Think Python: How to think like a computer scientist. Green Tea Press. This book is licensed under Creative Commons Attribution-NonCommercial 3.0 Unported (CC BY-NC 3.0).