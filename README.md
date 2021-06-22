## urban-walkability

Walkability measures how accessible an environment is by walking. 
graphs are.....


### Intersection counts

graph from place

**2 simplifying graphs**

The resulting graph is very dense and has a ton of nodes. This can be problematic. For example, when two roads that have sidewalks cross eachother, one real-life intersecion can turn into 4 nodes. In contrast, 2 walkways crossing eachother would result in just one node. In this analysis I'm trying to model actual intersections only, which is why the graph needs some simplification. To simplify the graph, i dissolved all nodes within a 10m radius of eachother into single nodes.

![Graph comparison](docs/graph_comparison.png)