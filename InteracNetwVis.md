# Introduction to Interactive Network Graph Visualization with Python

## Introduction:

Network graphs, are a powerful way to represent and analyze relationships between various entities, such as social networks, communication networks, biological systems, and more. Interactive network graph visualization in Python has gained significant popularity due to its ability to provide insights into complex data structures and make them easily understandable.

Python, a versatile and widely-used programming language, offers numerous libraries and tools to create interactive network graph visualizations. In this introduction, we will explore the key components and popular Python libraries that enable the creation of interactive network graph visualizations.

### Key Components of Interactive Network Graphs:

1. **Nodes:** Nodes represent individual entities within the network. They can represent people, devices, websites, or any other object of interest in your data.

2. **Edges:** Edges are the connections or relationships between nodes. They indicate how nodes are related to each other and can carry additional information, such as weight or direction.

3. **Attributes:** Both nodes and edges can have attributes that provide additional information about them. These attributes can be used to color, size, or label the elements of the network.

4. **Interactivity:** The power of interactive network graph visualization lies in the ability to explore and analyze the data dynamically. Users can zoom, pan, click on nodes or edges to reveal more information, and filter or highlight specific components of the network.

### Popular Python Libraries for Interactive Network Graph Visualization:

1. **NetworkX:** NetworkX is a Python library for the creation, manipulation, and study of complex networks. While it does not provide direct interactive visualization capabilities, it is often used to prepare and analyze network data before passing it to other libraries for visualization.

2. **D3.js:** D3.js is a powerful JavaScript library for creating interactive data visualizations. Python developers often use it in conjunction with Python libraries like Flask or Dash to build web applications that display interactive network graphs.

3. **Plotly:** Plotly is a Python graphing library that offers interactive network graph visualization capabilities. It is especially popular for creating web-based dashboards with interactive charts and graphs.

4. **Cytoscape.js:** Cytoscape.js is a JavaScript library that specializes in network graph visualization. Python developers can use Cytoscape.js through Jupyter notebooks or web applications to create highly interactive and customizable network graphs.

5. **Bokeh:** Bokeh is a Python library for creating interactive, web-ready visualizations. It can be used to build interactive network graph visualizations that can be embedded in web applications or viewed in Jupyter notebooks.

6. **Pyvis:** Pyvis is a Python library specifically designed for creating interactive network graph visualizations. It is built on top of NetworkX and allows users to generate visually appealing and interactive network graphs with ease. Pyvis provides a straightforward way to add nodes, edges, and customize the appearance and interactivity of the resulting graph directly from Python code. This library is suitable for both small-scale exploratory data analysis and larger network graph visualization projects.

Including Pyvis in your arsenal of tools for interactive network graph visualization with Python can make the process more efficient and user-friendly. You can use Pyvis to create visually engaging graphs and customize various aspects of the visualization to meet your specific requirements. For this reason, the focus of this repository will be on an **application on pyvis**.

### Conclusion:

Interactive network graph visualization with Python opens up a world of possibilities for exploring complex relationships and patterns within your data. By leveraging the right Python libraries and tools, you can create interactive network graphs that are not only informative but also engaging for your audience. In the following guides and tutorials, we will dive deeper into the practical aspects of creating such visualizations using the mentioned libraries.



```python
### First simple example
from pyvis import network as net
import networkx as nx

g=net.Network(notebook=True)
nxg = nx.complete_graph(5)
g.from_nx(nxg)

g.show("example.html")
```

    Warning: When  cdn_resources is 'local' jupyter notebook has issues displaying graphics on chrome/safari. Use cdn_resources='in_line' or cdn_resources='remote' if you have issues viewing graphics in a notebook.
    example.html






<iframe
    width="100%"
    height="600px"
    src="example.html"
    frameborder="0"
    allowfullscreen

></iframe>





```python
### Import Libraries

#!{sys.executable} -m pip install matplotlib
#!{sys.executable} -m pip install numpy
#!{sys.executable} -m pip install pandas
#!{sys.executable} -m pip install networkx
#!{sys.executable} -m pip install pyvis

import sys
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import networkx as nx
import pyvis as pv
```


```python
from pyvis.network import Network
import pandas as pd

got_net = Network(height="750px", width="100%", bgcolor="#222222", font_color="white", notebook=True)

# set the physics layout of the network
got_net.barnes_hut()
got_data = pd.read_csv("stormofswords.csv")

sources = got_data['Source']
targets = got_data['Target']
weights = got_data['Weight']

edge_data = zip(sources, targets, weights)

for e in edge_data:
                src = e[0]
                dst = e[1]
                w = e[2]

                got_net.add_node(src, src, title=src)
                got_net.add_node(dst, dst, title=dst)
                got_net.add_edge(src, dst, value=w)

neighbor_map = got_net.get_adj_list()

# add neighbor data to node hover data
for node in got_net.nodes:
                node["title"] += " Neighbors:<br>" + "<br>".join(neighbor_map[node["id"]])
                node["value"] = len(neighbor_map[node["id"]])

got_net.show("networkgraph.html")

```

    Warning: When  cdn_resources is 'local' jupyter notebook has issues displaying graphics on chrome/safari. Use cdn_resources='in_line' or cdn_resources='remote' if you have issues viewing graphics in a notebook.
    networkgraph.html






<iframe
    width="100%"
    height="750px"
    src="networkgraph.html"
    frameborder="0"
    allowfullscreen

></iframe>



