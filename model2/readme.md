# 📈 Model 2: Real-Time Demand-Based Dynamic Pricing Using Pathway

## 🔍 Objective
In this model, we simulate **real-time dynamic pricing** for urban parking lots using **streaming data**. We leverage the [Pathway](https://pathway.com) framework to read data as a stream and update demand-based prices in near real-time.

---

## 🧮 Demand Function

We define a custom demand function that incorporates several real-world parking dynamics:

\[
\text{Demand} = \alpha \cdot \frac{\text{Occupancy}}{\text{Capacity}} + \beta \cdot \text{QueueLength} - \gamma \cdot \text{TrafficLevel} + \delta \cdot \text{IsSpecialDay} + \epsilon \cdot \text{VehicleTypeWeight}
\]

Where:
- **Occupancy/Capacity**: Measures how full the parking lot is.
- **QueueLength**: Number of vehicles waiting.
- **TrafficLevel**: Affects accessibility and urgency.
- **IsSpecialDay**: Holidays/events increase parking demand.
- **VehicleTypeWeight**: Different vehicle types (car/bike/truck) influence demand.

### Constants Used:
| Parameter | Value | Meaning |
|----------|--------|---------|
| α (alpha)   | 1.0  | Weight of occupancy |
| β (beta)    | 0.5  | Weight of queue |
| γ (gamma)   | 0.8  | Traffic penalty |
| δ (delta)   | 1.2  | Event-day boost |
| ε (epsilon) | 0.6  | Vehicle type influence |

---

## 💸 Pricing Function

Once demand is calculated, pricing is computed dynamically:

\[
\text{Price} = \text{BasePrice} \cdot (1 + \lambda \cdot \text{NormalizedDemand})
\]

- **BasePrice**: ₹10 (can be changed).
- **λ (lambda)**: 1.5 (controls price sensitivity).
- Prices are clipped between **₹5 and ₹20** to avoid outliers.

---

## 🤔 Assumptions Made

- Parking lots have a base price of ₹10.
- Traffic condition levels: `{low: 0.5, medium: 1.0, high: 1.5}`
- Vehicle weights: `{car: 1.0, bike: 0.7, truck: 1.5}`
- We assume higher queue length and special days increase demand.
- No direct competition data is used — it's indirectly reflected in demand via queue/occupancy.

---

## 🧠 Demand vs. Competition

While explicit competitor pricing is not modeled, **competition's effect on demand is captured** through:
- **Queue Length**: Indicates popularity and possibly less competition.
- **Occupancy**: High occupancy = high demand = possibly low competition.
- **Special Days**: More competition on festive days → captured through `IsSpecialDay`.

Thus, prices automatically adjust based on **internal demand signals**, which are in turn affected by external factors like traffic, time, and special events.

---

## 📊 Bokeh Visualizations

We used **Bokeh** to create interactive plots for dynamic price changes across multiple parking lots.

### Example Visualization:
```python
from bokeh.plotting import figure, show, output_notebook
from bokeh.models import ColumnDataSource
from bokeh.palettes import Category10

output_notebook()

# Sample 3 lots
lot_ids = df['ID'].unique()[:3]
p = figure(title="Model 2: Demand-Based Dynamic Pricing",
           x_axis_label='Time',
           y_axis_label='Price ($)',
           x_axis_type='datetime',
           width=800, height=400)

colors = Category10[10]

for i, lot in enumerate(lot_ids):
    lot_df = df[df['ID'] == lot]
    source = ColumnDataSource(data={
        'x': lot_df['Timestamp'],
        'y': lot_df['Price']
    })
    p.line('x', 'y', source=source, line_width=2, color=colors[i], legend_label=f'Lot: {lot}')
    p.scatter('x', 'y', source=source, fill_color=colors[i], size=5)

p.legend.location = "top_left"
p.legend.click_policy = "hide"
show(p)

---

📌 Interpretation:
Price increases as demand surges (due to occupancy, queues, events).

Sharp price spikes during special days are evident.

Real-time updates allow adaptive pricing.

---

🚀 Real-Time Streaming with Pathway
We used Pathway's streaming mode to simulate a new data row every second. Custom UDFs (compute_demand, price_from_demand) dynamically update prices based on incoming data.

The output is written to:
output_pathway.jsonl

Which can be consumed for downstream visualization or deployment in production systems.

---

📝 Conclusion
Model 2 introduces a real-time adaptive pricing engine using streaming data. It intelligently adjusts prices based on internal signals without relying on external APIs, making it scalable and efficient.

---