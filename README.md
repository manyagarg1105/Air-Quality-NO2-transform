# Air Quality NO2 Transformation & PDF Estimation

## Overview

This project uses the NO₂ column from the “India Air Quality Data” dataset and applies a roll-number-based transformation:
[
z = x + a_r \sin(b_r x)
]
After transformation, we estimate the parameters (\lambda), (\mu), and (c) for the density model:
[
\hat p(z) = c e^{-\lambda (z-\mu)^2}
]

## Roll Number Parameters

Roll Number: **102303254**

[
a_r = 0.05 \times (r \bmod 7)
]
[
b_r = 0.3 \times ((r \bmod 5) + 1)
]

For **r = 102303254**:

* (r \bmod 7 = 1 \Rightarrow a_r = 0.05)
* (r \bmod 5 = 4 \Rightarrow b_r = 1.5)

So the final transformation used is:
[
z = x + 0.05\sin(1.5x)
]

## Methodology

### 1. Data Loading & Cleaning

* The dataset is read from `data.csv`.
* Column names are stripped of extra spaces.
* The NO₂ column is automatically detected by searching for `"no2"` (case-insensitive).
* Values are converted to numeric and missing values are removed.

### 2. Transformation (x → z)

Each valid NO₂ sample (x_i) is transformed into (z_i) using:
[
z_i = x_i + a_r \sin(b_r x_i)
]

### 3. Parameter Estimation for (\hat p(z))

We model (\hat p(z)) as:
[
\hat p(z) = c e^{-\lambda (z-\mu)^2}
]

To estimate parameters:

* (\mu) is taken as the mean of (z)
* variance is computed from (z)
* (\lambda = \frac{1}{2 \cdot \text{variance}})
* (c = \frac{1}{\sqrt{2\pi \cdot \text{variance}}})

These values are stored in a result table.

## Results

### Result Table

The result table is saved at:

* `results/result_table.csv`

It includes:

* roll_number
* a_r, b_r
* mu
* variance
* lambda
* c
* NO2 column used
* number of samples used

### Result Graph

The plot is saved at:

* `results/result_graph.png`

The graph contains:

* Histogram of transformed values (z) (empirical PDF approximation)
* Overlay curve of the fitted model (\hat p(z) = c e^{-\lambda(z-\mu)^2})

## How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Keep the dataset as

Place the dataset in the same folder and name it:

* `data.csv`

### 3. Run

```bash
python main.py
```

### Output files generated

* `results/result_table.csv`
* `results/result_graph.png`

## Notes

* If the dataset uses a different encoding, this code reads using `latin1` to avoid UnicodeDecodeError.
* If NO₂ column name differs, the code automatically detects it as long as it contains `no2`.
