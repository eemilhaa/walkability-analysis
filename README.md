## walkability-analysis

Walkability sounds like a self-explanatory term: it measures how accessible an environment is by walking. However, the factors that walkability is composed of are hard to define. To say a place is walkable could for example mean that the network of streets is dense or that a wide selection of services can be accessed on foot. Other elements such as green space, air quality or the amount of traffic affect walkability too.

graphs are.....

1. OSMnx graphs 

2. Walkability based on intersection counts

3. Walkability based on network analysis



### 1. OSMnx and intersection counts

Also, when dealing with OSM data, one should keep in mind that some of the variance in data coverage and detail is just an inevitable by-product of the various mapping habits of OSM contributors.

![Graph overview](docs/graph_overview.png)

**2 simplifying graphs**

The resulting graph is very dense and has a ton of nodes. This can be problematic. For example, when two streets that have sidewalks cross eachother, one real-life intersecion can turn into 4 nodes. In contrast, 2 walkways crossing eachother would result in just one node. In this analysis I tried to model actual intersections only, which is why I chose to simplify the graph a bit. I dissolved all nodes within a 10m radius of eachother into single nodes and excluded all graph edges that are dead-ends. The result (picture 1) is far from perfect, but i think it represents the actual "real life" intersections better than the original graph.

![Graph comparison](docs/graph_comparison.png)

