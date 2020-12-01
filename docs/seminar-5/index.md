# Episode V: Applying Everything We've Learned--Quantum Teleportation!

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

Let us first initialize our circuit with the right amount of qubits (3) and classical bits (2), along with another classical bit that will represent our "teleported" state. 

```python
cr1 = ClassicalRegister(1, name = "cr1") # Classical bit 1
cr2 = ClassicalRegister(1, name = "cr2") # Classical bit 2
c_result = ClassicalRegister(1, name = "c_result") # Classical result

qubit0 = QuantumRegister(1, name = "psi") # The quantum state we want to send (Psi)
qubit1 = QuantumRegister(1, name = "qubit1") # Alice's qubit
qubit2 = QuantumRegister(1, name = "qubit2") # Bob's qubit
```

Our next step is to initialize our qubit "Psi" with the correct quantum state. Let us suppose that we want to send the quantum state `|1⟩` to Bob. We can do it like so:

```python
psi = [0, 1] # We want to send |1> to Bob
initial_gate = Initialize(psi)
initial_gate.label = "Initial Gate"

circuit.initialize(psi, qubit0) # Set the quantum state to Psi
```


Following the algorithm, we must then create a Bell pair between qubit A and B, which is just refers to a pair of entangled qubits. 

This is done by applying a Hadamard gate on qubit A, and a CNOT gate with A as the control and B as the target:

```python
circuit.h(qubit1)
circuit.cnot(qubit1, qubit2)
```

*Note*: When we design more intricate quantum algorithms, our circuits will start to look a little messy. Qiskit offers a `.barrier()` method that will allow us to visually separate our gates on our circuits. It does not serve any purpose in the quantum algorithm itself.

Continuing our circuit:

```python
circuit.barrier()
circuit.cnot(qubit0, qubit1)
circuit.h(qubit0)
circuit.barrier()
```

This is where Alice applies a CNOT gate with our quantum state `|Psi>` as the control, and qubit A as the target.

Our next step is to measure our qubits to our classical bits. After this step, Alice sends the classical bits to Bob. This is done in Qiskit like so:

```python
circuit.measure(qubit0, cr1)
circuit.measure(qubit1, cr2)
```

When Bob receives these qubits, he must apply certain gates depending on the states of the classical bits. Recall step 4 from our brief overview of the algorithm:

```
Bob applies certain gates based on the state of the classical bits:
	 00 -> Nothing
	 01 -> X gate
	 10 -> Z gate
	 11 -> ZX gate
```

This can be effectively boiled down to the following two lines using circuit methods offered by Qiskit:

```python
circuit.x(qubit2).c_if(cr2, 1)  
circuit.z(qubit2).c_if(cr1, 1)
```

# Disentanglers ****

```python
inverse_init_gate = initial_gate.gates_to_uncompute() # this is our disentangler
circuit.measure(qubit2, c_result) # measure our result to our third classical bit
```






































