# Project_ML

## Running this code locally

To run this credit card fraud detection analysis on your local machine, follow these steps:

### 1. Prerequisites

Make sure you have the following installed:

*   **Python 3.x**: Recommended version 3.8 or higher.
*   **pip**: Python package installer (usually comes with Python).
*   **Jupyter Notebook** or **JupyterLab**: For running `.ipynb` files.
*   **Git**: For cloning the repository (if applicable).

### 2. Setup Your Environment

#### a. Clone the Repository (if applicable)

If this notebook is part of a Git repository, clone it to your local machine:

```bash
git clone <repository_url>
cd <repository_name>
```

#### b. Create a Virtual Environment (Recommended)

It's good practice to use a virtual environment to manage dependencies:

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

#### c. Install Dependencies

Install the required Python libraries. You can create a `requirements.txt` file from the `!pip install` commands in the notebook, or install them manually:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost torch
```

Or if you have a `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 3. Obtain the Dataset

This notebook uses the "ULB Credit Card Fraud Detection" dataset, typically available on Kaggle. 

1.  **Download `creditcard.csv`** from [Kaggle](https://www.kaggle.com/datasets/mlg-gza/creditcardfraud).
2.  **Place the `creditcard.csv` file** in the same directory as this notebook, or update the `pd.read_csv()` path in the notebook (around cell `mf2I11-sgjfz`) to point to the correct location of your downloaded file.

    *Note: The current notebook loads the data from `/content/drive/MyDrive/creditcard.csv`, which is specific to Google Colab and Google Drive. You will need to change this path to your local file path.* For example:

    ```python
    df = pd.read_csv('./creditcard.csv') # Assuming creditcard.csv is in the same directory
    ```

### 4. Run the Notebook

#### a. Start Jupyter

Open a terminal or command prompt in the directory where your notebook and `creditcard.csv` are located, and start Jupyter:

```bash
jupyter notebook
# or
jupyter lab
```

#### b. Open and Execute the Notebook

Your web browser will open with the Jupyter interface. Navigate to this notebook file (e.g., `your_notebook_name.ipynb`) and open it. You can then run all cells by selecting "Cell" > "Run All" from the menu, or execute cells one by one.
