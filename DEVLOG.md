# Development Log – The Torchbearer

**Student Name:** Charlie Pham
**Student ID:** 828249377

---

## Entry 1 – [5/9/2026]: Initial Plan

I plan to first implement Dijkstra's algorithm so that I can compute the shortest paths between important nodes. After, I will precompute and store distances before implementing recursive backtracking search. I think that the hardest part for me will be backtracking since it has recursion, pruning, and state management. To test my code, I will be using the tests at the bottom of torchbearer.py and debug any cases that fail step by step.

---

## Entry 2 – [5/9/2026]: Implemented Dijkstra and Precomputation

Today I implemented the Dijkstra algorithm, source selection, and the precomputed distance table. At first, I incorrectly thought that all distances should start at 0, but I realized that would incorrectly assume that every node was already reachable with a zero cost. I saw the "Unreachable nodes map to float('inf')." note and initialized all distances to float('inf') except for the source node, which starts at 0. I also learned how stale heap entries work and why they need to be skipped during Dijkstra's processing. I completed the README sections for Parts 1 and 2 and the implementations.

---

## Entry 3 – [5/9/2026]: Correctness and Search Design

Today I completed the README sections for Parts 3 and 4. I worked through the Dijkstra invariant and why nonnegative edge weights guarantee correctness when nodes are finalized. I also analyzed why a greedy strategy might fail for the relic problem and why the algorithm needs to explore different visiting orders instead of only choosing the best next relic.

---

## Entry 4 – [5/10/2026]: [State and Search Space and Pruning]

Today I implemented and completed parts 5 and 6. I worked on the recursive state representation using the current location, remaining relics, relic visiting order, and total fuel cost so far. I also implemented pruning using the best route found so far and learned how backtracking restores the state after exploring each recursive branch.

---

## Entry 5 – [5/10/2026]: Post-Implementation Reflection

After finishing my implementation, I think that the one thing that I would improve on given more time is the pruning strategy. As of now, the pruning only compares the current cost to the best complete route found so far, but stronger lower bound estimates could reduce the number of recursive branches explored. I would also improve on the readability of the recursive search by separating some of the logic into smaller helper functions.

---

## Final Entry – [5/10/2026]: Time Estimate

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 5 |
| Part 2: Precomputation Design | 80 |
| Part 3: Algorithm Correctness | 5 |
| Part 4: Search Design | 5 |
| Part 5: State and Search Space | 30 |
| Part 6: Pruning | 45 |
| Part 7: Implementation | 30 |
| README and DEVLOG writing | 200 |
| **Total** | 400 |
