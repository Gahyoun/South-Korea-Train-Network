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

## 🛠 How to Use

### 1. Node List (`*_node_list.txt`)
Each node file contains station names along with their geolocation information:
```csv
Station,Latitude,Longitude
StationA,37.5665,126.9780
StationB,37.5678,126.9882
