
https://gephi.org

---

`Gephi` is an **open-source network analysis and visualization tool**. Think of it as a kind of "Photoshop for graphs."

Instead of editing images, you use `Gephi` to explore and manipulate **networks** such as:

- Social networks (e.g., Twitter user connections)

- IT and security data (e.g., infrastructure maps, attack surfaces)

- Biological networks (e.g., protein interactions)

- Citation or knowledge graphs


Key Features

- **Graph visualization** – Create interactive visualizations of networks (nodes and edges).

- **Layout algorithms** – Automatically rearrange graphs for clarity (e.g., `ForceAtlas2` for clusters).

- **Metrics** – Compute graph statistics like centrality, modularity (community detection), shortest paths, etc.

- **Filtering** – Focus on specific nodes or relationships.

- **Dynamic graphs** – Analyze how networks evolve over time.

- **Plugins** – Extend functionality with custom modules.

---

**Create desktop Entry**
```
nano ~/.local/share/applications/gephi.desktop
```

```
[Desktop Entry]
Name=Gephi
Comment=Graph Visualization Platform
Exec=/opt/gephi-0.10.1/bin/gephi
Icon=/opt/gephi-0.10.1/flathub/gephi.png
Terminal=false
Type=Application
Categories=Education;Science;
```