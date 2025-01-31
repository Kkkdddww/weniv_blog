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




