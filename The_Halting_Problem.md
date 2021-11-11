# The Halting Problem

We often talk about "hard" problems, which are problems that do not have efficient solutions and will take a very long time to solve. But, as long as we have enough memory and enough time, when we run a program for a hard problem eventually we will reach a solution. However, there are problems that, no matter how much time and memory we have, a program designed to solve it will run indefinitely and never reach a solution. These problems are called "impossible" or "undecidable" problems. An important question in computability theory is, given such a program and some input, can we determine that the program will terminate? This infamous question has become known as the Halting Problem because we want to know if a particular program will terminate, or halt (Shaffer, 2011, p. 555). 

You might think that to see if a program will terminate, all we have to do is look at the program. And sometimes, this is sufficient to know immediately that it will result in an infinite loop. For example, a simple program that only contains a while loop such as: "while (True) continue;" will obviously run forever. But there are many programs where we cannot tell just by looking at it whether it will run forever, so this is not a reliable method. We could also just run the program and see if it ends, but that poses its own problems. For instance, if we have infinite resources, how long do we have to run the program before we can reasonably determine that it has resulted in an infinite loop? Is 10 days acceptable? 10 months? 10 years? What if we make the cutoff 10 years but it turns out that just one more month would have resulted in the program terminating on its own? As such, running the program is also not a reliable method (Programming Word of the Day, 2018).

Fortunately, Alan Turing saved us some time by proving in 1936 that the Halting Problem is in fact unsolvable using a proof by contradiction (Brilliant.org). First we assume that we have a function called *halts* that takes another program as its input as parameters and returns whether or not the program will terminate. 

```java
boolean halts(String program, String input) { 
    //special code here 
};
```

Then we write a program that will return the opposite of what the *halts* function produces. That is, function *contrary* takes a program and an input, and if that program terminates, we produce an infinite loop. If the program does not terminate, we return true. 

```java
boolean contrary(program, input) {
    if (halts(program, input)) {
	while(true) continue;
        return true;
    } else {
        return false
    }
}
```

Now, what will happen if *contrary* calls itself using itself as both arguments? This call would look like:

```java
contrary(contrary, contrary);
```

which will result in the call:

```java
halts(contrary, contrary);
```

Because we have assumed that halts exist, it should properly tell us whether contrary will produce the correct result. 

Let's say that in this case, *halts* returns true, meaning that if *contrary* takes itself as an argument, it will terminate. But, if *halts* returns true, then *contrary* ends up in an infinite loop. So, this result contradicts itself.

Now let's say that *halts* returns false, meaning that *contrary* will *not* terminate if it takes itself as an argument. But if *halts* returns false, then *contrary* returns false and terminates! Since *halts* incorrectly predicts in both cases whether *contrary* will terminate, we know that no function can exist that can properly predict whether a function will terminate (Shaffer, 2011, p. 559-560). 

The Halting Problem is incredibly important because we can use it to prove that other problems are also unsolvable by reduction. If we assume that a computer program does exist that can solve the problem, all we have to do is use it to solve another problem that has already been proven to be unsolvable (Schaffer, 2011, p. 560).

## References

[Brilliant.org](http://brilliant.org/). (n.d.). Halting problem. Retrieved from [https://brilliant.org/wiki/halting-problem/](https://brilliant.org/wiki/halting-problem/)

Programming Word of the Day. (2018, June 19). What is halting problem? Retrieved from [https://programmingwords.com/home/halting-problem](https://programmingwords.com/home/halting-problem)

Shaffer, C. (2011). A Practical Introduction to Data Structures and Algorithm Analysis. Blacksburg: Virginia Tech.