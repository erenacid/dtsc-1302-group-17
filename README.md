# DTSC 1302 – Group 17: College Cost Analysis

This project analyzes the cost of attending U.S. colleges using the `College_Data_17.csv` dataset.  
We engineer new features, explore relationships between variables, and build a multiple linear regression model to understand how institutional spending and enrollment characteristics relate to overall student cost. We also compare private vs. public institutions on both cost and expenditure.

## Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Research Questions](#research-questions)
- [Methods](#methods)
- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
- [How to Run the Notebooks](#how-to-run-the-notebooks)
- [Results Summary](#results-summary)
- [Notes and Limitations](#notes-and-limitations)
- [Contributors](#contributors)

---

## Project Overview

The goal of this project is to explore factors that drive the **total cost** of attending a college and to understand how those costs differ between **private** and **public** institutions.

We:

- Engineer a combined **Cost** variable that aggregates several student expense categories.
- Create additional features that capture:
  - Total undergraduate enrollment (`Undergrad`)
  - Enrollment yield (`Enrollment`)
  - Acceptance rate (`Acceptance`)
- Explore relationships between cost and key predictors using:
  - Scatterplots and pairplots
  - Correlation matrices
  - Distribution plots
- Fit an **OLS multiple linear regression model** to predict cost.
- Check model assumptions using VIF and component-plus-residual (CCPR) plots.
- Compare average **cost** and **expenditure per student** between private and public institutions.

---

## Dataset

**File:** `College_Data_17.csv`  
**Source:** Hosted in this repository and loaded via raw GitHub URL.

Key columns used (not exhaustive):

- `Private`: Whether the college is private (`Yes`/`No`)
- `Outstate`: Out-of-state tuition
- `Room.Board`: Room and board cost
- `Books`: Book cost
- `Personal`: Personal expenses
- `P.Undergrad`: Part-time undergraduate enrollment
- `F.Undergrad`: Full-time undergraduate enrollment
- `Apps`: Number of applications received
- `Accept`: Number of students accepted
- `Enroll`: Number of students enrolled
- `Expend`: Instructional expenditure per student
- `Top10perc`, `Terminal`, etc. (other institutional quality measures, some of which are dropped in feature engineering)

### Engineered Features

We create several new columns:

- `Cost`  
  ```python
  df['Cost'] = df['Outstate'] + df['Room.Board'] + df['Books'] + df['Personal']
