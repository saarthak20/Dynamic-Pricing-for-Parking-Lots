# Dynamic Parking Pricing System 🚗📈

## 🪐 Overview

This project implements **dynamic, real-time parking pricing** for 17 parking lots using **Pathway, Python, and Bokeh**, aligning with demand patterns, competitor prices, and contextual factors (traffic, vehicle type, special days).

It aims to optimize revenue while maintaining fairness and transparency in pricing, with clear visual justification for each price movement across all lots.

---

## 🚀 Models Developed

The Models have 1 day tumbling window for the live data stream but it  can be tunned from anywhere 30 minutes to 2 days to get accurate restults.

### **✅ Model 1: Linear Demand-Based Pricing**


- **Version 1:** Price increases linearly with demand:
   Price = Privous Price + alpha * Demand
  where **Demand = Occupancy / Capacity** over 30-minute windows.

- **Version 2 (Refined):** Uses **constant base price**, adjusts **only the demand-based component**:
  Price = Base Price + alpha * Demand
  yielding **more stable and realistic pricing**.

---

### **✅ Model 2: Contextual Dynamic Pricing**

Incorporates:
- **Occupancy Rate (Demand)**
- **Traffic Level (Low/Avg/High)**
- **Vehicle Type Weighting (bike, car, truck)**
- **Normalised Queue Length**
- **Special Days**

The demand formula:
Demand = alpha * (Occupancy Rate)
- gamma * (Traffic Level)
+ delta * (Special Day)
+ Vehicle Factor

Normalized and applied:
Price = Base Price * (1 + lambda * Normalized Demand)


✅ **All parameters (`base_price`, `alpha`, `gamma`, `delta`, `lambda_`) are currently hardcoded for stability during development** but can be **tuned dynamically** for smoother, highly accurate pricing adjustments in production.

---

## 📊 Visualization & Analysis

- **Bokeh** was used to generate **real-time updating line plots** for:
  - Each parking lot’s dynamic price.
  - Comparative analysis with the **nearest competitor’s dynamic price**, computed automatically by mapping each lot to its geographically closest neighbor.

- This **visually justifies pricing behavior**, showing how prices adapt with:
  - Peak demand periods.
  - Competitor pricing strategies.
  - Traffic and vehicle composition.

- **17 comparative interactive graphs** were produced, one for each parking lot, enabling clear demonstration during analysis and reporting.

---

## 🛠️ Tech Stack

- **Python**
- **Pathway** (real-time stream processing and windowing)
- **Bokeh + Panel** (interactive plotting and dashboards)
- **Pandas, NumPy** (data preprocessing)
- **Google Colab** (development environment)

---


## 🖼️ Architecture Diagram

```mermaid
flowchart LR
    A[Parking Data CSV / Live Stream] --> B[Pathway Replay CSV]
    B --> C[Preprocessing & Feature Engineering]
    C --> D[Windowing Tumbling Sliding]
    D --> E[Model 1 and Model 2 Pricing]
    E --> F[Price Data Table]
    F --> G[Bokeh Interactive Visualizations]
    G --> H[Panel Dashboard]
    F --> I[Competitor Mapping and Comparison]
    I --> G
