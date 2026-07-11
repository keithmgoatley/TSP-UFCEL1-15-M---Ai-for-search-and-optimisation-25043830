# UFCEL1_15_M_Ai for search and optimisation - 25043830

## Overview

The project looks at the **Travelling Salesman Problem** using a dataset of 50 cities. 

Two optimisation approaches are implemented and compared:

- Hill Climbing
- Genetic Algorithm

My aim was to evaluate both in terms of solution quality, the computational efficiency, any convergence behaviour, and their ability to scale. 

## Contents

- `UFCEL1_15_M_Ai_for_search_and_optimisation_Resit_25043830.ipynb`
- `cities.csv` 
- `hill_climbing_best_route.txt` 
- `genetic_algorithm_best_route.txt` 
- `README.md` - project overview and usage instructions

## Structure

The notebook includes the following stages:
- Loading and visualising the city dataset.
- Defining the route distance objective function.
- Implementing Hill Climbing using a 2-opt style neighbourhood search.
- Implementing a Genetic Algorithm for population-based optimisation.
- Plotting the best route found by each algorithm.
- Saving the best route from each algorithm to external text files.
- Running scalability tests on different problem sizes.

## How to Run

- Download or clone the repository.
- Open the notebook in **Google Colab** or **Jupyter Notebook**.
- Add the `cities.csv` in the same working directory as the notebook.
- Run the notebook cells in order from top to bottom.
- View the route visualisations, and saved route files.

## Outputs

Running the notebook produces:

- the visualisation of the 50 city locations
- the best-route plot for Hill Climbing
- the best-route plot for the Genetic Algorithm
- a saved route text files for both methods
- the scalability comparison results and plots

## Scalability Testing

The project tests both algorithms on subsets of the dataset with:

- 10 cities
- 20 cities
- 30 cities
- 40 cities
- 50 cities

This then helps compare how each method performs as problem size increases.

## Purpose

The projct shows the application of search and optimisation techniques to the TSP. It shows outputs by saving final routes created by both algorithms. 

------------

Keith Goatley  
Student Number: 25043830
