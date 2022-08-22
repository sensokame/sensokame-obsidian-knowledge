# Big O Notation
big O notation is used to classify algorithms according to how their run time or space requirements grow as the input size grows
> we can read more in the [Wikipedia page](https://en.wikipedia.org/wiki/Big_O_notation)

In computer science the lower the big o value of the code the better it is.

It is also important to note that, calculating the minimum big o of the input (which is basically the number of variables of a function) can provide a better idea on what solution is allowed. In other words, if the input's big O notation is larger than the allowed time limit of the function, then brute forcing is probably out of the question.

>**NOTE:** the time limit of a function can be approximated by taking the largest input allowed in relation to the average number of operation per second the machine is capable of handling
>Ordinary computer processes about 10^8-10^9 operations per second
>So an O(n) algirothm with a maximum input limit of 10^8 will take at most 1 second of execution time, this is crucial information that helps to determine the algorithm complexity allowed for a time limit specified.
>this is better explained in the [codeforces blog](https://codeforces.com/blog/entry/21344) about  determining the algorithm based on the constraints

