# Netflix Dataset — Exploratory Data Analysis (EDA)

A beginner-friendly, reproducible exploratory data analysis project using Python, Pandas, and Matplotlib.

## Dataset
- **Source:** [Netflix Movies and TV Shows — Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- **Expected file:** `netflix_titles.csv`
- **Dataset contents:** title, type, director, cast, country, date added, release year, rating, duration, categories, and description.
- The notebook inspects the downloaded file's actual shape and columns rather than assuming fixed numbers.

## Run the notebook
### Option A — Google Colab
1. Open `EDA_Netflix.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Run cells from top to bottom.
3. If automatic download does not work, download the CSV from the Kaggle link above and upload it when prompted.

### Option B — Local Jupyter
```bash
python -m venv .venv
# Windows:
.venv\\Scripts\\activate
# macOS/Linux:
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook EDA_Netflix.ipynb
```
Download `netflix_titles.csv` from Kaggle into the same folder before running if automatic download is unavailable.

## Analysis included
- Dataset shape, dtypes, memory usage, first/last rows, and duplicate check
- Missing-value counts, percentages, and a missingness chart
- Numeric summary statistics and categorical value counts
- Six question-driven visualizations with data-based interpretations
- Automatically generated 3–5 findings and limitations

## Interpretation notes
- Catalogue counts do not indicate what people watched or how popular a title was.
- Country and category fields may contain multiple comma-separated values.
- Missing values are not automatically imputed.
- Correlation is not causation.

## Repository structure
```
EDA_Netflix.ipynb
README.md
requirements.txt
```

**Submission note:** Run the notebook top-to-bottom and review the computed findings. Add your own explanation of the most interesting result before submitting.
