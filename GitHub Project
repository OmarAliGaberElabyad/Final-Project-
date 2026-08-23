import requests
import pandas as pd
import sqlite3
import matplotlib.pyplot as plt

# Number of repositories that we want to collect
number_of_repos = 30

# GitHub API link
url = "https://api.github.com/search/repositories"

# Search settings
params = {
    "q": "data",
    "sort": "stars",
    "order": "desc",
    "per_page": number_of_repos
}

print("Getting data from GitHub...")

# Get data from GitHub
response = requests.get(url, params=params)

# Convert the response to JSON
github_data = response.json()

# Empty list to store the data
repos_data = []

# Get the information that we need from every repository
for repo in github_data["items"]:

    repo_info = {
        "name": repo["name"],
        "owner": repo["owner"]["login"],
        "stars": repo["stargazers_count"],
        "forks": repo["forks_count"],
        "language": repo["language"],
        "created_at": repo["created_at"],
        "url": repo["html_url"]
    }

    repos_data.append(repo_info)

# Create a DataFrame
df = pd.DataFrame(repos_data)

# Replace missing programming languages
df["language"] = df["language"].fillna("Unknown")

# Save the data as CSV
df.to_csv("github_repositories.csv", index=False)

print("CSV file created successfully!")
print("\nFirst 5 rows:")
print(df.head())

# -------------------------
# SQLite Database
# -------------------------

print("\nCreating SQLite database...")

# Connect to the database
conn = sqlite3.connect("github_data.db")

# Save DataFrame in the database
df.to_sql("repositories", conn, if_exists="replace", index=False)

# -------------------------
# SQL Analysis
# -------------------------

print("\nTop 10 repositories by stars:")

query1 = """
SELECT name, stars, forks, language
FROM repositories
ORDER BY stars DESC
LIMIT 10
"""

top_repos = pd.read_sql_query(query1, conn)

print(top_repos)

print("\nNumber of repositories for each language:")

query2 = """
SELECT language, COUNT(*) AS total
FROM repositories
GROUP BY language
ORDER BY total DESC
"""

language_data = pd.read_sql_query(query2, conn)

print(language_data)

# Close database
conn.close()

# -------------------------
# Visualization
# -------------------------

print("\nCreating charts...")

# Chart 1: Top repositories by stars
top_repos = top_repos.sort_values("stars")

plt.figure(figsize=(10, 6))

plt.barh(
    top_repos["name"],
    top_repos["stars"]
)

plt.title("Top GitHub Repositories by Stars")
plt.xlabel("Stars")
plt.ylabel("Repository")

plt.tight_layout()

plt.savefig("top_repositories.png")

plt.show()


# Chart 2: Programming languages
languages = df["language"].value_counts().head(10)

plt.figure(figsize=(10, 6))

plt.bar(
    languages.index,
    languages.values
)

plt.title("Most Common Programming Languages")
plt.xlabel("Language")
plt.ylabel("Number of Repositories")

plt.xticks(rotation=45)

plt.tight_layout()

plt.savefig("languages.png")

plt.show()

print("\nProject finished successfully!")
