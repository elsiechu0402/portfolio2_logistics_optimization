# Logistics Optimization for Cost-Efficient E-Commerce Distribution Decisions

## Project Summary

This project develops a logistics optimization framework for e-commerce distribution decisions using the Brazilian E-Commerce Public Dataset by Olist. It compares a simple nearest-center baseline policy with a capacity-constrained transportation allocation model.

The baseline policy achieves shorter distance but violates fulfillment capacity constraints. The optimized model eliminates all capacity violations and excess demand by reallocating customer-zone demand across candidate fulfillment centers.

---

## Research Question

**How can optimization models support cost-efficient e-commerce distribution decisions by allocating customer demand zones to fulfillment centers under distance and capacity constraints?**

---

## Project Highlights

- Built an end-to-end logistics optimization workflow using real public e-commerce data.
- Constructed customer demand zones from city-state-level customer locations.
- Constructed candidate fulfillment centers from high-volume seller zip-code locations.
- Calculated customer-center distance using geolocation data.
- Compared a nearest-center baseline with a capacity-constrained allocation model.
- Conducted capacity sensitivity analysis to evaluate how fulfillment capacity affects transportation cost and service distance.

---

## Data and Optimization Setting

| Component | Value |
|---|---:|
| Customer demand zones | 30 |
| Candidate fulfillment centers | 12 |
| Selected customer demand | 51,291 |
| Main-scenario total capacity | 56,421 |
| Main capacity buffer | 1.10 |

Candidate fulfillment centers are constructed from seller zip-code locations. They are used as potential fulfillment nodes for optimization modeling.

---

## Methodology

### Baseline Policy

The baseline policy assigns each customer demand zone to the nearest fulfillment center based only on geographic distance.

This rule is simple, but it ignores fulfillment center capacity.

### Optimized Policy

The optimized policy uses a capacity-constrained transportation allocation model.

The model minimizes total distance-weighted transportation cost while satisfying two constraints:

1. Each customer demand zone's full demand must be served.
2. Each fulfillment center's assigned demand cannot exceed its capacity.

Because each customer zone represents aggregated order volume, demand from one zone can be split across multiple fulfillment centers.

---

## Key Results

| Metric | Baseline | Optimized |
|---|---:|---:|
| Total transportation cost | 15,115,364.07 | 17,701,059.42 |
| Weighted average distance | 294.70 km | 345.11 km |
| Capacity violated centers | 4 | 0 |
| Total excess demand | 26,201 | 0 |
| Maximum utilization rate | 6.08 | 1.00 |

The optimized policy increased transportation cost by **17.11%**, but it reduced capacity violated centers from **4 to 0** and total excess demand from **26,201 to 0**.

This result shows that the lowest-distance logistics policy is not necessarily operationally feasible once capacity constraints are included.

---

## Results Figures

### Total Transportation Cost

![Total Transportation Cost](assets/figures/fig_01_total_transportation_cost.png)

### Weighted Average Distance

![Weighted Average Distance](assets/figures/fig_02_weighted_avg_distance.png)

### Total Excess Demand

![Total Excess Demand](assets/figures/fig_03_excess_demand.png)

### Optimized Fulfillment Center Utilization

![Optimized Fulfillment Center Utilization](assets/figures/fig_04_optimized_capacity_utilization.png)

---

## Capacity Sensitivity Analysis

The capacity sensitivity analysis tests capacity buffers from 1.00 to 1.30.

As the capacity buffer increases, total transportation cost and weighted average distance decline. This suggests that additional fulfillment capacity improves routing flexibility and allows the model to allocate more demand to closer centers.

| Capacity Buffer | Total Transportation Cost | Weighted Avg Distance |
|---:|---:|---:|
| 1.00 | 18,415,335.87 | 359.04 km |
| 1.30 | 16,345,438.15 | 318.68 km |

The cost reduction from buffer 1.00 to 1.30 is **2,069,897.72**, and the weighted average distance reduction is **40.36 km**.

### Transportation Cost under Different Capacity Buffers

![Capacity Buffer Cost](assets/figures/fig_05_capacity_buffer_cost.png)

### Weighted Average Distance under Different Capacity Buffers

![Capacity Buffer Distance](assets/figures/fig_06_capacity_buffer_distance.png)

### Fulfillment Center Utilization under Different Capacity Buffers

![Capacity Buffer Utilization](assets/figures/fig_07_capacity_buffer_utilization.png)

---

## Operational Interpretation

The nearest-center baseline is distance-efficient but capacity-infeasible. It overloads several nearby fulfillment centers.

The optimized allocation model produces a feasible logistics plan by redistributing demand across centers while respecting capacity constraints. This increases cost compared with the nearest-center rule, but it removes all excess demand and capacity violations.

This is a practical operations research trade-off: a solution that looks cheaper under a simple rule may not be feasible under real operational constraints.

---

## Limitations

This project uses public e-commerce data and constructed assumptions. The Olist dataset does not provide real warehouse capacity, actual warehouse locations, or true transportation cost parameters.

Therefore:

- Candidate fulfillment centers are constructed from high-volume seller zip-code locations.
- Capacity is estimated using historical seller order volume and a buffer assumption.
- Transportation cost is represented as a distance-weighted cost unit.
- Straight-line geographic distance is used instead of road network distance.

The project is intended as an applied logistics optimization demonstration, not as a reconstruction of Olist's real logistics network.

---

## Files

- Final report: `report/final_report.md`
- Figures: `outputs/figures`
- Tables: `outputs/tables`
- Notebooks: `notebooks`
- Processed data: `data/processed`

---

## Tools Used

- Python
- pandas
- NumPy
- matplotlib
- PuLP
- Jupyter Notebook
