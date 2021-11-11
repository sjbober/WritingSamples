# P, NP, NP-Complete, and NP-Hard Problems

In order to fully understand what an NP-Complete problem is, we first need to define some terms.

*P* refers to the set of problems which can be solved in polynomial time, meaning the time to solve it is written as a function of its size raised to some constant c. Essentially this means that *P* includes any problem that can be solved in O(n^c), where c is any integer including zero. An important distinction here is that a problem that takes exponential time, O(2^n), is NOT contained in set *P*. *NP* refers to the set of *decision* (ie, yes or no) problems that when you are given the solution, you can verify that the solution is correct in polynomial time, but you may not necessarily be able to solve it quickly (Erickson, 2019, p. 381). 

The following image shows the relationship between problems in *P* and *NP*.

![Relationship between P and NP](/images/NPandP.png)

Naturally, if a problem can be solved quickly, its solution can also be checked quickly, because we can do so by just solving the problem. However, a problem whose solution can be checked quickly cannot necessarily be solved quickly. 

An example of a problem that is in *NP* but not *P* would be a sudoku puzzle (hackerdashery, 2014). When given a solution to a sudoku puzzle, it's very easy to check and make sure that it is correct. But, for large puzzle sizes, it becomes incredibly difficult to solve and with a large enough grid it becomes impossible for even the fastest computers.

An example of a problem in *P* and *NP* would be a multiplication problem (hackerdashery, 2014). We can easily check if a solution to a multiplication problem is correct, making the problem in *NP*, but the easiest way to check is to solve the problem directly, which makes the problem also in *P*. 

*NP-Complete* problems are the hardest problems in *NP* and do not currently have efficient solutions. It turns out that they are essentially different versions of each other, meaning that one *NP-Complete* problem can be reduced (transformed) to another in polynomial time. These problems arise from a variety of disciplines and include sudoku, protein folding, job scheduling, and the Traveling Salesman Problem. Essentially, if a solution is found for one *NP-Complete* problem, then that same solution could be used to solve other NP-Complete problem, collapsing the boundary between *P* and *NP* (hackerdashery, 2014). The two requirements for an NP-Complete problem is that it is in *NP*, and that there must exist some problem in *NP* that can be reduced to it in polynomial time. 

An *NP-Hard* problem does not necessarily have to be in *NP* (ironic because of its name) but there must exist a problem in NP that can be transformed into it in polynomial time. As stated before, we know that an NP-Complete problem must also have a corresponding problem in NP that can be transformed to it, which makes NP-Complete problems.

The following image shows the relationship between problems in *P,* *NP*, *NP-Hard* and *NP-Complete*.

![Relationship between P, NP, NP-Complete, and NP-Hard](/images/NPandPandNPHard.png)

## References

Erickson, J. (2019). Algorithms. Retrieved from [https://jeffe.cs.illinois.edu/teaching/algorithms/book/Algorithms-JeffE.pdf](https://jeffe.cs.illinois.edu/teaching/algorithms/book/Algorithms-JeffE.pdf)

hackerdashery. (2014, August 26). P vs. NP and the Computational Complexity Zoo. Retrieved from [https://www.youtube.com/watch?v=YX40hbAHx3s&t=310s](https://www.youtube.com/watch?v=YX40hbAHx3s&t=310s)

Shaffer, C. (2011). A Practical Introduction to Data Structures and Algorithm Analysis. Blacksburg: Virginia Tech.