# Air Quality NO₂ Transformation and Probability Density Estimation

## Project Overview

This project analyzes NO₂ air quality data using a roll-number-parameterized nonlinear transformation and estimates the parameters of a probability density function. The objective is to transform the original dataset and learn the parameters of a Gaussian-style density model using statistical estimation.

Dataset source:  
https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data

---

## Roll Number Based Parameters

University Roll Number: **102303254**

The transformation parameters are defined as:

\[
a_r = 0.05 \times (r \bmod 7)
\]

\[
b_r = 0.3 \times ((r \bmod 5) + 1)
\]

For r = 102303254:

- r mod 7 = 1 → aᵣ = **0.05**
- r mod 5 = 4 → bᵣ = **1.5**

Final transformation applied:

\[
z = x + 0.05 \sin(1.5x)
\]

where x represents the NO₂ concentration.

---

## Methodology

### 1. Data Loading and Cleaning

- The dataset is loaded from `data.csv`
- Encoding is set to `latin1` to prevent Unicode decoding errors
- Column names are cleaned to remove extra spaces
- The NO₂ column is automatically detected in a case-insensitive manner
- Non-numeric and missing values are removed

This ensures only valid numerical samples are processed.

---

### 2. Nonlinear Transformation

Each NO₂ value \(x_i\) is transformed using:

\[
z_i = x_i + a_r \sin(b_r x_i)
\]

This produces a new transformed dataset z.

---

### 3. Probability Density Estimation

We model the transformed data using:

\[
\hat p(z) = c e^{-\lambda (z-\mu)^2}
\]

The parameters are estimated as:

- μ = mean of z
- variance = variance of z
- λ = 1 / (2 × variance)
- c = 1 / √(2π × variance)

These values summarize the learned probability distribution.

---

## Results

### Result Table

The computed parameters are stored in:

```
results/result_table.csv
```

The table contains:

- roll number
- aᵣ and bᵣ
- μ
- variance
- λ
- c
- number of samples used
- detected NO₂ column name

---

### Result Graph

Saved at:

```
results/result_graph.png
```

The graph includes:

- Histogram of transformed values z
- Fitted probability density curve
- Visual comparison of empirical vs modeled distribution

This validates the accuracy of the estimation.

---

## Project Structure

```
Air-Quality-NO2-transform/
│── Probability Density Functions.py
│── README.md
│── requirements.txt
│── results/
│     ├── result_table.csv
│     └── result_graph.png
```

---

## How to Run the Project

### Step 1 — Install dependencies

```
pip install -r requirements.txt
```

### Step 2 — Place dataset

Download the dataset from Kaggle and save as:

```
data.csv
```

inside the project folder.

### Step 3 — Execute the program

```
Probability Density Functions.py
```

---

## Output Files

Running the program generates:

```
results/result_table.csv
results/result_graph.png
```

These contain the final parameter estimates and visualization.

---

## Notes

- The program automatically detects the NO₂ column
- Handles encoding issues safely
- Removes missing values
- Uses roll-number-based reproducible parameters

---

## Conclusion

This project demonstrates:

- Real-world dataset preprocessing
- Nonlinear mathematical transformation
- Statistical density estimation
- Model fitting and validation

The estimated probability density function closely approximates the transformed NO₂ distribution, confirming the effectiveness of the methodology.


