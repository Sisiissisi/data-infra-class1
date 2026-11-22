# Data dictionary

This file describes the tables your pipeline publishes. Copy the Columns section once per table. In Session 5, an AI model will read it to write SQL
against your data, so a clear description here means better answers there. Write it for a
smart reader who has never seen your data.

## The table 1

**Table name on MotherDuck:** ` course.main.shed_permits_clean`

**One row is:** (the grain, e.g. "one country in one year")
One distinct sidewalk shed permit record in Manhattan, including initial permits and renewals. One record does not necessarily represent one physical sidewalk shed.

**Source:** (API name and link to its documentation)
NYC Open Data — DOB NOW: Build – Approved Permits.
Dataset: https://data.cityofnewyork.us/d/rbx6-tga4
API documentation: https://dev.socrata.com/docs/endpoint

**Refreshed:** (e.g. "daily at 6 AM New York time by GitHub Actions; a full snapshot of the last 14 days")
The pipeline is scheduled to run daily through GitHub Actions and can also be run manually. The current configuration collects records issued within the past 30 days.

**Removed on purpose:** (rows the pipeline drops, and why, e.g. "regions like 'World', so averages count countries only")
Records outside Manhattan, records that are not sidewalk shed permits, and records outside the selected time period are excluded. Exact duplicate records are removed to avoid double counting.

## Columns


| Column | Type | What it means | Units or allowed values | Example |
|---|---|---|---|---|
| work_permit | VARCHAR | Permit identifier | Text | M01412019-S1-SH |
| sequence_number | BIGINT | Sequence number associated with a permit record | Integer | 1 |
| filing_reason | VARCHAR | Reason for the permit filing | Initial Permit, Renewal, etc. | Initial Permit |
| work_type | VARCHAR | Type of construction work | Sidewalk Shed | Sidewalk Shed |
| borough | VARCHAR | Borough where the permit is located | Manhattan | Manhattan |
| bin | VARCHAR | Building Identification Number | Building code | 1084726 |
| community_board | VARCHAR | Community Board identifier | Board code | 108 |
| issued_date | TIMESTAMP | Date when the permit was issued | Date and time | 2026-11-20 |
| expired_date | TIMESTAMP | Date when the permit expires | Date and time | 2027-01-01 |
| permit_status | VARCHAR | Status of the permit | Status category | Permit Issued |

## What this data can't tell you

(2–3 limits: years not covered, places missing, how values are estimated, anything a user might wrongly assume)
First, the dataset contains permit records rather than the exact number of physical sidewalk sheds. A single shed may have multiple permits or renewals.
Second, the current pipeline only collects records from the past 30 days, so it cannot show the complete permit history.
Third, the permit status does not independently confirm whether a sidewalk shed is currently installed.

## Example questions it can answer

1.How many sidewalk shed permit records were issued in Manhattan during the selected period?
2.How many records are initial permits and how many are renewals?
3.What are the issue and expiration dates of different permit records?

## The table 2

**Table name on MotherDuck:** ` course.main.shed_by_district`

**One row is:** (the grain, e.g. "one country in one year")
One Manhattan Community Board with summarized sidewalk shed permit information.

**Source:** (API name and link to its documentation)
NYC Open Data — DOB NOW: Build – Approved Permits, summarized from shed_permits_clean.
Dataset: https://data.cityofnewyork.us/d/rbx6-tga4
API documentation: https://dev.socrata.com/docs/endpoints

**Refreshed:** (e.g. "daily at 6 AM New York time by GitHub Actions; a full snapshot of the last 14 days")
The pipeline is scheduled to run daily through GitHub Actions and can also run manually. The current table summarizes permit records from the past 30 days.

**Removed on purpose:** (rows the pipeline drops, and why, e.g. "regions like 'World', so averages count countries only")
Records without Community Board information are excluded from this summary because they cannot be assigned to a district. Exact duplicate records have already been removed from the clean table.


## Columns

| Column | Type | What it means | Units or allowed values | Example |
|---|---|---|---|---|
| community_board | VARCHAR | Community Board identifier | Board code | 108 |
| permit_records | BIGINT | Total number of permit records in the board | Records | 165 |
| distinct_buildings | BIGINT | Number of distinct buildings identified by BIN | Buildings | 152 |
| distinct_permit_numbers | BIGINT | Number of distinct work permit identifiers | Permits | Nonnegative integer |
| renewal_records | BIGINT | Number of permit records identified as renewals | Records | 138 |
| median_days_since_issue | DOUBLE | Median number of days since permit issuance | Days | Numeric value |



## What this data can't tell you

