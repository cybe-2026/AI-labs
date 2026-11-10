# Lab 2

**Topic:** Uninformed Search Algorithms


## Task: Compare BFS and DFS


### Comparison Table

| Algorithm | Path Length | Maximum Frontier |
| :--- | :---: | :---: |
| **BFS** | 8 | 3 |
| **DFS** | 8 | 3 |

---
### Answers these Questions

**Q1.Which algorithm found the shorter path?**

**Ans:** BFS (Breadth-First Search) found the shorter path because it explores all nearby nodes level by level.

**Q2.Which algorithm had the larger maximum frontier?**

**Ans:** BFS usually had the larger maximum frontier because it stores multiple nodes at each level before exploring the next level.

**Q3.Why did the two algorithms produce different paths on the same maze?**

**Ans:** BFS explores nodes level by level, while DFS (Depth-First Search) explores one path as deeply as possible before backtracking. Therefore, they may find different routes.

**Q4.Does DFS always produce the shortest path? Why or why not?**

**Ans:** No. DFS does not always produce the shortest path because it follows one path deeply without checking whether a shorter route exists.

**Q5.Does BFS always produce the shortest path when every movement costs 1? Why?**

**Ans:** Yes,BFS always finds the shortest path when every movement has equal cost because it explores all paths in order of increasing distance from the starting point.


# Experiment 1 — Change the Neighbor Order.


### Code Cell

 ```python
directions = [
    (0, 1),   # right
    (1, 0),   # down
    (0, -1),  # left
    (-1, 0)   # up
]

dfs_path2, dfs_frontier2 = dfs(maze, start, goal)

print("DFS path (new order):", dfs_path2)
print("DFS path length:", len(dfs_path2) - 1)
print("DFS maximum frontier:", dfs_frontier2)

print()
print_maze(maze, dfs_path2)


# Reset directions to the original order
directions = [
    (-1, 0),   # up
    (1, 0),    # down
    (0, -1),   # left
    (0, 1)     # right
]
---
```
### Output
```text
DFS path (new order): [(0, 0), (1, 0), (2, 0), (2, 1), (2, 2), (3, 2), (3, 3), (3, 4), (4, 4)]
DFS path length: 8
DFS maximum frontier: 3
```
### Answers to the Questions

**Q1.Did the DFS path change?**

**Ans:** Yes, the DFS path changed because we changed the order of directions. Previously, DFS explored the upper route, but with the new order, it explored the lower route.

**Q2.Did BFS's path (Section 4) depend on this ordering the same way? Why or why not?**

**Ans:** BFS also uses the neighbor order when exploring positions. Its selected path can change when multiple shortest paths are available. However, BFS always finds a shortest path when every movement has an equal cost. In this experiment, we only ran DFS again, so the original BFS result remained unchanged.


# Experiment 2: Change Start and Goal

## Code Cell

 ```python

directions = [
    (-1, 0),   # up
    (1, 0),    # down
    (0, -1),   # left
    (0, 1)     # right
]

# Three different start and goal pairs
test_pairs = [
    ((0, 0), (2, 2)),
    ((0, 0), (2, 4)),
    ((4, 0), (0, 4))
]

# Run BFS and DFS for each pair
for number, (start, goal) in enumerate(test_pairs, start=1):

    print("Trial:", number)
    print("Start:", start)
    print("Goal:", goal)

    bfs_path, bfs_frontier = bfs(maze, start, goal)

    dfs_path, dfs_frontier = dfs(maze, start, goal)

    print("BFS path:", bfs_path)
    print("BFS path length:", len(bfs_path) - 1)
    print("BFS maximum frontier:", bfs_frontier)

    print("DFS path:", dfs_path)
    print("DFS path length:", len(dfs_path) - 1)
    print("DFS maximum frontier:", dfs_frontier)

    print("Same path:", bfs_path == dfs_path)

    print("--------------------------------")

# Reset original start and goal
start = (0, 0)
goal = (4, 4)
---
```
### Output
```text

Trial : 1
Start: (0, 0)
Goal: (2, 2)
BFS path: [(0, 0), (1, 0), (2, 0), (2, 1), (2, 2)]
BFS path length: 4
BFS maximum frontier: 3
DFS path: [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 4), (2, 4), (3, 4), (3, 3), (3, 2), (2, 2)]
DFS path length: 10
DFS maximum frontier: 3
Same path: False
--------------------------------
Trial: 2
Start: (0, 0)
Goal: (2, 4)
BFS path: [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 4), (2, 4)]
BFS path length: 6
BFS maximum frontier: 3
DFS path: [(0, 0), (0, 1), (0, 2), (0, 3), (0, 4), (1, 4), (2, 4)]
DFS path length: 6
DFS maximum frontier: 2
Same path: True
--------------------------------
Trial: 3
Start: (4, 0)
Goal: (0, 4)
BFS path: [(4, 0), (3, 0), (2, 0), (1, 0), (0, 0), (0, 1), (0, 2), (0, 3), (0, 4)]
BFS path length: 8
BFS maximum frontier: 3
DFS path: [(4, 0), (3, 0), (2, 0), (2, 1), (2, 2), (3, 2), (3, 3), (3, 4), (2, 4), (1, 4), (0, 4)]
DFS path length: 10
DFS maximum frontier: 3
Same path: False
--------------------------------
```
# Comparison Table


| Start | Goal | BFS Length | BFS Max Frontier | DFS Length | DFS Max Frontier |
| :--- | :--- | :---: | :---: | :---: | :---: |
| (0, 0) | (2, 2) | 4 | 3 | 10 | 3 |
| (0, 0) | (2, 4) | 6 | 3 | 6 | 2 |
| (4, 0) | (0, 4) | 8 | 3 | 10 | 3 |

# Answers these Questions.

**Q6: Does BFS's path length ever change if you re-run it with the same start/goal? Does DFS's?**

**Ans:** No, both algorithms produce the same path length when the maze, start, goal, and neighbor order remain unchanged. However, DFS may produce a different path length if the neighbor order changes.

**Q7. As the distance between start and goal grows, what happens to the maximum frontier size for each algorithm?**

**Ans:** The maximum frontier size does not always increase with distance. It depends on the maze structure and the available paths. In our experiment, BFS's maximum frontier remained 3, while DFS's maximum frontier was 3, 2, and 3.

**Q8. Can you find a (start, goal) pair where BFS and DFS return the same path? What does that tell you about the maze structure between those two points?**

**Ans:** Yes. For start (0, 0) and goal (2, 4), both algorithms found the same path. This shows that DFS explored the direct shortest route first. The maze has a clear open route between these points, although other longer routes may also exist.

**Q9. What happens if the goal is unreachable from the start?**

**Ans:** When the goal is unreachable, both BFS and DFS return None because they cannot find a path. They continue exploring all reachable positions until no positions remain in the frontier.



