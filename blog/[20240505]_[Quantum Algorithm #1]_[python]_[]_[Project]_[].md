### Deutsch's Algorithm

Assumption : **f(x) : {0,1} -> {0,1}.** The result is **either 0 or 1** depending on input value x, but we don't know the actual value of f(0) and f(1). Also, calculation of f(x) takes a long time, so we want to minimize the number of f(x) calculation.

Challenging : Can we decide whether the value of **f(0)** and **f(1)** are the **same** or **different** only through a **single** calculation?

Yes! When we need to use the **quantum superposition** of the input state and **quantum interference**.


![싱글](img/QAD/single.png)

Our goal is to check constant (value is same) or balanced (value is different).

**Classically, We have to take two measurement.** For example, one for checking f(0) and two for checking f(1). And we can say that It's same or different. 

Then, How about quantum algorithm?

First, I will assume Unitary gate that operates modulo 2 addition.

![유니터리](img/QAD/유니터리.png)

> Accept two input value and produce two output value.

Here is quantum circuit for Deutsch's problem.

![회로](img/QAD/회로.png)

To analyze Deutsch's algorithm, we will trace through the action of the circuit.



