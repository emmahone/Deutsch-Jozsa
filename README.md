# The Deutsch-Jozsa Algorithm
The Deutsch-Jozsa algorithm is a quantum algorithm that solves the problem of determining whether a given function is constant or balanced. This problem can be formulated as follows:

Given a function f(x) that maps a binary string x of length n to a single bit, determine whether f(x) is a constant function (i.e., f(x) takes on the same value for all possible inputs) or a balanced function (i.e., f(x) takes on each possible value equally often, with half of the inputs mapping to 0 and half mapping to 1).

The classical solution to this problem requires evaluating the function for half of the possible inputs, and then checking whether all of the outputs are the same or not. In the worst case, this requires evaluating the function for 2^(n-1) + 1 inputs, which grows exponentially with n.

The Deutsch-Jozsa algorithm solves this problem with just one evaluation of the function f(x), using a quantum circuit consisting of n+1 qubits. The algorithm works as follows:
```mermaid
graph TD
    A["Initialize n qubits in |0> state"] --> B{Apply Hadamard gates to all qubits}
    B --> C[Perform oracle function U_f]
    C --> D{Apply Hadamard gates to all qubits}
    D --> E[Measure all qubits]
    E --> F{"If all qubits are in |0> state, f(x) is constant; otherwise, f(x) is balanced"}
```
1. Initialize the first n qubits in the |0⟩ state and the last qubit in the |1⟩ state.
2. Apply Hadamard gates to all n+1 qubits.
3. Apply the function f(x) to the first n qubits, controlled by the last qubit.
4. Apply Hadamard gates to the first n qubits.
5. Measure the first n qubits.
6. The output of the algorithm will be 0 if the function f(x) is constant, and 1 if the function f(x) is balanced.

The key insight behind the Deutsch-Jozsa algorithm is that the Hadamard gates create a superposition of all possible inputs to the function f(x), which allows the algorithm to evaluate the function in parallel for all possible inputs. The controlled application of the function f(x) ensures that the quantum state contains information about the balance of the function, which can be extracted by applying Hadamard gates and measuring the first n qubits.

The Deutsch-Jozsa algorithm is an important early example of a quantum algorithm that provides a speedup over classical algorithms, and helped to establish the field of quantum computing as an area of active research.

# Example
Suppose we have a black box function f(x) that takes in a 3-bit string x and returns either 0 or 1. We want to determine whether f(x) is a constant function that returns 0 for all inputs or a balanced function that returns 0 for half of the inputs and 1 for the other half of the inputs.

1. Prepare the state of the qubits

We start by preparing our input qubits. In this case, we need 4 qubits: 3 for the input to the black box function and 1 ancilla qubit. We initialize the input qubits to |000⟩ and the ancilla qubit to |1⟩.
```scss
|ψ⟩ = |0001⟩
```

2. Apply Hadamard Gates
Next, we apply Hadamard gates to the input qubits, putting them into a superposition of all possible states.
```scss
|ψ⟩ = (1/2)(|0001⟩ + |0011⟩ + |0101⟩ + |0111⟩ + |1000⟩ + |1010⟩ + |1100⟩ + |1110⟩)
```
3. Apply the Oracle
We apply the black box function to the input qubits using a quantum oracle. Since we don't know whether the function is constant or balanced, we use a general oracle that applies a phase flip to the state if the function outputs 1.

Suppose the black box function is balanced and takes the input |101⟩, then it outputs 1. To apply the oracle, we flip the phase of the |101⟩ state by applying a Z gate to the ancilla qubit.
```scss
|ψ⟩ = (1/2)(|0001⟩ + |0011⟩ + |0101⟩ + |0111⟩ - |1000⟩ - |1010⟩ - |1100⟩ - |1110⟩)
```
4. Apply Hadamard Gates
Next, we apply Hadamard gates to the input qubits again.
```scss
|ψ⟩ = (1/2)(|00⟩ - |01⟩ + |10⟩ - |11⟩)
```
5. Measure
Finally, we measure the input qubits. If the result is |00⟩, then the function is constant. If the result is any other state, then the function is balanced.

In this example, we get the state |01⟩ as a result, which means that the function is balanced.
