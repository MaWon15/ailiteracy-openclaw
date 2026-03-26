# Week 2 Lecture Notes: Search Algorithms and Problem Solving

## Problem-Solving Agents

Problem-solving agents use **search algorithms** to find sequences of actions that achieve goals.

### Components
- **Problem Definition**: Initial state, actions, goal test, path cost
- **Search Algorithm**: Systematic exploration of state space
- **Solution**: Sequence of actions from initial to goal state

## Search Strategies

### Uninformed (Blind) Search
- **Breadth-First Search (BFS)**: Explores all nodes at current depth before going deeper
  - Complete: Yes (for finite spaces)
  - Optimal: Yes (if all actions cost 1)
  - Time/Space: O(b^d)

- **Depth-First Search (DFS)**: Explores one branch completely before backtracking
  - Complete: No (infinite spaces)
  - Optimal: No
  - Time/Space: O(bm) worst case

- **Uniform Cost Search**: Expands lowest path cost first
  - Complete: Yes
  - Optimal: Yes
  - Time/Space: Depends on cost range

### Informed (Heuristic) Search
- **Greedy Best-First Search**: Expands node with lowest heuristic value
  - Complete: No
  - Optimal: No
  - Fast but suboptimal

- **A* Search**: Combines path cost + heuristic
  - Complete: Yes (admissible heuristic)
  - Optimal: Yes (admissible + consistent heuristic)
  - Time/Space: Exponential but often efficient

## Heuristics

### Admissible Heuristics
- Never overestimate true cost to goal
- Guarantees optimality in A* search

### Consistent Heuristics
- h(n) ≤ c(n,n') + h(n') for all neighbors n'
- Guarantees that first solution found is optimal

### Examples
- **8-puzzle**: Manhattan distance, misplaced tiles
- **Route finding**: Straight-line distance
- **Sliding puzzles**: Pattern databases

## Search in Practice

### Real-World Considerations
- **Time constraints**: Need fast, approximate solutions
- **Memory limitations**: Can't store entire search tree
- **Inadmissible heuristics**: Trade optimality for speed
- **Learning heuristics**: Improve performance over time

### Applications
- **Pathfinding**: GPS navigation, robotics
- **Game playing**: Chess, Go, strategy games
- **Planning**: Automated planning systems
- **Optimization**: Resource allocation, scheduling

## Discussion Questions

1. When should you use uninformed vs informed search?
2. How do you design good heuristics?
3. What are the trade-offs between optimality and efficiency?
4. How do real-world constraints affect algorithm choice?

## Key Takeaways

- Search algorithms systematically explore solution spaces
- Different problems require different search strategies
- Heuristics can dramatically improve performance
- Understanding algorithm properties helps choose the right tool
- Real-world search often involves approximations and learning