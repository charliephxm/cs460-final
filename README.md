# The Torchbearer

**Student Name:** Charlie Pham
**Student ID:** 828249377
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  It is not enough because even though it computes shortest distances from S, it does not tell us the order in which the relics should be visited.

- **What decision remains after all inter-location costs are known:**
  The decision that remains is determining the optimal order of travel between the relics.

- **Why this requires a search over orders (one sentence):**
  There are many different orders, with differing costs, so one calculation could not compare all the possibilities.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| spawn node | The path begins at the spawn node, so we find the shortest costs from it. |
| relic nodes | After each relic, the path may continue to another relic or to the exit. |

### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name | nested dictionary |
| What the keys represent | First keys are source nodes, second keys are destination nodes |
| What the values represent | The shortest distance from the source node to the destination node. |
| Lookup time complexity | O(1) |
| Why O(1) lookup is possible | Dictionaries allow direct access to values using keys. |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** k + 1
- **Cost per run:** O(m log n)
- **Total complexity:**
(k + 1) * O(m log n)
= O((k + 1)m log n)
= O(km log n)
- **Justification (one line):** Dijkstra runs once from the spawn node and once from each relic node.

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  Once a node is finalized, its shortest distance cannot become any smaller later.

- **For nodes not yet finalized (not in S):**
  Their current distances are the best known distances so far, but shorter distances can be found later.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
  Initially, only the source node has a known shortest distance of 0, while all the other nodes are unreachable with infinity.

- **Maintenance : why finalizing the min-dist node is always correct:**
  Nonnegative edge weights guarantee that a finalized min-dist node is always correct because any future paths can only increase the total cost, and not decrease it.

- **Termination : what the invariant guarantees when the algorithm ends:**
  When the algorithm ends, all reachable nodes have been finalized, so their shortest distances have been found.

### Part 3c: Why This Matters for the Route Planner

The precomputed shortest distances have to be correct so that the planner can choose the optimal route and compute accurate total costs.

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** Greedy only looks at the best/cheapest immediate move, but does not consider how that choice may consider future total cost.
- **Counter-example setup:** Suppose S -> B = 1, S -> C = 2, B -> C = 100, C -> B = 1, both B and C connect to T with a cost of 1.
- **What greedy picks:** Greedy would pick B first since it is the shortest distance relic from S.
- **What optimal picks:** Optimal would pick C first, then B, then exit to T.
- **Why greedy loses:** Greedy loses because it picks the best immediate choice, B, but that causes it to take an expensive route from B to C, costing 100.

### What the Algorithm Must Explore

- The algorithm must explore the different orders of visiting relics since the total route will ultimately depend on the path order.

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | Node where search currently is |
| Relics already collected | relics_visited_order | list | Relics collected so far, in the order they're visited in |
| Fuel cost so far | cost_so_far | float | Total fuel used by the current partial route |

### Part 5b: Data Structure for Visited Relics

| Property | Your answer |
|---|---|
| Data structure chosen | set |
| Operation: check if relic already collected | Time complexity: O(1) avg |
| Operation: mark a relic as collected | Time complexity: O(1) avg |
| Operation: unmark a relic (backtrack) | Time complexity: O(1) avg |
| Why this structure fits | Sets allows for fast membership checks and fast adding and removing operations during backtracking |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** k!
- **Why:** In worst case, the algorithm may need to try every possible order of the k relics.

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** Best is tracking the lowest fuel cost path and its respective relic travel order.
- **When it is used:** It is used when a complete route is found, to compare to decide whether to update the best path, and during recursion, to stop branches that already cost more than the best path.
- **What it allows the algorithm to skip:** It allows the algorithm to skip paths that are already more expensive than the shortest cost found so far.

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** At the current state, the algorithm currently knows the current location, the relics already collected, the fuel cost so far, and the relics that still remain.
- **What the lower bound accounts for:** It accounts for the fuel already spent in the current partial route.
- **Why it never overestimates:** Because all remaining edge weights are nonnegative, the total end cost will never be less than the cost so far.

### Part 6c: Pruning Correctness

- If the cost so far is already at least the best complete path cost, the branch is safe to prune since all future travel costs are nonnegative and can't make the route any cheaper.

---

## References

- Lecture notes only
