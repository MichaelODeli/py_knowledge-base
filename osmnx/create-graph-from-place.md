# Create graph from place

### Import

```python
import numpy as np
import osmnx as ox
import pandas as pd
import geopandas as gpd
from shapely.geometry import Point, LineString
import plotly.express as px
import plotly.graph_objects as go
ox.settings.log_console=True
ox.config(
    max_query_area_size=50000000000, 
    use_cache=True, 
    cache_folder='C:/Users/MichaelODeli/OneDrive/DEVELOP/work/Python/projects/py_railway_navigation/osmnx_cache'
    )
```

### Load geometry from place

```python
# Загрузка геометрии
ox.settings.useful_tags_way += ["railway"]
G = ox.graph_from_place(
    "Свердловская область, Россия",
    retain_all=False,
    truncate_by_edge=True,
    simplify=True,
    custom_filter='["railway"]',
)
# Визуализация сети
fig, ax = ox.plot_graph(G, node_size=0, edge_color="w", edge_linewidth=0.2)
```

### Routing

```python
origin = (56.859603, 60.605155)
destination = (56.858718, 62.702409)
# Определение ближайшей вершины графа
origin_node = ox.distance.nearest_nodes(G, origin[1], origin[0])
destination_node = ox.distance.nearest_nodes(G, destination[1], destination[0])
# Определение кратчайшего пути
route = ox.shortest_path(G, origin_node, destination_node)
fig, ax = ox.plot_graph_route(G, route, route_color="c", node_size=0)
```

### Visualisation

```python
# Интерактивная визуализация в folium
ox.folium.plot_route_folium(G, route, edge_color="w", edge_linewidth=0.2, tiles='openstreetmap')
```
