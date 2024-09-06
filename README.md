# Hacker News Post Analysis

## Overview

This project analyzes Hacker News posts, focusing specifically on "Ask HN" and "Show HN" posts. The analysis includes:

- Counting the average number of comments per hour for "Ask HN" posts.
- Comparing comment activity between "Ask HN" and "Show HN" posts.
- Identifying the hours of the day when "Ask HN" posts receive the most engagement.

## Features

- Load and display the Hacker News dataset.
- Extract and filter "Ask HN" and "Show HN" posts.
- Analyze and visualize the average number of comments for "Ask HN" posts by hour of the day.

## Requirements

- Python 3.11
- Pandas library (`pip install pandas`)

## Instructions

1. Load the dataset using `pd.read_csv("hacks.csv")`.
2. Extract "Ask HN" and "Show HN" posts by filtering the dataset based on post titles.
3. Perform data analysis to compute the average number of comments per hour for "Ask HN" posts.
4. Use `.sort_values()` to rank the hours by the number of comments.

## Example Usage

```python
import pandas as pd

# Load dataset
hn = pd.read_csv("hacks.csv")

# Filter 'Ask HN' posts
ask_bol = hn["title"].str.lower().str.startswith("ask hn")
ask_posts = hn[ask_bol]

# Convert 'created_at' to datetime and extract hour
ask_posts["created_at"] = pd.to_datetime(ask_posts["created_at"])
ask_posts["hour"] = ask_posts["created_at"].dt.hour

# Calculate average comments by hour
avg_comnts = ask_posts.pivot_table(index="hour", values="num_comments", aggfunc="mean")

# Display results
print(avg_comnts.sort_values("num_comments", ascending=False).head())
```
