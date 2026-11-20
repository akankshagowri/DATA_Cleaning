# Netflix Dataset Cleaning

A Jupyter Notebook project that loads the Netflix Movies and TV Shows dataset from Kaggle and cleans it with Pandas. The focus is on understanding **why** values are missing and making deliberate decisions for each column, not just dropping nulls.

**Project page URL:** https://roadmap.sh/projects/cleaning-netflix-dataset

**GitHub repository:** https://github.com/akankshagowri/netflix-data-cleaning

## Dataset

[Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) by Shivam Bansal (Kaggle). The notebook downloads it automatically with `kagglehub`.

## What the project does

1. Downloads the dataset from Kaggle
2. Inspects it with `.head()`, `.info()` and `.describe()`
3. Finds missing values and handles each column deliberately
4. Fixes mixed-type columns (for example `duration` values like `"90 min"` and `"2 Seasons"`)
5. Parses date columns into proper `datetime` objects
6. Exports the cleaned DataFrame to a new CSV file

## Requirements

- Python 3.9 or newer
- pandas
- kagglehub
- Jupyter Notebook

## How to run

```bash
# 1. Clone the repository
git clone https://github.com/akankshagowri/netflix-data-cleaning.git
cd netflix-data-cleaning

# 2. Install the dependencies
pip install -r requirements.txt

# 3. Start Jupyter and open the notebook
jupyter notebook netflix_cleaning.ipynb
```

In Jupyter, choose **Run > Run All Cells**. The first cell downloads the dataset, and the last cell saves the result as `netflix_titles_cleaned.csv` in the folder you started Jupyter from.

## Cleaning decisions

| Column | Problem | Decision |
|---|---|---|
| `director` | Missing for many documentaries, stand-up specials and TV shows | Filled with `"Unknown"`, rows kept |
| `cast` | Missing for documentaries and some reality shows | Filled with `"Unknown"` |
| `country` | Production country not recorded for some titles | Filled with `"Unknown"` |
| `date_added` | Stored as text (for example `"August 14, 2020"`), a few missing | Converted to `datetime`. Missing values stay empty instead of being invented. |
| `rating` | Some blanks, and some rows have the duration typed into this column | Misplaced durations moved to `duration`, remaining blanks filled with `"Unknown"` |
| `duration` | Mixed units in one text column (minutes and seasons) | Split into `duration_minutes` (movies) and `seasons` (TV shows) |
| all text columns | Extra whitespace, empty strings | Stripped, empty strings treated as missing |
| whole table | Possible duplicate rows | Duplicates removed |

## New columns in the output

| Column | Description |
|---|---|
| `duration_minutes` | Length in minutes (movies only) |
| `seasons` | Number of seasons (TV shows only) |
| `year_added` | Year the title was added to Netflix |
| `month_added` | Month the title was added to Netflix |

## Project structure

```
.
├── netflix_cleaning.ipynb       # the notebook with all cleaning steps
├── netflix_titles_cleaned.csv   # cleaned output (created when you run the notebook)
├── requirements.txt
└── README.md
```

## License

Released under the MIT License. The dataset belongs to its original author on Kaggle and is subject to its own license.
