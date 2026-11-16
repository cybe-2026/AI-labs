# Lab 4: Hill-Climbing Search with the N-Queens Problem

## Answer these questions.

**Q1: What is the purpose of the evaluation function in Hill-Climbing?**

**Ans:** The evaluation function measures the quality or 'goodness' of a state. It acts as a heuristic guide that tells the search algorithm which states are closer to the goal, allowing it to make local greedy decisions to move towards better states.

**Q2: Why is an evaluation score of zero the best result in our N-Queens implementation?**

**Ans:** Our evaluation function is defined as -count_conflicts(state). Since the N-Queens objective is to have zero conflicts (no two queens threatening each other) and conflicts cannot be negative, the maximum possible value of -count_conflicts(state) is 0, indicating a perfect, conflict-free board state.

**Q3: What is the difference between a local maximum and a global maximum?**

**Ans:** Local Maximum: A state that is better than all of its immediate neighbors, but is not the best possible overall state.
Global Maximum: The absolute best state possible across the entire state space (in our case, any state with an evaluation score of 0).

**Q4: Why can basic Hill-Climbing stop without finding a solution even when a solution exists?**

**Ans:** Basic Hill-Climbing is a greedy local search algorithm that only moves to a neighbor if that neighbor has a strictly higher evaluation score. If it reaches a local maximum where no neighbor is better than the current state, the search terminates because it cannot escape without taking a downhill step.

**Q5: Does reaching a local maximum always mean that the algorithm has failed? Explain.**

**Ans:** Yes, in the context of finding a perfect solution to the constraint satisfaction problem (N-Queens), reaching a local maximum with an evaluation score  <0  is a failure because the state still contains conflicts.

**Q6: For N = 8, how many neighbors does each state have in our implementation?**

**Ans** For an  N -Queens board where each queen is placed in a unique column, each queen (out of  N ) can be moved to any of the other  N−1  rows in its column. For  N=8 :
Neighbors=N×(N−1)=8×7=56 neighbors 

**Q7: What does the evaluation-score graph tell you about the behavior of Hill-Climbing?**

The graph shows that Hill-Climbing makes rapid progress initially, with the evaluation score increasing sharply in the first few iterations. However, it quickly flattens out and terminates within very few steps once it hits a local or global maximum, showing how short-sighted greedy local search is.

**Q8: Explain probabilistic completeness in your own words.**

Probabilistic completeness means that if a solution exists, the probability that the algorithm will find it approaches 100% (or 1) as the number of independent random attempts (restarts) or run time approaches infinity.

**Q9: Why does Random-Restart Hill-Climbing improve the chance of finding a solution?**

**Ans** Because basic Hill-Climbing is highly dependent on the random starting point. By resetting the algorithm with a new random starting state when it gets stuck, it explores entirely different areas of the search space, giving it multiple independent trials to find a basin of attraction that leads to the global maximum.

**Q10: Does probabilistic completeness guarantee that a solution will be found within 100 restarts? Why or why not?**
 
 **Ans:** No, it does not guarantee a solution within any finite boundary like 100 restarts Probabilistic completeness is an asymptotic guarantee (as restarts k -> infinity). For any finite k, there is always a non-zero probability that all k independent runs will end in local maxima.

## Extension Task

Modify the experiment to solve the N-Queens problem for N = 20.

Record the following:

* Number of conflicts in the final state.
* Number of iterations in a basic Hill-Climbing run.
* Number of restarts required by Random-Restart Hill-Climbing.
* Whether a valid solution was found.

---

 **1.Basic Hill-Climbing for N = 20**
 ### Code Cell

```python
state_basic, scores_basic = hill_climbing(20)
conflicts_basic = count_conflicts(state_basic)
print("--- Basic Hill-Climbing ---")
print(f"Final state: {state_basic}")
print(f"Number of conflicts in the final state: {conflicts_basic}")
print(f"Number of iterations: {len(scores_basic)}")
print(f"Valid solution found: {conflicts_basic == 0}\n")
```
 **2.Random-Restart Hill-Climbing for N = 20**
  ### Code Cell
```python

state_restart, restarts_needed, best_scores_restart = random_restart_hill_climbing(20, max_restarts=500)
conflicts_restart = count_conflicts(state_restart)
print("--- Random-Restart Hill-Climbing ---")
print(f"Final state: {state_restart}")
print(f"Number of conflicts in the final state: {conflicts_restart}")
print(f"Number of restarts required: {restarts_needed}")
print(f"Valid solution found: {conflicts_restart == 0}")
```
###  output

```python

N = 20 Extension Experiment ===

--- Basic Hill-Climbing ---
Final state: [1, 8, 15, 2, 18, 16, 4, 9, 12, 5, 3, 17, 0, 10, 19, 9, 11, 13, 7, 19]
Number of conflicts in the final state: 3
Number of iterations: 9
Valid solution found: False

--- Random-Restart Hill-Climbing ---
Final state: [9, 4, 15, 7, 10, 16, 13, 5, 0, 17, 3, 11, 6, 12, 19, 1, 18, 14, 2, 8]
Number of conflicts in the final state: 0
Number of restarts required: 67
Valid solution found: True

```
