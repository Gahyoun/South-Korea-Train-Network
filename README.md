# 🚉 South Korea Train Network

The **South Korea Train Network** project provides pre-processed railway network data for researchers, developers, and enthusiasts. The dataset includes geolocation-enriched nodes, weighted edges, and serialized network files for easy use in analysis and visualization.

---

## 📂 Dataset Contents

This repository contains the following files and folders:

### 1. Raw Data
- **`ktrain_node_link_data.xlsx`**: The original railway network data from the [KRIC Open Data Portal](https://data.kric.go.kr/rips/M_01_01/intro.do).

### 2. Processed Data
- **`ktrain_data(25.01.10).zip`**: A compressed file containing processed network data for all lines, including:
  - Node lists (`*_node_list.txt`) with geolocation information (latitude and longitude).
  - Edge lists (`*_edge_list.txt`) with weights based on the inverse of Euclidean distances.
  - Serialized network files (`*.pkl`) for direct use in Python.

### 3. Examples
- Example files included in the repository:
  - `Seoul_Metropolitan_Line_1_node_list.txt`
  - `Seoul_Metropolitan_Line_1_edge_list.txt`
  - `Seoul_Metropolitan_Line_1.pkl`

---
## Data list 
### 🚇 **도시철도**

#### 수도권
- **경강선**: `Gyeonggang_Line`
- **경의중앙선**: `Gyeongui-Jungang_Line`
- **경인선**: `Gyeongin_Line`
- **경춘선**: `Gyeongchun_Line`
- **분당선**: `Bundang_Line`
- **서해선**: `Seohae_Line`
- **수도권 1호선**: `Seoul_Metropolitan_Line_1`
- **수도권 2호선 (성수지선)**: `Seoul_Metropolitan_Line_2_(Seongsu_Branch)`
- **수도권 2호선 (순환선)**: `Seoul_Metropolitan_Line_2_(Main_Loop)`
- **수도권 2호선 (신정지선)**: `Seoul_Metropolitan_Line_2_(Sinjeong_Branch)`
- **수도권 3호선**: `Seoul_Metropolitan_Line_3`
- **수도권 4호선**: `Seoul_Metropolitan_Line_4`
- **수도권 5호선**: `Seoul_Metropolitan_Line_5`
- **수도권 6호선**: `Seoul_Metropolitan_Line_6`
- **수도권 7호선**: `Seoul_Metropolitan_Line_7`
- **수도권 8호선**: `Seoul_Metropolitan_Line_8`
- **수도권 9호선**: `Seoul_Metropolitan_Line_9`
- **수도권 경량도시철도 에버라인**: `Seoul_Metropolitan_Light_Rail_Everline`
- **수도권 경량도시철도 신림선**: `Seoul_Metropolitan_Light_Rail_Sillim_Line`
- **수도권 경량도시철도 우이신설선**: `Seoul_Metropolitan_Light_Rail_Ui-Sinseol_Line`

#### 인천
- **인천국제공항선**: `Incheon_Airport_Line`
- **인천지하철 1호선**: `Incheon_Metro_Line_1`
- **인천지하철 2호선**: `Incheon_Metro_Line_2`

#### 경기
- **안산·과천선**: `Ansan-Gwacheon_Line`
- **수인선**: `Suin_Line`
- **신분당선**: `Shinbundang_Line`
- **일산선**: `Ilsan_Line`
- **의정부 경전철**: `Uijeongbu_Light_Rail`

#### 대전
- **대전 도시철도 1호선**: `Daejeon_Metro_Line_1`

#### 대구
- **대구 도시철도 1호선**: `Daegu_Metro_Line_1`
- **대구 도시철도 2호선**: `Daegu_Metro_Line_2`
- **대구 도시철도 3호선**: `Daegu_Metro_Line_3`

#### 부산
- **부산 경량도시철도 4호선**: `Busan_Gimhae_Light_Rail_Transit_(Line_4)`
- **부산 도시철도 1호선**: `Busan_Metro_Line_1`
- **부산 도시철도 2호선**: `Busan_Metro_Line_2`
- **부산 도시철도 3호선**: `Busan_Metro_Line_3`

#### 광주
- **광주 도시철도 1호선**: `Gwangju_Metro_Line_1`

---

### 🚄 **고속철도**
- **경부선**: `Gyeongbu_Line`
- **경원선**: `Gyeongwon_Line`
- **동해선**: `Donghae_Line`
- **진접선**: `Jinjeop_Line`
- **김포골드라인**: `Gimpo_Gold_Line`
- **자기부상철도**: `Maglev_Train`
- ---
### 🛠 How to Use

### 1. Data Structure

Each Node List file contains station names along with their geolocation information. These files are essential for building and visualizing railway networks.

#### File Structure
The Node List is formatted as a CSV file with the following columns:
- **Station**: The name of the station.
- **Latitude**: The latitude coordinate of the station.
- **Longitude**: The longitude coordinate of the station.

#### Example Node List File
```csv
Station,Latitude,Longitude
StationA,37.5665,126.9780
StationB,37.5678,126.9882
StationC,37.5689,126.9975
```
### 2. Loading the Network from a Serialized Graph (`*.pkl`)

Serialized NetworkX graphs (`*.pkl` files) are ready-to-use network representations that include:
- **Node attributes**: e.g., latitude, longitude.
- **Edge attributes**: e.g., weights representing the inverse of Euclidean distance.

This format allows you to quickly load and analyze the railway network without manually constructing the graph.

#### Python Code: Loading a Network from a `.pkl` File
```python
import pickle
import networkx as nx

# Load the serialized graph
pkl_file = "Seoul_Metropolitan_Line_1.pkl"
with open(pkl_file, "rb") as f:
    G = pickle.load(f)

# Check nodes and their attributes
print("Graph Nodes with Attributes:")
for node, data in G.nodes(data=True):
    print(f"Station: {node}, Latitude: {data.get('latitude')}, Longitude: {data.get('longitude')}")

# Check edges and their attributes
print("\nGraph Edges with Attributes:")
for u, v, data in G.edges(data=True):
    print(f"Edge: {u} -> {v}, Weight: {data.get('weight')}")
```

If you want to construct the railway network manually, you can use the provided **Node List (`*_node_list.txt`)** and **Edge List (`*_edge_list.txt`)**. These files provide station information and connections between stations, respectively.

#### File Requirements:
- **Node List**: Contains station names along with geolocation information (latitude and longitude).
- **Edge List**: Defines connections between stations, including weights (inverse of Euclidean distance).

#### Python Code: Building the Network from Node List & Edge List
```python
import pandas as pd
import networkx as nx

# Load the Node List
node_list_file = "Seoul_Metropolitan_Line_1_node_list.txt"
nodes = pd.read_csv(node_list_file)

# Load the Edge List
edge_list_file = "Seoul_Metropolitan_Line_1_edge_list.txt"
edges = pd.read_csv(edge_list_file)

# Create a graph and add nodes with attributes
G = nx.Graph()

# Add nodes with geolocation attributes
for _, row in nodes.iterrows():
    G.add_node(row['Station'], latitude=row['Latitude'], longitude=row['Longitude'])

# Add edges with weights
for _, row in edges.iterrows():
    G.add_edge(row['Source'], row['Target'], weight=row['Weight'])

# Check nodes and their attributes
print("Graph Nodes with Attributes:")
for node, data in G.nodes(data=True):
    print(f"Station: {node}, Latitude: {data.get('latitude')}, Longitude: {data.get('longitude')}")

# Check edges and their attributes
print("\nGraph Edges with Attributes:")
for u, v, data in G.edges(data=True):
    print(f"Edge: {u} -> {v}, Weight: {data.get('weight')}")
```

