# Computational Complexity

## <mark style="color:purple;">Fundamentals of Algorithms Analysis</mark>

<mark style="color:purple;"></mark>

In this chapter, you will learn:

-   What's the best way to measure your code's performance regardless of what hardware you use.
-   Learn how to use Big O notation to compare algorithms.
-   How to use algorithms analysis to improve your programs speed.

Before going deeper into space and time complexity, let's cover the basics real quick.

**What are Algorithms?**

Algorithms (as you might know) are steps of how to do some tasks. When you cook, you follow a recipe (or an algorithm) to prepare a dish. Let's say you want to make a pizza.

Example of an algorithm to make pizza

```
import { rollOut, applyToppings, Oven } from '../pizza-utils';

function makePizza(dough, toppings = ['cheese']) {
    const oven = new Oven(450);
    const rolledDough = rollOut(dough);
    const rawPizza = applyToppings(rolledDough, toppings);
    const pizzaPromise = oven.bake(rawPizza, { minutes: 20 });
    return pizzaPromise;
}
```

If you play a game, you'll devise strategies (or algorithms) to win. Likewise, algorithms in computers are a set of instructions used to solve a problem.

|

Tip

\| Algorithms are the steps on how to perform a task. |

**Comparing Algorithms**

Not all algorithms are created equal. There are "good" and "bad" algorithms. The good ones are fast; the bad ones are slow. Slow algorithms cost more money to run. Inefficient algorithms could make some calculations impossible in our lifespan!

Let's say you want to compute the shortest path from Boston to San Francisco. Slow algorithms can take hours or crash before finishing. On the other hand, a "good" algorithm might compute in a few seconds.

Usually, algorithms time grows as the size of the input increases. For instance, calculating the shortest distance from your house to the local supermarket will take less time than other destination thousands of miles away.

