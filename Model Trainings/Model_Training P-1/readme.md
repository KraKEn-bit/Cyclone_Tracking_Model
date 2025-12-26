## 📊 Comparative Performance Metrics

The following table summarizes the performance of each model architecture. The **Average Displacement Error (ADE)** and **Final Displacement Error (FDE)** were calculated based on the 24-hour lead-time predictions for Cyclone Mocha (2023).

| Model Architecture | Spatial Awareness | Temporal Memory | Track Consistency | Relative Accuracy |
| :--- | :---: | :---: | :---: | :---: |
| **MLP (Baseline)** | ❌ None | ❌ Low | 🔴 Jittery / Linear | Lowest |
| **LSTM (Baseline)** | ❌ None | ✅ High | 🟠 Lagging / Smooth | Moderate |
| **CNN-LSTM** | ✅ High | ✅ High | 🔵 Accurate / Stable | High |
| **CNN-GRU (Proposed)** | ✅ High | ✅ Efficient | 🟢 Most Precise | **Highest** |



### 🔍 Technical Analysis of Results

1. **The Baseline Gap:** Simple models like **MLP** and **LSTM** lack "Spatial Context." While they can remember previous coordinates, they do not understand the geographical constraints of the Bay of Bengal. This results in the "Drift Error" seen in the baseline plots.

2. **The Hybrid Advantage:** The **CNN-LSTM** and **CNN-GRU** models utilize Convolutional layers to process the surrounding coordinate grid as a spatial feature map. This allows the models to "anticipate" turns in the trajectory based on spatial patterns in the historical data.

3. **Why CNN-GRU Won:** In our experiments on the Bangladesh regional dataset, the **CNN-GRU** outperformed the CNN-LSTM. This is attributed to the GRU's streamlined architecture (Reset and Update gates), which prevents the vanishing gradient problem more effectively than LSTM when working with the specific sample sizes available in the North Indian Ocean IBTrACS subset.

4. **Landfall Precision:** The **FDE (Final Displacement Error)**—which measures the distance between the predicted and actual landfall points—was lowest in the CNN-GRU model. This is the most critical metric for disaster management and evacuation planning in Cox's Bazar and coastal regions.



---

## 📈 Summary of Achievements
* **Regional Specialization:** Successfully pivoted the Indian "Michaung" methodology to create a Bangladesh-centric "Mocha" validation set.
* **Architecture Optimization:** Identified CNN-GRU as the most resource-efficient and accurate model for the Bay of Bengal.
* **Geospatial Validation:** Integrated high-resolution Cartopy mapping to prove that AI-driven tracks align with real-world geographical landmarks.
