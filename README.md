
# 🚗 Urban Parking Dynamic Pricing System

This project implements dynamic pricing models for urban parking lots using historical and real-time data streams. Built as part of **Summer Analytics 2025**, it showcases three models of increasing complexity using Python, pandas, Bokeh, and the [Pathway](https://pathway.com) real-time data framework.

---

## 📁 Folder Structure

```
DYNAMIC-PARKING-PRICING/
│
├── dataset/
│   └── dataset.csv                      # Static dataset for Model 1
│
├── model1/
│   ├── dynamic_pricing_m1.ipynb         # Model 1: Occupancy-based pricing (baseline)
│   └── readme.md                        # Model-specific README
│
├── model2/
│   ├── dynamic_pricing_m2.ipynb         # Model 2: Real-time demand-based pricing using Pathway
│   └── readme.md                        # Model-specific README
│
├── model3/
│   ├── dataset_with_timestamp.csv       # Input stream data for Model 3
│   ├── external_events_weather.csv      # External events and weather for Model 3
│   ├── dynamic_pricing_m3.ipynb         # Model 3: Demand + external influence
│   ├── model3_output.jsonl              # Output from Model 3
│   └── readme.md                        # Model-specific README
│
├── LICENSE                              # MIT License
└── README.md                            # Global README
```

---

## 🧠 Models Overview

### ✅ Model 1: Occupancy-Based Pricing

**Objective**: Implements a simple dynamic pricing model where prices adjust based on occupancy levels.

**Formula**:  
`Price_t = Previous Price + α × (Occupancy / Capacity)`

- `BASE_PRICE = ₹10`
- `α = 2.0`
- If capacity is 0 → retain previous price.
- Uses temporal smoothing by retaining last price.

**Tools**:  
- Python, Pandas, Bokeh  
- No real-time streaming, no external data

**Limitation**:  
Does not consider external influences like events, traffic, etc.

---

### 🚦 Model 2: Real-Time Demand-Based Pricing

**Objective**: Leverages the [Pathway](https://pathway.com) streaming engine to simulate real-time price updates using demand metrics.

**Demand Function**:  
`Demand = α × (Occupancy / Capacity) + β × QueueLength - γ × TrafficLevel + δ × IsSpecialDay + ε × VehicleTypeWeight`

**Price Function**:  
`Price = BasePrice × (1 + λ × NormalizedDemand)`

**Constants**:

| Symbol | Value | Meaning               |
|--------|-------|------------------------|
| α      | 1.0   | Occupancy weight       |
| β      | 0.5   | Queue weight           |
| γ      | 0.8   | Traffic penalty        |
| δ      | 1.2   | Special day boost      |
| ε      | 0.6   | Vehicle type influence |
| λ      | 1.5   | Price sensitivity      |

**Assumptions**:
- Base price = ₹10
- Prices clipped between ₹5 and ₹20
- Streaming simulation: 1 row/second

**Tools**:  
- Python, Pandas, Pathway, Bokeh

**Output File**:  
`model2_output.jsonl`

### 🌐 Model 3: Demand + External Influences

**Objective**: Enhances Model 2 by incorporating **external events** (e.g., concerts, parades) and **weather** data to affect demand and pricing.

**Extended Demand Function**:  
`Demand = α × (Occupancy / Capacity) + β × QueueLength - γ × TrafficLevel + δ × IsSpecialDay + ε × VehicleTypeWeight + ζ × EventImpact + η × WeatherImpact`

**Price Function**:  
`Price = BasePrice × (1 + λ × Demand)`

- Prices are clipped between **0.5x and 2x** of base price
- Event/Weather impacts are mapped via dictionaries

**Input Files**:
- `dataset_with_timestamp.csv` — main streaming data
- `external_events_weather.csv` — weather & events stream

**Output File**:
- `model3_output.jsonl`

**Execution**:
1. Install dependencies: `pip install pathway`
2. Run: `dynamic_pricing_m3.ipynb`
3. Output will be saved as `model3_output.jsonl`


---

## 📦 Installation

```bash
pip install pathway pandas numpy bokeh
```

---

## ▶️ How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/ayush1k/urban-parking-dynamic-pricing.git
   cd urban-parking-dynamic-pricing
   ```

2. Run any of the models using Jupyter Notebook or VSCode.

3. Input files are located inside respective model folders.

4. Model 2 and Model 3 use **Pathway** to simulate streaming.

---

## 📊 Visualization

- All models use **Bokeh** for interactive price trend visualizations.
- Explore how prices evolve for multiple lots across time.

---

## ⚠️ Limitations

- Data is synthetic/simulated.
- Model does not integrate live GPS, camera, or payment systems.
- Competition modeling is indirect.

---

## 📜 License

This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute this work with attribution.

---

## 👤 Author

**Ayush Kumar**  
Dynamic Pricing Model Developer – Summer Analytics 2025  
🔗 GitHub: [@ayush1k](https://github.com/ayush1k)

---

## 🤝 Acknowledgments

- [Pathway.com](https://pathway.com) for the real-time streaming framework
- Summer Analytics 2025 team for the challenge structure

---