(2–3 limits: years not covered, places missing, how values are estimated, anything a user might wrongly assume)
First, the table counts permit records, not physical sidewalk sheds. Multiple permit records may refer to the same structure.
Second, the median days since issue measures the time since the recorded permit was issued, not how long a sidewalk shed has remained installed.
Third, the table only uses recent data, so it cannot describe the full history of sidewalk sheds in each Community Board.



## Example questions it can answer

1.Which Manhattan Community Board has the most sidewalk shed permit records?
2.How many renewal permit records are there in each Community Board?
3.How does the median time since permit issuance differ across Community Boards?


## The table 3

**Table name on MotherDuck:** ` course.main.shed_by_month`

**One row is:** (the grain, e.g. "one country in one year")
One month of sidewalk shed permit issuance in Manhattan.

**Source:** (API name and link to its documentation)
NYC Open Data — DOB NOW: Build – Approved Permits, summarized from shed_permits_clean.
Dataset: https://data.cityofnewyork.us/d/rbx6-tga4
API documentation: https://dev.socrata.com/docs/endpoints

**Refreshed:** (e.g. "daily at 6 AM New York time by GitHub Actions; a full snapshot of the last 14 days")
The pipeline is scheduled to run daily through GitHub Actions. The table summarizes permits from the current 30-day data window.

**Removed on purpose:** (rows the pipeline drops, and why, e.g. "regions like 'World', so averages count countries only")
Records without an issue date are excluded because they cannot be assigned to a month. Exact duplicate records have already been removed from the clean table.

## Columns

| Column | Type | What it means | Units or allowed values | Example |
|---|---|---|---|---|
| issued_month | DATE | Month when the permits were issued | Month | 2026-11-01 |
| permit_records | BIGINT | Number of permit records issued during the month | Records | 741 |
| distinct_buildings | BIGINT | Number of distinct buildings identified by BIN | Buildings | Nonnegative integer |


## What this data can't tell you

(2–3 limits: years not covered, places missing, how values are estimated, anything a user might wrongly assume)
First, the table only covers the selected 30-day period, so it cannot show long-term trends in sidewalk shed permits.
Second, the first and last months may be incomplete because the data window does not cover full calendar months.
Third, the number of permit records does not represent the number of physical sidewalk sheds installed during each month.

## Example questions it can answer

1.How many sidewalk shed permit records were issued each month?
2.Which month has the most permit records within the available data?
3.How many distinct buildings have permit records in each month?

## The table 4

**Table name on MotherDuck:** ` course.main.shed_top_districts`

**One row is:** (the grain, e.g. "one country in one year")
One of the 10 Manhattan Community Boards with the highest number of sidewalk shed permit records.

**Source:** (API name and link to its documentation)
NYC Open Data — DOB NOW: Build – Approved Permits, summarized from shed_by_district.
Dataset: https://data.cityofnewyork.us/d/rbx6-tga4
API documentation: https://dev.socrata.com/docs/endpoints

**Refreshed:** (e.g. "daily at 6 AM New York time by GitHub Actions; a full snapshot of the last 14 days")
The pipeline is scheduled to run daily through GitHub Actions. The ranking is updated when the pipeline successfully processes new data.

**Removed on purpose:** (rows the pipeline drops, and why, e.g. "regions like 'World', so averages count countries only")
Community Boards outside the top 10 are excluded because this table is designed to show the ranking. Records without Community Board information were already excluded from the district summary.

## Columns

| Column | Type | What it means | Units or allowed values | Example |
|---|---|---|---|---|
| community_board | VARCHAR | Community Board identifier | Board code | 108 |
| permit_records | BIGINT | Number of permit records | Records | 165 |
| distinct_buildings | BIGINT | Number of distinct buildings by BIN | Buildings | 152 |
| renewal_records | BIGINT | Number of renewal records | Records | 138 |
| median_days_since_issue | DOUBLE | Median number of days since permit issuance | Days | Numeric value |


## What this data can't tell you

(2–3 limits: years not covered, places missing, how values are estimated, anything a user might wrongly assume)
First, the ranking is based on permit records, not the actual number of physical sidewalk sheds.
Second, the table only includes the top 10 Community Boards, so it does not show the complete distribution across Manhattan.
Third, the ranking is based on recent permit records and cannot tell us which Community Boards have the most long-standing sidewalk sheds.

## Example questions it can answer

1.Which 10 Manhattan Community Boards have the most sidewalk shed permit records?
2.Which Community Board has the most renewal permit records among the top 10?
3.How many distinct buildings have sidewalk shed permit records in each of the top 10 Community Boards?