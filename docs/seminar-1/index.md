# Seminar 1: Introduction to Quantum Computing

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

### Qubits in Qiskit
You can use the *QuantumCircuit* object to create qubits by passing a number as an argument (the number of qubits you want).
For example:

```python
my_circuit = QuantumCircuit(1) # Creates a quantum circuit with one qubit1: q0
```

An important thing to note is that qiskit always initializes qubits into the state |0⟩. If you want to manually change the initialization state of a qubit, you can use the *initialize()* method. For example, if we want to intialize one of our qubits to be in the state |1⟩, we can write:

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








