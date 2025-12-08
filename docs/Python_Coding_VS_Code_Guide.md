[Home](./)

# Python Coding in VS Code

You want to write Python code but aren't sure which editor to use, or you're looking for something lighter than PyCharm. Think of VS Code as a Swiss Army knife—it handles Python, R, JavaScript, and many other languages in one lightweight editor. This tutorial shows you how to set up Python in VS Code with smart features like code completion, interactive debugging, and web apps.

## Key Concepts

- **[Python Extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)** - VS Code extension by Microsoft that provides syntax highlighting, debugging, code execution, and Jupyter notebook support
- **[Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)** - Language server that enables fast IntelliSense, type checking, and auto-imports
- **[Virtual Environment](https://docs.python.org/3/library/venv.html)** - Isolated Python environment for managing project-specific packages
- **[Streamlit](https://streamlit.io/)** - Python library for creating interactive web apps with simple scripts

## What You'll Need

- VS Code already installed
- Internet connection to download Python and packages
- Basic familiarity with installing software
- 15-20 minutes

## Step 1: Install Python

You need Python 3.8 or higher for the best compatibility.

**Windows:**
- Download the latest Python from [python.org](https://www.python.org/downloads/)
- Run the installer
- **Check the box "Add python.exe to PATH"** before clicking Install Now

**macOS:**
- Download from [python.org](https://www.python.org/downloads/) and run the installer
- Or use Homebrew: open Terminal and type `brew install python`

**Linux:**
- Python is usually pre-installed. Check with `python3 --version`
- If needed: `sudo apt install python3 python3-pip python3-venv` (Ubuntu/Debian)

Verify by opening a terminal and typing `python3 --version` or `python --version`.

## Step 2: Install Python Extensions in VS Code

- Open VS Code
- Click the **Extensions** icon in the left sidebar
- Search for `ms-python.python` and click **Install** on the Python extension by Microsoft
- Pylance installs automatically with the Python extension

## Step 3: Create Your Python Project

- Create a new folder on your computer (e.g., `my-python-project`)
- In VS Code, click **File** → **Open Folder** and select your new folder
- Click **File** → **New File**
- Click **File** → **Save** and name it `analysis.py`

## Step 4: Select Python Interpreter

VS Code needs to know which Python installation to use.

- Click **View** → **Command Palette**
- Type `Python: Select Interpreter` and select it
- Choose the Python version you installed (e.g., `Python 3.12.x`)
- The selected interpreter appears in the bottom-right corner

## Step 5: Create a Virtual Environment

Virtual environments keep your project dependencies isolated.

- Click **View** → **Command Palette**
- Type `Python: Create Environment` and select it
- Choose **Venv** (built-in virtual environment)
- Select your Python interpreter from the list
- Wait for VS Code to create the environment (a `.venv` folder appears)
- VS Code automatically activates this environment for your project

You'll see `(.venv)` in your terminal prompt when the environment is active.

## Step 6: Install Required Packages

- Click **View** → **Terminal** to open a terminal
- The terminal should show `(.venv)` indicating your virtual environment is active
- Install packages:
  ```bash
  pip install pandas matplotlib streamlit
  ```
- Wait for installation (1-2 minutes)

If `(.venv)` doesn't appear, click **View** → **Command Palette**, run `Python: Select Interpreter`, and choose the one with `('.venv': venv)`.

## Step 7: Write Your First Python Script

Type this code into `analysis.py`:

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load the iris dataset
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
iris = pd.read_csv(url)

# View the first few rows
print(iris.head())

# Generate summary statistics
print("\nSummary Statistics:")
print(iris.describe())

# Create a histogram
plt.figure(figsize=(8, 6))
plt.hist(iris['sepal_length'], bins=20, color='steelblue', edgecolor='white')
plt.xlabel('Sepal Length (cm)')
plt.ylabel('Frequency')
plt.title('Distribution of Sepal Length')
plt.show()
```

- Click **File** → **Save**

## Step 8: Run Python Code

- With `analysis.py` open, click the **▶ Run Python File** button in the top-right corner
- Or right-click in the editor and select **Run Python File in Terminal**
- Watch the output in the terminal
- A histogram window pops up showing your plot
- You can also select specific lines and press `Shift+Enter` to run just those lines

## Step 9: Create a Simple Streamlit App

- Click **File** → **New File**
- Click **File** → **Save** and name it `app.py`
- Type this code:

```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

st.title("Interactive Histogram")

# Sidebar slider
bins = st.sidebar.slider(
    "Number of bins:",
    min_value=5,
    max_value=50,
    value=30
)

# Load data
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
iris = pd.read_csv(url)

# Create histogram
fig, ax = plt.subplots(figsize=(8, 6))
ax.hist(iris['sepal_length'], bins=bins, color='steelblue', edgecolor='white')
ax.set_xlabel('Sepal Length (cm)')
ax.set_ylabel('Frequency')
ax.set_title('Distribution of Sepal Length')

# Display in Streamlit
st.pyplot(fig)
```

- Click **File** → **Save**
- Open the terminal and run:
  ```bash
  streamlit run app.py
  ```
- The app opens in your browser (usually at `http://localhost:8501`)
- Move the slider and watch the histogram update
- Press `Ctrl+C` in the terminal to stop the app

## Step 10: Use Code Completion and IntelliSense

- In `analysis.py`, start typing `iris.` on a new line
- A dropdown appears with available methods and attributes
- Type `iris.gr` and watch it suggest `groupby()`
- Hover your mouse over `pd.read_csv`—a popup shows function documentation
- When you type a function call, IntelliSense shows parameter hints

## Step 11: Try Debugging

- In `analysis.py`, click to the left of line 8 (the `print(iris.head())` line) to set a breakpoint (red dot appears)
- Press **F5** or click **Run** → **Start Debugging**
- Select **Python File** when prompted
- Code pauses at the breakpoint
- Use the debug toolbar to step through code and inspect variables
- Press **F5** again to continue

## Next Steps

- Explore [pandas](https://pandas.pydata.org/) for data manipulation
- Learn [Jupyter notebooks](https://code.visualstudio.com/docs/datascience/jupyter-notebooks) in VS Code
- Try [Flask](https://flask.palletsprojects.com/) or [FastAPI](https://fastapi.tiangolo.com/) for web APIs

## Troubleshooting

- **"Python is not recognized" in terminal** - On Windows, reinstall Python and check "Add python.exe to PATH". On Mac/Linux, use `python3` instead of `python`. Restart VS Code.
- **No interpreter found** - Click the interpreter selector in bottom-right, or run `Python: Select Interpreter` from Command Palette. Select **Enter interpreter path** if your installation doesn't appear.
- **Virtual environment not activating** - VS Code should auto-activate when you open a terminal. If not, manually activate: Windows: `.venv\Scripts\activate`, Mac/Linux: `source .venv/bin/activate`.
- **IntelliSense not working** - Make sure Pylance is installed and enabled. Restart VS Code and wait 10-20 seconds after opening a file.
- **Streamlit app won't run** - Ensure streamlit is installed (`pip list | grep streamlit`). Check that no other app uses port 8501.

## Workflow Summary

VS Code provides a modern, lightweight environment for Python:

- **Unified environment** - Code Python, R, JavaScript, and more in one editor
- **Powerful IntelliSense** - Smart completions, type checking, and auto-imports via Pylance
- **Integrated debugging** - Set breakpoints, inspect variables, step through code
- **Jupyter support** - Run notebooks directly in VS Code
- **Version control** - Built-in Git integration

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
