# Model 3: Real-Time Pricing with External Event Integration

This module implements **Model 3** of the Urban Parking Dynamic Pricing project. It uses the [Pathway](https://pathway.com/) real-time data streaming framework to dynamically compute parking prices based on both **internal metrics** (e.g., occupancy, queue length) and **external influences** (e.g., events and weather conditions).

---

## 📊 Objective

The goal is to simulate real-time pricing for urban parking lots by considering both demand-side internal features and external contextual signals like:
- Ongoing events (concerts, parades, etc.)
- Weather conditions (rain, clear, etc.)

This creates a robust dynamic pricing model that adapts based on real-world stimuli.

---

## 🛠️ Technology Stack

- **Python**
- **Pathway** (Real-time data processing)
- **Pandas & NumPy** (Preprocessing)
- **CSV & JSONL** formats for streaming data

---

## 📁 Files

| File Name | Description |
|-----------|-------------|
| `model3_code.ipynb` | Main notebook implementing Model 3 logic using Pathway |
| `dataset_with_timestamp.csv` | Streaming parking lot data (timestamp, occupancy, etc.) |
| `external_events_weather.csv` | Streaming external data (event types, weather) |
| `model3_output.jsonl` | Final output stream containing computed price per timestamp |

---

## 🧠 How It Works

### 1. **Input Streams**
- `dataset_with_timestamp.csv`: Contains real-time parking lot data.
- `external_events_weather.csv`: Contains simulated external data (event & weather).

### 2. **Data Processing via Pathway**
- Streamed using `pw.io.csv.read()` in **streaming mode**.
- Custom `@pw.udf` functions calculate:
  - Demand based on both internal + external factors
  - Final price using dynamic pricing formula

### 3. **Demand Calculation Formula**
```python
demand = (
    alpha * (occupancy / capacity) +
    beta * queue_length -
    gamma * traffic_level +
    delta * is_special_day +
    epsilon * vehicle_type_weight +
    zeta * event_impact +
    eta * weather_impact
)

Where:

event_impact and weather_impact are derived from mappings of event types and weather conditions.

### 4. **Price Formula**
price = base_price * (1 + lambda_ * demand)
Clipped between 0.5x and 2x of base price.

---

📥 Output

The output is written as a JSONL stream:
Each line contains:
{
  "ID": "Lot123",
  "Timestamp": "01-07-2025 15:00:00",
  "Demand": 2.35,
  "Price": 27.25
}
Saved to:
model3_output.jsonl

---

⚙️ Run Instructions

1. Make sure all dependencies are installed (including pathway).
pip install pathway

2. Place all input files (dataset_with_timestamp.csv, external_events_weather.csv) in the same directory.

3. Run the notebook model3_code.ipynb.

4. Final output will be saved to model3_output.jsonl.

---

📌 Notes
Both internal and external signals are essential for accurate demand estimation.

Pathway enables simulated real-time streaming using autocommit_duration_ms.

---

🔓 License
This project is licensed under the MIT License.

---

👤 Author
Ayush Kumar
Dynamic Pricing Model Developer – Summer Analytics 2025
GitHub: @ayush1k

---


Let me know if you'd like:
- A `README.md` for the full repo
- A markdown or `.ipynb` export of `model3_code.ipynb`
- Help converting this into a GitHub-friendly structure automatically

---