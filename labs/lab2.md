# Lab 2 · Reflection

**Name:**
**Due:** Sunday, November 8 at 11:59 PM

Answer in a few sentences each. Specific beats long.

**1. Your join.** Which column connected your two tables? How many rows went in, how many came out, and what did you do about anything that didn't match?
I used Code and Year as a composite key to join the two tables. Table A had 21,565 rows, and Table B had 7,445 rows. After the inner join, 6,767 rows remained. Some rows did not match because of different year coverage or missing country codes. I excluded unmatched rows to compare life expectancy and GDP per capita for the same country and year.

**2. The reading.** Kleppmann describes tables (relational), documents (nested, like JSON) and graphs as different ways to model data. Would any of your two tables have been easier to work with as a document or a graph? Why or why not?
I think relational tables are more suitable for my datasets. As Kleppmann explains, relational models are useful for joining structured data, while document and graph models are better suited to nested or highly connected data. My two datasets are organized by country and year, so I can easily join them using Code and Year to compare life expectancy and GDP per capita.

---

**Checklist before you submit**

- [x] `notebooks/lab2_joins.ipynb`: Part A run in class, Part B completed with your own tables
- [ ] Every Part B text cell filled in (grain, unmatched rows, what the result tells you)
- [ ] This file answered
- [ ] Notebook saved (Cmd+S), then committed and pushed
- [ ] Repo URL submitted on CourseWorks
