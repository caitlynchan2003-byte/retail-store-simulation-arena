# Teja Fresh Mart: Discrete Event Simulation (Arena)

An expanded discrete event simulation (DES) of Teja Fresh Mart (TFM), a retail store in Bukit Kayu Putih, built in Rockwell Arena. It tests how fixed versus flexible staffing affects customer waiting, lost customers and staff utilisation.

This was a group assignment (Group 9) for SQQPK3033 Computer Modeling in Business at Universiti Utara Malaysia, Semester 1 2025/2026. The model in this repository is the **what-if scenario**, where the number of workers is fixed at 2 for the whole 24-hour cycle.

## Background

TFM sells fresh produce, bakery items, household goods, butchery, deli and dairy products. The fresh produce section, the butchery and the payment counter get the most customers, so the model focuses on these three areas. An earlier basic model simulated one customer type and up to 120 customers. This expanded version makes the store more realistic and lets us test staffing strategies.

## What the model includes

- **Multiple customer types:** produce only, butchery only, or both
- **Scheduled arrivals:** separate peak and off-peak arrival rates over a 24-hour cycle
- **Worker scheduling:** staff numbers change by shift in the basic model
- **Entrance screening and store capacity:** customers who fail screening, or who find the store full and will not wait, are lost
- **Balking:** customers leave if the produce or butchery queue is full
- **Re-entry loop:** 5% of customers are unsatisfied at the payment counter and restart the process
- **Cycle time tracking:** time spent in the produce section, the butchery and the whole store is recorded
- **Animations:** customers move visibly between stations

## Model flow

1. Customers arrive and pass entrance screening, then the store capacity check
2. Each customer is assigned a shopping list (produce, butchery or both)
3. They are routed to the fresh produce and/or butchery station, then to the payment counter
4. They leave through the exit, where their cycle times are recorded

![Entrance and shopping list flow](screenshots/model_entrance_flow.png)

![Station flow](screenshots/model_station_flow.png)

*The flowcharts above are from the basic model. The what-if model uses the same logic and only the staffing differs.*

## Experiment

| | Basic model | What-if model (this file) |
|---|---|---|
| Staffing | Flexible schedule that follows arrivals | 2 workers all day, in every section |
| Run length | 3 days (4,320 minutes) | 3 days (4,320 minutes) |

I verified the model by checking that the schedules repeat correctly over the 3-day run and that entity flow and resource logic behave as intended. I validated it by comparing it with the basic model, which could only handle 120 customers. The expanded model handled a full 4,320-minute run with variable loads, without crashes or endless queue growth.

## Results

Averages across replications [add the number of replications, found in Run > Setup in Arena].

| Measure | Basic model | What-if model | Change |
|---|---|---|---|
| Customers served | 364.0 | 373.8 | +9.8 |
| Average time in system | 19.56 min | 17.16 min | -2.40 min |
| Average waiting time | 4.62 min | 2.11 min | -2.51 min |
| Maximum waiting time | 746.16 min | 716.07 min | -30.09 min |
| Cashier utilisation | 45.86% | 47.71% | +1.85% |
| Fresh produce utilisation | 20.95% | 21.89% | +0.94% |
| Butchery utilisation | 23.39% | 23.79% | +0.40% |
| Lost customers | 16.8 (about 17) | 18.2 (about 18) | +1 |

## Findings and recommendation

Fixed staffing served slightly more customers and lowered the average total time and the average waiting time. However, maximum waits stayed above 700 minutes in both scenarios and lost customers rose slightly. This shows the queue builds up during peak periods, and one or two cashiers cannot clear it.

My group's recommendations for TFM:

- Keep a variable staffing schedule that matches arrival patterns, instead of fixed staffing
- Move staff from the quieter butchery and fresh produce sections to the payment counter when its queue passes four customers
- Reduce lost customers by adding payment queue space or self-service kiosks for peak periods

## Limitations

- Several assumptions were made, including the 5% dissatisfaction rate and consistent transfer times between stations
- Only the produce, butchery and payment sections are modelled, not the rest of the store
- The two scenarios are close on several measures, and the group report does not include a statistical test of the difference, so the comparison is indicative

## How to open the model

1. Install Rockwell Arena (version 16.20 or later).
2. Download the `.doe` file from this repository and open it in Arena.
3. Choose **Run > Setup** to check the run length and number of replications, then press **Go** to run the simulation.

## My contribution

[Describe what you personally did in this group project, for example building part of the model, running the experiments, analysing the output or writing sections of the report. Be specific.]

## Tools

Rockwell Arena 16.20, discrete event simulation, input distributions (Weibull, triangular), resource scheduling, what-if and sensitivity analysis

## Files

- `retail_store_fixed_workers.doe` - Arena model (what-if scenario, 2 workers all day)
- `screenshots/` - model flowcharts

## Author

Caitlyn Chan Rou Qian
[LinkedIn](https://linkedin.com/in/caitlyn-chan-385584384)
