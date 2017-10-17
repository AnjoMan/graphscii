# graphscii

Graphscii is a python library that turns ascii diagrams of networks into network objects. It returns a [networkx](https://networkx.github.io/) graph of nodes for each alpha-numeric element in the input text; nodes are connected in the graph to match the edges represented in the diagram by `-`, `/`, `\` and `|`.


## Usage

Graphscii expects a string containg a 2-d ascii diagram. Nodes can be an alphanumeric string composed of characters in `A-Z`, `a-z`, `0-9`, and `_, {, }`. Edges can be composed of `-`, `/`, `\` and `|` (with some restrictions on how corners work --- see the tests).

```python

import graphscii

network = graphscii.graph_from_ascii("""
          NodeA-----
                   |
                   |---NodeB
                                     """)

print(network)
>>> <networkx.classes.graph.Graph at 0x7f24c3a8b470>

print(list(network.edges()))
>>> [(NodeA, NodeB)]

print(list(network.nodes()))
>>> [NodeA, NodeB]

print(list(network.nodes(data=True)))
>>> [('NodeA', {'position': Point(1, 10)}), ('NodeB', {'position': Point(3, 23)})]

```

Networkx provides tools to attach data to nodes and edges; in the above example you can see that graphscii uses this to attach a `Point` object to each node indicating where on the _(x, y)_ plane each node starts ( _0,0_ is at the top-left).


```python
import graphscii


network = graphscii.graph_from_ascii("""
          s---p----1---nx
         /    |        |
        /     |        0---f
       6l-a   c--
      /   |      \--k
     /   ua         |  9e
    q      \        | /
            \-r7z   jud
                \    |
                 m   y
                  \  |
                   v-ow
                             """)
```