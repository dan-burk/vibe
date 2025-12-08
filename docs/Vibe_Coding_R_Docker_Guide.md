[Home](./)

# Vibe Coding in R with Claude Code and Docker

You've written R code by typing every line yourself. But what if you could describe what you want in plain English and watch the code appear? Vibe coding is like having a conversation with your computer—you describe the outcome, Claude Code builds it, you test and refine. It's not magic; it's a new way to work where you guide the vision and AI handles the implementation. This tutorial shows you how to build a real NBA stats dashboard using nothing but natural language requests.

## Key Concepts

- **[Vibe Coding](https://www.ibm.com/think/topics/vibe-coding)** - Programming by describing what you want in natural language, then iterating based on results
- **[Claude Code](https://code.claude.com/)** - AI coding assistant that writes, debugs, and refactors code from your requests
- **[hoopR](https://hoopr.sportsdataverse.org/)** - R package that provides easy access to NBA player statistics
- **Iterative refinement** - The core vibe coding pattern: describe → test → refine → commit

## What You'll Need

- Completed the [R Coding in Docker tutorial](./R_Coding_Docker_Guide.md)
- [GitHub Desktop](https://desktop.github.com/) installed and logged in
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) running
- The vibe project already cloned locally
- 25-30 minutes

## Step 1: Create New GitHub Repository

- Open GitHub Desktop
- Click **File** → **New Repository**
- Fill in:
  - **Name:** `nba-dashboard`
  - **Description:** `NBA stats dashboard built with vibe coding`
  - **Local Path:** Choose a location (e.g., Documents)
  - Check **Initialize this repository with a README**
- Click **Create Repository**
- Click **Publish repository** at the top
- Uncheck **Keep this code private** if you want it public (optional)
- Click **Publish Repository**

## Step 2: Copy Docker Configuration

Copy the `.devcontainer` folder from the vibe project to set up your Docker environment.

- Open File Explorer (Windows) or Finder (Mac)
- Navigate to your vibe project folder
- Find the `.devcontainer` folder
- Copy the entire folder
- Navigate to your new `nba-dashboard` folder
- Paste the `.devcontainer` folder

Your `nba-dashboard` folder should contain: `.devcontainer/`, `README.md`, and `.git/`

## Step 3: Open Project in Container

- Open VS Code
- Click **File** → **Open Folder**
- Navigate to `nba-dashboard` folder
- Click **Select Folder**
- A notification appears: **Folder contains a Dev Container configuration file**
- Click **Reopen in Container**
- If you don't see the notification, click the green icon in bottom-left and select **Reopen in Container**
- Wait for container build (3-5 minutes first time)
- When complete, the green icon shows **Dev Container: R in Docker**

## Step 4: Start Claude Code

- Click **Terminal** → **New Terminal**
- Type:
  ```bash
  claude
  ```
- A browser window opens for authentication
- Click **Continue with Google** or **Continue with Email**
- Log in with your Claude account
- Return to VS Code terminal
- You'll see Claude's welcome message

## Step 5: Create Context File

Claude works better when it knows your project goals.

- In Claude Code terminal, type:
  ```
  create a file called Claude.md with this content: This project builds an NBA stats dashboard using R and Shiny. We're using the hoopR package for data and practicing vibe coding.
  ```
- Press **Enter**
- Claude creates the file

## Step 6: First Vibe - Get NBA Data

Instead of looking up documentation, just describe what you want.

- In Claude Code terminal, type:
  ```
  Install the hoopR package and load current NBA player statistics. Show me the top 10 players by total points scored this season. Display it as a nice table.
  ```
- Press **Enter**
- Watch Claude install the package, write code, and run it
- Review the output showing player names, teams, and points

You just used vibe coding! No searching documentation—just describe and test.

## Step 7: Second Vibe - Explore the Data

- In Claude Code terminal, type:
  ```
  Show me what columns are available in this NBA data. Then create a summary showing: number of players, number of teams, average points per player, and who has the most assists and rebounds.
  ```
- Press **Enter**
- Claude explores the dataset and shows you statistics
- Look at the output to see available columns

## Step 8: Third Vibe - Create Basic Shiny App

- In Claude Code terminal, type:
  ```
  Create a Shiny app in a file called app.R that shows an interactive table of NBA player stats. Include columns for player name, team, points, assists, and rebounds. Add a slider to filter players by minimum points scored (from 0 to 1000). Make it look clean and professional.
  ```
- Press **Enter**
- Claude creates `app.R` with a complete Shiny application
- Wait for Claude to finish writing the file

## Step 9: Run the Shiny App

- In VS Code Explorer, open `app.R`
- Look for the **▶** button at the top right of the editor
- Click the dropdown and select **Run Shiny App**
- A notification appears: **Open in Browser**
- Click **Open in Browser**
- Try moving the points slider—the table filters in real-time

If something doesn't work, copy error messages and paste them to Claude.

## Step 10: Fourth Vibe - Add Visualization

- In Claude Code terminal, type:
  ```
  Add a bar chart below the table showing the top 15 players by points. Use different colors for each player. Also add a scatter plot showing the relationship between points and assists for all filtered players.
  ```
- Press **Enter**
- Claude updates `app.R`
- Refresh your browser
- You now see a colorful bar chart and scatter plot
- Move the slider—all visualizations update together

## Step 11: Fifth Vibe - Add Team Filter

- In Claude Code terminal, type:
  ```
  Add a dropdown menu to filter players by team. Put it at the top. When I select a team, show only players from that team. Include an "All Teams" option to show everyone.
  ```
- Press **Enter**
- Claude adds the team filter
- Refresh your browser
- Test the dropdown—select different teams

## Step 12: Review and Commit

- In VS Code Explorer, click `app.R` to review the code
- Open GitHub Desktop
- You'll see `app.R` listed as a new file
- In the **Summary** field, type:
  ```
  Create NBA dashboard with team filter and visualizations
  ```
- Click **Commit to main**
- Click **Push origin**

## Step 13: Iterate and Improve

Try adding features by describing them:

- "Add a player search box so I can type a player's name and jump to them"
- "Add a line chart showing points per game trend for the selected team"
- "Add tooltips to the scatter plot showing player names when I hover"

After each successful feature:
- Test in the browser
- If it works, commit with GitHub Desktop
- If it breaks, tell Claude the error and ask to fix it

## Step 14: The Vibe Coding Mindset

**Traditional coding:**
- Research documentation
- Figure out data structure
- Learn Shiny syntax
- Write code line by line
- Debug errors

**Vibe coding:**
- Describe what you want
- Claude builds it
- Test
- Describe improvements
- Test again
- Commit when working

**Key principles:**
- **Describe outcomes, not implementation** - Say "show top scorers" not "use arrange() and head()"
- **Iterate quickly** - Test → refine → test → refine
- **Commit working versions** - Save each success before trying new features
- **Embrace failures** - If Claude's code breaks, describe the error and ask to fix it

## Next Steps

- Apply vibe coding to your own data (research, business, hobbies)
- Try other packages like `nflfastR` for football or `worldfootballR` for soccer
- When Claude writes code, ask "explain what this function does" to learn R
- Deploy to [shinyapps.io](https://www.shinyapps.io/) (ask Claude how)

## Troubleshooting

- **hoopR installation fails** - Check your internet connection. Try `install.packages("hoopR")` in an R terminal to see detailed errors.
- **Shiny app won't start** - Verify the Shiny extension is installed (search "Posit.shiny" in Extensions). Check terminal for errors.
- **No data showing** - hoopR pulls live data; if NBA season hasn't started, ask Claude to use sample data.
- **Claude makes mistakes** - Normal! Copy the error, paste to Claude, and say "fix this error."

## Workflow Overview

- **GitHub Desktop** - Version control with visual interface
- **Docker container** - Isolated R environment with dependencies
- **VS Code** - Code editor that connects to the container
- **Claude Code** - AI assistant that writes R and Shiny code
- **hoopR package** - NBA data source
- **Shiny framework** - Interactive web apps in R

## Everyday Workflow

- **Start Docker Desktop** - Wait for green status
- **Open VS Code** - Open project, reopen in container if needed
- **Start Claude Code** - Type `claude` in terminal
- **Describe your goal** - "Add a feature that..." or "Fix the bug where..."
- **Test the changes** - Run your app, check if it works
- **Iterate or commit** - If broken, describe the fix; if working, commit
- **Push regularly** - Back up to GitHub

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
