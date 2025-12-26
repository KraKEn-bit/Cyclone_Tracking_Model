# Tropical Cyclone Trajectory Prediction for the Bangladesh Coastline

## Project Overview
This project develops and validates high-precision deep learning models to predict tropical cyclone trajectories in the Bay of Bengal, specifically targeting the Bangladesh coastline. Unlike global models, this addresses the unique geographical and meteorological challenges of the region, including the complex delta system and characteristic recurvature patterns.

Using **Cyclone Mocha (2023)** as a primary case study, I demonstrate that **hybrid spatiotemporal models** significantly outperform traditional baseline architectures in predicting cyclone landfall accurately.

---

##  Acknowledgments & References
This work is inspired by and builds upon research conducted for the Indian coastline:

- **Research Paper:** [Automatic Cyclone Tracking System (Paper Description)](https://github.com/MSR2201/Automatic-Cyclone-Track-Prediction/blob/main/Automatic%20Cyclone%20Tracking%20System.pdf)
- **Original Implementation:** [MSR2201/Automatic-Cyclone-Track-Prediction](https://github.com/MSR2201/Automatic-Cyclone-Track-Prediction/blob/main/Automatic_cyclone_tracking_system.ipynb)
- **Key Contribution:** While the reference work focuses on the Indian coast (Cyclone Michaung), this repository specializes the framework for the northernmost Bay of Bengal (Bangladesh), optimizing for sharp northeastward turns.

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
- 




## 🚀 How to Run (Inference)

To use the pre-trained models for predicting new cyclone coordinates, follow these steps:

### 1. Prerequisites
Ensure you have the following libraries installed:
```bash
pip install tensorflow pandas numpy matplotlib cartopy
- **Timing of Turns:** Predicting the exact hour of recurvature remains challenging, even for hybrid architectures.  
```

### **Load a Pre trained Model:**

```bash
import tensorflow as tf
from tensorflow.keras.models import load_model

# Load the best performing model
model = load_model('models/CNN_GRU.h5')

# Check model architecture
model.summary()
```

### Run a Prediction:

```bash
import numpy as np

# Example: Last 3 timesteps of a storm (Latitude, Longitude)
# Note: Input must be scaled/normalized if you used scaling during training
sample_input = np.array([[15.2, 88.5], [15.8, 89.1], [16.5, 89.8]])
sample_input = np.expand_dims(sample_input, axis=0) # Reshape for the model

# Predict the next coordinate
prediction = model.predict(sample_input)
print(f"Predicted Next Coordinate: {prediction}")
```


