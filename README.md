# VoltRelay Energy — Network Performance & Service Reliability Analysis

## Overview

This project presents an evidence-based analysis of VoltRelay Energy's battery-swapping network for 2W and 3W gig and logistics riders across Bengaluru, Delhi NCR, Hyderabad, Pune, Mumbai, and Jaipur.

The analysis uses operational, station, battery, rider, support-ticket, pricing, and city-context data to evaluate network growth, service reliability, station performance, battery health, customer experience, pricing patterns, contribution-margin trends, and rider usage behavior.

The objective is to identify measurable operational patterns and translate them into actionable recommendations for improving service reliability, network efficiency, and business performance.

---

## Problem Statement

VoltRelay operates a large battery-swapping network serving high-frequency commercial riders. As the network expands, operational failures such as battery unavailability, queue abandonment, station-level reliability issues, equipment differences, and customer-support problems can affect both rider experience and network economics.

This project analyzes the available historical data to answer key business questions:

* How has network activity and failure rate changed over time?
* Which cities and stations experience higher service-failure rates?
* How do Gen1 and Gen2 chargers differ in performance?
* Are there measurable differences in station charging performance?
* Do 2W and 3W riders experience different service outcomes?
* What patterns appear in battery state of health across suppliers?
* What are the major customer-support issues?
* How have pricing and contribution-margin proxies changed?
* What operational areas should receive priority attention?

---

## Dataset

The analysis uses the following datasets provided for the hackathon:

| Dataset                        | Description                                                                                                 |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| `swap_events.csv.gz`           | Individual battery-swap attempts, outcomes, queue times, battery telemetry, pricing, and energy information |
| `station_hourly_status.csv.gz` | Hourly station availability, charging, outage, temperature, and telemetry information                       |
| `riders.csv`                   | Rider profiles, vehicle class, signup information, plans, and partner associations                          |
| `batteries.csv`                | Battery supplier, manufacturing, commissioning, health, capacity, and retirement information                |
| `support_tickets.csv`          | Customer-support interactions, issue categories, resolution times, and CSAT                                 |
| `stations.csv`                 | Station location, city, equipment generation, capacity, rent, maintenance, and connectivity information     |
| `city_daily_context.csv`       | Daily weather, disruption, holiday, event, competitor, and grid-outage context                              |
| `fleet_partners.csv`           | Partner contracts, discounts, vehicle segments, payment terms, and active cities                            |

### Dataset Scale

The primary swap-events dataset contains approximately **3.87 million swap attempts** covering:

**January 2024 – June 2025**

The analysis combines this high-volume event data with station, battery, rider, support, partner, and city-level datasets.

---

## Analytical Approach

The project follows a structured exploratory and business-analysis workflow:

1. **Data loading and validation**

   * Loaded all provided datasets.
   * Inspected dimensions, data types, missing values, duplicates, and key identifiers.
   * Verified event IDs and relationships between datasets.

2. **Data preparation**

   * Converted date/time fields to appropriate datetime formats.
   * Used categorical and numeric data types where appropriate.
   * Identified structural missing values associated with failed swap attempts.
   * Clipped small SOC/SOH telemetry values outside the physical 0–100% range for analytical calculations.

3. **Dataset integration**

   * Joined swap events with station information.
   * Combined completed swaps with battery and station cost information.
   * Connected operational data with city, vehicle, battery, and support dimensions.

4. **KPI analysis**

   * Swap attempts
   * Completed swaps
   * Failure rate
   * Revenue
   * Average revenue per completed swap
   * Queue wait time
   * Charging performance
   * Battery state of health
   * Support-ticket volume
   * CSAT
   * Contribution-margin proxy

5. **Segmentation**

   * City
   * Station
   * Charger generation
   * Firmware
   * Vehicle class
   * Battery supplier
   * Support-ticket category
   * Tariff type
   * Time period

6. **Visualization**

   * Created eight analytical visualizations to communicate the most important findings and operational patterns.

---

## Key Findings

### 1. Network activity increased substantially

Monthly swap attempts increased from approximately **110K in January 2024 to 264K in December 2024**, while completed swaps increased from approximately **105K to 253K**.

This indicates substantial network utilization growth during the period.

### 2. A significant service-failure spike occurred in April–June 2024

The network-wide failure rate reached approximately **12.27% in May 2024**, compared with approximately **4.4% during January–March 2024**.

Failure rates subsequently returned to approximately 4.2–4.4% from July onward.

### 3. Failure rates differed substantially across cities

Across the full analysis period, higher observed failure rates occurred in:

* Jaipur: **7.85%**
* Delhi NCR: **7.35%**
* Hyderabad: **6.69%**

Lower observed rates occurred in:

* Pune: **4.99%**
* Bengaluru: **4.56%**
* Mumbai: **4.45%**

The geographic differences were particularly pronounced during the May 2024 service-failure spike.

### 4. Gen1 chargers showed higher failure rates than Gen2 during May 2024

During May 2024:

* **Gen1:** 16.52% failure rate
* **Gen2:** 6.77% failure rate

Within-city comparisons also showed higher Gen1 failure rates where both generations were present.

The analysis identifies this as an operational association rather than proof of causation.

### 5. Gen1 stations showed weaker charging performance

During May 2024, Gen1 stations showed:

* Lower minimum charged-battery availability
* Longer average charging times
* Higher recorded outage minutes
* Lower minimum charged 2W and 3W battery availability

Average charging time was approximately **110 minutes for Gen1 versus 65 minutes for Gen2**.

