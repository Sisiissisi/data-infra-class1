# App evaluation

<!--
Lab 5. Ask your app five questions and judge each answer like an editor would.
Use your findings (docs/findings.md) for the first three: you already know the right answer,
so you can tell whether the app got it right.
Open "How this answer was made" every time: read the SQL and the rows, not just the sentence.
-->

**App URL:** https://sidewalk-sheds-sisi.streamlit.app/

**Tables the app uses:**

- `course.main.shed_permits_clean`
- `course.main.shed_by_district`
- `course.main.shed_by_month`
- `course.main.shed_top_districts`

## The five questions

| # | Kind | Question you asked | What the app said | SQL right? (yes / partly / no) | Verdict (good / weak / wrong) | Why |
|---|---|---|---|---|---|---|
| 1 | From finding 1 | Which Manhattan Community Boards have the most sidewalk shed permit records? | CB 108 has 164 records, CB 105 has 146, and CB 107 has 119. | Yes| Good | The answer matches the returned data. The small differences from my previous findings are likely due to the rolling 30-day data window. |
| 2 | From finding 2 | Which Manhattan Community Boards have the most sidewalk shed permit renewals? | CB 108 has 137 renewal records, followed by CB 105 with 130 and CB 107 with 102. | Yes| Good | The AI used the correct column, and its answer matches the returned data. |
| 3 | From finding 3 | How many sidewalk shed permit records were issued in each month covered by the dataset? | There were 248 records in October 2026 and 791 in November 2026. | Yes | Weak | The numbers are correct, but the AI did not explain that both months were only partially covered. The difference does not necessarily show a monthly increase. |
| 4 | A harder one | What percentage of permits are renewal permits? | The first answer was 0.0%. The second answer was 81.9%. | Partly | Wrong | The first answer was incorrect. The second used a reasonable calculation, but the different answers show that the AI is not always consistent. |
| 5 | One your data can't answer | Which borough has the most sidewalk shed permits? | The dataset only covers Manhattan, so it cannot compare different boroughs. | N/A | Good | The AI correctly identified the limitation of the dataset instead of guessing an answer. |



**Verdict guide**

- **Good:** right number, right table, the sentence matches the rows.
- **Weak:** roughly right, but it used the wrong table, missed a filter, or the sentence overstates what the rows show.
- **Wrong:** wrong number, an error, or it made up an answer to a question the data can't answer.

## One improvement, tested

**Question:** What percentage of permits are renewal permits?

**What was wrong:** The AI initially answered 0.0%, which was inconsistent with my previous findings that many permit records were renewals.

**What I changed:**

- [ ] the data dictionary (`docs/data_dictionary.md`)
- [x] `extra_instructions` in `app.toml`
- [ ] a new or changed table in `project.toml`

I added an instruction to calculate the percentage by dividing the sum of `renewal_records` by the sum of `permit_records` from `course.main.shed_by_district` and multiplying by 100.

**Before:** Renewal permits make up 0.0% of all permits.

**After:** Renewal permits make up about 81.9% of the total permits.


## What leaves your control

This is acceptable for my project because the sidewalk shed permit data comes from NYC Open Data and is publicly available. However, if I used non-public data, I would remove sensitive and personal information before sending any data to the AI. I would also use an AI service with stronger privacy and data protection policies.

