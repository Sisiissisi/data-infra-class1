# Labs 3 + 4 · Pipeline submission

**Name:**
**Due:** Sunday, November 22 at 11:59 PM

## Links

**A successful run of your pipeline** (Actions tab → the green run → copy the address):https://github.com/Sisiissisi/data-infra-class1/actions/runs/45069348222

**A deliberately failed run** (Run workflow with "Break the data on purpose" ticked → the red run → copy the address):https://github.com/Sisiissisi/data-infra-class1/actions/runs/45069759242

**Your table on MotherDuck:** `course.main.manhattan_sidewalk_sheds`

## Reflections

Answer in a few sentences each. Specific beats long.

**1. Your checks.** Which of your checks would you be most worried to see fail, and what would go wrong for a user of your app if bad data got through?
I would be most worried about the uniqueness check failing. In Lab 3, I found duplicate permit records and records with the same permit number but different issue dates. If these problems are not handled correctly, users may see inaccurate permit counts and analysis results.

**2. Run it twice.** What happens to your MotherDuck table if your pipeline runs twice in one day? How do you know?
If my pipeline runs twice in one day, the MotherDuck tables will be replaced instead of adding duplicate records. I know this because the pipeline uses CREATE OR REPLACE TABLE. The results may change if the API data has been updated between the two runs.

**3. Your schedule.** How often does your source actually update? Is daily the right schedule for it, and would you take a full copy or only what's new?
The NYC DOB dataset is updated daily, so running the pipeline once a day is appropriate. I would prefer to take a full copy because older permit records may have status changes or corrections. If I only collect new records, I might miss these updates.

**4. What leaves your control.** Next week an AI model will see your table's description and users' questions. Is there anything in your data, or anything a user might type, that shouldn't be sent to a free AI service? Why or why not?
My dataset comes from a public government API, so it does not contain the kind of private information I would expect in personal records. However, users might enter personal information in their questions, such as names or addresses. I would avoid sending this information to a free AI service without permission because I cannot fully control how it will be stored or used.

---

## Set up your secrets (once)

Your MotherDuck token is a password. It goes in two secret stores, **never** in a file, a notebook, or an AI chat.

**Get a token:** app.motherduck.com → your name (bottom left) → **Settings** → **Access Tokens** → **Create token**. Name it `codespaces`. Copy it.

**A. For your Codespace** (so `python pipeline.py` can publish):
github.com → your profile picture → **Settings** → **Codespaces** → **New secret**. Name `MOTHERDUCK_TOKEN`, paste the token, choose your course repo under **Repository access**, **Add secret**. Then restart your Codespace.

**B. For GitHub Actions** (so the daily run can publish):
your course repo on github.com → **Settings** (repo tab, not your profile) → **Secrets and variables** → **Actions** → **New repository secret**. Name `MOTHERDUCK_TOKEN`, paste the same token, **Add secret**.

If a token ever leaks, delete it in MotherDuck right away and make a new one (then update both secrets).

---

**Checklist before you submit**

- [ ] `project.toml` points to **your** API, with at least five checks of your own (each with a why) and at least three tables: one clean table and at least two analysis tables (trend, key metrics or ranking)
- [ ] `docs/findings.md`: three findings, each backed by one of your tables
- [ ] A green run and a red run on the Actions tab, both linked above
- [ ] `docs/data_dictionary.md` filled in for every table you publish
- [ ] This file answered
- [ ] No token anywhere in your files (tokens start with `eyJ`: search your repo with Cmd+Shift+F)
- [ ] Committed and pushed; repo URL submitted on CourseWorks
