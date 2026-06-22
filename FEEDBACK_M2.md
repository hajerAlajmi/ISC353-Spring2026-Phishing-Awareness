# M2 Pregrade — Instructor Feedback

**Pair 3** — Hajar Alajmi & Hajar Thamer Alsahaib
**Assigned project:** Project 1 — Phishing Simulation & Awareness Platform
**Reviewed commit:** `93ea025` on `main`
**Reviewed on:** 2026-05-03 (Sunday, the day of the M2 deadline)
**Reviewer:** Dr. Shaikhah Alkhadhr (sole grader, ISC353)

---

> **What this document is.** This is a **pregrade** — a formative review of your repository state ahead of the official M2 grading on **Tuesday, 2026-05-05** (two days after the M2 deadline). It is *not* your final mark. Treat the scores below as advisory: they show you exactly where the rubric currently lands based on what's in your repo today, and where the easiest points are still on the table. You have a short window to act on this feedback before the summative grade is locked in.
>
> The official M2 grade will be computed against **the full Moodle submission** (PDF report + GitHub repo + demo video). Several rubric rows below are scored as `0` *in this pregrade* simply because they live in the PDF/video, not the repo — they will be re-scored fairly from your full submission.

---

## A note before the score table

Two things stood out when I opened the repo, and I want to surface them up front so the score table makes sense:

1. **The repo is currently empty.** It contains a single 2-line `README.md` and no project artifacts — no campaign configurations, no email templates, no landing pages, no consent records, no analysis scripts, no exported click/submission data. Phishing is one of the projects where a fair share of the work lives in non-code artifacts (GoPhish campaign exports, anonymized consent records, screenshots), but those still need to be committed somewhere. If your campaigns ran successfully and the data is sitting on your laptop, the next 24 hours is the moment to get it into the repo — even rough exports are better than none.

2. **Only one author appears in the commit history.** The single commit on `main` is by `hajerAlajmi <hajar.alajmi@sci.ku.edu.kw>`. I'm **not** treating this as a partner-work deduction in the pregrade, since you may simply be sharing one machine — but for the official grade I'll need to see Hajar Thamer Alsahaib's involvement reflected somewhere (commits from her account, or a clear written split in the PDF).

---

## Pregrade score table (repo-only)

| Rubric row | Max | Pregrade | Notes |
|---|---:|---:|---|
| Technical Correctness | 30 | **0 / 30** | No P1 deliverables present in repo: no campaign configs, no landing pages, no email templates, no consent records, no exported data, no analysis scripts. If campaigns did run successfully, this number can move substantially before Tuesday by committing the artifacts. |
| Code Quality | 15 | **1 / 15** | Single GitHub-default *"Initial commit"*. The 2-line README correctly identifies the project. No `.gitignore`, no `requirements.txt`, no folder structure. |
| Results & Evidence | 15 | **0 / 15** | *Will be re-scored from full submission* (screenshots of GoPhish dashboard, click/submission rate tables, CSV exports). |
| Technical Writing | 15 | **0 / 15** | *Will be re-scored from full submission* (PDF report). |
| Demo Video | 10 | **0 / 10** | *Will be re-scored from full submission* (3–5 min demo video). |
| Challenges Reflection | 5 | **0 / 5** | *Will be re-scored from full submission* (PDF). |
| Week 3 Plan & AI Disclosure | 10 | **0 / 10** | *Will be re-scored from full submission* (PDF). |
| **Pregrade total** | **100** | **1 / 100** | The 55 marks tied to PDF + video are recoverable on Tuesday. The 45 marks tied to the repo (Technical Correctness + Code Quality) need real artifacts committed **before** official grading to recover meaningfully. |

---

## What's working well

The honest truth is the repo doesn't yet have artifacts I can review on technical merit — but a few things are right that I want to acknowledge:

