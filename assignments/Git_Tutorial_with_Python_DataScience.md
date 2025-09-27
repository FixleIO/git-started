# Git Tutorial: Building a Simple Data Analysis Project in Python

This guide walks data science students through creating a basic data analysis project in Python while practicing Git. We'll build a script that loads a dataset (using the built-in Iris dataset), performs summary statistics, and generates visualizations with pandas and matplotlib. It's designed for first-year data science students, using core libraries. We'll commit incrementally and add unit tests with pytest. This reinforces Git workflows for collaborative data projects.

## Prerequisites
- You've set up your GitHub account and Git on your local machine. Refer to [GitHub_Setup_Instructions.md](../GitHub_Setup_Instructions.md) if needed.
- You understand basic Git areas (working directory, staging, repository). See [Git_Areas.md](../Git_Areas.md).
- You worked through the the basic Git workflow. See [GitHub_Student_Workflow.md](../GitHub_Student_Workflow.md)
- Python 3.8+ installed. For data science, we recommend **Miniconda** (lighter than full Anaconda) to manage environments and packages. Download from [docs.conda.io/miniconda](https://docs.conda.io/en/latest/miniconda.html). Why? It handles dependencies like pandas/numpy easily without conflicts. If you do not have Miniconda configured, you can follow [this guide](Git_Python_Miniconda.md).
- Basic Python knowledge: functions, imports, data structures.
- Code editor like VS Code with Python extension.

If using Miniconda:
1. Install and create an environment: `conda create -n ds-git python=3.13`
2. Activate: `conda activate ds-git`
3. Install packages: `conda install pandas matplotlib scikit-learn pytest` (or `pip install` if preferred).

## Step 1: Set Up Your Repository and Initial Script
1. Create a GitHub repo called `python-ds-analysis`.
    - Make it public or private as you prefer.
    - Initialize it with a README.md file.
    - Add a .gitignore file and select `Python`. [More information about .gitignore](https://docs.github.com/en/get-started/git-basics/ignoring-files)
2. Clone locally:
Remember to replace `your-username` with your _actual_ GitHub username.
   ```
   git clone https://github.com/your-username/python-ds-analysis.git
   cd python-ds-analysis
   ```
   Alternativerly, clone using SSH, if you configured your SSH key with GitHub:
   ```
   git clone git@github.com:your-username/python-ds-analysis.git
   cd python-ds-analysis
   ```
3. Create `analysis.py` with basic imports and load data:
   ```python
   import pandas as pd
   from sklearn.datasets import load_iris

   def main():
       print("Welcome to Iris Data Analysis!")
       iris = load_iris()
       df = pd.DataFrame(iris.data, columns=iris.feature_names)
       print(df.head())

   if __name__ == "__main__":
       main()
   ```
4. Run: `python analysis.py` (should print first 5 rows).
5. Commit:
   ```
   git add analysis.py
   git commit -m "Initial: Set up script with Iris dataset load"
   git push origin main
   ```

Your base project is on GitHub!

## Step 2: Add Summary Statistics
Compute basic stats like mean and std.

1. Update `analysis.py`:
   ```python
   import pandas as pd
   from sklearn.datasets import load_iris

   def load_data():
       iris = load_iris()
       return pd.DataFrame(iris.data, columns=iris.feature_names)

   def compute_stats(df):
       return df.describe()

   def main():
       print("Welcome to Iris Data Analysis!")
       df = load_data()
       stats = compute_stats(df)
       print(stats)

   if __name__ == "__main__":
       main()
   ```
2. Run to see stats table.

3. Commit:
   ```
   git add analysis.py
   git commit -m "Add functions for loading data and computing summary stats"
   git push origin main
   ```

## Step 3: Add Visualization
Plot a simple histogram.

1. Update `analysis.py`:
   ```python
   import pandas as pd
   import matplotlib.pyplot as plt
   from sklearn.datasets import load_iris

   def load_data():
       iris = load_iris()
       return pd.DataFrame(iris.data, columns=iris.feature_names)

   def compute_stats(df):
       return df.describe()

   def plot_histogram(df, column):
       df[column].hist()
       plt.title(f"Histogram of {column}")
       plt.show()

   def main():
       print("Welcome to Iris Data Analysis!")
       df = load_data()
       stats = compute_stats(df)
       print(stats)
       plot_histogram(df, 'sepal length (cm)')

   if __name__ == "__main__":
       main()
   ```
2. Run; a plot window should appear.

3. Commit:
   ```
   git add analysis.py
   git commit -m "Add histogram visualization function"
   git push origin main
   ```

## Step 4: Refactor for Testability
Separate logic; add a `data_utils.py` for reusable functions.

1. Create `data_utils.py`:
   ```python
   import pandas as pd
   from sklearn.datasets import load_iris

   def load_iris_data():
       iris = load_iris()
       return pd.DataFrame(iris.data, columns=iris.feature_names)

   def compute_summary_stats(df):
       return df.describe()
   ```
2. Update `analysis.py`:
   ```python
   import matplotlib.pyplot as plt
   from data_utils import load_iris_data, compute_summary_stats

   def plot_histogram(df, column):
       df[column].hist()
       plt.title(f"Histogram of {column}")
       plt.show()

   def main():
       print("Welcome to Iris Data Analysis!")
       df = load_iris_data()
       stats = compute_summary_stats(df)
       print(stats)
       plot_histogram(df, 'sepal length (cm)')

   if __name__ == "__main__":
       main()
   ```
3. Run to verify.

4. Commit:
   ```
   git add data_utils.py analysis.py
   git commit -m "Refactor: Move data functions to data_utils.py"
   git push origin main
   ```

## Step 5: Add Unit Tests with Pytest
Test core functions in `data_utils.py`.

1. Create `test_data_utils.py`:
   ```python
   import pytest
   import pandas as pd
   from data_utils import load_iris_data, compute_summary_stats

   def test_load_iris_data():
       df = load_iris_data()
       assert isinstance(df, pd.DataFrame)
       assert df.shape == (150, 4)
       assert 'sepal length (cm)' in df.columns

   def test_compute_summary_stats():
       df = load_iris_data()
       stats = compute_summary_stats(df)
       assert isinstance(stats, pd.DataFrame)
       assert not stats.empty
       assert 'mean' in stats.index
   ```
2. Run tests: `pytest test_data_utils.py -v` (install pytest if needed: `pip install pytest` or `conda install pytest`).

3. Commit:
   ```
   git add test_data_utils.py
   git commit -m "Add pytest unit tests for data_utils functions"
   git push origin main
   ```

## Step 6: Add More Tests and Edge Cases
Test stats on subset data.

1. Update `test_data_utils.py`:
   ```python
   import pytest
   import pandas as pd
   from data_utils import load_iris_data, compute_summary_stats

   def test_load_iris_data():
       df = load_iris_data()
       assert isinstance(df, pd.DataFrame)
       assert df.shape == (150, 4)
       assert 'sepal length (cm)' in df.columns

   def test_compute_summary_stats():
       df = load_iris_data()
       stats = compute_summary_stats(df)
       assert isinstance(stats, pd.DataFrame)
       assert not stats.empty
       assert 'mean' in stats.index

   def test_compute_summary_stats_empty():
       empty_df = pd.DataFrame()
       with pytest.raises(ValueError):  # describe() on empty raises warning, but we can check
           compute_summary_stats(empty_df)
   ```
   (Note: `describe()` on empty DF returns empty; adjust assert if needed for real edge case.)

2. Run: `pytest test_data_utils.py -v`

3. Commit:
   ```
   git add test_data_utils.py
   git commit -m "Add edge case test for empty DataFrame"
   git push origin main
   ```

## Step 7: Update README
Add to `README.md`:
```
[Instructions for setting up this repo](https://github.com/FixleIO/git-started/blob/main/assignments/Git_Tutorial_with_Python_DataScience.md)

## Running the Analysis
conda activate ds-git  # or your env
python analysis.py


## Running Tests
pytest test_data_utils.py -v
```

Commit:
```
git add README.md
git commit -m "Update README with run and test instructions"
git push origin main
```

## Why Anaconda/Miniconda?
- Manages virtual environments to avoid package conflicts (common in DS with many libs).
- Pre-installs data science staples like pandas, numpy.
- Alternative: Use `python -m venv ds-env` and `pip install pandas matplotlib scikit-learn pytest`, but conda is more DS-friendly for reproducibility.


## Next Steps
- Add more viz (scatter plots) or ML (simple classification).
- Use `git log` to review; branch for experiments.
- For real data: Add a `data/` folder with CSV; commit sample files.

Check GitHub for your commits! 🚀