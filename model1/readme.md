## Model 1: Occupancy-Based Pricing Strategy

### 🧠 Objective
This model implements a simple yet effective **occupancy-based dynamic pricing strategy**, where the parking price adjusts over time based on the occupancy level of each lot. It is a baseline model and **does not require real-time streaming** or Pathway integration.

### 📊 Pricing Logic
For each parking lot:
- Price starts at a `BASE_PRICE` of ₹10.
- At each timestamp, the price is updated based on the **occupancy ratio** (Occupancy / Capacity) using the formula:

\[
\text{Price}_t = \text{Previous Price} + \alpha \cdot \left(\frac{\text{Occupancy}}{\text{Capacity}}\right)
\]

- `α` (alpha) is a sensitivity constant (set to 2.0 in this model).
- If capacity is 0, the previous price is retained.

### 🔁 Temporal Smoothing
- This model **retains memory of previous price** to avoid sudden fluctuations.
- Suitable for environments where gradual price changes are preferred.

### 📈 Visualization
- Bokeh is used to plot price trends over time for 3 parking lots.
- The plots show how price evolves based on changing occupancy levels.

### ✅ Key Features
- No external streaming or real-time framework used.
- Uses `pandas` for preprocessing and pricing logic.
- Ideal for comparing against more complex models like Model 2 (Pathway-based).

### ⚠️ Limitations
- Not suitable for real-time deployment.
- Ignores external features like traffic, vehicle type, or special days.

