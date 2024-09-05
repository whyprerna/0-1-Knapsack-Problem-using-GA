# Genetic Algorithm for 0/1 Knapsack Problem - Report

## Overview

This report details the implementation and results of a genetic algorithm designed to solve the 0/1 Knapsack problem. The goal of the algorithm is to maximize the total profit of selected items while adhering to the knapsack's capacity constraints. The genetic algorithm employs random mutation to introduce variability into the population.

## Problem Formulation

### Objective

Maximize the total profit by selecting items such that the total weight does not exceed the knapsack's capacity.

**Objective Function:**
\[ \text{Maximize} \quad \sum_{i} p_i \cdot x_i \]
where \( x_i \in \{0, 1\} \) represents whether item \( i \) is included (1) or not (0).

### Constraint

The total weight of the selected items must not exceed the knapsack's capacity.

**Constraint:**
\[ \sum_{i} w_i \cdot x_i \leq C \]
where \( C = 50 \) (capacity).

### Items Details

| Sl No | Object | Weight (wᵢ) | Profit (pᵢ) |
|-------|--------|-------------|-------------|
| 1     | a      | 11          | 22          |
| 2     | b      | 5           | 12          |
| 3     | c      | 7           | 18          |
| 4     | d      | 12          | 31          |
| 5     | e      | 21          | 39          |
| 6     | f      | 18          | 32          |

## Genetic Algorithm Approach

### Parameters

- **Population Size**: 50
- **Number of Generations**: 40
- **Mutation Rate**: 0.1
- **Maximum Perturbation (Δ)**: 1.0

### Functions

1. **Initialization**: Generates an initial population of solutions with binary encoding.

2. **Fitness Function**: Evaluates the quality of solutions considering both profit and weight constraints. The fitness function is defined as:
   \[
   \text{Fitness} = \sum_{i} p_i \cdot x_i + \text{min}\left(0, \text{penalty\_factor} \times (C - \sum_{i} w_i \cdot x_i)\right)
   \]
   where:
   - \( \sum_{i} p_i \cdot x_i \) is the total profit of the selected items.
   - \( \sum_{i} w_i \cdot x_i \) is the total weight of the selected items.
   - The penalty term \( \text{min}(0, \text{penalty\_factor} \times (C - \sum_{i} w_i \cdot x_i)) \) is added if the total weight exceeds the capacity, where the penalty factor is 1000.

3. **Selection**: Uses tournament selection to choose individuals for reproduction. The fitness scores of randomly selected individuals are compared, and the best individual among them is chosen.

4. **Crossover**: Applies single-point crossover to create offspring from selected parents. The crossover point is randomly chosen, and the offspring inherit segments from both parents.

5. **Random Mutation**: Modifies solutions by a random perturbation, calculated as:
   \[
   P_{\text{mutated}} = P_{\text{original}} + (r - 0.5) \times \Delta
   \]
   where:
   - \( P_{\text{original}} \) is the original solution value.
   - \( r \) is a random number between 0.0 and 1.0.
   - \( \Delta \) is the maximum perturbation (set to 1.0 in this case).

6. **Genetic Algorithm Execution**: Runs the genetic algorithm, evolving the population through selection, crossover, and mutation over several generations.

## Results

The algorithm outputs the best solution and its corresponding profit after the final generation. Additionally, trends of best and average fitness values over generations are plotted to show the algorithm's performance.


## Conclusion

The genetic algorithm effectively addresses the 0/1 Knapsack problem, optimizing for profit while respecting weight constraints. The use of random mutation helps maintain diversity within the population, potentially improving the quality of solutions.

