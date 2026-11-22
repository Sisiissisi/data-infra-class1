# Lab 3 · Reflection and project dataset choice

**Name:**
**Due:** Sunday, November 15 at 11:59 PM

Answer in a few sentences each. Specific beats long.

**1. Your checks.** Which of your five checks would you be most worried to see fail, and what would go wrong downstream if it did?
I would be most worried about the uniqueness check failing. In this lab, I found duplicate permit records and records with the same permit number but different issue dates. If I do not identify these problems, I may overcount sidewalk shed permits and get inaccurate results when comparing community districts.

**2. Local vs. cloud.** Your data now lives in two places: `lab3.duckdb` in your Codespace and a table on MotherDuck. When would you want each one?
I would use local DuckDB to clean data, run quality checks, and test my analysis. I would use MotherDuck to store validated data and make it available for my interactive website. This would allow my website to access the data without depending on my local Codespace.
**3. The reading.** *Fundamentals of Data Engineering* Chapter 7 describes ingestion as more than "download the file": how often data arrives, whether you take a full copy or only what changed, and what happens when the source changes its format. Pick one of those and say how it applies to your API.
My API data is updated daily, so I would collect a full snapshot of Manhattan sidewalk shed permits each day. I would choose a full copy instead of only new records because older permits may have status changes or corrections. This would help me track changes and keep my analysis more accurate.

---

## Project dataset choice

**API name and link to its documentation:
API: NYC Open Data — DOB NOW: Build – Approved Permits

Dataset: https://data.cityofnewyork.us/d/rbx6-tga4

API Documentation: https://dev.socrata.com/docs/endpoints

**The request URL you used** (no keys or tokens in it):
https://data.cityofnewyork.us/resource/rbx6-tga4.json?%24select=work_permit%2Csequence_number%2Cfiling_reason%2Cwork_type%2Cborough%2Cbin%2Ccommunity_board%2Cissued_date%2Cexpired_date%2Cpermit_status&%24where=upper%28borough%29%3D%27MANHATTAN%27+AND+work_type%3D%27Sidewalk+Shed%27+AND+issued_date+IS+NOT+NULL&%24order=issued_date+DESC%2C%3Aid+ASC&%24limit=2



**Sample response** (paste 1–2 records, or a short excerpt):

```
[
  {
    "work_permit": "M01412019-S1-SH",
    "sequence_number": "1",
    "filing_reason": "Initial Permit",
    "work_type": "Sidewalk Shed",
    "borough": "Manhattan",
    "bin": "1084726",
    "community_board": "108",
    "issued_date": "2026-11-20T00:00:00.000",
    "expired_date": "2027-01-01T00:00:00.000",
    "permit_status": "Permit Issued"
  }
]
```

**What one row means (the grain):
Each row represents one sidewalk shed permit record, including initial permits and renewals. One row does not necessarily represent one unique physical sidewalk shed.

**Why it fits your project idea** (2–3 sentences):
My project examines how sidewalk shed permits are distributed across Manhattan and how permit age varies by community district. This API provides permit dates, community board codes, and renewal information, which can help me analyze these patterns. I also want to explore how long-standing sidewalk sheds affect people's experiences of public space.

---

## Set up your MotherDuck token (do this once)

Your token is a password. It goes in a Codespaces secret, **never** in a notebook, a file, or an AI chat.

1. Go to **app.motherduck.com** → click your name (bottom left) → **Settings** → **Access Tokens** → **Create token**. Name it `codespaces`, then copy it.
2. Go to **github.com** → your profile picture → **Settings** → **Codespaces** (left menu) → **New secret**.
3. Name: `MOTHERDUCK_TOKEN` (GitHub shows secret names in capitals). Value: paste the token. Under **Repository access**, pick your course repo. Click **Add secret**.
4. Back in your Codespace, a banner may offer to reload. If not: **Cmd+Shift+P** → type **Rebuild** → choose **Codespaces: Rebuild Container**, or stop and restart the Codespace.
5. Rerun cell A7. It should print `rows_in_cloud`.

---

**Checklist before you submit**

- [x] `notebooks/lab3_live_data.ipynb`: Part A run in class; Part B completed with your own API (two or more pages, five checks with a why for each, written to MotherDuck)
- [x] This file answered, including the project dataset choice
- [ ] No token anywhere in your files: tokens start with `eyJ`, so search your repo (Cmd+Shift+F) for `eyJ`
- [ ] Notebook saved (Cmd+S), then committed and pushed
- [ ] Repo URL submitted on CourseWorks
