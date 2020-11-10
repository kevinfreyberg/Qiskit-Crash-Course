# Welcome to the Qiskit Crash Course!

This an introduction to Qiskit, an open-source quantum computing framework from IBM. This guide is inspired by lectures given by Dr. Walter O. Krawec at the University of Connecticut.

**Important note:**

Please make sure you are importing the correct modules when designing your circuits. In this guide, you'll be expected to follow the following import structure:

```python
from qiskit import QuantumCircuit, execute, Aer, IBMQ, ClassicalRegister, QuantumRegister
from qiskit.compiler import transpile, assemble
from qiskit.tools.jupyter import *
from qiskit.visualization import *
import math
```

Feel free to import any additional modules if need be.