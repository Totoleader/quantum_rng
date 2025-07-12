# Quantum RNG

A simple **Quantum Random Number Generator** built with [Qiskit](https://qiskit.org/).

---

## Overview

Traditional digital computers generate *pseudo-random* numbers based on algorithms, which are deterministic and can be predicted if the seed is known.

Quantum computers, on the other hand, can generate **true random numbers** by exploiting the inherent randomness of quantum mechanics.

---

## How It Works

- Each qubit starts in the \|0⟩ state.
- Applying a **Hadamard (H) gate** to a qubit puts it into an equal superposition of \|0⟩ and \|1⟩.
- Measuring the qubit collapses it to either 0 or 1 with a 50% chance each.
- By applying the Hadamard gate to **all qubits in an 8-qubit circuit**, you get a random 8-bit binary string.
- This binary string corresponds to a truly random integer between **0 and 255**.

---

## Usage

```python
# Example: Generate a random 8-bit number using Qiskit

from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator
 
 #create a quantum circuit a 8 bits
n = 8
qc = QuantumCircuit(n)
 
 #apply hadamard gate to randomize each bit
for i in range(n):
    qc.h(i)

#maps the problem from quantum to digital
qc.measure_all()

#optimises the code for QPU
sim = AerSimulator()
qc = transpile(qc, sim)

#runs the simulation (only once)
job = sim.run(qc, shots=1)
result = job.result()
counts = result.get_counts()

#prints out the output
number = int(list(counts.keys())[0], 2)
print(number)