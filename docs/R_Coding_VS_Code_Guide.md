[Home](./)

# R Coding in VS Code

You want to write R code but RStudio feels heavy or you prefer VS Code's flexibility. Think of VS Code as a Swiss Army knife—it can handle R, Python, and many other languages in one lightweight editor. This tutorial shows you how to set up R in VS Code with smart features like code completion, interactive plots, and Shiny apps.

## Key Concepts

- **[languageserver](https://github.com/REditorSupport/languageserver)** - R package that enables code completion, syntax checking, and hover documentation in VS Code
- **[R Extension](https://marketplace.visualstudio.com/items?itemName=REditorSupport.r)** - VS Code extension that connects your editor to R with syntax highlighting, code execution, and debugging
- **[Shiny Extension](https://marketplace.visualstudio.com/items?itemName=Posit.shiny)** - VS Code extension for creating and running interactive Shiny web apps with auto-reload

## What You'll Need

- VS Code already installed
- Internet connection to download R and packages
- Basic familiarity with installing software
- 15-20 minutes

## Step 1: Install or Update R

You need R version 4.0 or higher for the best compatibility.

**Windows:**
- Download the latest R from [CRAN Windows](https://cran.r-project.org/bin/windows/base/) and run the installer
- **Note the installation path** (for example: `C:\Program Files\R\R-4.5.3`)
- If you have an old version, uninstall it first via **Settings** → **Apps**

**macOS:**
- Download from [CRAN macOS](https://cran.r-project.org/bin/macosx/) and run the .pkg installer
- Note whether you're using Intel (`/Library/Frameworks/R.framework/Resources/bin/R`) or Apple Silicon with Homebrew (`/opt/homebrew/bin/R`)

**Linux:**
- Use your package manager (e.g., `sudo apt install r-base` on Ubuntu)
- Or follow [CRAN Linux](https://cran.r-project.org/bin/linux/) instructions

## Step 2: Install R Extensions in VS Code

- Open VS Code
- Click the **Extensions** icon in the left sidebar
- Search for `REditorSupport.r` and click **Install** on the R extension by REditorSupport
- Search for `Posit.shiny` and click **Install** on the Shiny extension by Posit

## Step 3: Find Your R Installation Path

Before configuring VS Code, find where R is installed on your system.

**Windows:**
- Open **File Explorer**
- Navigate to `C:\Program Files\R\`
- You'll see a folder like `R-4.5.3` (your version may differ)
- Open that folder → Open the `bin` folder
- The full path is: `C:\Program Files\R\R-4.5.3\bin\R.exe`

**macOS:**
- Open **Terminal** and type:
  ```bash
  which R
  ```
- Common paths:
  - Standard installation: `/Library/Frameworks/R.framework/Resources/bin/R`
  - Homebrew on Apple Silicon: `/opt/homebrew/bin/R`
  - Homebrew on Intel: `/usr/local/bin/R`

**Linux:**
- R is typically at `/usr/bin/R`
- Verify by running `which R` in terminal

## Step 4: Configure VS Code to Find R

- In VS Code, click the **gear icon** in the lower left corner
- Select **Settings**
- In the search bar, type `r.rpath.windows` (Windows), `r.rpath.mac` (macOS), or `r.rpath.linux` (Linux)
- Click **Edit in settings.json** below the setting
- Add the appropriate configuration inside the curly braces `{}`

**For Windows** (replace `R-4.5.3` with your version):
```json
"r.rpath.windows": "C:\\Program Files\\R\\R-4.5.3\\bin\\R.exe",
```

**Why two backslashes?** In JSON, the backslash `\` is a special character. To represent a single backslash, you must type `\\`.

**For macOS:**
```json
"r.rpath.mac": "/Library/Frameworks/R.framework/Resources/bin/R",
```

Or if using Homebrew on Apple Silicon:
```json
"r.rpath.mac": "/opt/homebrew/bin/R",
```

**For Linux:**
```json
"r.rpath.linux": "/usr/bin/R",
```

- Click **File** → **Save**
- **Restart VS Code** for changes to take effect

## Step 5: Install Required R Packages

- In VS Code, click **View** → **Command Palette**
- Type `R: Create R Terminal` and select it
- An R console appears in the terminal panel
- Install packages by typing:
  ```r
  install.packages("languageserver")
  install.packages("shiny")
  ```
- Wait for installation to complete
- Type `q()` and press **Enter** to exit R
- Type `n` when asked about saving workspace

## Step 6: Create Your R Project

- Create a new folder on your computer (e.g., `my-r-project`)
- In VS Code, click **File** → **Open Folder** and select your new folder
- Click **File** → **New File**
- Click **File** → **Save** and name it `analysis.R`

## Step 7: Write Your First R Script

Type this code into `analysis.R`:

```r
# Load the iris dataset
data(iris)

# View the first few rows
head(iris)

# Generate summary statistics
summary(iris)

hist(iris$Sepal.Length)
```

- Click **File** → **Save**

## Step 8: Run R Code Interactively

- With `analysis.R` open, select a line of code
- Press `Ctrl+Enter` (Windows/Linux) or `Cmd+Enter` (Mac) to run it
- The first time opens an R terminal; the second runs the code
- Watch the output appear in the terminal
- The plot opens in a separate window
- Select multiple lines and run them together with the same shortcut

## Step 9: Create a Simple Shiny App

- Click **File** → **New File**
- Click **File** → **Save** and name it `app.R`
- Type this code:

```r
library(shiny)

ui <- fluidPage(
  titlePanel("Interactive Histogram"),

  sidebarLayout(
    sidebarPanel(
      sliderInput("bins",
                  "Number of bins:",
                  min = 5,
                  max = 50,
                  value = 30)
    ),

    mainPanel(
      plotOutput("histogram")
    )
  )
)

server <- function(input, output) {
  output$histogram <- renderPlot({
    x <- faithful$waiting
    bins <- seq(min(x), max(x), length.out = input$bins + 1)

    hist(x, breaks = bins, col = "steelblue", border = "white",
         xlab = "Waiting time (minutes)",
         main = "Distribution of Waiting Times")
  })
}

shinyApp(ui = ui, server = server)
```

- Click **File** → **Save**
- Look for the **▶** button at the top right of the editor
- Click the dropdown and select **Run Shiny App**
- The app opens in a browser or VS Code panel
- Move the slider to see the histogram update instantly

## Step 10: Use Code Completion and Hover Help

- In `analysis.R`, start typing `mea` on a new line
- A dropdown appears with suggestions—select `mean()` by pressing **Enter**
- Hover your mouse over `mean` in your code
- A popup shows function documentation and usage examples
- Try hovering over `lm`, `summary`, or `plot` to see their documentation

## Next Steps

- Create a multi-file Shiny app with separate `ui.R` and `server.R` files
- Explore [ggplot2](https://ggplot2.tidyverse.org/) for advanced data visualization
- Try the [tidyverse](https://www.tidyverse.org/) packages for data manipulation

## Troubleshooting

- **"R is not recognized" in VS Code terminal** - Check your settings.json (Step 4). Verify the R path is correct and points to `R.exe` (Windows) or the R binary (Mac/Linux). Restart VS Code after fixing.
- **R version mismatch in settings** - If you updated R, update the version number in your settings.json `r.rpath` configuration to match the new installation.
- **Code completion not working** - Make sure languageserver installed successfully (Step 5). Restart VS Code and wait 10-20 seconds after opening an R file.
- **Shiny app won't run** - Verify the Shiny extension is installed (Step 2), shiny package is installed (Step 5), and your file is named `app.R`.

## Workflow Summary

VS Code provides a modern, lightweight alternative to RStudio:

- **Unified environment** - Code R, Python, JavaScript, and more in one editor
- **Customizable** - Install only the extensions you need
- **Integrated terminal** - Run R, Git, and shell commands side-by-side
- **Shiny development** - One-click app launching with auto-reload
- **Version control** - Built-in Git integration

---

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 7, 2025.
