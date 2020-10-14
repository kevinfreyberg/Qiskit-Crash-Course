# Seminar 1: Introduction to Quantum Computing

In this chapter, we will introduce Qiskit and create a basic quantum circuit that:
- Places a qubit into superposition
- Performs a Z-measurement on the qubit



### Quantum Bits (qubits)

As you might know, classical bits are represented with either 0 or 1. For the longest time, we have utilized classical 
bits for many different applications of computing. However, they contain some limitations--adversaries can copy them.

Quantum computers introduce **qubits**. As opposed to classical bits, qubits are the fundamental units of quantum information.
Unlike classical bits, qubits cannot be copied according to the **no-cloning theorem**. This will prove to be beneficial in our
quantum computing endeavor.

Remember when I mentioned classical bits can be either 0 or 1? What about qubits? 

### Qubit states
Qubits can be 0, 1, or a **superposition** of 0 and 1. Their states are represented through ket-notation:

```
State 0: |0⟩ 
State 1: |1⟩
Superposition: α|0⟩ + β|1⟩ where α and β are probability amplitudes. 
```
How can this be represented in Qiskit? Let's hop into the IBM Quantum Lab.

By default, new notebooks in the Quantum Lab only import a handful of standard Qiskit libraries. You'll want to adjust the first import statement so we can use the ClassicalRegister and QuantumRegister objects.

```python
from qiskit import QuantumCircuit, execute, Aer, IBMQ, ClassicalRegister, QuantumRegister
```

### Qubits in Qiskit
You can use the *QuantumCircuit* object to create qubits by passing a number as an argument (the number of qubits you want).
For example:

```python
my_circuit = QuantumCircuit(1, 1) # Creates a quantum circuit with one qubit, one classic bit
```

Alternatively, you can use the *QuantumRegister* and *ClassicalRegister* objects. *QuantumRegister* is used to create a qubit on the quantum register, and *ClassicalRegister* is used to create a classical bit on the classical register. These two objects can be passed as arguments to *QuantumCircuit* to create a circuit.

```python
qubit0 = QuantumRegister(1, name = "qubit0")
classic_bit0 = ClassicalRegister(1, name = "classic_bit0")
circuit = QuantumCircuit(qubit0, classic_bit0)
```
*QuantumRegister* and *ClassicalRegister* take two arguments: a number of qubits/bits, and a label for the circuit drawing.

An important thing to note is that qiskit always initializes qubits into the state `|0⟩`. If you want to manually change the initialization state of a qubit, you can use the *initialize()* method. For example, if we want to intialize one of our qubits to be in the state `|1⟩`, we can write:

```python
my_circuit = QuantumCircuit(1)
state = [0, 1] # This is a vector in the form of a list: [alpha, beta]
my_circuit.initialize(state, 0) # Initializes q0 to state |1⟩
```

Note that our state is in the form of [alpha, beta]. If you wanted to put your qubit into a superposition, you need to satisfy the property:

```
|α|^2 + |β|^2 = 1
```

For example, this is valid:
```python
state = [math.sqrt(1/3), math.sqrt(2/3)]
```

This is **not** valid:
```python
state = [math.sqrt(1/4), math.sqrt(1/4)]
```








