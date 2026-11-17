# CS453 AI Project - Library Retrieval Agent

**Student:** AYA HAMAD SHALLOUF, ID 09221024
**GitHub username:** m09221024-ai
**Project choice:** Library Retrieval
**Assigned variant:** variant 0 - start S, target shelf zone G, removed road A-D

## Open the notebook
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/m09221024-ai/09221024/blob/master/project.ipynb)

## Task and scope
A library retrieval agent starts at S on a map of 8 locations (S, A-G) connected
by unit-cost roads. It must reach the assigned shelf zone G and retrieve one
requested item. The state is (location, has_item). Retrieval is legal only at G
and only while the item is not yet held; moves cost 1 and RETRIEVE adds no
travel cost.
Scope limits: a small fixed map, one agent and one item, and no physical details
such as shelf height, grasping or book availability.

## Files and environment
- `project.ipynb`: agent simulator, BFS, A*, assigned mission outputs and explanations.
- `README.md`: overview and run instructions.

Python 3 / Colab CPU (Python 3.13.18 was printed in the notebook). Only Python's
standard library is used (`collections.deque`, `heapq`, `copy`, `itertools`).

## Run steps
1. Open `project.ipynb` in Colab using authorized GitHub access, or download it
   and use Colab's Upload tab.
2. No file uploads are needed: the graph and heuristic table are defined in code.
3. Restart the session and run all cells in order. Inspect the BFS and A*
   assigned mission outputs.

## Progress
| Milestone | Date | Commit link | Evidence |
|---|---|---|---|
| Setup | Nov 17, 2026 | [cf93678](https://github.com/m09221024-ai/09221024/commit/cf93678) | Name, ID, project and variant 0 recorded |
| Simulator, BFS, A*, disclosure | Nov 17, 2026 | [068d4a9](https://github.com/m09221024-ai/09221024/commit/068d4a9) | Legal actions, BFS and A* route S-B-E-G + RETRIEVE (3 moves) |

The final commit link is submitted in Classroom.

## Search methods
**BFS (uninformed)** uses a FIFO queue, so it explores the states 1 action away,
then 2, and so on. It uses no estimate of the distance to the goal. A `parent`
dictionary prevents repeated states and rebuilds the route. With unit costs, the
first goal found has the fewest moves. Assigned mission: S -> B -> E -> G, then
RETRIEVE (3 moves); it expanded 7 states.

**A\* (informed)** orders a priority queue by f(n) = g(n) + h(n), where g is the
real cost so far and h is the supplied heuristic for my target G (0 once the item
is held). `best_cost` keeps the cheapest known cost per state, and the goal is
tested when a state is removed from the queue. The supplied h values are
shortest distances in the original graph. My variant removes road A-D, and
removing a road can never shorten a route, so h never overestimates the real
cost (for example h(A) = 2 but the real cost is now 3). I checked h <= real cost
for every node in the notebook. Assigned mission: the same route and cost 3,
with 5 expanded states.

## Sources and assistance
The graph, `make_variant` and the `HEURISTICS` table are supplied by the
workbook. I used the course notebooks `graph-search` and `informed-search` for
the ideas behind BFS and A*. I used Claude (Anthropic) to explain the assignment
and the concepts, suggest and correct code, and review my results. I ran all
cells and checked the results myself. Details are in Task 10 of the notebook.
