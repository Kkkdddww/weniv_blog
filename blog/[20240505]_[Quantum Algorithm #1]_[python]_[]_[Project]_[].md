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

![계산](img/QAD/cal.png)

If the final measuremnet of x qubit is |0>, then value is constant. If not, the value is balanced. Like this, we need only **one** measurement. 


Now, We will implement for using Python.

Before we make code, I will define unitary gate for four case. Because I can't generalize unique modulo 2 addition into python code. So, I will define 4 gate to work same role with unitary gate.

![코드1](img/QAD/code1.png)

The unitary gate for deutsch algorithm operate like this.

![코드2](img/QAD/code2.png)

This is 4 gate that works same role with unitary gate for deutsch algorithm.

In **case1,** we need **no gate.** In case2, we need **CNOT gate.** In **case3,** we need **CNOT gate and X gate.** In **case4,** we need **X gate.**

With this 4 gate , we can simulate Deutsch algorithm! 

Here is code. I use jupyther notebook workspace.

![코드3](img/QAD/code3.png)

I definite 4 case of function which works for unitary gate. And I display unitary gate for function 3.

![코드4](img/QAD/code4.png)

I definite a circuit for using deutsch algorithm we talked about. In center, the unitary gate that we definite before is appending. 

![코드5](img/QAD/code5.png)

This is the algorithm that checks constant or balanced. As we talked before, if we measure 0, it's constant and measure 1, it's balanced.

In this case, we consider function3 ( x'). So, the result comes 'balanced'.

This is all about **Deutsch's algorithm**. In this algorithm, the advantage is not that strong. Because classic is two measurement and quantum is one measurement. **Just one versus two.** Then, I will show you **Deutsch-Josza algorithm** that has more advantage. It's just **expansion** of Deutsch algorithm!

![조사](img/QAD/jozsa.png)

This is basic circuit. we need to perform hadamard operation on each n qubit.

So, the Deutsch Jozsa algorithm's problem just expands Deutsch algorithm.

**f : {0,1}^n -> {0,1} vs f : {0,1} -> {0,1}**

**Checking constant or balanced**

**constant : same function value(all 0 or all 1)**

**balanced : not constant**

We need other form of hadamard operation to calculate well.

![h](img/QAD/H.png)

When we use this form, we can calculate Unitary gate well.

Also, we need other method to operate unitary gate. A.K.A **phase kickback**

![pka](img/QAD/PKB.png)


If you understand other form of hadamard gate and phase kickback, it's ready!

We operate hadamard gate, unitary gate, hadarmard gate, and measure!

![코드6](img/QAD/code6.png)

This is a specific calculation of first hadamard gate.

![코드7](img/QAD/code7.png)

This is a specific calculation of unitary gate, second hadamard gate and measurement.

The special thing is that we measure |all 0>.