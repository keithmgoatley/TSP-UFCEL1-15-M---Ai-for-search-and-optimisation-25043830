# Solving the Traveling Salesman Problem with Hill Climbing and a Genetic Algorithm

**Module:** UFCEL1-15-M — AI for Search and Optimisation  
**Student:** Keith Goatley (25043830)

---

## Overview

This project implements and compares two search-based approaches to the Traveling Salesman Problem (TSP) on a 50-city instance:

1. **Random Restart Hill Climbing** with a **2-opt** neighbourhood. It's a single-solution local search that iteratively improves one candidate tour and restarts from a fresh random tour when the search stalls.
2. **A Genetic Algorithm** — a population-based search using Order Crossover, swap mutation, and tournament selection.

Both algorithms are evaluated on **solution quality** (tour distance), **computational efficiency** and **robustness**, and their **scalability** is compared on instances of 10, 20, 30, 40 and 50 cities.

### Headline result

Over 10 independent seeded runs on the full 50-city instance:

| Algorithm | Mean distance | Std dev | Best | Mean time |
|---|---|---|---|---|
| Random Restart Hill Climbing (2-opt) | **589.65** | 12.91 | 573.06 | ~2.1 s |
| Genetic Algorithm | 700.78 | 57.15 | 598.83 | ~15.4 s |

The difference is statistically significant under both Welch's t-test (p = 0.000137) and the Mann-Whitney U test (p = 0.000440). Hill Climbing wins on quality, speed and consistency — despite using roughly one fifth of the fitness-evaluation budget.

---

## Repository structure

```
.
├── README.md                                    Project documentation
├── UFCEL1_15_M_Ai_for_search_and_optimisation_Resit_25043830.ipynb
│                                                Main notebook (all code)
├── cities.csv 
├── hill_climbing_best_route.txt             Best tour found by Hill Climbing
├── genetic_algorithm_best_route.txt         Best tour found by the GA
├── scalability_results.csv                  Raw scalability experiment data
└── scalability_comparison.png               Scalability comparison chart
   
```

---

## Setup

**Requirements:** Python 3.9+ and Jupyter.

```bash
# Clone the repository
git clone <repo-url>
cd <repo-name>

# Install dependencies
pip install numpy pandas matplotlib scipy jupyter
```

| Library | Purpose |
|---|---|
| NumPy | Numerical operations and distance calculations |
| pandas | Loading `cities.csv`, tabulating results |
| Matplotlib | Route plots, convergence curves, comparison charts |
| SciPy | Welch's t-test and Mann-Whitney U test |

---

## Usage

```bash
jupyter notebook UFCEL1_15_M_Ai_for_search_and_optimisation_Resit_25043830.ipynb
```

Run the cells in order. The notebook is organised as:

| Section | Contents |
|---|---|
| Data loading | Reads `cities.csv`, plots the 50 city locations |
| Distance calculation | Euclidean distance and closed-tour objective function |
| Stage 1: Hill Climbing | Baseline swap neighbourhood, then the 2-opt refinement |
| Hill Climbing tuning | Stall-limit sweep with seeded repeats |
| Stage 2: Genetic Algorithm | OX crossover, swap mutation, tournament selection, elitism |
| GA tuning | Mutation-rate and population-size screening |
| Scalability | Both algorithms at 10, 20, 30, 40 and 50 cities |
| Statistical testing | Welch's t-test and Mann-Whitney U over 10 seeded runs |
| Conclusions | Discussion of results and deployment recommendations |

**Note on paths:** the notebook reads `cities.csv` and writes its route files relative to the working directory. If you move the data into `data/`, update the `load_cities()` call accordingly.

### Reproducibility

All stochastic experiments are seeded (`SEED = 42`, with each repeat run using `SEED + run_index`), so re-running the notebook reproduces the reported figures exactly.

---

## Design decisions

**Why I chose Random Restart Hill Climbing?** Simulated Annealing is sensitive to its cooling schedule, and Tabu Search adds memory overhead plus two further hyperparameters. Random restarts escape local optima with a single, intuitive hyperparameter, which is the stall limit. This makes the exploration/exploitation balance easy to control and analyse.

**Why I west with 2-opt over a swap neighbourhood?** The swap-based implementation produced tours with visible self-crossings, capping quality at 793.32. The 2-opt move reverses a segment between two edges, which removes crossings directly. Under an identical iteration budget this improved the best tour to 603.59 — a 23.9% gain from changing the neighbourhood alone.

**Why Order Crossover and tournament selection?** Single-point crossover applied to a permutation produces invalid tours, and roulette-wheel selection requires converting a minimisation objective into a maximisable fitness. OX preserves permutation validity by construction, and tournament selection operates directly on raw distances.

---

## Licensing

The `cities.csv` dataset was provided by the module for this assessment. The dependencies (NumPy, pandas, Matplotlib, SciPy) are released under permissive BSD-style licences permitting academic and commercial use.