- **You picked the project that requires the most operational discipline.** P1 Phishing has the strictest safety rules (consent forms, instructor pre-approval, no real credentials captured, no off-campus targets). Choosing it shows you're willing to engage with the operational/ethical side of security, not just the technical side.
- **The repo title and README correctly identify the project.** Small thing, but it tells me you and your partner are aligned on what you're building.
- **You added me as a collaborator and the repo is reachable.** The submission plumbing is in place — that's a precondition for everything else, and not every pair gets it right.

If your campaigns ran on schedule (which I'll see in the demo video and PDF), the substance of the work *exists*; the gap is that it isn't reflected in the repo yet. That's a fixable problem in 24 hours.

---

## Suggestions to strengthen things before official grading

Framed as advisory — these are the moves that will recover the most marks in the time remaining.

### Suggestion 1 — Commit the artifacts you already have

Phishing project artifacts that should live in the repo (regardless of whether they're code or exports):

```
Phishing-Awareness-Project/
├── README.md                         # project, team, what you built, how to read this repo
├── requirements.txt                  # pandas, matplotlib, jinja2 — whatever your analysis needs
├── .gitignore                        # __pycache__, .venv, .env, raw_data/private/
├── campaigns/
│   ├── campaign_1_config.json        # exported from GoPhish (Sending Profile + Template + Landing Page IDs)
│   └── campaign_2_config.json
├── templates/
│   ├── email_template_1.html         # the phishing email body (with placeholders stripped)
│   └── landing_page_1.html           # spoofed login page that logs submissions but stores no credentials
├── data/
│   ├── campaign_1_results.csv        # exported event log from GoPhish (anonymized: hash IDs, no real names)
│   └── campaign_2_results.csv
├── analysis/
│   └── click_rate_analysis.ipynb     # or .py — compute click rate, submission rate, time-to-click
├── consents/
│   └── consents_summary.md           # count + categories; do NOT commit signed PDFs with real names
└── screenshots/
    └── gophish_dashboard.png         # captioned figure for the report
```

If even half of this lands in the repo before Tuesday, Technical Correctness lifts from 0 toward the M2 expected deliverable (*"Live campaigns + raw data collected"*).

**Important — do not commit personal data.** Hash or anonymize student IDs in your CSV exports before committing. A column like `participant_id` should look like `p_a3f9b1` rather than the real KU ID.

### Suggestion 2 — A click-rate analysis starter (drop into `analysis/click_rate_analysis.py`)

If you've exported the GoPhish campaign timeline as CSV, this script gives you the headline metrics the rubric expects:

```python
import pandas as pd

# GoPhish campaign export columns: email, time, message
# message values: "Email Sent", "Email Opened", "Clicked Link", "Submitted Data", "Email Reported"
df = pd.read_csv("data/campaign_1_results.csv")

# anonymize before any later step
df["participant_id"] = df["email"].apply(lambda e: "p_" + str(abs(hash(e)))[:6])
df = df.drop(columns=["email"])

total_sent = (df["message"] == "Email Sent").sum()
opened     = df[df["message"] == "Email Opened"]["participant_id"].nunique()
clicked    = df[df["message"] == "Clicked Link"]["participant_id"].nunique()
submitted  = df[df["message"] == "Submitted Data"]["participant_id"].nunique()
reported   = df[df["message"] == "Email Reported"]["participant_id"].nunique()

print(f"Total sent:      {total_sent}")
print(f"Open rate:       {opened/total_sent:.1%}")
print(f"Click rate:      {clicked/total_sent:.1%}")
print(f"Submission rate: {submitted/total_sent:.1%}")
print(f"Report rate:     {reported/total_sent:.1%}")

# time-to-click: median seconds between Email Sent and Clicked Link per participant
df["time"] = pd.to_datetime(df["time"])
sent_times = df[df["message"] == "Email Sent"].set_index("participant_id")["time"]
click_times = df[df["message"] == "Clicked Link"].set_index("participant_id")["time"]
joined = pd.concat([sent_times.rename("sent"), click_times.rename("clicked")], axis=1).dropna()
joined["delta_sec"] = (joined["clicked"] - joined["sent"]).dt.total_seconds()
print(f"Median time-to-click: {joined['delta_sec'].median():.0f} seconds")
```

Output of this script (committed as `analysis/results_summary.txt`) is concrete evidence for the Results & Evidence row of the rubric.

### Suggestion 3 — A safe landing page starter (drop into `templates/landing_page_1.html`)

The brief is explicit: "Fake pages log submission attempts only" — never real credentials. A safe landing page logs the *fact* of submission without persisting the password field:

```html
<!doctype html>
<html lang="en">
<head><meta charset="utf-8"><title>KU SSO — Sign in</title></head>
<body>
<form id="login" method="POST" action="/log_attempt">
  <h2>KU Single Sign-On</h2>
  <input name="username" placeholder="Student ID" required>
  <input name="password" type="password" placeholder="Password" required>
  <button type="submit">Sign in</button>
</form>
<script>
document.getElementById("login").addEventListener("submit", function(e) {
  e.preventDefault();
  // log only WHO clicked + WHEN — strip the password field entirely
  const fd = new FormData(e.target);
  fd.delete("password");
  fd.append("logged_at", new Date().toISOString());
  fetch("/log_attempt", { method: "POST", body: fd });
  // redirect to a debrief page explaining this was a simulation
  window.location.href = "/debrief.html";
});
</script>
</body>
</html>
```

The matching server-side handler should write a single row to `data/submissions.log` with `participant_id, timestamp` — and then redirect to a **debrief page** explaining this was a simulation and pointing to your training materials. That last step is genuinely important; it's the difference between a phishing exercise and a phishing trap.

### Suggestion 4 — Expand the README and add repo hygiene

Even a 1-page README and basic hygiene files cost very little and recover Code Quality marks directly:

- **README.md** — replace the 2-line stub with: project name, team members, what you built (campaigns + analysis), how to reproduce the analysis (`pip install -r requirements.txt; python analysis/click_rate_analysis.py`), and a one-paragraph explanation of your safety/consent protocol.
- **`requirements.txt`** — `pandas`, `matplotlib`, `jupyter` (or whatever you used).
- **`.gitignore`** — `__pycache__/`, `*.pyc`, `.venv/`, `.env`, `consents/signed_pdfs/` if you keep raw signed forms locally.
- **At least 2-3 real `git commit` messages**, not just *"Initial commit"*. Even retroactive commits like `add campaign 1 config`, `add click-rate analysis`, `add landing page template` tell me a story about how the work happened.

---

## Priority list — what to address first

In this order, starting today:

1. **Commit whatever you already have** — even rough exports, partial templates, or screenshots. Empty repo → populated repo is the single biggest mark recovery available (45 marks of repo-side rubric depend on this).
2. **Anonymize before committing** — hash student IDs / emails in any CSV before pushing. This is non-negotiable for the consent terms you signed up for.
3. **Add the click-rate analysis script** (Suggestion 2) and run it; commit the output as `analysis/results_summary.txt`. That single artifact unlocks Results & Evidence on the rubric.
4. **Expand the README and add `.gitignore` + `requirements.txt`** (Suggestion 4 — 30 minutes, real Code Quality marks).
5. **Make sure your PDF report and demo video are uploaded to Moodle by 11:59 PM tonight** — those rows account for 55/100 and are currently sitting at 0 in this pregrade only because they're not on GitHub. They will be graded fairly from Moodle.
6. **Get one real commit in from Hajar Thamer Alsahaib's account** before Tuesday's official grading (or document the split clearly in the PDF appendix).

---

## Closing note

Hajar — please don't read the `1/100` as a final judgment. It reflects what's *in the repo today*, not what you and Hajar have actually accomplished if your campaigns ran. P1 is one of the harder projects to evidence in code (a lot of it is operational), but committing the artifacts you already have — campaign exports, templates, even just screenshots — closes most of the visible gap. Focus on Priority 1: get something into the repo today, even if it's rough. Polish on Tuesday morning. And there are still 55 marks fully recoverable from your Moodle submission tonight.

You've got the harder half done (running the campaigns); the remaining half is just getting the evidence into the repo. Let's get it across the line.

— Dr. Shaikhah
