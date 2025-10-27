# Autonomous CSV Data Analyst Crew

This project uses **CrewAI** to create an autonomous team of AI agents that perform a complete data analysis pipeline on any CSV file.

You provide a CSV, and the crew will automatically:
1.  **Ingest & Clean** the data.
2.  Perform **Exploratory Data Analysis (EDA)**.
3.  Generate **Visualizations** (as PNG files).
4.  Write a final **Markdown Report** with key insights and actionable recommendations.

---

> ⚠️ **CRITICAL SECURITY WARNING: REMOVE YOUR API KEY**
>
> Your code contains a hardcoded `OPENAI_API_KEY`. **Do not commit this file to GitHub or share it.** Anyone who sees it can use your key and spend your money.
>
> You must remove it and use a `.env` file instead. The instructions below show you exactly how to do this.

---

## Architecture: The Analyst Crew

The project works using a hierarchical CrewAI setup. A manager agent plans and delegates tasks to a team of specialists:

* **Analytics Manager:** The team lead. It reviews the goal, delegates tasks in order (Ingestion -> EDA -> Viz -> Insights), verifies the output of each step, and requests fixes if files are missing or malformed.
* **Data Ingestion & Cleaning Engineer:** Loads the raw CSV, cleans column names, handles missing values (NA), flags outliers, and saves the cleaned data as `df_cleaned.pkl` and a `schema.json`.
* **EDA Specialist:** Analyzes the cleaned data to find descriptive stats, correlations, and distributions. It outputs an `eda_summary.json` that includes a list of `candidate_plots` for the next agent.
* **Visualization Engineer:** Reads the `candidate_plots` list and generates the actual PNG plots (e.g., histograms, bar charts, line plots) using Matplotlib. It saves them to the `/out
