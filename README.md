# The Torchbearer

**Student Name:** Charlie Pham
**Student ID:** 828249377
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
  It is not enough because even though it computes shortest distances from S, it does not tell us the order in which the relics should be visited.

- **What decision remains after all inter-location costs are known:**
  The decision that remains is determining the optimal order of travel between the relics.

- **Why this requires a search over orders (one sentence):**
  There are many different orders, with differing costs, so one calculation could not compare all the possibilities.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| spawn node | The path begins at the spawn node, so we find the shortest costs from it. |
| relic nodes | After each relic, the path may continue to another relic or to the exit. |

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | nested dictionary |
| What the keys represent | First keys are source nodes, second keys are destination nodes |
| What the values represent | The shortest distance from the source node to the destination node. |
| Lookup time complexity | O(1) |
| Why O(1) lookup is possible | Dictionaries allow direct access to values using keys. |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** k + 1
- **Cost per run:** O(m log n)
- **Total complexity:**
(k + 1) * O(m log n)
= O((k + 1)m log n)
= O(km log n)
- **Justification (one line):** Dijkstra runs once from the spawn node and once from each relic node.

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  Once a node is finalized, its shortest distance cannot become any smaller later.

- **For nodes not yet finalized (not in S):**
  Their current distances are the best known distances so far, but shorter distances can be found later.

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  Initially, only the source node has a known shortest distance of 0, while all the other nodes are unreachable with infinity.

- **Maintenance : why finalizing the min-dist node is always correct:**
  Nonnegative edge weights guarantee that a finalized min-dist node is always correct because any future paths can only increase the total cost, and not decrease it.

- **Termination : what the invariant guarantees when the algorithm ends:**
  When the algorithm ends, all reachable nodes have been finalized, so their shortest distances have been found.

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

The precomputed shortest distances have to be correct so that the planner can choose the optimal route and compute accurate total costs.

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** Greedy only looks at the best/cheapest immediate move, but does not consider how that cchoice may consider future total cost.
- **Counter-example setup:** Suppose S -> B = 1, S -> C = 2, B -> C = 100, C -> B = 1, both B and C connect to T with a cost of 1.
- **What greedy picks:** Greedy would pick B first since it is the shortest distance relic from S.
- **What optimal picks:** Optimal would pick C first, then B, then exit to T.
- **Why greedy loses:** Greedy loses because it picks the best immediate choice, B, but that causes it to take an expensive route from B to C, costing 100.

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- The algorithm must explore the different orders of visiting relics since the total route will ultimately depend on the path order.

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
