# Improved NSGA-II

An improved implementation of NSGA-II (Non-dominated Sorting Genetic Algorithm II) with modern optimization techniques for solving multi-objective optimization problems.

> Vietnamese translation: see [README.vi.md](README.vi.md).

## Table of Contents

- [Overview](#overview)
- [Key Improvements](#key-improvements)
- [Experimental Results](#experimental-results)
- [Algorithm Complexity](#algorithm-complexity)
- [Installation](#installation)
- [Usage](#usage)
- [References](#references)

## Overview

Improved NSGA-II is an enhanced version of the classic NSGA-II algorithm, designed to improve:

- **Solution quality**: Better convergence toward the true Pareto front
- **Diversity**: More uniform distribution of solutions on the Pareto front
- **Performance**: Faster convergence with fewer generations
- **Exploration ability**: Reduced risk of getting trapped in local optima

## Key Improvements

### 1. Opposition-Based Learning (OBL)

- **Purpose**: Improve initial population quality
- **Method**: For each random individual `x`, generate an opposite individual `x_opp = lb + ub - x`
- **Benefit**: Increases search-space exploration from the start and reduces required generations to converge

### 2. Adaptive Mutation Probability

- **Formula**: `pm(t) = pm_max - (pm_max - pm_min) × (t / T)`
- **pm_max**: 0.3 (early generations - stronger exploration)
- **pm_min**: 0.05 (late generations - stronger exploitation)
- **Benefit**: Balances exploration and exploitation over time

### 3. Simulated Binary Crossover (SBX)

- **Parameter**: `eta_c = 20` (distribution index)
- **Characteristic**: Offspring tend to stay close to parents, suitable for continuous optimization
- **Benefit**: Produces high-quality variants from good solutions

### 4. Polynomial Mutation

- **Parameter**: `eta_m = 20` (distribution index)
- **Characteristic**: Mutation magnitude gradually decreases near optimal solutions
- **Benefit**: Effective fine-tuning in later stages

### 5. Tournament Selection

- **Tournament size**: 2
- **Criterion**: Prefer lower rank, then larger crowding distance
- **Benefit**: Maintains moderate selection pressure while preserving diversity

## Experimental Results

### Comparison with Other Algorithms

Improved NSGA-II is compared with the following advanced algorithms:

- **NSGA-II**: Original baseline version (Deb et al., 2002)
- **RNSGA-II**: Reference-point based NSGA-II
- **DNSGA-II**: Dynamic NSGA-II
- **MOPSO-CD**: Multi-Objective Particle Swarm Optimization with Crowding Distance

### Results on the ZDT Benchmark Suite

| Problem   | Rating                      | Details                                                       |
| --------- | --------------------------- | ------------------------------------------------------------- |
| **ZDT1**  | ⭐⭐⭐⭐⭐ **Best overall**    | Low IGD, high HV, fast and stable convergence                |
| **ZDT2**  | ⭐⭐⭐⭐⭐ **Best overall**    | Strong balance between convergence quality and diversity      |
| **ZDT3**  | ⭐⭐⭐⭐ **Best HV**          | Outstanding Pareto-front coverage in terms of hypervolume    |
| **ZDT4**  | ⭐⭐⭐⭐⭐ **Best overall**    | High effectiveness on many-local-optima landscapes           |
| **ZDT6**  | ⭐⭐⭐⭐⭐ **Best overall**    | Handles uneven Pareto fronts and nonlinear search spaces well |

### Evaluation Metrics

- **IGD (Inverted Generational Distance)**: Average distance from the true Pareto front to the approximated set
  - _Lower is better_
  - Improved NSGA-II gives the strongest results on ZDT1, ZDT2, ZDT4, and ZDT6

- **HV (Hypervolume)**: Volume of objective space dominated by the solution set
  - _Higher is better_
  - Improved NSGA-II achieves strong HV across the full ZDT suite, and is best on ZDT3

- **Stability**: Standard deviation across multiple runs
  - ZDT1, ZDT2, ZDT4, ZDT6: Most stable with best overall results
  - ZDT3: Particularly strong in HV

### Main Strengths

- [x] **High solution quality**: Best results on ZDT1, ZDT2, ZDT4, and ZDT6
- [x] **Excellent coverage**: Very high HV, especially on ZDT3
- [x] **Strong exploration**: Performs well on ZDT4 (many local optima)
- [x] **Adaptivity**: OBL and adaptive mutation accelerate convergence
- [x] **Diversity preservation**: Maintains good spread on complex Pareto fronts

## Algorithm Complexity

### Time Complexity

Given population size $N$ and number of objectives $M$:

| Component              | Complexity              | Explanation                                      |
| ---------------------- | ----------------------- | ------------------------------------------------ |
| **OBL Initialization** | $O(N \cdot n_{var})$    | Generate $N$ individuals and $N$ opposite ones   |
| **Non-dominated Sort** | $O(M \cdot N^2)$        | Fast Non-dominated Sort algorithm (Deb)          |
| **Crowding Distance**  | $O(M \cdot N \log N)$  | Sort by each objective                           |
| **Selection**          | $O(N)$                  | Tournament selection                             |
| **Crossover**          | $O(N \cdot n_{var})$    | SBX for each parent pair                         |
| **Mutation**           | $O(N \cdot n_{var})$    | Polynomial mutation                              |
| **Evaluation**         | $O(N \cdot T_{eval})$   | $T_{eval}$ = evaluation time per individual      |

**Total per generation**: $O(M \cdot N^2 + N \cdot n_{var} + N \cdot T_{eval})$

In practice:

- If $T_{eval}$ is small (simple objective functions): dominant cost is **Non-dominated Sort** $O(M \cdot N^2)$
- If $T_{eval}$ is large (complex simulations): dominant cost is **Evaluation** $O(N \cdot T_{eval})$

### Space Complexity

$O(N \cdot (n_{var} + M))$

- Population storage: $N$ individuals
- Each individual: $n_{var}$ decision variables + $M$ objective values
- Metadata: rank, crowding distance

### Comparison with Original NSGA-II

| Algorithm              | Time / Generation | Space          | Notes                  |
| ---------------------- | ----------------- | -------------- | ---------------------- |
| NSGA-II                | $O(M \cdot N^2)$  | $O(N \cdot M)$ | Baseline               |
| **Improved NSGA-II**   | $O(M \cdot N^2)$  | $O(N \cdot M)$ | No asymptotic increase |

**Conclusion**: The improvements (OBL, adaptive mutation) do not increase asymptotic complexity, only small constant overhead.

## Installation

### System Requirements

- Python 3.8+
- pip or conda

### Install Dependencies

```bash
# Clone repository (if available)
git clone <repository-url>
cd source_code

# Install required dependencies
pip install -r requirements.txt
```

### Main Libraries

- `numpy`: Numerical computing and arrays
- `pandas`: Data processing and result export
- `matplotlib`: Plotting
- `seaborn`: Advanced visualization
- `pymoo`: Multi-objective optimization framework (provides ZDT/DTLZ benchmark suites)
- `tabulate`: Pretty console tables

## Usage

```bash
# Run with population 100, 200 generations, 10 runs
python benchmark.py --pop 100 --gen 200 --runs 10

# Run with larger population and more generations
python benchmark.py --pop 200 --gen 300 --runs 20

# Run DTLZ benchmark suite (3 objectives)
python benchmark.py --suite dtlz --pop 150 --gen 250
```

### Command-Line Arguments

| Argument  | Default | Description                                 |
| --------- | ------- | ------------------------------------------- |
| `--suite` | `zdt`   | Benchmark suite: `zdt` or `dtlz`            |
| `--pop`   | `100`   | Population size                             |
| `--gen`   | `200`   | Maximum number of generations               |
| `--runs`  | `10`    | Number of repeated runs (for mean ± std)    |
| `--seed`  | `42`    | Base random seed                            |

### Output

After execution, you will get:

1. **Convergence plots**: IGD, HV over generations + 2D/3D Pareto front
   - Displays the true Pareto front (black curve)
   - Displays NSGA-II front (hollow red markers)

2. **Boxplots**: IGD and HV distributions across all problems

3. **Summary table** (console): Mean ± std for IGD, HV, and time

4. **CSV files**:
   - `benchmark_raw.csv`: Raw data for each run
   - `benchmark_summary.csv`: Aggregated results (mean, std)

### Use in Python Code

```python
from nsga2_improved import NSGA2ImprovedSmart, ProblemWrapper
from pymoo.problems import get_problem
import numpy as np

# Define the problem
problem = get_problem("zdt1", n_var=30)
wrapper = ProblemWrapper(problem)

# Initialize the algorithm
solver = NSGA2ImprovedSmart(wrapper, pop_size=100, n_gen=200)

# Run the algorithm
pareto_front = solver.run()

# Results
print(f"Number of Pareto solutions: {len(pareto_front)}")
print(f"Objective values:\n{pareto_front}")
```

## References

1. **Deb, K., et al. (2002)**  
   _"A fast and elitist multiobjective genetic algorithm: NSGA-II"_  
   IEEE Transactions on Evolutionary Computation, 6(2), 182-197.  
   Link: https://doi.org/10.1109/4235.996017

2. **Tizhoosh, H. R. (2005)**  
   _"Opposition-based learning: A new scheme for machine intelligence"_  
   International Conference on Computational Intelligence for Modelling, Control and Automation.  
   Link: https://ieeexplore.ieee.org/abstract/document/1631345/

3. **Deb, K., & Agrawal, R. B. (1995)**  
   _"Simulated binary crossover for continuous search space"_  
   Complex Systems, 9(2), 115-148.  
   Link: https://www.complex-systems.com/abstracts/v09_i02_a02/

4. **Zitzler, E., et al. (2000)**  
   _"Comparison of multiobjective evolutionary algorithms: Empirical results"_  
   Evolutionary Computation, 8(2), 173-195.  
   Link: https://doi.org/10.1162/106365600568202

5. **Deb, K., Thiele, L., Laumanns, M., & Zitzler, E. (2005)**  
   _"Scalable test problems for evolutionary multiobjective optimization"_  
   Evolutionary Multiobjective Optimization, 105-145.  
   Link: https://doi.org/10.1007/1-84628-137-7_6

6. **Zitzler, E., Knowles, J., & Thiele, L. (2008)**  
   _"Quality assessment of Pareto set approximations"_  
   Multiobjective Optimization, 373-404.  
   Link: https://doi.org/10.1007/978-3-540-88908-3_14

7. **Ishibuchi, H., Masuda, H., Tanigaki, Y., & Nojima, Y. (2015)**  
   _"Modified distance calculation in generational distance and inverted generational distance"_  
   EMO 2015, Part I, LNCS 9018, 110-125.  
   Link: https://doi.org/10.1007/978-3-319-15892-1_8

8. **Blank, J., & Deb, K. (2020)**  
   _"pymoo: Multi-objective optimization in Python"_  
   IEEE Access, 8, 89497-89509.  
   Link: https://ieeexplore.ieee.org/abstract/document/9078759/

## License

MIT License - Free to use for research and commercial purposes.

## Contact

If you have questions or issues, please open an Issue on GitHub.

---

**Improved NSGA-II** - Effective multi-objective optimization for the 21st century.
