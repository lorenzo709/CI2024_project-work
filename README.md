I WORKED WITH ALESSANDRO CARLONE s326994

Link to his project: https://github.com/AlesCarl/CI2024_project-work

### Introduction

The provided code implements a **genetic programming algorithm**, a technique inspired by biological evolution, to generate mathematical expressions that closely approximate a given dataset. By using **tree structures** to represent expressions, the algorithm iterates through generations of potential solutions, refining them through the use of **mutation, crossover, and selection** mechanisms. The goal is to evolve increasingly accurate mathematical models that fit the input data.

## Key components

### **Tree Representation**

The core of the genetic programming approach lies in its tree-based structure:

- Each tree is composed of `Node` objects.
- Nodes may represent **unary functions** (e.g., `sin`, `cos`, `log`) or **binary functions** (e.g., `add`, `subtract`, `multiply`).
- Terminal nodes include both **variables** (`x0, x1, x2, ...`) and **constants** (ranging from -9 to 9).
- Evaluation of a tree is performed recursively using NumPy operations, with special handling to prevent errors such as **division by zero** and **logarithms of non-positive numbers**.

### **Population Initialization**

A diverse initial population is crucial for effective evolution. Two different methods are used:

- **Full Method**: Generates trees of a fixed maximum depth, ensuring all branches reach the same depth.
- **Grow Method**: Produces trees with varying depths, leading to more structural variety in the initial population.

This mixture of approaches helps maintain **genetic diversity** in the population and allows the algorithm to explore a wide range of potential solutions.

### **Genetic Operators**

To evolve the population, the algorithm applies several genetic operators:

- **Mutation**:
    - `point_mutation`: Randomly replaces function nodes with other functions of the same type.
    - `subtree_mutation`: Replaces entire subtrees with new randomly generated subtrees.
- **Crossover**:
    - `crossover`: Swaps subtrees between two parent trees to generate offspring with mixed characteristics.
- **Selection**:
    - `tournament_selection`: Chooses the best individual from a random subset of the population, ensuring that stronger candidates have a higher probability of reproducing.

### **Fitness Evaluation**

The quality of each tree is measured using a **fitness function**, which calculates:

- **Mean Squared Error (MSE)**: Measures how closely the tree's predictions match `y_data`.
- **Depth Penalty**: Introduced to discourage overly complex trees, which could lead to overfitting.

The balance between accuracy and simplicity ensures that the algorithm generates expressive yet manageable expressions.

## Evolutionary Process

The genetic programming algorithm progresses through **multiple generations**:

- **Population Size**: 20,000 trees are maintained per generation, providing a large search space.
- **Generations**: The process runs for **50 iterations**, continuously refining solutions.
- **Elitism**: The best individuals from each generation are carried over to the next, ensuring that the highest-quality expressions persist.
- **Mutation and Crossover Rates**: A **mutation rate of 70%** introduces significant variation, while crossover helps recombine useful traits.

Each generation undergoes rigorous evaluation, and the best-performing solution is reported at each step.

**5. Performance Considerations** While the algorithm is designed to explore a vast space of potential expressions, computational efficiency remains a concern. Some key considerations include:

- **Computational Cost**: Evaluating large populations can be time-consuming, suggesting potential benefits from parallel processing.
- **Depth Control**: The depth penalty helps prevent trees from growing too large, which can slow evaluation.
- **Mutation Strategy**: A **high mutation rate** encourages exploration but may hinder convergence in some cases.
