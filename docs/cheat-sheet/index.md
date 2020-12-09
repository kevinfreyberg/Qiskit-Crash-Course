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

## Fundamental Gates
---
#### Hadamard Gate

The *h()* method takes a qubit as an argument and applies a Hadamard gate to it:

```python
circuit.h(qubit) # Applies a Hadamard gate to qubit
```

#### X-gate

The *x()* method takes a qubit as an argument and applies an X-gate to it:

```python
circuit.x(qubit) # Applies an X-gate to qubit
```

#### Y-gate

The *y()* method takes a qubit as an argument and applies a Y-gate to it:

```python
circuit.y(qubit) # Applies a Y-gate to qubit
```

#### Z-gate

The *z()* method takes a qubit as an argument and applies a Z-gate to it:

```python
circuit.z(qubit) # Applies a Z-gate to qubit
```

#### CNOT gate

The *cx()* method takes a control qubit (for the first argument), and a target qubit (for the second argument) and applies a CNOT gate to them:

```python
circuit.cx(control, target) # Applies a CNOT using the control and target qubits
```

#### R(phi)-gate

The *rz()* method takes one qubit and phi radians as arguments and applies an R(phi)-gate to the qubit:

```python
circuit.rz(phi, qubit) # where phi is in radians
```

#### S-gate and its conjugate transpose

The *s()* method takes a qubit as an argument and applies an S-gate to it:

```python
circuit.s(qubit)
```

The conjugate transpose, the *sdg()* method, also takes a qubit as an argument and applies an S-dagger gate to it:

```python
circuit.sdg(qubit)
```

## Entanglement with the Bell Pair function

```python
def bellPair(circuit, qubit0, qubit1): # entangles qubits
    circuit.h(qubit0) 
    circuit.cx(qubit0,qubit1) 
```

## Simulator Functions
---
#### Qasm

```python
def simulateQasm(circuit):
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