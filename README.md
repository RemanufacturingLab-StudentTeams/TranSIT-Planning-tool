# TranSIT Planning Tool

A job shop scheduling optimization toolkit implementing genetic algorithms and mixed-integer programming (MIP) to minimize makespan while meeting delivery deadlines.

## Overview

This repository contains algorithms for solving the **Job Shop Scheduling Problem (JSSP)** - a classic NP-hard combinatorial optimization problem. The goal is to schedule jobs across machines such that:

1. Products are delivered before their deadline
2. The time between delivery and deadline is minimized (minimizing makespan)

## Features

- **Genetic Algorithm (GA)** implementation for large-scale instances
- **Mixed-Integer Programming (MIP)** solver using Gurobi for optimal solutions
- **Multiple dispatching rules** for initial solution generation:
  - SPT (Shortest Processing Time)
  - SRPT (Shortest Remaining Processing Time)
  - Completion Rate heuristic
  - Random shuffle
- **Crossover operators**: Random crossover and block crossover
- **Mutation operators**: Swap, inversion, and rotation mutations
- **Visualization**: Gantt charts for schedule visualization
- **Benchmark datasets**: Standard JSSP test instances included

## Repository Structure

```
TranSIT-Planning-tool/
├── README.md
├── Planningtool-WvL/
│   ├── Demo GA.ipynb          # Main algorithm implementation
│   ├── README.md
│   └── Test datasets/         # Benchmark problem instances
│       ├── README.md
│       ├── ft20csv.csv        # Fisher & Thompson instance
│       ├── la01csv.csv        # Lawrence instances
│       ├── la06csv.csv
│       ├── la31csv.csv
│       ├── la32csv.csv
│       ├── la33csv.csv
│       ├── la34csv.csv
│       ├── la35csv.csv
│       ├── sw01csv.csv        # Storer & Wu instances
│       ├── sw02csv.csv
│       └── ta01csv.csv        # Taillard instance
```

## Requirements

- Python 3.x
- pandas
- numpy
- matplotlib
- gurobipy (requires Gurobi license)

## Usage

Open the Jupyter notebook `Planningtool-WvL/Demo GA.ipynb` to:

1. Load benchmark datasets
2. Solve instances using MIP (exact solution for small problems)
3. Apply genetic algorithm for larger instances
4. Visualize results with Gantt charts

### Quick Start

```python
# Load a dataset
jobs, machines, V, pro, pr = Orders('la01')

# Create initial population
population = create_pop(16, jobs, machines, V, pro, pr)

# Run genetic algorithm
solution, timeline = GA(population, iterations=1000, ...)

# Visualize result
gantt(Ganttmodel(solution[0][1]))
```

## Algorithm Details

### Genetic Algorithm Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| P | Population size | 16 |
| g | Number of iterations | 1000 |
| Cp | Crossover type (0=random, 1=block) | 1 |
| Mu | Mutation probability | 0.5 |
| El | Elitism rate | 0.2 |

### Solution Representation

Solutions are represented as a list of machine orderings, where each sublist contains the sequence of jobs to be processed on that machine.

## Benchmark Results

The algorithm has been tested on standard JSSP benchmark instances:

| Instance | Size (Jobs x Machines) | Optimal Makespan |
|----------|------------------------|------------------|
| ft06 | 6 x 6 | 55 |
| ft20 | 20 x 5 | 1165 |
| la01 | 10 x 5 | 666 |
| sw01 | 20 x 10 | 1407 |
| la31 | 30 x 10 | 1784 |

## Author

Algorithm developed by W. van Leur (Mathematics BSc student)

## License

Academic use - see repository for details.
