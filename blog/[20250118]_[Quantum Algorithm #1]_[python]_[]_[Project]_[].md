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

### Deutsch-Jozsa algorithm

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

Now, I will implement on IBM qiskit using python.

First, we need to make a code that works for **unitary gate.** This code is quite difficult. The whole code is like this.

![코드8](img/QAD/code8.png)

```python
def dj_function(num_qubits):
    qc = QuantumCircuit(num_qubits + 1)
    if np.random.randint(0, 2):
        # Flip output qubit with 50% chance
        qc.x(num_qubits)
    if np.random.randint(0, 2):
        # return constant circuit with 50% chance
        return qc
```

dj_function is for unitary operation.

In this function, we make x qubits and y qubits. Why I make quantumcircuit for n + 1 qubit is that for y qubit. (+1 for y).

In first if, we make random number either 0 or 1. When 1 comes out, we append x gate on last qubit (y qubit). When 0 comes out, we do not thing.

In second if, we also make random number either 0 or 1. When 1 comes out, just return that quantum circuit. When 0 comes out, just continue.

This two of if statement operate when it is **constant function**.

![코드9](img/QAD/code9.png)

> First if statement : 1 -> f(x) = 1 (constant) / 0 -> f(x) = 0 (constant)

> Second if statement : 1 -> constant's U gate / 0 -> follow more code


```python
 # next, choose half the possible input states
    on_states = np.random.choice(
        range(2**num_qubits),  # numbers to sample from
        2**num_qubits // 2,  # number of samples
        replace=False,  # makes sure states are only sampled once
    )
```

This code is the first step of unitary gate for balanced function. (Half 0, Half 1).

n qubit have 2^n state. So, we have to make half random number for state.

For example, the output is [7 4 2 1] for that code. Then only four input stae ( |111> |100> |010> |001> ) have output of "1". And other state have output of "0"

We make random half state that have output of "1"


```python
 def add_cx(qc, bit_string):
        for qubit, bit in enumerate(reversed(bit_string)):
            if bit == "1":
                qc.x(qubit)
        return qc
```

And we definite "add_cx". Keep in mind this function is in "dj_function"

Let's understand 'enumerate(reversed(bit_string))'

![코드10](img/QAD/code10.png)

```python
for state in on_states:
        qc.barrier()  # Barriers are added to help visualize how the functions are created. They can safely be removed.
        qc = add_cx(qc, f"{state:0b}")
        qc.mcx(list(range(num_qubits)), num_qubits)
        qc = add_cx(qc, f"{state:0b}")

    qc.barrier()

    return qc
```

Last code of dj_function!

`on_states' is qubit number that have output of 1.

Then, Using add_cx function to make real state in circuit. 

Next, operate MCX gate to operate same rule for unitary gate.

![코드11](img/QAD/code11.png)


In my case, the result unitary gate comes out like this.

![코드12](img/QAD/code12.png)


Next is making whole circuit for Deutsch-Jozsa algorithm

```python
def compile_circuit(function: QuantumCircuit):
    """
    Compiles a circuit for use in the Deutsch-Jozsa algorithm.
    """
    n = function.num_qubits - 1
    qc = QuantumCircuit(n + 1, n)
    qc.x(n)
    qc.h(range(n + 1))
    qc.compose(function, inplace=True)
    qc.h(range(n))
    qc.measure(range(n), range(n))
    return qc
```

n is the only input qubit (x qubit).

Next, make quantum circuit that has n + 1 qubit (x, y) and n classical bit for saving measurement.

Next, append x gate on last qubit (y qubit). And append H gate on every qubit (x, y) qubit.

Next, append Unitary gate (dj_function for code).

Lastly, append x gate on only n qubit (x). And measure it and save on classical bit.

Now we will simulate to check either constant or balanced.

The code is this.

![코드13](img/QAD/code13.png)

When '1' is in measurement result, then it is balanced function.