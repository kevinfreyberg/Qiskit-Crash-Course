# Seminar 4: Applying Everything We've Learned--Quantum Teleportation!

In this chapter, we will introduce an interesting algorithm: Quantum Teleportation. By the end of this chapter, we will have created a circuit that:
- Uses our knowledge of Qiskit to simulate teleportation

## Quantum Teleportation?

No, we aren't referring to interdimensional travel. However, quantum teleportation is an interesting notion of sending quantum information through the aid of classical communication and entangled quantum states.

The backbone of teleportation is the no-cloning theorem in quantum mechanics, which states that you cannot make a copy of an unknown quantum state. We will leverage this in our simulation.

## The Algorithm

The following snippet outlines the entire algorithm. It might seem slightly esoteric at first, but we will be able to break this down into Qiskit.

```
Suppose A, B, and |Psi> are qubits. |Psi> = alpha|0> + beta|1>

Alice wants to send qubit state |Psi> to Bob.

Steps:
1. Create entangled pair of qubits (Bell pair)
	-Transfer qubit A to X-basis ( |+> and |-> ) by applying a Hadamard gate. Apply Hadamard to |Psi>
	-Apply a CNOT gate with A as the control, and B as a target.
	-Alice is given qubit A and qubit |Psi>. Bob is given qubit B.

2. Alice applies a CNOT gate with |Psi> as the control, and qubit A as the target.

3. Alice measures qubit A and |Psi> into two classical bits. She sends these two classical bits to Bob.

4. Bob applies certain gates based on the state of the classical bits:
	 00 -> Nothing
	 01 -> X gate
	 10 -> Z gate
	 11 -> ZX gate
```

## Creating the circuit in Qiskit

Let us first initialize our circuit with the right amount of qubits (3) and classical bits (2). 

```python
cr1 = ClassicalRegister(1, name = "cr1")
cr2 = ClassicalRegister(1, name = "cr2")
qubit0 = QuantumRegister(1, name = "qubit0")
qubit1 = QuantumRegister(1, name = "qubit1")
qubit2 = QuantumRegister(1, name = "qubit2")

circuit = QuantumCircuit(qubit0, qubit1, qubit2, cr1, cr2)
```

Our first step is to create a Bell pair between qubit A and B, which is just a pair of entangled qubits. 

This is done by applying a Hadamard gate on qubit A, and a CNOT gate with A as the control and B as the target:

```python
circuit.h(qubit1)
circuit.cnot(qubit1, qubit2)
```





