### 6. 3W riders experienced higher service-failure rates

Across the analysis period:

* 2W failure rate: **5.42%**
* 3W failure rate: **10.35%**

Average queue wait was almost identical between the two vehicle classes, suggesting that the higher 3W failure rate cannot be explained simply by longer average queue waits.

### 7. Battery health differed across suppliers

Observed average SOH of batteries used in completed swaps varied by supplier:

| Supplier | Observed Avg. SOH |
| -------- | ----------------: |
| Kyron    |            82.02% |
| Cellora  |            89.81% |
| Amptek   |            89.84% |

These differences are observational and may reflect differences in battery age, utilization, manufacturing lots, or fleet composition.

### 8. Battery availability was the largest support-ticket category

The largest support-ticket categories included:

* `no_battery_available`
* `other`
* `low_range`
* `app_issue`
* `long_queue`

`no_battery_available` was the largest individual category, with **11,647 tickets**.

### 9. Contribution-margin proxy improved over time

The calculated contribution-margin proxy per completed swap increased from approximately:

**₹17.58 in January 2024 → ₹36.32 in June 2025**

The proxy subtracts estimated electricity costs and allocated station rent/maintenance costs from swap revenue.

It should not be interpreted as full accounting contribution margin because other operating costs are not included.

### 10. Rider retention requires high-frequency usage metrics

A conventional 30-day return metric is not particularly informative for this dataset because riders use battery-swapping services frequently.

Therefore, active-day behavior was examined as an additional indicator of rider engagement.

---

## Visualizations

The project includes eight main visualizations:

1. **Network Growth and Failure Rate**
2. **Revenue and Contribution Margin**
3. **City-Level Failure Rate**
4. **Gen1 vs Gen2 Failure Rate**
5. **Gen1 vs Gen2 Station Performance**
6. **2W vs 3W Failure Rate**
7. **Battery Supplier State of Health**
8. **Customer Support Tickets by Category**

All figures are available in:

```text
outputs/figures/
```

---

## Project Structure

```text
VoltRelay-Hackathon/
│
├── data/
│   ├── swap_events.csv.gz
│   ├── station_hourly_status.csv.gz
│   ├── riders.csv
│   ├── batteries.csv
│   ├── support_tickets.csv
│   ├── stations.csv
│   ├── city_daily_context.csv
│   └── fleet_partners.csv
│
├── notebooks/
│   └── VoltRelay_Analysis.ipynb
│
├── src/
│
├── outputs/
│   ├── figures/
│   └── tables/
│
├── report/
│
├── presentation/
│
├── video/
│
├── README.md
│
└── requirements.txt
```

---

## Technologies Used

* **Python**
* **Pandas** — data manipulation and analysis
* **NumPy** — numerical operations
* **Matplotlib** — data visualization
* **Seaborn** — statistical visualization
* **SciPy** — statistical analysis
* **Jupyter Notebook** — analysis workflow

---

## Running the Analysis

### 1. Clone or download the repository

Place the project in a local directory.

### 2. Create a virtual environment

```bash
python -m venv .venv
```

### 3. Activate the environment

Windows:

```bash
.venv\Scripts\activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Open the notebook

Open:

```text
notebooks/VoltRelay_Analysis.ipynb
```

using Jupyter Notebook or VS Code.

### 6. Run the notebook

Run the cells sequentially from top to bottom.

The notebook reads datasets from:

```text
../data/
```

and saves visualizations to:

```text
../outputs/figures/
```

---

## Methodological Notes

### Failure Rate

Failure rate is calculated as:

```text
Failure Rate =
Failed Attempts / Total Attempts × 100
```

where failed attempts include swap attempts that were not successfully completed.

### Contribution-Margin Proxy

The project uses the following operational proxy:

```text
Contribution Margin Proxy =
Swap Revenue
− Electricity Cost
− Station Rent
− Station Maintenance
```

Electricity cost is estimated using the recorded recharge energy and station grid tariff.

This metric is intended for comparative analysis rather than financial accounting.

### Telemetry Cleaning

SOC and SOH values outside the expected 0–100% range were clipped to the valid range for analytical calculations.

Missing outgoing battery and energy fields for failed swap attempts were treated as structural rather than imputed.

---

## Limitations

* The analysis is observational and does not establish causality.
* Differences between charger generations may be influenced by deployment timing, geography, station characteristics, or other operational factors.
* Battery supplier comparisons may be affected by battery age, utilization, manufacturing lots, and fleet composition.
* The contribution-margin calculation is a proxy and excludes several potential operating costs.
* Some station-level comparisons can be sensitive to sample size and operational exposure.
* Rider retention is difficult to represent using conventional return-window metrics because battery swapping is a high-frequency service.
* External factors such as weather, grid conditions, competitor activity, and local events may contribute to observed operational patterns.

---

## Deliverables

The project submission contains:

* Analytical Jupyter Notebook
* Processed analytical outputs
* Eight visualization figures
* Detailed analysis report
* Final presentation
* Project documentation

---

## AI Tool Disclosure

AI tools were used as an assistive resource during the project for tasks such as brainstorming analytical approaches, refining documentation, improving presentation structure, and assisting with code-related problem solving.

All data analysis, calculations, visualizations, findings, and conclusions were reviewed and validated against the provided hackathon datasets.

AI tools were not used to provide a pre-built analysis or replace the underlying analytical work.

---

## Author

**Ranjeet Chauhan**

B.Tech — Artificial Intelligence & Machine Learning