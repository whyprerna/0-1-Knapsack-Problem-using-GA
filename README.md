# Genetic Algorithm for 0/1 Knapsack Problem 

## Overview

This report details the implementation of a genetic algorithm designed to solve the 0/1 Knapsack problem. The objective is to maximize the total profit of selected items while ensuring that the total weight does not exceed the knapsack's capacity. The genetic algorithm utilizes random mutation to introduce variability and explore different solutions.


### Objective

Maximize the total profit of selected items such that the total weight does not exceed the knapsack's capacity.

**Objective Function:**

Maximize: Σ (p_i * x_i)

where:
- p_i is the profit of item i.
- x_i is a binary variable indicating whether item i is included (1) or not (0).

### Constraint

The total weight of selected items must not exceed the knapsack's capacity.

**Constraint:**

Σ (w_i * x_i) ≤ C

where:
- w_i is the weight of item i.
- c = 50 is the maximum capacity of the knapsack.

### Items Details

| Sl No | Object | Weight (\( w_i \)) | Profit (\( p_i \)) |
|-------|--------|---------------------|--------------------|
| 1     | a      | 11                  | 22                 |
| 2     | b      | 5                   | 12                 |
| 3     | c      | 7                   | 18                 |
| 4     | d      | 12                  | 31                 |
| 5     | e      | 21                  | 39                 |
| 6     | f      | 18                  | 32                 |

## Genetic Algorithm Approach

### Parameters

- **Population Size**: 50
- **Number of Generations**: 40
- **Mutation Rate**: 0.1
- **Maximum Perturbation (\( \Delta \))**: 1.0

### Functions

1. **Initialization**

   Generates an initial population of solutions where each solution is represented as a binary vector indicating the inclusion of items.

2. **Fitness Function**

   Evaluates the quality of each solution considering both profit and weight constraints.

   **Fitness Function:**

   Fitness = Σ (p_i * x_i) + min(0, penalty_factor * (C - Σ (w_i * x_i)))

   penalty_factor=1000


   where:
   - Σ (p_i * x_i) is the total profit of the selected items.
   - Σ (w_i * x_i) is the total weight of the selected items.
   - The penalty term is added if the total weight exceeds the capacity, with the penalty factor set to 1000.

3. **Selection**

   Uses tournament selection to choose individuals for reproduction. A subset of the population is randomly selected, and the individual with the highest fitness within this subset is chosen.

4. **Mating Pool**
   The mating pool is created by selecting a subset of the population based on fitness probabilities. Each individual in the mating pool is chosen proportionally to their fitness score. This pool is used to        generate new offspring through crossover and mutation.
   
6. **Crossover**

   Applies single-point crossover to generate offspring. A crossover point is randomly chosen, and the offspring inherit segments from both parents.

   **Crossover Operation:**
   child1 = parent1[:crossover_point] + parent2[crossover_point:]
   child2 = parent2[:crossover_point] + parent1[crossover_point:]

7. **Random Mutation**

   Introduces random changes to individuals to maintain genetic diversity. The mutation is performed as follows:

   **Mutation Formula:**

   P_mutated = P_original + (r - 0.5) × Δ

   where:
   - P_original is the original value.
   - r is a random number between 0.0 and 1.0.
   - Δ is the maximum perturbation (set to 1.0 in this case).

8. **Genetic Algorithm Execution**

   Executes the genetic algorithm by evolving the population through selection, crossover, and mutation over several generations. 

   - The best individual from the current generation is carried forward to the next generation to ensure the best solution is not lost.

## Results

The algorithm outputs the best solution and its corresponding profit after the final generation. Additionally, trends of the best and average fitness values over generations are plotted to demonstrate the algorithm’s performance. The graphs in the code visualize the genetic algorithm's performance: one shows the best fitness score per generation, indicating how the optimal solution improves over time, while the other depicts the average fitness score, reflecting the overall population performance and convergence trends.


## Conclusion

The genetic algorithm effectively addresses the 0/1 Knapsack problem by using a structured approach that involves initializing a population of binary solutions, evaluating fitness based on profit and weight constraints, and iteratively refining solutions through selection, crossover, and random mutation. The algorithm ensures the preservation of high-quality solutions through elitism and explores diverse solutions across generations. The results demonstrate the algorithm's ability to optimize the total profit while respecting the knapsack's capacity constraints, highlighting its effectiveness in solving complex optimization problems through evolutionary techniques.

