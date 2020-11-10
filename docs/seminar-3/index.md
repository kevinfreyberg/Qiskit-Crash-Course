# Seminar 3: Entanglement

In this chapter, we will introduce the use of multiple qubits and how to manipulate them in Qiskit. At the end of this chapter, we will have created a circuit that:
- Creates a bell pair

## The CNOT Gate

This one's important. The CNOT gate works on two qubits, and is the backbone of creating a bell pair. The first qubit is known as the control  and the second qubit as the target. In Qiskit, it is represented by:

```python
circuit.cx(control, target)
```

At first glance, the CNOT gate might appear to have some funky behavior. For one, it leaves the control qubit unchanged. Secondly, it performs an X-gate on the target qubit if the state of the control is `|1⟩`. 

However, when we deal with entanglement, we have a lot to thank the CNOT gate for.

## Bell pair

The structure of a Bell pair is quite simple. Among two-qubits, itt is created by applying a Hadamard gate on the control qubit, and then applying a CNOT gate on the control and target.

Let's try it in Qiskit:

```python
qubit0 = QuantumRegister(1, name = "qubit0") # Create a qubit on the quantum register
qubit1 = QuantumRegister(1, name = "qubit0") # Create a qubit on the quantum register

classic_bit0 = ClassicalRegister(1, name = "classic_bit0") # Create a classic bit on the classical register
circuit = QuantumCircuit(qubit0, qubit1, classic_bit0) # Create a quantum circuit from our qubit/bit

circuit.h(qubit0) # Apply a Hadamard
circuit.cx(qubit0, qubit1) # Apply a CNOT
```

After this process, there are only two possible states: `|00⟩` and `|11⟩`. Essentially, this means that the qubits are *entangled*. 

## Entanglement of qubits

You might have heard of quantum entanglement in a science-fiction movie as some sort of mystical, complicated phenomenon. However, in reality, it isn't *too* complex. In fact, entanglement (let us assume there are two qubits in a Bell state) just means that two qubits share the same quantum state.

This notion of quantum entanglement is used in quantum algorithms, such as Quantum teleportation. In the next chapter, we will actually simulate the teleportation of qubit states. 































