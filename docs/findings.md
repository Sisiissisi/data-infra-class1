# Findings report

Three things your data shows, each backed by one of your published tables.
Next week you'll ask your AI app these questions and check whether it gets the same answers.

## Finding 1 Distribution of Sidewalk Shed Permits

**What I found** (one or two sentences, with a number):
Manhattan Community Board 108 has the highest number of sidewalk shed permit records, with 165 records covering 152 distinct buildings. Community Board 105 ranks second with 141 records.

**From table:** `course.main.shed_top_districts`

**The query or row that shows it:**

```
SELECT
    community_board,
    permit_records,
    distinct_buildings
FROM course.main.shed_top_districts
ORDER BY permit_records DESC
LIMIT 5;

```

**A question a user could ask the app to discover this:
Which Manhattan Community Boards have the most sidewalk shed permit records?**

## Finding 2 Permit Renewals

**What I found:
Community Board 108 has 138 renewal records out of 165 total permit records. This shows that renewals account for a large share of the permit records in this community board.**

**From table:** `course.main.shed_by_district`

**The query or row that shows it:**

```
SELECT
    community_board,
    renewal_records,
    permit_records
FROM course.main.shed_by_district
ORDER BY renewal_records DESC
LIMIT 5;
```

**A question a user could ask the app to discover this:
Which Manhattan Community Boards have the most sidewalk shed permit renewals?**

## Finding 3 Monthly Permit Records


**What I found:
The dataset contains 741 sidewalk shed permit records issued in November 2026 and 293 in October 2026. However, the pipeline only covers the past 30 days, so these numbers represent partial months.

**From table:** `course.main.shed_by_month`

**The query or row that shows it:**

```
SELECT
    issued_month,
    permit_records
FROM course.main.shed_by_month
ORDER BY issued_month DESC;

```

**A question a user could ask the app to discover this:**
How many sidewalk shed permit records were issued each month in the available data?

---

## What this data can't tell you

One limit a reader should know before trusting these findings (missing places, short time span, how values are collected):
The dataset counts permit records rather than physical sidewalk sheds, so one shed may be associated with multiple permits or renewals.
The current pipeline only collects data from the past 30 days, which means it cannot show long-term trends or the full history of sidewalk sheds in Manhattan. It also cannot confirm whether each sidewalk shed is still physically installed.
