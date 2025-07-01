# 🚗 Urban Parking Dynamic Pricing System

This project implements dynamic pricing models for urban parking lots using historical and real-time data streams. Built as part of **Summer Analytics 2025**, it showcases three models of increasing complexity using Python, pandas, Bokeh, and the [Pathway](https://pathway.com) real-time data framework.

---

## 📁 Folder Structure

DYNAMIC-PARKING-PRICING/
│
├── dataset/
│ └── dataset.csv # Static dataset for Model 1
│
├── model1/
│ ├── dynamic_pricing_m1.ipynb # Model 1: Occupancy-based pricing (baseline)
│ └── readme.md # Model-specific README
│
├── model2/
│ ├── dynamic_pricing_m2.ipynb # Model 2: Real-time demand-based pricing using Pathway
│ └── readme.md # Model-specific README
│
├── model3/
│ ├── dataset_with_timestamp.csv # Input stream data for Model 3
│ ├── external_events_weather.csv # External events and weather for Model 3
│ ├── dynamic_pricing_m3.ipynb # Model 3: Demand + external influence
│ ├── model3_output.jsonl # Output from Model 3
│ └── readme.md # Model-specific README
│
├── LICENSE # MIT License
└── README.md # Global README

---


---

## 🧠 Models Overview

### ✅ Model 1: Occupancy-Based Pricing

- 📂 Path: `model1/dynamic_pricing_m1.ipynb`
- Uses historical data (`dataset.csv`) to simulate price change based on occupancy ratio.
- Formula:
  \[
  \text{Price}_t = \text{Previous Price} + \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right)
  \]
- Gradual price adjustment with memory of previous price.
- Built using `pandas` and `Bokeh`.

---

### 🚦 Model 2: Real-Time Demand-Based Pricing

- 📂 Path: `model2/dynamic_pricing_m2.ipynb`
- Simulates real-time demand-based pricing using Pathway.
- Demand Formula:
  \[
  \text{Demand} = \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right) + \beta \cdot \text{QueueLength} - \gamma \cdot \text{TrafficLevel} + \delta \cdot \text{IsSpecialDay} + \epsilon \cdot \text{VehicleTypeWeight}
  \]
- Output is streamed to `output_pathway.jsonl`.

---

### 🌐 Model 3: Demand + External Influences

- 📂 Path: `model3/dynamic_pricing_m3.ipynb`
- Adds **event** and **weather** data to influence demand and pricing.
- Uses:
  - `dataset_with_timestamp.csv` (real-time internal features)
  - `external_events_weather.csv` (external influences)
- Output: `model3_output.jsonl`

#### Extended Demand Formula:
\[
\text{Demand} = \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right) + \beta \cdot \text{QueueLength} - \gamma \cdot \text{TrafficLevel} + \delta \cdot \text{IsSpecialDay} + \epsilon \cdot \text{VehicleTypeWeight} + \zeta \cdot \text{EventImpact} + \eta \cdot \text{WeatherImpact}
\]

---

▶️ How to Run
1. Clone the repository:
git clone https://github.com/ayush1k/urban-parking-dynamic-pricing.git
cd urban-parking-dynamic-pricing

2. Run any of the models using Jupyter Notebook or VSCode.

3. Input files are located inside respective model folders.

4. Model 2 and Model 3 use Pathway to simulate streaming.

---

📊 Visualization
All models use Bokeh for interactive price trend visualizations.

Explore how prices evolve for multiple lots across time.

---

⚠️ Limitations
Data is synthetic/simulated.

Model does not integrate live GPS, camera, or payment systems.

Competition modeling is indirect.

---

📜 License
This project is licensed under the MIT License.
You are free to use, modify, and distribute this work with attribution.

---

👤 Author
Ayush Kumar
Dynamic Pricing Model Developer – Summer Analytics 2025
🔗 GitHub: @ayush1k

---

🤝 Acknowledgments
Pathway.com for the real-time streaming framework

Summer Analytics 2025 team for the challenge structure

---

