---
layout: default
title: dag
nav_order: 5
parent: Standard library
aux_links:
  "Library directory": "https://github.com/graphology/graphology/tree/master/src/dag"
  "Changelog": "https://github.com/graphology/graphology/tree/master/src/dag/CHANGELOG.md"
---

# Graphology DAG

Functions related to Directed Acyclic Graphs (DAGs) and to be used with [`graphology`](..).

## Installation

```
npm install graphology-dag
```

## Usage

- [hasCycle](#hascycle)
- [willCreateCycle](#willcreatecycle)
- [topologicalSort](#topologicalsort)
- [forEachNodeInTopologicalOrder](#foreachnodeintopologicalorder)

### hasCycle

Function returning whether the given directed graph contains at least one cycle.

Note that this function will also work with a disconnected graph.

```js
import {hasCycle} from 'graphology-dag';
// Alternatively, to load only the relevant code:
import hasCycle from 'graphology-dag/has-cycle';

const graph = new DirectedGraph();
graph.mergeEdge(0, 1);
graph.mergeEdge(1, 2);
graph.mergeEdge(2, 3);

hasCycle(graph);
>>> false

graph.mergeEdge(3, 0);

hasCycle(graph);
>>> true
```

### willCreateCycle

Function returning whether adding the given directed edge to a DAG will create an undesired cycle.

Note that this function expects a valid DAG and even if passing a cyclic graph could work it could also very well lead to undefined behavior ranging from an infinite loop to overkill memory usage.

Note finally that this function will also work with DAG forests (sets of disconnected DAGs living in the same graph instance).

```js
import {willCreateCycle} from 'graphology-dag';
// Alternatively, to load only the relevant code:
import willCreateCycle from 'graphology-dag/will-create-cycle';

const graph = new DirectedGraph();
graph.mergeEdge(0, 1);
graph.mergeEdge(1, 2);
graph.mergeEdge(2, 3);

willCreateCycle(graph, 3, 0);
>>> true
willCreateCycle(graph, 0, 2);
>>> false
```

### topologicalSort

Function returning an array of nodes representing a possible topological ordering of the given DAG.

Note that this function will throw if given graph has any cycle, is able to work on mixed graphs containing only directed edges and can work on disconnected graphs (a DAG forest).

```js
import {topologicalSort} from 'graphology-dag';
// Alternatively, to load only the relevant code:
import {topologicalSort} from 'graphology-dag/topological-sort';

const graph = new DirectedGraph();
graph.mergeEdge(0, 1);
graph.mergeEdge(1, 2);
graph.mergeEdge(2, 3);

topologicalSort(graph)
>>> ['0', '1', '2', '3'];
```

### forEachNodeInTopologicalOrder

Function iterating over the given DAG's nodes in topological order using a callback function.

Note that this function will throw if given graph has any cycle, is able to work on mixed graphs containing only directed edges and can work on disconnected graphs (a DAG forest).

```js
import {forEachNodeInTopologicalOrder} from 'graphology-dag';
// Alternatively, to load only the relevant code:
import {forEachNodeInTopologicalOrder} from 'graphology-dag/topological-sort';

const graph = new DirectedGraph();
graph.mergeEdge(0, 1);
graph.mergeEdge(1, 2);
graph.mergeEdge(2, 3);

forEachNodeInTopologicalOrder(graph, (node, attr) => {
  console.log(node, attr);
});
```

