[Home](./)

# R Coding in VS Code via Docker Container

Ever tried to share your R code with a colleague, only to spend hours debugging "but it works on my machine" issues? Docker containers are like shipping containers for code—they package your R environment, libraries, and dependencies into a sealed box that works the same everywhere. Plus, you get access to pre-built images on [Docker Hub](https://hub.docker.com/) where developers publish ready-to-use environments. This tutorial shows you how to run R in an isolated, reproducible environment using VS Code and Docker Desktop.

## Key Concepts

- **[Docker Desktop](https://www.docker.com/products/docker-desktop/)** - Application that runs containers on your computer, managing isolated environments
- **[Dev Container](https://code.visualstudio.com/docs/devcontainers/containers)** - VS Code feature that lets you code inside a Docker container with full IDE support
- **Container Isolation** - Your code runs in a separate Linux environment that only sees your project folder
- **[Rocker](https://rocker-project.org/)** - Pre-built Docker images specifically designed for R development

## What You'll Need

- [VS Code](https://code.visualstudio.com/) already installed
- [GitHub Desktop](https://desktop.github.com/) already installed
- Internet connection
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

## Step 3: Clone the Vibe Project with GitHub Desktop

- Open GitHub Desktop
- Click **File** → **Clone repository**
- Click the **URL** tab
- In **Repository URL**, paste: `https://github.com/gexijin/vibe`
- Choose where to save the project (the **Local Path** field)
- Click **Clone**

## Step 4: Open Project in VS Code

- In VS Code, click **File** → **Open Folder**
- Navigate to the `vibe` folder you just cloned
- Click **Select Folder**

## Step 5: Reopen in Container

- Look for a notification: **Folder contains a Dev Container configuration file**
- Click **Reopen in Container**
- If you don't see the notification, click the green icon in the bottom-left corner and select **Reopen in Container**
- VS Code builds the container (5-10 minutes the first time)
- When complete, the green icon shows **Dev Container: R in Docker**

## Step 6: Understand the Container Environment

You're now coding inside a Linux container.

- Click **Terminal** → **New Terminal**
- Check your location:
  ```bash
  pwd
  ```

You'll see `/workspaces/vibe`—your project folder inside the container.

- List the files:
  ```bash
  ls
  ```

You'll see the project files: `R/`, `.devcontainer/`, `README.md`, etc.

- Try going up one directory:
  ```bash
  cd ..
  ls
  ```

You'll only see `vibe/`—the container is isolated. You can't access your computer's other folders.

- Return to the project:
  ```bash
  cd vibe
  ```

## Step 7: Run R Code Line by Line

- In VS Code Explorer, navigate to `R/iris_analysis.R`
- Click to open the file
- Select the first line: `data(iris)`
- Press `Ctrl+Enter` (Windows/Linux) or `Cmd+Enter` (Mac) to run it
- The first time creates an R terminal; the second runs the code
- Continue running each line one at a time
- When you run `head(iris)`, you'll see the first 6 rows
- When you run `summary(iris)`, you'll see statistical summaries
- When you run `hist()`, a plot window opens

## Step 8: Install Shiny Extension and Run the App

- Click the **Extensions** icon in the left sidebar
- Search for `Posit.shiny`
- Click **Install** on the **Shiny** extension by Posit
- In VS Code Explorer, navigate to `R/app.R`
- Click to open the file
- Look for the **▶** button at the top right of the editor
- Click the dropdown and select **Run Shiny App**
- A notification appears: **Open in Browser**
- Click **Open in Browser**
- Move the slider to change the histogram bins—the chart updates in real-time

## Step 9: Make a Simple Change

- Keep the app running
- In VS Code, edit `R/app.R`
- Find line 16: `titlePanel("Old Faithful Geyser Data")`
- Change it to:
  ```r
  titlePanel("My First R Docker App")
  ```
- Click **File** → **Save**
- Refresh your browser
- The title now shows your custom text

## Step 10: Understanding the Dockerfile (Optional)

- In VS Code Explorer, navigate to `.devcontainer/Dockerfile`
- Click to open the file

**Key parts:**
- `FROM rocker/shiny-verse:latest` - Base image with R, Shiny, and tidyverse pre-installed
- `RUN apt-get install` - Linux system libraries for R packages
- `RUN R -q -e 'install.packages(...)'` - Permanently installs R packages
- `EXPOSE 3838` - Opens port 3838 for Shiny apps

**Other Rocker images:**
- `rocker/r-ver:4.5.3` - Just R (specific version)
- `rocker/rstudio:latest` - R with RStudio Server
- `rocker/tidyverse:latest` - R with tidyverse packages
- `rocker/shiny-verse:latest` - R with Shiny and tidyverse (what we're using)

## Step 11: Install R Packages Permanently (Optional)

Packages installed via `install.packages()` in the R console are temporary. To make them permanent:

- Open `.devcontainer/Dockerfile`
- Find line 11: `RUN R -q -e 'install.packages(c("rstudioapi", "languageserver"), ...)'`
- Add a new line below:
  ```dockerfile
  RUN R -q -e 'install.packages("data.table", repos="https://cloud.r-project.org")'
  ```
- Click **File** → **Save**
- Click the green icon in bottom-left corner
- Select **Rebuild Container**
- Wait for rebuild (2-5 minutes)
- Verify by opening an R terminal:
  ```r
  library(data.table)
  ```

## Next Steps

- Create a new R script in the `R/` folder using built-in datasets like `mtcars` or `iris`
- Add packages to the Dockerfile and rebuild the container
- Explore tidyverse with `dplyr` and `ggplot2`

## Troubleshooting

- **Docker Desktop not running** - Open Docker Desktop and wait for the green status indicator before reopening the container.
- **Container build fails** - Check your internet connection; the first build downloads ~2GB. Click **Rebuild Container** to retry.
- **Port 3838 already in use** - Stop other apps using that port, or change it in `.devcontainer/devcontainer.json`.

## Workflow Overview

- **VS Code** provides the code editor with syntax highlighting and IntelliSense
- **Docker container** runs an isolated Linux environment with R and dependencies
- **Rocker image** includes R, Shiny, tidyverse, and development tools
- **Dev Container config** automatically installs VS Code extensions
- **Port forwarding** lets you access Shiny apps from your browser

## Everyday Workflow

- **Start Docker Desktop** - Open the app and wait for green status
- **Open VS Code** - Open your project folder
- **Reopen in Container** - Click the green icon and select **Reopen in Container** if needed
- **Write and run code** - Edit `.R` files, run with `Ctrl+Enter`/`Cmd+Enter`, or run Shiny apps
- **Save your work** - Code files are saved to your computer and persist across sessions
- **Commit and push** - Use GitHub Desktop to commit and push changes

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