Another example is sorting an array. A good sorting algorithm is [part04-algorithmic-toolbox.asc](https://github.com/amejiarosario/dsa.js-data-structures-algorithms-javascript/blob/master/book/content/part01/part04-algorithmic-toolbox.asc#merge-sort), and an inefficient algorithm for large inputs is [part04-algorithmic-toolbox.asc](https://github.com/amejiarosario/dsa.js-data-structures-algorithms-javascript/blob/master/book/content/part01/part04-algorithmic-toolbox.asc#selection-sort). Organizing 1 million elements with merge sort could take 20 seconds, for instance, while selection sort takes 12 days, ouch! The fantastic thing is that both programs solve the same problem with comparable data and hardware; yet, there's a big difference in time! Bad algorithms would perform poorly, even on a supercomputer.

To give you a clearer picture of how different algorithms perform as the input size grows, look at the following problems and how their relative execution time changes as the input size increases.

Table 1. Relationship between algorithm input size and time taken to complete

| Input size → | 10  | 100 | 10k | 100k | 1M  |
| ------------ | --- | --- | --- | ---- | --- |
|              |     |     |     |      |     |

Finding if a number is odd

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

\| |

Sorting array with merge sort

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

few sec.

|

20 sec.

\| |

Sorting array with Selection Sort

|

< 1 sec.

|

< 1 sec.

|

2 minutes

|

3 hours

|

12 days

\| |

Finding all subsets

|

< 1 sec.

|

40,170 trillion years

|

> centillion years

|

∞

|

∞

\| |

Finding string permutations

|

4 sec.

|

> vigintillion years

|

> centillion years

|

∞

|

∞

|

As you can see in the table, most algorithms on the table are affected by the input size. But not all and not at the same rate. Finding out if a number is odd will take the same if it is 1 or 1 million. We say then that the growth rate is constant. Others grow very fast. Finding all the permutations on a string of length 10 takes a few seconds, while if the string has a size of 100, it won't even finish!

After completing this book, you are going to _think algorithmically_. You will be able to tell the growth rate of your programs and scale them. You'll find bottlenecks of existing software and have an [part04-algorithmic-toolbox.asc](https://github.com/amejiarosario/dsa.js-data-structures-algorithms-javascript/blob/master/book/content/part01/part04-algorithmic-toolbox.asc#algorithms-toolbox).

**Increasing your code performance**

The first step to improve your code performance is to learn how to measure it. As somebody said:

> Measurement is the first step that leads to control and eventually to improvement. If you can't measure something, you can't understand it. If you can't understand it, you can't control it. If you can't control it, you can't improve it.

\--- H. J. Harrington

This section will learn the basics of measuring our current code performance and compare it with other algorithms.

**Calculating Time Complexity**

In computer science, time complexity describes the number of operations a program will execute given the size of the input `n`.

How do you get a function that gives you the rough number of operations that the CPU will execute?

One idea is to analyze your code line by line and mind code inside loops. Let's do an example to explain this point. For instance, we have a function to find the minimum value on an array called `getMin`.

[![Operations per line](https://github.com/amejiarosario/dsa.js-data-structures-algorithms-javascript/raw/master/book/images/image4.png)](https://github.com/amejiarosario/dsa.js-data-structures-algorithms-javascript/blob/master/book/images/image4.png)

Figure 1. Translating lines of code to an approximate number of operations

Assuming that each line of code is an operation, we get the following:

_3n + 3_

`n` = input size.

That means that if you have an array of 3 elements, e.g. `getMin([3, 2, 9])`, then it will execute around _3(3)+3 = 12_ operations. Of course, this is not for every case. For instance, Line 12 is only executed if the condition on line 11 is met. As you might learn in the next section, we want to get the big picture and get rid of smaller terms to compare algorithms easier.

**Space Complexity**

Space complexity is similar to time complexity. However, instead of the count of operations executed, it will account for the amount of memory used additionally to the input.

For calculating the space complexity, we keep track of the "variables" and memory used. In the `getMin` example, we create a variable called `min`, which only holds one value at a time. So, the space complexity is `1`. On other algorithms, If we have to use an auxiliary array that holds the same number of elements as the input, then the space complexity would be `n`.

**Simplifying Complexity with Asymptotic Analysis**

When we compare algorithms, we about the growth rate when the input gets huge (towards infinity). Then you have a function like `20*n^3 + 100`. If `n` is one million. The term `+ 100` makes a tiny contribution to the result (less than 0.000001%). Here is when the asymptotic analysis comes to the rescue.

|

Tip

\| Asymptotic analysis describes the behavior of functions as their inputs approach to infinity. |

In the previous example, we analyzed `getMin` with an array of size 3; what happens if the size is 10, 10k, or 10 million?

Table 2. Operations performed by an algorithm with a time complexity of `3n + 3`

| n (size) | Operations | total |
| -------- | ---------- | ----- |
|          |            |       |

10

|

3(10) + 3

|

33

\| |

10k

|

3(10k)+3

|

30,003

\| |

1M

|

3(1M)+3

|

3,000,003

|

As the input size `n` grows bigger and bigger, then the expression _3n + 3_ is closer and closer to _3n_. Dropping terms might look like a stretch at first, but you will see that what matters the most is the higher-order terms of the function rather than lesser terms and constants.

**What is Big O Notation?**

There's a notation called Big O, where `O` refers to the order of a function in the worst-case scenario.

|

Tip

\| Big O = Big Order (rate of growth) of a function. |

If you have a program that has a runtime of:

_7n3 + 3n2 + 5_

You can express it in Big O notation as _O(n3)_. The other terms (_3n2 + 5_) will become less significant as the input grows bigger.

Big O notation only cares about the "biggest" terms in the time/space complexity. It combines what we learn about time and space complexity, asymptotic analysis and adds a worst-case scenario.

All algorithms have three scenarios:

-   Best-case scenario: the most favorable input arrangement where the program will take the least amount of operations to complete. E.g., a sorted array is beneficial for some sorting algorithms.
-   Average-case scenario: this is the most common case. E.g., array items in random order for a sorting algorithm.
-   Worst-case scenario: the inputs are arranged in such a way that causes the program to take the longest to complete. E.g., array items in reversed order for some sorting algorithm will take the longest to run.

To sum up:

|

Tip

\| Big O only cares about the run time function's highest order in the worst-case scenario. |

|

Warning

\| Don't drop terms that are multiplying other terms. _O(n log n)_ is not equivalent to _O(n)_. However, _O(n + log n)_ is. |

There are many common notations like polynomial, _O(n2)_ as we saw in the `getMin` example, constant _O(1)_, and many more that we are going to explore in the next chapter.

Again,

|

Tip

\| the time complexity is not a direct measure of how long a program takes to execute, but rather how many operations it performs given the input size. |

Nevertheless, there's a relationship between time complexity and clock time, as shown in the following table.

Table 3. How long an algorithm takes to run based on their time complexity and input size

| Input Size | O(1) | O(n) | O(n log n) | O(n2) | O(2n) | O(n!) |
| ---------- | ---- | ---- | ---------- | ----- | ----- | ----- |
|            |      |      |            |       |       |       |

1

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

\| |

10

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

4 seconds

\| |

10k

|

< 1 sec.

|

< 1 sec.

|

< 1 sec.

|

2 minutes

|

∞

|

∞

\| |

100k

|

< 1 sec.

|

< 1 sec.

|

1 second

|

3 hours

|

∞

|

∞

\| |

1M

|

< 1 sec.

|

1 second

|

20 seconds

|

12 days

|

∞

|

∞

|

|

Note

\| This is just an illustration since, in different hardware, the times will be distinct. These times are under the assumption of running on 1 GHz CPU, and it can execute on average one instruction in 1 nanosecond (usually takes more time). Also, keep in mind that each line might be translated into dozens of CPU instructions depending on the programming language. |
