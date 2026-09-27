# Assignment 1 — Git, NumPy & Pandas

This repository contains my solutions for Assignment 1, covering Git, NumPy, and Pandas.

## Project Structure

```text
assignment-1/
├── answers/
│   ├── 01_git_theory.md
│   ├── 02_numpy.py
│   └── 03_pandas.ipynb
├── data/
│   ├── make_data.py
│   └── scores_raw.csv
├── outputs/
│   └── summary.csv
├── .gitignore
├── requirements.txt
└── README.md
```

## Topics Covered

* Git concepts and commands
* NumPy arrays, indexing, slicing, masking, broadcasting, vectorization, and statistics
* Pandas Series and DataFrames
* Data cleaning and missing values
* Duplicate removal
* Date handling
* GroupBy and pivot tables
* Data export to CSV

## How to Run

1. Create and activate a Python virtual environment.
2. Install the required packages:

```bash
pip install -r requirements.txt
```

3. Run the NumPy solution:

```bash
python answers/02_numpy.py
```

4. Open `answers/03_pandas.ipynb` in Jupyter Notebook or VS Code and run all cells.

## Output

The Pandas analysis produces:

```text
outputs/summary.csv
```

This file contains the subject-wise summary generated in Part C.
