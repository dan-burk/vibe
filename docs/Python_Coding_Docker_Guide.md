[Home](./)

# Python Coding in VS Code via Docker Container

Ever tried to share your Python code with a colleague, only to spend hours debugging "but it works on my machine" issues? Docker containers are like shipping containers for code—they package your Python environment, libraries, and dependencies into a sealed box that works the same everywhere. Plus, you get access to pre-built images on [Docker Hub](https://hub.docker.com/) where developers publish ready-to-use environments. This tutorial shows you how to run Python in an isolated, reproducible environment using VS Code and Docker Desktop.

## Key Concepts

- **[Docker Desktop](https://www.docker.com/products/docker-desktop/)** - Application that runs containers on your computer, managing isolated environments
- **[Dev Container](https://code.visualstudio.com/docs/devcontainers/containers)** - VS Code feature that lets you code inside a Docker container with full IDE support
- **Container Isolation** - Your code runs in a separate Linux environment that only sees your project folder
- **[Python Official Images](https://hub.docker.com/_/python)** - Pre-built Docker images with Python and essential tools

## What You'll Need

- [VS Code](https://code.visualstudio.com/) already installed
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- [GitHub Desktop](https://desktop.github.com/) already installed (optional)
- 20-25 minutes

## Step 1: Install Docker Desktop

- Visit [Docker Desktop download page](https://www.docker.com/products/docker-desktop/)
- Click **Download for Windows** (or Mac/Linux based on your system)
- Run the installer and follow the wizard
- When prompted, enable WSL 2 (Windows users) or accept default settings
- Launch Docker Desktop
- Wait for the Docker engine to start (green status indicator in bottom left)

## Step 2: Install Dev Containers Extension

- Open VS Code
- Click the **Extensions** icon in the left sidebar (or click **View** → **Extensions**)
- Type `dev containers` in the search box
- Find **Dev Containers** by Microsoft
- Click **Install**

## Step 3: Create a Python Project Folder

- Create a new folder on your computer named `python-docker-demo`
- Inside it, create a subfolder named `.devcontainer`
- Inside it, create a subfolder named `python`

Your structure: `python-docker-demo/.devcontainer/` and `python-docker-demo/python/`

## Step 4: Create the Dockerfile

- In VS Code, click **File** → **Open Folder**
- Navigate to the `python-docker-demo` folder
- Click **Select Folder**
- In Explorer, right-click the `.devcontainer` folder
- Click **New File** and name it `Dockerfile`
- Paste:

```dockerfile
# Choose the official Python slim image
FROM python:3.12-slim

# 1. Install system dependencies
RUN apt-get update && apt-get install -y \
    git curl build-essential && \
    rm -rf /var/lib/apt/lists/*

# 2. Install Python packages for data science and web apps
RUN pip install --no-cache-dir \
    pandas matplotlib seaborn streamlit jupyter

# 3. Install Node.js LTS from NodeSource
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - \
    && apt-get install -y nodejs \
    && npm install -g npm@latest

# 4. Install Claude Code globally
RUN npm install -g @anthropic-ai/claude-code

# 5. Expose Streamlit port
EXPOSE 8501
```

- Click **File** → **Save**

## Step 5: Create the Dev Container Configuration

- In the `.devcontainer` folder, create a new file named `devcontainer.json`
- Paste:

```json
{
  "name": "Python in Docker",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "ms-python.python",
        "ms-python.debugpy"
      ]
    }
  },
  "forwardPorts": [8501],
  "postCreateCommand": "python3 --version"
}
```

- Click **File** → **Save**

## Step 6: Create a Python Data Analysis Script

- In the `python` folder, create a new file named `iris_analysis.py`
- Paste:

```python
# Simple data analysis using the iris dataset
import pandas as pd
import matplotlib.pyplot as plt

# Load the iris dataset from URL
url = "https://raw.githubusercontent.com/mwaskom/seaborn-data/master/iris.csv"
df = pd.read_csv(url)

# Display first few rows
print(df.head())

# Summary statistics
print("\nSummary statistics:")
print(df.describe())

# Create histograms
plt.figure(figsize=(10, 6))
plt.hist(df['sepal_length'], bins=20, alpha=0.7, label='Sepal Length')
plt.hist(df['sepal_width'], bins=20, alpha=0.7, label='Sepal Width')
plt.xlabel('Measurement (cm)')
plt.ylabel('Frequency')
plt.title('Iris Sepal Measurements')
plt.legend()
plt.show()
```

- Click **File** → **Save**

## Step 7: Create a Streamlit Web App

- In the `python` folder, create a new file named `app.py`
- Paste:

```python
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

st.title("Old Faithful Geyser Data")

# Slider for number of bins
bins = st.slider("Number of bins:", min_value=5, max_value=50, value=30)

# Generate sample data (simulating Old Faithful eruption durations)
np.random.seed(42)
data = np.concatenate([
    np.random.normal(2, 0.5, 100),
    np.random.normal(4.5, 0.5, 150)
])

# Create histogram
fig, ax = plt.subplots()
ax.hist(data, bins=bins, edgecolor='black')
ax.set_xlabel('Eruption Duration (minutes)')
ax.set_ylabel('Frequency')
ax.set_title(f'Histogram with {bins} bins')

st.pyplot(fig)
```

- Click **File** → **Save**

## Step 8: Reopen in Container

- Click the green icon in the bottom-left corner of VS Code
- Select **Reopen in Container**
- VS Code builds the container (5-10 minutes the first time)
- When complete, the green icon shows **Dev Container: Python in Docker**

## Step 9: Understand the Container Environment

You're now coding inside a Linux container.

- Click **Terminal** → **New Terminal**
- Check your location:
  ```bash
  pwd
  ```

You'll see `/workspaces/python-docker-demo`—your project folder inside the container.

- List files:
  ```bash
  ls
  ```

You'll see `.devcontainer/`, `python/`, etc.

- Try going up one directory:
  ```bash
  cd ..
  ls
  ```

You'll only see `python-docker-demo/`—the container is isolated.

- Return to project:
  ```bash
  cd python-docker-demo
  ```

## Step 10: Run Python Code Line by Line

- In VS Code Explorer, navigate to `python/iris_analysis.py`
- Click to open the file
- Select the first line: `import pandas as pd`
- Press `Shift+Enter` to run it in an interactive Python terminal
- Continue running each line or block with `Shift+Enter`
- When you run `print(df.head())`, you'll see the first 5 rows
- When you run `print(df.describe())`, you'll see statistics
- When you run the histogram code, a plot window opens

## Step 11: Run the Streamlit App

- In VS Code Explorer, navigate to `python/app.py`
- Click to open the file
- Click **Terminal** → **New Terminal**
- Run the app:
  ```bash
  cd python
  streamlit run app.py
  ```
- A notification appears: **Open in Browser**
- Click **Open in Browser**
- Move the slider to change histogram bins—the chart updates in real-time

## Step 12: Make a Simple Change

- Keep the app running
- In VS Code, edit `python/app.py`
- Find line 6: `st.title("Old Faithful Geyser Data")`
- Change it to:
  ```python
  st.title("My First Python Docker App")
  ```
- Click **File** → **Save**
- In your browser, click **Always rerun** in the top-right corner
- The title shows your custom text

## Step 13: Install Python Packages Permanently (Optional)

Packages installed via `pip install` in the terminal are temporary. To make them permanent:

- Open `.devcontainer/Dockerfile`
- Find line 9: `RUN pip install --no-cache-dir ...`
- Add `scikit-learn` to the list:
  ```dockerfile
  RUN pip install --no-cache-dir \
      pandas matplotlib seaborn streamlit jupyter scikit-learn
  ```
- Click **File** → **Save**
- Click the green icon in bottom-left corner
- Select **Rebuild Container**
- Wait for rebuild (2-5 minutes)
- Verify:
  ```python
  import sklearn
  print(sklearn.__version__)
  ```

## Next Steps

- Create new Python scripts in the `python/` folder with your own data analysis
- Add packages to the Dockerfile and rebuild the container
- Build interactive dashboards with Streamlit or Flask

## Troubleshooting

- **Docker Desktop not running** - Open Docker Desktop and wait for the green status indicator before reopening the container.
- **Container build fails** - Check your internet connection; the first build downloads images and packages. Click **Rebuild Container** to retry.
- **Port 8501 already in use** - Stop other apps using that port, or change it in the Dockerfile and `devcontainer.json`.

## Workflow Overview

- **VS Code** provides the code editor with syntax highlighting, IntelliSense, and debugging
- **Docker container** runs an isolated Linux environment with Python and dependencies
- **Python official image** includes Python, pip, and essential tools
- **Dev Container config** automatically installs VS Code extensions
- **Port forwarding** lets you access web apps from your browser

## Everyday Workflow

- **Start Docker Desktop** - Open the app and wait for green status
- **Open VS Code** - Open your project folder
- **Reopen in Container** - Click the green icon and select **Reopen in Container** if needed
- **Write and run code** - Edit `.py` files, run with `Shift+Enter`, or run apps with `streamlit run app.py`
- **Save your work** - Code files are saved to your computer and persist across sessions
- **Commit and push** - Use GitHub Desktop to commit and push changes

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
