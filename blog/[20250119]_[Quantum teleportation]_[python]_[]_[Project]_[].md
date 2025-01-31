### Quantum teleportation

First, we need to talk about quantum teleportaion protocol.
The point of this protocol is **making a entangled quantum state** between 
sender (Alice) and reciever (Bob).

* A = Alice , B = Bob , Q = Qubit that Alice wish to send

**This is an overview of the protocol, and I will go through the detailed calculations with the circuit later.**

1.&nbsp; Make the entangled quantum state between Alice and Bob.

![얽힘상태](img/QT/entangled.png)

2.&nbsp; Alice performs a **controlled-NOT operation** on the pair (A,Q). Q is the control qubit and A is the target qubit. and then performs a **hadamard operation** on Q.

> Hardamard gate makes **superposion** and c-not gate makes **entanglement**.
we makes another entanglement between Q and Alice.

3.&nbsp; Alice measures both A and Q, with a standard measurement and transmits classical outcomes to Bob. Let measurement outcome of A as a and Q as b.

4.&nbsp; Bob receives a and b from Alice, and depending on the values of these bits he performs several operation.


**Analysis**

![회로](img/QT/QTcircuit.png)

![계산](img/QT/QTcal.png)

**Conclusion**

1.&nbsp; In all four cases for Bob's operation, final result is same with Q qubit.
So, the teleportation protocol works correctly. Then, we might think that this teleportation is faster than light. It seems that quantum information transmit to bob immediately. But, Bob need to take several operation according to Alice's classical transportation. Quantum teleportaion protocal needs classical transportation. So, Superluminal transportation not happens!

2.&nbsp; Bob can get four cases of information that happens 1/4 probability. This means no cloning theorem is correct.


**Let's implement on IBM qiskit using python!**
I'm going to use Jupyter notebook.

![코드1](img/QT/code1.png)

> QuantumCircuit : make and manipulate quantum circuit , QuantumRegister : make a set of qubit , ClassicalRegister : make a set of classic bit.

> AerSimulator : simulate quantum circuit, not a real quantum computer.

> plot_histogram : draw histogram of result , array_to_latex : transform array to latex.

> marginal_distribution : calculate distribution of qubit from measurement.

> Ugate : import unitary gate , pi : pi(math) , random : generate random number.

![코드2](img/QT/code2.png)

> Output result

![코드3](img/QT/code3.png)

![코드4](img/QT/code4.png)

> We need to generate Unitary gate. According to postulate of quantum mechanics, every transform can be described by unitary map. U|0> = a|0> + b|1>. Then, when we apply inverse of these U gate, we can get inital state |0>. Using this method to check protocal works correctly.

![코드5](img/QT/code5.png)

> Appending Unitary gate and its inverse to first whole gate.

![코드6](img/QT/code6.png)

![코드7](img/QT/code7.png)

> This simulation tells that Bob's measurement always has |0> state. Because we put X and Z gate for specific condition. Also, every state has probability that near by 1/4.

> But why not the probaaility is accurately 1/4? Because of the statistical error.
![에러](img/QT/error.png)
Considering standard deviation, the result makes sense. If we simulate 1 million times, the result shows almost accurately 1/4.

![코드9](img/QT/code9.png)

> This result shows that we simulate 1024 times.


**Reference**

1.&nbsp; IBM Quantum documantion

2.&nbsp; Zubairy[Quantum Mechanics for Beginnner]

3.&nbsp; Nealson,Chuang[Quantum computation and Quantum information]

