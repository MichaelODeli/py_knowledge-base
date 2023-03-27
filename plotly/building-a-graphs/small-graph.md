# Small graph

```python
import plotly.graph_objects as go

origin = (56.859603, 60.605155)
destination = (56.858718, 62.702409)

fig_train = go.Figure()
map_center = go.layout.mapbox.Center(lat=58., lon=60.)
fig_train.update_layout(mapbox_style="open-street-map",  autosize=False,
    width=1000,
    height=800,
                mapbox=dict(center=map_center, zoom=6))
fig_train.add_trace(go.Scattermapbox(lat=[origin[0], destination[0]], lon=[origin[1], destination[1]], mode='markers', text=['From', 'To'],
                            marker={'color':'blue', 'size':10}))
fig_train.show()
```
