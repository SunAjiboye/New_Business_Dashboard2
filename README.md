# New_Business_Dashboard2
---
title: "README: Retail Dashboard Shiny App"
Retail Dashboard Shiny App
Overview
This project is an interactive Shiny dashboard for visualizing retail sales data from online_retail.xlsx. It features vibrant visualizations, including value boxes with coral-like, emerald-like, and sapphire-like gradients, geospatial scatter plots, sales bar charts, monthly sales trends, and a country coordinates table. The app includes reactive widgets for filtering by country, date range, sales threshold, and customizing plot themes and colors. Geospatial processing adds country coordinates to the data, and performance optimizations (caching, debouncing, sampling) ensure fast rendering.
Features

Value Boxes: Display unique customers, total sales, and average order value with red (coral-like), green (emerald-like), and blue (sapphire-like) gradients.
Plots:
Scatter Plot: Customer locations on a longitude-latitude map, colored by country or quantity (sampled to 1000 points for performance).
Bar Plot: Total sales by country with customizable colors and optional white borders.
Line Plot: Monthly sales trends with a blue-to-coral gradient.


Interactive Widgets:
Filter by multiple countries, date range, and minimum sales.
Customize plot themes (theme_minimal, theme_dark, etc.), color palettes (Custom, Set1, Paired), scatter point size, and bar borders.
Toggle plot visibility and table columns/rows.


Country Table: Displays coordinates for selected countries with server-side rendering.
Performance:
Cached data (retail_data_merged.rds, sales_by_country.rds, etc.) for faster loading.
Debounced filtering (500ms) to reduce reactive overhead.
Sampled scatter plot and pre-aggregated data for plots.



Prerequisites

R: Version 4.0 or higher (download from CRAN).
RStudio: Recommended for running Shiny apps (download from RStudio).
Dependencies: Install required R packages:install.packages(c("DT", "shinydashboard", "RColorBrewer", "bslib", "shiny", "dplyr", "ggplot2", "lubridate", "sf", "rnaturalearth"))


Data: Ensure the following files are in your working directory:
retail_data_merged.rds: Merged retail data with coordinates.
country_data.rds: Country coordinates.
sales_by_country.rds: Pre-aggregated sales by country.
monthly_sales.rds: Pre-aggregated monthly sales.
If these are missing, regenerate them using geospatial.R and online_retail.xlsx.



Setup

Clone the Repository:git clone <repository-url>
cd <repository-folder>


Install Dependencies:Run the following in R or RStudio:install.packages(c("DT", "shinydashboard", "RColorBrewer", "bslib", "shiny", "dplyr", "ggplot2", "lubridate", "sf", "rnaturalearth"))


Prepare Data:
If you have retail_data_merged.rds, country_data.rds, sales_by_country.rds, and monthly_sales.rds, place them in the working directory.
If not, ensure online_retail.xlsx is available and run the geospatial processing script:source("geospatial.R")

This generates the required .rds files.



Usage

Run the Shiny App:
Open app.R in RStudio and click "Run App", or run:source("app.R")


The app will open in a browser or RStudio viewer.


Interact with the Dashboard:
Data Filters:
Select countries (e.g., united kingdom, france) or "All".
Adjust the date range (e.g., 2010-12-01 to 2011-12-31).
Set a minimum sales threshold via the slider.


Plot Customization:
Choose a color variable (Country, Quantity).
Select a plot theme (Minimal, Dark, etc.).
Pick a color palette (Custom, Set1, Paired).
Toggle bar borders and adjust scatter point size.


Display Options:
Show/hide scatter, bar, or line plots.
Set table rows (5–50) and select columns (Country, Longitude, Latitude).




View Outputs:
Value Boxes: Unique customers (red/coral), total sales (green/emerald), average order value (blue/sapphire).
Plots: Geospatial scatter, country sales bar, monthly sales line.
Table: Country coordinates with sapphire header and alternating row colors.



File Structure
retail-dashboard/
├── app.R                    # Shiny app script
├── geospatial.R             # Geospatial processing script
├── online_retail.xlsx       # Input data (required if regenerating .rds files)
├── retail_data_merged.rds   # Cached retail data with coordinates
├── country_data.rds         # Cached country coordinates
├── sales_by_country.rds     # Cached sales by country
├── monthly_sales.rds        # Cached monthly sales
├── README.md                # This file

Troubleshooting

Error: "Invalid color: coral/emerald/sapphire":
Ensure app.R uses color = "red", color = "green", color = "blue" in valueBox calls, styled via CSS.
Check the CSS in app.R for .bg-red, .bg-green, .bg-blue classes.


Error: Palette has fewer colors than values:
The app now uses 38 colors to handle all countries. If errors persist, check unique(retail_data$Country) and share output.


Slow Performance:
Verify that .rds files are used (faster than processing online_retail.xlsx).
Check nrow(retail_data); if large (>100,000 rows), consider further sampling in app.R.


Missing Cache Files:
Run geospatial.R with online_retail.xlsx in the working directory to generate .rds files.


Table Not Rendering:
Check console for Unique countries and Country table before rendering logs.
Share any warnings (e.g., missing coordinates).


General Issues:
Share console output, str(retail_data), and browser details (e.g., Chrome, Firefox).
Ensure all packages are installed and up-to-date.



Contributing
Contributions are welcome! Please:

Fork the repository.
Create a branch (git checkout -b feature/your-feature).
Commit changes (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a pull request.

License
This project is licensed under the MIT License.
MIT License

Copyright (c) 2025 [Sun Ajiboye, sun.ajiboye@outlook.com]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.


