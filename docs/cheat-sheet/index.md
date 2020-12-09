# Qiskit Cheatsheet (WIP)
---
This page is designed to be an example-based reference for using the various Qiskit classes, functions, and methods we have discussed throughout the guide.

## Circuit Basics
---
#### Qubit Creation

The *QuantumRegister* object takes two arguments: the number of qubits you want to use, and a label:

```python
qubit0 = QuantumRegister(1, name = "qubit0")
```

The *ClassicalRegister* object takes two arguments: the number of bits you want to use, and a label:

```python
classic_bit0 = ClassicalRegister(1, name = "classic_bit0")
```

#### Circuit Creation

The *QuantumCircuit* object takes your *QuantumRegister* and *ClassicalRegister* objects as arguments and creates a circuit:

```python
circuit = QuantumCircuit(qubit0, classic_bit0)
```

Alternatively, you can pass in integer values if you do not want to create separate *QuantumRegister*/*ClassicalRegister* objects:

```python
circuit = QuantumCircuit(1, 1)
```

#### Circuit Methods

Using your *QuantumCircuit* object, you can initialize your qubit state with the *initialize()* method:

```python
state = [0, 1] # This is a vector in the form of a list: [alpha, beta]
circuit.initialize(state, qubit0) # Initializes qubit0 to the defined state
```

To measure, you can use *measure()*:

```python
circuit.measure(qubit0, classic_bit0) # Perform Z-measurement on qubit0
```

To visualize your circuit, you can use *draw()*:

```python
circuit.draw()
```

## Simulator Functions
---
#### Qasm

```python
def qasm(circuit):
    backend = Aer.get_backend('qasm_simulator') # Loads the qasm simulator
    job = execute(circuit, backend, shots=1024).result().get_counts() # Retrives results from simulation
    return plot_histogram(data)
```

#### Statevector Simulator

```python
def simulateStateVector(circuit):
    backend = Aer.get_backend('statevector_simulator') # Loads the statevector simulator
    data = execute(circuit, backend).result().get_statevector() # Retrives results and statevector from simulation
    return plot_histogram(data) # Presents data with a histogram
```

#### Bloch Sphere Simulator

```python
def simulateBlochSphere(circuit):
    backend = Aer.get_backend('statevector_simulator') # Loads the statevector simulator
    job = execute(circuit,backend).result().get_statevector() # Retrives results and statevector from simulation
    return plot_bloch_multivector(job) # Presents the Bloch sphere
```