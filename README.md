# Graph building (Java)

Java examples for representing graphs as adjacency structures and traversing them. The repository mixes a **minimal teaching setup** (`basic-stage`) with a **richer graph type** at the project root aimed at nodes that carry a file or source suffix.

## Repository layout

| Path | Role |
|------|------|
| `basic-stage/src/Graph.java` | Adjacency list: `HashMap<String, LinkedList<String>>`, directed edges via `addEdge(node1, node2)`. |
| `basic-stage/src/Search.java` | Loads edges from `g.txt`, runs depth-first search from `A` to `B`, prints each path found. |
| `basic-stage/g.txt` | Sample graph: two tokens per line (`from to`). |
| `GraphBuildingBasic.java` | Minimal adjacency list (same idea as `basic-stage`’s `Graph`, `HashMap` + `LinkedList`). |
| `Graph.java` | Adjacency map with `LinkedHashSet` neighbors; supports nodes named `name@id` and logic to connect matching `name` across different `@id` values. |

## Requirements

- A Java Development Kit (JDK) 8 or newer.

## Basic stage: compile and run

`Search` reads `g.txt` from the **current working directory**, so run commands from `basic-stage`.

```bash
cd basic-stage
javac -d bin src/Graph.java src/Search.java
java -cp bin Search
```

The program uses `START = "A"` and `END = "B"` (see `Search.java`). Output is whitespace-separated node sequences, one line per path from `A` to `B`.

### `g.txt` format

Each line is two strings: source vertex and destination vertex. Example:

```text
A m1
m1 m2
m1 B
```

## Root `Graph.java` (nodes with `@`)

- **Edges**: `addEdge(node1, node2)` adds `node2` to `node1`’s adjacency set (one direction unless you add the reverse yourself).
- **Naming**: Several methods assume node keys contain `@` and split on it: the part before `@` is treated as a logical name (e.g. species), the part after as a disambiguator (e.g. file id).
- **`connectGraphs()`**: For every pair of distinct keys whose prefix (before `@`) matches case-insensitively, adds mutual adjacency so those variants are linked in the map.

`GraphBuildingBasic.java` is a stripped-down adjacency list without that naming or linking behavior.

## Notes

- There is no Maven or Gradle project; compile with `javac` as shown.
- Root-level `Graph.java` and `GraphBuildingBasic.java` are not wired to a `main` in this repo; use or extend them from your own entry point if needed.
