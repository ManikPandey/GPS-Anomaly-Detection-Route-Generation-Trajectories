# GPS Anomaly Detection and "Normal Route" Generation

This project demonstrates a robust pipeline for analyzing large-scale GPS trajectory data to identify anomalous driving routes and generate a "normal" route between common origins and destinations. It highlights core skills in data processing, geospatial analysis, anomaly detection, and presents a conceptual link to generative AI and distributed computing.

---

## Project Goals

- **Generate "Normal Routes":** Learn and derive typical travel paths between frequently used origin-destination (O-D) locations.
- **Detect Anomalies:** Automatically flag deviations from typical routes that may indicate inefficiency, unauthorized use, or operational issues.

---

## Key Features

- **Trajectory Parsing:** Efficiently processes raw GPS `.plt` files.
- **Driving Segment Detection:** Filters for vehicle-like movements based on estimated speed from geodesic calculations.
- **O-D Pair Clustering:** Uses DBSCAN clustering on trip start and end-points to identify common travel pairs.
- **Normal Route Generation:** For selected O-D pairs, the script creates a representative route—either by choosing the most common trajectory or a density-based estimation.
- **Anomaly Detection:** Calculates distance from each point in a test trajectory to the "normal route" and flags points that exceed a configurable anomaly threshold.
- **Interactive Visualization:** Outputs an interactive HTML map (using Folium) showing routes and detected anomalies.
- **Scalability Discussion:** Explains how the solution could scale to big data with Apache Spark.

---

## Dataset

- **Source:** [Geolife GPS Trajectories Dataset (Microsoft Research)](https://www.microsoft.com/en-us/research/publication/geolife-traces-dataset/)
- **Format:** `.plt` files with latitude, longitude, altitude, date, time

---

## Technical Approach

1. **Preprocessing:**  
   - Parses `.plt` files.
   - Combines date and time into timestamps.
   - Assigns unique trip IDs.

2. **Spatial Analysis:**  
   - Calculates segment speeds using the Haversine formula.
   - Filters for driving-like segments (by heuristics on speed).
   - Clusters O-D points with DBSCAN to find frequently used locations.
   - Generates a "normal route" for a selected O-D cluster.

3. **Anomaly Detection:**  
   - Computes the minimum Haversine distance from each point on a test trip to the normal route.
   - Flags points exceeding a set distance threshold as anomalies.

4. **Visualization:**  
   - Creates a Folium HTML map showing the:
     - Normal route (blue)
     - Test trip (green)
     - Anomalous points (red)

5. **Scalability:**  
   - Concepts are provided for extending the pipeline with PySpark for distributed processing, clustering, and anomaly detection.

---

## Setup & Usage

### 1. Clone and Prepare Data

pip install pandas scikit-learn folium geopy numpy shapely

- Loads and processes GPS trajectories
- Clusters O-D pairs and generates a normal route
- Performs anomaly detection and saves `geolife_route_analysis.html` for interactive exploration.

### 4. Results

Open `geolife_route_analysis.html` in a web browser to:
- View the learned normal route and test trip
- Inspect points flagged as anomalous (in red)

---

<img width="1717" height="937" alt="Screenshot 2025-07-31 102503" src="https://github.com/user-attachments/assets/00b0e0f1-bef3-4b46-a5fc-f5ffc76c6373" />


## Future Enhancements

- **Advanced Route Generation:** Trajectory clustering with DTW, density maps, or sequence modeling.
- **ML-Based Anomaly Detection:** LSTM autoencoders, Isolation Forests, or one-class SVMs.
- **Generative AI for Route Planning:** Use GNNs or seq2seq models for optimal, context-aware route synthesis.
- **Real-time Analysis:** Integrate streaming data tools (Kafka + Spark).
- **Enhanced Feature Engineering:** Incorporate live traffic, road networks, and weather.
- **Full Distributed Processing:** Build an end-to-end Spark pipeline for petabyte-scale GPS data.

---

