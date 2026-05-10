# Development Log – The Torchbearer

**Student Name:** Charlie Pham
**Student ID:** 828249377

> Instructions: Write at least four dated entries. Required entry types are marked below.
> Two to five sentences per entry is sufficient. Write entries as you go, not all in one
> sitting. Graders check that entries reflect genuine work across multiple sessions.
> Delete all blockquotes before submitting.

---

## Entry 1 – [5/9/2026]: Initial Plan

> Required. Write this before writing any code. Describe your plan: what you will
> implement first, what parts you expect to be difficult, and how you plan to test.

I plan to first implement Dijkstra's algorithm so that I can compute the shortest paths between important nodes. After, I will precompute and store distances before implementing recursive backtracking search. I think that the hardest part for me will be backtracking since it has recursion, pruning, and state management. To test my code, I will be using the tests at the bottom of torchbearer.py and debug any cases that fail step by step.

---

## Entry 2 – [5/9/2026]: Implemented Dijkstra and Precomputation

> Required. At least one entry must describe a bug, wrong assumption, or design change
> you encountered. Describe what went wrong and how you resolved it.

Today I implemented the Dijkstra algorithm, source selection, and the precomputed distance table. At first, I incorrectly thought that all distances should start at 0, but I realized that would incorrectly assume that every node was already reachable with a zero cost. I saw the "Unreachable nodes map to float('inf')." note and initialized all distances to float('inf') except for the source node, which starts at 0. I also learned how stale heap entries work and why they need to be skipped during Dijkstra's processing. I completed the README sections for Parts 1 and 2 and the implementations.

---

## Entry 3 – [5/9/2026]: Correctness and Search Design

Today I completed the README sections for Parts 3 and 4. I worked through the Dijkstra invariant and why nonnegative edge weights guarantee correctness when nodes are finalized. I also analyzed why a greedy strategy might fail for the relic problem and why the algorithm needs to explore different visiting orders instead of only choosing the best next relic.

---

## Entry 4 – [Date]: [Description]

_Your entry here._

---

## Entry 5 – [Date]: Post-Implementation Reflection

> Required. Written after your implementation is complete. Describe what you would
> change or improve given more time.

_Your entry here._

---

## Final Entry – [Date]: Time Estimate

> Required. Estimate minutes spent per part. Honesty is expected; accuracy is not graded.

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 0.25 |
| Part 2: Precomputation Design | 2 |
| Part 3: Algorithm Correctness | 0.25 |
| Part 4: Search Design | 0.33 |
| Part 5: State and Search Space |  |
| Part 6: Pruning |  |
| Part 7: Implementation |  |
| README and DEVLOG writing |  |
| **Total** |  |
