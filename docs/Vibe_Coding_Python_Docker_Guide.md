[Home](./)

# Vibe Coding in Python with Claude Code and Docker

You've written Python code by typing every line yourself. But what if you could describe what you want in plain English and watch the code appear? Vibe coding is like having a conversation with your computer—you describe the outcome, Claude Code builds it, you test and refine. It's not magic; it's a new way to work where you guide the vision and AI handles the implementation. This tutorial shows you how to analyze the classic Iris flower dataset using nothing but natural language requests.

## Key Concepts

- **[Vibe Coding](https://www.ibm.com/think/topics/vibe-coding)** - Programming by describing what you want in natural language, then iterating based on results rather than writing code line-by-line
- **[Claude Code](https://code.claude.com/)** - AI coding assistant that writes, debugs, and refactors code based on your natural language requests
- **[Iris Dataset](https://scikit-learn.org/stable/datasets/toy_dataset.html#iris-dataset)** - Classic dataset containing measurements of 150 iris flowers from three species
- **Iterative refinement** - The core vibe coding pattern: describe → test → refine → commit working versions

## What You'll Need

- Finished [Python Coding in VS Code via Docker](./Python_Coding_Docker_Guide)
- Finished [Using GitHub Desktop with Claude Code](./GitHub_Desktop_Claude_Code_Workflow)
- 20-25 minutes

## Step 1: Create New GitHub Repository

- Open GitHub Desktop
- Click **File > New Repository**
- Fill in the details:
  - **Name:** `iris-analysis`
  - **Description:** `Iris data analysis built with vibe coding`
  - **Local Path:** Choose a location (e.g., Documents or work folder)
  - Check **Initialize this repository with a README**
- Click **Create Repository**
- Click **Publish repository** at the top
- Uncheck **Keep this code private** if you want it public (optional)
- Click **Publish Repository**

You now have a local Git repository and a backup on GitHub.

## Step 2: Copy Docker Configuration

You need the `.devcontainer` folder from the vibe project to set up your Docker environment.

- Open File Explorer (Windows) or Finder (Mac)
- Navigate to your vibe project folder (e.g., `Documents/vibe`)
- Find the `.devcontainer` folder
- Copy the entire folder (it contains `Dockerfile` and `devcontainer.json`)
- Navigate to your new `iris-analysis` folder
- Paste the `.devcontainer` folder there

Your `iris-analysis` folder should now contain:
- `.devcontainer/` (folder you just copied)
- `README.md` (created by GitHub Desktop)
- `.git/` (hidden folder for version control)

## Step 3: Open Project in Container

- Open VS Code
- Click **File > Open Folder**
- Navigate to `iris-analysis` folder
- Click **Select Folder**
- A notification appears in the bottom right: **Folder contains a Dev Container configuration file**
- Click **Reopen in Container**
- If you don't see the notification, click the green icon in bottom-left corner and select **Reopen in Container**
- VS Code builds the Docker container (takes 3-5 minutes first time)
- Watch the progress notification showing build steps
- When complete, the green icon shows **Dev Container: Python in Docker**

## Step 4: Start Claude Code

- In VS Code, click **Terminal > New Terminal**
- You're now inside the Docker container
- Type this command to start Claude Code:

```bash
claude
```

- A browser window opens for authentication
- Click **Continue with Google** or **Continue with Email**
- Log in with your Claude account (or create one)
- After authentication succeeds, return to VS Code terminal
- You'll see Claude's welcome message

Claude Code is now running and ready for your requests.

## Step 5: Create Context File

Claude works better when it knows what your project is about. Create a simple context file.

- In the Claude Code terminal, type:

```
create a file called CLAUDE.md with this content: This project analyzes the Iris flower dataset using Python. We use pandas for data manipulation and matplotlib for visualizations. We're practicing vibe coding - describing what we want in plain English.
```

- Press Enter
- Claude creates the file
- This context helps Claude understand your project goals

## Step 6: First Vibe - Load the Data

Now the fun begins. Instead of looking up documentation, just describe what you want.

- In the Claude Code terminal, type:

```
Load the iris dataset from scikit-learn. Convert it to a pandas dataframe with proper column names. Add the species names as a column (not just numbers). Show me the first 10 rows. Save the code to a file called iris_exploration.py
```

- Press Enter
- Watch Claude:
  - Write Python code to load the data
  - Create a script with proper imports
  - Run the code to show you results
- Review the output showing flower measurements and species names

You just used vibe coding! No searching documentation, no trial and error—just describe and test.

## Step 7: Second Vibe - Summary Statistics

Before creating visualizations, understand what the data contains.

- In Claude Code terminal, type:

```
Show me summary statistics for the iris data grouped by species. I want to see the mean, min, and max for each measurement (sepal length, sepal width, petal length, petal width) for each of the three species. Add this to iris_exploration.py
```

- Press Enter
- Claude updates the script and shows statistics
- Notice how different species have different measurement ranges
- Setosa has much smaller petals than Virginica

This exploration helps you understand patterns in the data.

## Step 8: Third Vibe - Create a Histogram

Time to visualize the data.

- In Claude Code terminal, type:

```
Create a histogram showing the distribution of petal lengths for all flowers. Use 20 bins. Add a title and axis labels. Save the plot as petal_length_histogram.png. Add this code to iris_exploration.py
```

- Press Enter
- Claude creates the visualization code
- A PNG file appears in your project folder
- Open `petal_length_histogram.png` to see the chart
- Notice the two peaks—this shows the species have different petal lengths

## Step 9: Fourth Vibe - Scatter Plot

Scatter plots show relationships between two variables.

- In Claude Code terminal, type:

```
Create a scatter plot with petal length on the x-axis and petal width on the y-axis. Color each point by species using different colors. Add a legend showing which color is which species. Save as petal_scatter.png. Add this to iris_exploration.py
```

- Press Enter
- Claude creates the scatter plot
- Open `petal_scatter.png` to see the result
- Notice how the three species form distinct clusters
- Setosa (small petals) is clearly separated from the others

This is vibe coding in action: describe the visualization, test it, iterate.

## Step 10: Fifth Vibe - Box Plot

Box plots are great for comparing distributions across groups.

- In Claude Code terminal, type:

```
Create a box plot comparing petal lengths across the three species. Put species on the x-axis and petal length on the y-axis. Use different colors for each species. Add a title. Save as species_boxplot.png. Add this to iris_exploration.py
```

- Press Enter
- Claude adds the box plot code
- Open `species_boxplot.png` to see the comparison
- The boxes show the median and quartiles for each species
- You can clearly see Virginica has the longest petals

## Step 11: Review and Commit

Before committing, review what Claude built.

- In VS Code Explorer, click on `iris_exploration.py` to open it
- Skim through the code—notice the imports, data loading, and plotting sections
- You don't need to understand every line, but get a sense of the structure
- Check that all PNG files were created: `petal_length_histogram.png`, `petal_scatter.png`, `species_boxplot.png`
- Open GitHub Desktop
- You'll see all new files listed (the Python script and PNG images)
- In the **Summary** field at bottom left, type:

```
Iris data analysis with histograms, scatter plots, and box plots
```

- Click **Commit to main**
- Click **Push origin** to back up to GitHub

You've saved your first working analysis!

## Next Steps

- **Try different datasets** - Ask Claude to use the wine dataset, digits dataset, or load a CSV file
- **Explore more visualizations** - Try heatmaps, pair plots, or violin plots
- **Learn by asking** - When Claude writes code, ask "explain what this line does" to learn Python
- **Apply to your own data** - Use vibe coding to analyze your research or work data
- **Read about vibe coding** - Visit [IBM's guide](https://www.ibm.com/think/topics/vibe-coding) to learn more about this coding style

## Troubleshooting

- **Plot doesn't display** - The code saves plots as PNG files. Look in your project folder and open the image file directly in VS Code.
- **Import errors** - The Docker container should have pandas, matplotlib, and scikit-learn pre-installed. If not, ask Claude to install them with pip.
- **Claude makes mistakes** - Normal! Copy the error message, paste it to Claude, and say "fix this error." Vibe coding includes iteration and debugging.
- **Can't push to GitHub** - Make sure you're logged into GitHub Desktop and published the repository (Step 1). Check your internet connection.
- **Container won't start** - Make sure Docker Desktop is running (green status indicator). Try clicking the green icon in VS Code and selecting **Rebuild Container**.

## Workflow Overview

This tutorial combined several technologies into one workflow:

- **GitHub Desktop** - Version control with visual interface (create repos, commit, push)
- **Docker container** - Isolated Python environment with all dependencies pre-installed
- **VS Code** - Code editor that connects to the Docker container
- **Claude Code** - AI assistant that writes Python code from your descriptions
- **scikit-learn** - Provides the Iris dataset and machine learning tools
- **pandas** - Data manipulation and analysis
- **matplotlib** - Creating visualizations

The magic isn't any single tool—it's how vibe coding lets you describe what you want and iterate rapidly. You went from empty project to complete data analysis with multiple visualizations in 20 minutes without writing a single line of code manually.

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 11, 2025.
