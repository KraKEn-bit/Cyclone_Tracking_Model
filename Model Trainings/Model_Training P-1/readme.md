# Tropical Cyclone Trajectory Prediction for the Bangladesh Coastline

## Project Overview
This project develops and validates high-precision deep learning models to predict tropical cyclone trajectories in the Bay of Bengal, specifically targeting the Bangladesh coastline. Unlike global models, this research addresses the unique geographical and meteorological challenges of the region, including the complex delta system and characteristic recurvature patterns.

Using **Cyclone Mocha (2023)** as a primary case study, we demonstrate that **hybrid spatiotemporal models** significantly outperform traditional baseline architectures in predicting cyclone landfall accurately.

---

##  Acknowledgments & References
This work is inspired by and builds upon research conducted for the Indian coastline:

- **Research Paper:** [Automatic Cyclone Tracking System (Paper Description)]([link-to-paper](https://github.com/MSR2201/Automatic-Cyclone-Track-Prediction/blob/main/Automatic%20Cyclone%20Tracking%20System.pdf))
- **Original Implementation:** [MSR2201/Automatic-Cyclone-Track-Prediction]([link-to-repo](https://github.com/MSR2201/Automatic-Cyclone-Track-Prediction/blob/main/Automatic_cyclone_tracking_system.ipynb))
- **Key Contribution:** While the reference work focuses on the Indian coast (e.g., Cyclone Michaung), this repository specializes the framework for the northernmost Bay of Bengal (Bangladesh), optimizing for sharp northeastward turns.

---

##  Methodology
We implemented four neural network architectures to compare their efficacy in predicting cyclone trajectories:

| Model | Description |
|-------|-------------|
| **MLP (Multi-Layer Perceptron)** | Basic feed-forward baseline. |
| **LSTM (Long Short-Term Memory)** | Temporal model capturing sequential dependencies. |
| **CNN-LSTM (Hybrid)** | Convolutional layers for spatial features + LSTM for time-series forecasting. |
| **CNN-GRU (Proposed Best)** | Gated Recurrent Units for improved efficiency and reduced overfitting on regional data. |

---

##  Performance Metrics
Models were evaluated using **Cyclone Mocha (2023)**. Accuracy measured how closely predicted paths aligned with **IBTrACS data**.

| Architecture | Spatial Awareness | Temporal Memory | Track Stability | Error Level |
|--------------|-----------------|----------------|----------------|-------------|
| **MLP** | ❌ None | ❌ Low | 🔴 High Deviation | High |
| **LSTM** | ❌ None | ✅ High | 🟠 Sequential Lag | Moderate |
| **CNN-LSTM** | ✅ High | ✅ High | 🔵 Accurate Curve | Low |
| **CNN-GRU** | ✅ High | ✅ Optimized | 🟢 Most Precise | Lowest |

**Key Observations:**

- **Recurvature Problem:** Baseline models (MLP/LSTM) often drift straight, failing to capture sharp turns toward Cox's Bazar.  
- **Hybrid Advantage:** CNN layers identify spatial environmental features, enabling CNN-GRU to follow the actual storm bend.  
- **Landfall Accuracy:** CNN-GRU has the lowest Final Displacement Error (FDE), making it most suitable for real-world evacuation planning.  

---

##  Geospatial Validation
Validation used **Cartopy** with high-resolution (10m) land features for precise visualization.

- **Actual Track:** Red (IBTrACS Data)  
- **Predicted Tracks:** Blue / Orange / Magenta (Model Outputs)  

---

##  Challenges & Limitations
- **Regional Data Density:** Bay of Bengal has fewer historical data points than the Pacific, affecting model generalization.  
- **Feature Constraints:** Currently, models rely on Lat/Lon coordinates. Future work should include **Sea Surface Temperature (SST)** and **Wind Shear** for better intensity-movement coupling.  
- **Timing of Turns:** Predicting the exact hour of recurvature remains challenging, even for hybrid architectures.  

---

