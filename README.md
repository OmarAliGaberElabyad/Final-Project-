# Final Project - GitHub Repository Analysis

## Project Description

This project collects data about GitHub repositories using the GitHub API.

The collected data is then analyzed using Python, SQLite, SQL queries, and data visualization.

## Project Goals

The main goals of this project are:

- Collect repository data from GitHub.
- Save the collected data in a CSV file.
- Store the data in a SQLite database.
- Analyze the data using SQL queries.
- Create charts to visualize the results.
- Upload the complete project to GitHub.

## Technologies Used

- Python
- GitHub API
- Pandas
- Requests
- SQLite
- SQL
- Matplotlib
- Git
- GitHub

## Project Files

### github_project.py

This is the main Python file.

It collects data from GitHub, creates a CSV file, creates a SQLite database, performs SQL analysis, and creates charts.

### github_repositories.csv

This file contains the collected repository data.

### github_data.db

This is the SQLite database used to store the project data.

### top_repositories.png

This chart shows the top GitHub repositories based on the number of stars.

### languages.png

This chart shows the most common programming languages in the collected data.

## How the Project Works

1. The program connects to the GitHub API.
2. It collects information about GitHub repositories.
3. The information is stored in a Pandas DataFrame.
4. The data is saved in a CSV file.
5. The data is stored in a SQLite database.
6. SQL queries are used to analyze the data.
7. Charts are created using Matplotlib.

## How to Run the Project

First, install the required libraries:

```bash
pip install requests pandas matplotlib
