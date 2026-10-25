# Lab 1

**Name:**
**Due:** Sunday, October 25 at 11:59 PM
**Submit:** your repo URL in the Lab 1 assignment on CourseWorks

| Part | Where | File |
|---|---|---|
| **In class:** first DuckDB query on the penguins data | Session 1 | `notebooks/lab1_first_query.ipynb` |
| **At home:** two related tables of your own in DuckDB | Before Sunday | `notebooks/lab1_home_your_data.ipynb` |
| **At home:** lifecycle map of your data | Before Sunday | This file (below) |

---

## Lifecycle map of your data

In class we named five stages every data system has. Trace them for the two tables you loaded at home. Some rows ask what you did this week; the last two ask you to look ahead to the system you'll build by December. Educated guesses are fine; say where you're unsure.

**My tables:** (main table) + (second table)

| Stage | For your data | Your answer |
|---|---|---|
| **1. Ingestion** | Where did each file come from, and how did you get it (portal download, export, API)? If the source changed its format tomorrow, what would break?| I downloaded both CSV files from Our World in Data and uploaded them to the data folder in GitHub Codespaces. I then used DuckDB to load the files into two tables.If the source changes the column names or file format, my SQL queries may no longer work. |
| **2. Validation** | What did `DESCRIBE`, `SUMMARIZE` and the key check reveal? Name one check you'd want to run *every time* new data arrives. |I used DESCRIBE and SUMMARIZE to check the data types, missing values, and ranges. All column types were correct, but I found 1,348 records with missing country codes in the life expectancy dataset. The key check showed 204 shared code values between the two tables. I would check missing country codes and matching keys whenever new data arrives. |
| **3. Transformation** | What did you change to make the data usable (e.g. the missing-value fix)? What would you still need to clean, join or calculate to answer your question? | No data type corrections were needed. However, I would still need to handle missing country codes and regional records. I would also join the two tables using Code and Year to compare GDP per capita and life expectancy for the same country and year.|
| **4. Scheduling** | How often does the source publish updates (check its website)? If your app used this data, how often would it need to refresh to stay useful, and why? |According to Our World in Data, the life expectancy dataset is updated approximately annually, while the GDP dataset is updated periodically, with its next update expected in January 2027. If I built an app using these datasets, I would check for updates monthly and refresh the data when new versions are available. Daily updates are not necessary because these indicators change relatively slowly. |
| **5. Interface** | Who would want answers from this data? Write the plain-English question they'd ask, and what a good answer would show them. | Students, researchers, and the general public may be interested in how economic development relates to life expectancy. They might ask: "Do countries with higher GDP per capita also have higher life expectancy?" I would create an interactive website with maps and charts to show differences across countries and changes over time.|

**Which stage feels most fragile for your data, and why?** (two or three sentences)

---
I think validation is the most fragile stage because the two datasets have different geographic and time coverage. There are 1,348 records with missing country codes in the life expectancy dataset, and not all country codes match between the two tables. If I do not check these differences carefully, the analysis may produce incomplete or misleading results.
## Checklist before you submit

- [x] In-class notebook: every cell ran, including your own query and three observations
- [x] At-home notebook: both CSVs in `data/`, both tables loaded and checked, the key relationship described, five queries each with a one-line note, three observations, two dataset cards
- [ ] This lifecycle map filled in, plus the "most fragile" answer
- [ ] Every notebook saved (Cmd+S), then committed and pushed
- [ ] Repo URL pasted into CourseWorks
