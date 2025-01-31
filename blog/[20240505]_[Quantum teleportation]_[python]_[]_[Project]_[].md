### Quantum teleportation

First, we need to talk about quantum teleportaion protocal.
The point of this protocal is **making a entangled quantum state** between 
sender (Alice) and reciever (Bob).

* A = Alice , B = Bob , Q = Qubit that Alice wish to send

**This is an overview of the protocol, and I will go through the detailed calculations with the circuit later.**

1. Make the entangled quantum state between Alice and Bob.

![얽힘상태](img/entangled.png)

2. Alice performs a **controlled-NOT operation** on the pair (A,Q). Q is the control qubit and A is the target qubit. and then performs a **hadamard operation on Q.

> Hardamard gate makes **superposion** and c-not gate makes **entanglement**.
we makes another entanglement between Q and Alice.

3. Alice measures both A and Q, with a standard measurement and transmits classical outcomes to Bob. Let measurement outcome of A as a and Q as b.

4. Bob receives a and b from Alice, and depending on the values of these bits he performs several operation.



