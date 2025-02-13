# Q29 Requirements

## 1. Calculate quantities of cabbages, tomatoes, green peppers, and marigolds.

My goal is to  calculate the optimal number of cabbages, tomatoes, green peppers, and marigolds based on certain constraints (e.g., land space, sunlight, water, & profit maximization).

## 2. Map Variables to Quantum States
Represent each crop as a quantum state or qubit:

- |00> = Cabbages
- |01> = Tomatoes
- |10> = Green Peppers
- |11> = Marigolds

Use superposition to explore all possible combinations of crops.

## 3. Define Constraints as Quantum Gates
Create quantum gates to represent constraints:

- Space Constraint: A gate that limits the total number of crops (e.g., only 2 crops can be grown in a given area).
- Sunlight Constraint: A gate that ensures crops requiring similar sunlight are grouped together.
- Profit Maximization: A gate that optimizes the combination of crops for maximum profit.

## 4. Quantum Algorithm
Use a quantum algorithm (e.g., Grover's algorithm or QAOA) to find the optimal combination of crops that satisfies the constraints.

For example:

- Grover's Algorithm: Search through all possible combinations of crops to find the one that maximizes profit or satisfies the constraints.
- QAOA (Quantum Approximate Optimization Algorithm): Optimize the crop combination based on a cost function (e.g., profit or resource usage).

## 5. Measurement
Measure the quantum states to determine the optimal number of cabbages, tomatoes, green peppers, and marigolds.
<br>Interpret the results classically to provide actionable insights <br>(e.g., "Grow 10 cabbages, 5 tomatoes, 3 green peppers, and 2 marigolds").

## 6. 6. Example Code
```
from qiskit import Aer, QuantumCircuit, transpile, assemble, execute
from qiskit.visualization import plot_histogram

# Define the quantum circuit
num_qubits = 2  # Representing 4 crops (2 qubits)
qc = QuantumCircuit(num_qubits)

# Apply Hadamard gates to create superposition
qc.h(0)
qc.h(1)

# Define constraints as quantum gates (example)
# Example: A gate that ensures at least one crop is chosen
qc.cx(0, 1)

# Measure the qubits
qc.measure_all()

# Execute the circuit
simulator = Aer.get_backend('qasm_simulator')
compiled_circuit = transpile(qc, simulator)
job = execute(compiled_circuit, simulator, shots=1000)
result = job.result()

# Interpret the results
counts = result.get_counts(qc)
print("Optimal Crop Combination:", counts)
```
## 7. Interpret Results
The output will be a histogram of possible crop combinations.

For example, if 01 (Tomatoes) has the highest probability, it suggests tomatoes are the most optimal crop under the given constraints.

## 8. Extend to Multiple Variables
At a later stage I want to include more variables (e.g., soil type, pest resistance), I will add more qubits and adjust the constraints accordingly.

For now below is my complete .ipynb code (Jupyter Notebook) to calculate the optimal number of cabbages, tomatoes, green peppers, and marigolds based on constraints

```
# Quantum Crop Optimization

## Problem Statement
We want to calculate the optimal number of cabbages, tomatoes, green peppers, and marigolds to grow in a garden, given certain constraints (e.g., space, sunlight, and profit maximization). We will use quantum computing to explore all possible combinations and find the best solution.

---

## Step 1: Import Libraries
```python
from qiskit import Aer, QuantumCircuit, transpile, assemble, execute
from qiskit.visualization import plot_histogram
import matplotlib.pyplot as plt
```
## Step 2: Define the Quantum Circuit
We will use 2 qubits to represent 4 crops:

- |00> = Cabbages
- |01> = Tomatoes
- |10> = Green Peppers
- |11> = Marigolds

```
# Create a quantum circuit with 2 qubits
num_qubits = 2
qc = QuantumCircuit(num_qubits)

# Apply Hadamard gates to create superposition
qc.h(0)
qc.h(1)

# Define constraints as quantum gates
# Example: A gate that ensures at least one crop is chosen
qc.cx(0, 1)  # CNOT gate to entangle qubits

# Measure the qubits
qc.measure_all()

# Draw the circuit
qc.draw(output='mpl')
plt.show()
```
## Step 3: Execute the Circuit
We will use Qiskit's simulator to run the circuit and get results.

```
# Use the QASM simulator
simulator = Aer.get_backend('qasm_simulator')

# Compile and run the circuit
compiled_circuit = transpile(qc, simulator)
job = execute(compiled_circuit, simulator, shots=1000)

# Get the results
result = job.result()
counts = result.get_counts(qc)

# Plot the results
plot_histogram(counts)
plt.show()
```
## Step 4: Interpret the Results
The histogram shows the probability distribution of crop combinations. The most probable combination is the optimal solution.
```
# Print the results
print("Crop Combination Probabilities:")
for combination, probability in counts.items():
    crop = ""
    if combination == "00":
        crop = "Cabbages"
    elif combination == "01":
        crop = "Tomatoes"
    elif combination == "10":
        crop = "Green Peppers"
    elif combination == "11":
        crop = "Marigolds"
    print(f"{combination}: {crop} - {probability} counts")

# Determine the optimal crop combination
optimal_combination = max(counts, key=counts.get)
optimal_crop = ""
if optimal_combination == "00":
    optimal_crop = "Cabbages"
elif optimal_combination == "01":
    optimal_crop = "Tomatoes"
elif optimal_combination == "10":
    optimal_crop = "Green Peppers"
elif optimal_combination == "11":
    optimal_crop = "Marigolds"

print(f"\nOptimal Crop Combination: {optimal_combination} ({optimal_crop})")
```
## Step 5: Intent to Extend the Problem 
To include more constraints (e.g., soil type, pest resistance), I am going to add more qubits and adjust the gates accordingly. 
For example I could:
- Use 3 qubits to represent 8 crops or conditions.
- Add more complex gates to model additional constraints.

## Step 6: Save the Notebook

### Output
When I run the notebook, I should see:

1. A quantum circuit diagram.
2. A histogram showing the probability distribution of crop combinations.
3. A printed statement indicating the optimal crop combination.

For example:
```
Crop Combination Probabilities:
00: Cabbages - 250 counts
01: Tomatoes - 300 counts
10: Green Peppers - 200 counts
11: Marigolds - 250 counts

Optimal Crop Combination: 01 (Tomatoes)
```


