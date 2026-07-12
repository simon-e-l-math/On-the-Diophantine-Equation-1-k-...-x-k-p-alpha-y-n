# Computations for the article: On the Diophantine Equation $1^k + 2^k + \dots + x^k = p^{\alpha}y^n$

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.PLACEHOLDER.svg)](https://doi.org/10.5281/zenodo.PLACEHOLDER)

### Overview
This repository contains the SageMath and PARI/GP implementations used to computationally investigate near-solutions to Schäffer's conjecture. Specifically, the codebase assists in completely solving the Diophantine equation:

$$1^k + 2^k + \dots + x^k = p^\alpha y^n$$

for fixed values of $k \in \{2, 4, 5, 6, 7, 8, 9, 10, 11\}$, where $n \geq 2$, $p$ is a prime number, and $\alpha$ is a positive integer strictly less than $n$. 

### Historical & Mathematical Context
In 1875, Édouard Lucas posed the "Lucas Cannonball Problem," asking for all integer solutions to $1^2 + 2^2 + \dots + x^2 = y^2$. In 1956, Schäffer extended this to arbitrary exponents, showing that the general equation $1^k + 2^k + \dots + x^k = y^n$ has finitely many solutions outside of a few specific cases. 

This project extends the problem by searching for cases that are "near" solutions to Schäffer's conjecture in the sense of prime factorization: values of $x$ where the sum of consecutive powers is a perfect power but for one prime factor.

### Computational Methodology
Solving this equation requires an algorithmic approach. The notebooks in this repository implement:

* **Divisibility Conditions:** Applying Faulhaber's formula to express the sum of powers as a polynomial and extract divisibility conditions.
* **Elliptic Curve Reductions:** Transforming the equations for even values of $n$ into Weierstrass form to compute integral points and isolate valid values for $x$.
* **Linear Forms in Logarithms:** Applying Baker's method (via Laurent's theorem) to compute absolute upper bounds on the exponent $n$.
* **Local Methods:** Searching for auxiliary primes of the form $q = mn + 1$ to rule out integer solutions modulo $q$.
* **Unconditional Thue Equation Solvers:** Utilizing the PARI/GP `gp.thue` algorithm (with `flag=1` to ensure results do not rely on the Generalized Riemann Hypothesis) to resolve remaining low-exponent cases.

### Dependencies
* **SageMath:** Version 10.4 or higher.
* **PARI/GP:** Version 2.15.5 or higher.

### Notebook Guide & Repository Structure
To facilitate reproducibility, the codebase is divided into six sequential Jupyter Notebooks that map directly to the sections of the accompanying manuscript.

* **`01_sec2_polynomials_divisibility.ipynb`**
  Generates the Faulhaber polynomials, extracts the constant $C_k$, isolates the polynomial $T_k(x)$, and computes the divisibility conditions found in Tables 1 and 2 of Section 2.
* **`02_sec3_even_k_even_n.ipynb`**
  Implements the ad-hoc elliptic curve reductions required to solve the equation when $n$ is even (for $k \in \{4, 6, 8, 10\}$), as well as the specific binomial Thue equation resolutions for $k=2$ when $4 \mid n$.
* **`03_sec4_even_k_odd_n_pipeline.ipynb`**
  The primary orchestration pipeline for even $k$ and odd $n$. It derives linear forms in two logarithms and upper bounds thereon, reduces modulo auxiliary primes to eliminate small primes $n < n_0$, and routes surviving cases to the PARI/GP unconditional Thue solver.
* **`04_sec4_resistant_k10_cases.ipynb`**
  Resolves the five resistant cases for $k=10$ and $n=7$ that bypass standard algorithms. It factors $T_{10}(x)$ over $\mathbb{Q}(\sqrt{5})$ to generate and solve 42 distinct Thue equations, which it then solves.
* **`05_sec5_odd_k_even_n.ipynb`**
  Handles the polynomial reductions and elliptic curve mappings for odd values of $k \in \{5, 7, 9, 11\}$ when $n$ is even. Includes the verification of the sparse solutions discovered via the Pell numbers for $k=7$.
* **`06_sec6_k9_odd_n.ipynb`**
  Executes the computations required for $k=9$ when $n$ is an odd prime. Includes the Laurent's Theorem bounds, auxiliary prime reductions, and the additional Thue equations required to solve for low exponents ($n \leq 7$).

### Citing This Work
If you use this code in your own research, please cite the accompanying paper and the Zenodo archive.

**The Manuscript:**
```bibtex
@article{earplynch2026cannonball,
  title={On the Diophantine Equation $1^k + 2^k + \dots + x^k = p^{\alpha}y^n$},
  author={Earp-Lynch, Benjamin and Earp-Lynch, Simon and Kihel, Omar},
  journal={Preprint},
  year={2026},
  URL={tbd}
}
```

**The Code (Zenodo DOI):**
```bibtex
@software{earplynch_cannonball_code_2026,
  author       = {Earp-Lynch, Benjamin and Earp-Lynch, Simon and Kihel, Omar},
  title        = {Computations for the article: On the Diophantine Equation $1^k + 2^k + \dots + x^k = p^{\alpha}y^n},
  month        = {July},
  year         = {2026},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.PLACEHOLDER},
  url          = {[https://doi.org/10.5281/zenodo.PLACEHOLDER](https://doi.org/10.5281/zenodo.PLACEHOLDER)}
}
```

### Acknowledgments
This code relies on the open-source mathematical software ecosystem. We thank the developers of **SageMath** and **PARI/GP** for their tools.  These scripts have been reformatted from the versions used in the PhD thesis of the second author.  Those preliminary versions can be found at the following URL: 
https://cocalc.com/share/public_paths/d6cf03380b3172df1d992f2a612b2737f4f8e2ba