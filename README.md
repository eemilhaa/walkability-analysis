## Analysing urban walkability

Urban walkability sounds like a self-explanatory term: it measures how accessible an urban environment is by walking. However, the factors that make up walkability are hard to define, and, consequently, walkability can be understood and measured in many different ways. To say a place is walkable could, for example, mean that the network of streets is dense or that a wide selection of services can be accessed on foot. Other urban elements such as green space, air quality or the amount of traffic affect walkability too.

In this post I will analyze urban walkability with two network-based approaches. First, I will focus on the structure of a street network by simply calculating intersection densities. Then, with a bit more complex approach, I will run a city-wide routing analysis to find out how different points of interest can be accessed on foot within an urban area.

All the analyses are done with OpenStreetMap (OSM) data, using the [OSMnx](https://osmnx.readthedocs.io/en/stable/), [pandana](https://udst.github.io/pandana/) and [geopandas](https://geopandas.org/) python packages. Visualizations are a mix of QGIS and matplotlib. While in this post I mainly analyze the walkability in Warsaw, Poland, the workflow is directly transferable across any city with sufficient OSM data.

<br/>

### 1. Intersection counts

**OSMnx and graphs**

From OSMnx's documentation:

>*OSMnx is a Python package that lets you download geospatial data from OpenStreetMap and model, project, visualize, and analyze real-world street networks and any other geospatial geometries.* 

In this analysis I used OSMnx to download the walkable street network of the analysis area, and to construct a graph from that network. A graph comprises of edges (walkable paths in this case) and nodes (points in which the edges intersect).


![Graph overview](docs/graph_overview.png)
*The egdes of Warsaw's walkable street network*

The resulting graph is very dense and has a ton of nodes. This can be problematic. For example, if two paths merge with a third path at even slightly different points, one real-life intersecion can turn into 2 nodes. In this analysis I tried to model actual intersections only, which is why I chose to simplify the graph a bit. I dissolved all nodes within five meters of eachother into single nodes and excluded all dead-ends. The result is not perfect, but I think it represents the "real life" intersections better than the original graph.

![Graph comparison](docs/graph_comparison.png)
*The original (left) and simplified (right) graphs side by side*

<br/>

**Visualizing intersection density**

The simplification nearly halved the intersection count: from 177 207 to 96 414. Still, just a heap of nodes isn't really an informative display of the data. To better visualize the intersection density I first used matplotlib's hexbin functionality and then experimented a bit with seaborn's kernel density plotting (kde).

![Intersection grid](docs/intersection_hexbin.png)
*Intersection density visualized with hexbins*

<br/>

![Intersection kde](docs/intersection_kde.png)
*Seaborn's kde plotting is another cool way to visualize densities*

### 2. Network analysis

For the network analysis I used the complete walkable network without any simplification. Instead of just nodes, the routing analysis uses the whole graph, and keeping the precise geometry leads to more accurate walk times.

![Walk_access](docs/walk_access.png)

Also, when dealing with OSM data, one should keep in mind that some of the variance in data coverage and detail is just an inevitable by-product of the various mapping habits of OSM contributors.

<br/>

### 3. References

Boeing, G. 2017. OSMnx: New Methods for Acquiring, Constructing, Analyzing, and Visualizing Complex Street Networks. *Computers, Environment and Urban Systems 65*, 126-139. doi:10.1016/j.compenvurbsys.2017.05.004



