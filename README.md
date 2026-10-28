# CareerPilot AI — Job Recommendation & Skill Gap Analyzer

A **fully functioning, self-contained data science capstone demo** for personalized job recommendations, explainable skill-gap analysis, and learning roadmaps. The entire interactive web application is contained in **`index.html`** (~47 KB). It works without any backend, installation, credentials, real API, or internet access.

> **Important:** All 32 job postings, employers, salaries, and posted dates are **synthetic demonstration content**, not real vacancies or market research. The recommendation score is a deterministic heuristic, not a trained AI model or a hiring probability. “AI” in the branding describes the project domain and intended future direction.

## Launch the website

1. Download `index.html`.
2. Double-click it to open in Chrome, Edge, Firefox, or Safari. Alternatively, right-click → **Open with** → browser.
3. The Dashboard shows recommended jobs based on the prefilled example profile. No server is necessary.
4. Open **My Profile**, select your existing skills, preferred role, location and experience, then click **Save profile & refresh matches**.
5. Visit **Explore Jobs** to search, filter, compare scores, bookmark opportunities and export CSV results.
6. Visit **Skill Gap Analysis**, choose a target role, and click **Build learning roadmap**.
7. In **Learning Roadmap**, check off tasks to track progress and download the Markdown learning plan.

## Main screens

| Screen | Working features |
|---|---|
| Dashboard | Hero, 4 live statistics, top 4 jobs, skill donut, skill-demand frequency |
| Explore Jobs | Search by job/company/skill, filter by role/city/work mode, sorting, matching, CSV export |
| Skill Gap Analysis | Select from 8 role families, view coverage and individual missing skills |
| Learning Roadmap | Three phases, persistent checkboxes, learning links, Markdown export |
| Saved Jobs | Bookmark/remove jobs, persist list between visits |
| My Profile | Name, experience, role, location, skill selector, resume-text skill extraction, JSON export |
| About Project | Transparent methodology description, dataset JSON export |

## Explanation of matching

For a posting with required skills `R` and your skills `U`:

```
skill_overlap = |R ∩ U| / |R|
experience_compatibility = 1 if user_years >= required_years
                           else max(0, 1 - 0.35 * (required_years - user_years))
location_affinity = 1 if preferred_location == 'Any'
                    or preferred_location == job_location
                    or job_mode == 'Remote'
                    else 0.25
match_score = round(100 * (0.75 * skill_overlap
                         + 0.15 * experience_compatibility
                         + 0.10 * location_affinity))
```

The score is bounded between 0 and 100. The skill-gap list is `required_skills - user_skills`; career-level coverage uses each role's canonical skill list. See `docs/METHODOLOGY.md` for numerical examples and limitations.

## Data source and persistence

- **Synthetic data** is declared in JavaScript in `index.html`. The site generates **32 fixed fictional listings** from curated role templates and company names.
- All calculations and text detection happen **locally in the browser**. No data is transmitted by this demo.
- Profile, bookmarks, task completion, and theme are saved using browser `localStorage`. Browser private mode or clearing site data can erase them.
- The **Download bundled dataset JSON**, **Export matches CSV**, **Export profile JSON**, and **Download learning plan** buttons create real files.

## Project structure

```
careerpilot_project/
├── index.html                 # Standalone working website (also separately downloadable)
├── README.md                  # This launch and usage guide
└── docs/
    ├── PROJECT_OVERVIEW.md
    ├── PROBLEM_STATEMENT.md
    ├── REQUIREMENTS.md
    ├── ARCHITECTURE.md
    ├── METHODOLOGY.md
    ├── DATA_DICTIONARY.md
    ├── USER_GUIDE.md
    ├── TEST_PLAN.md
    ├── API_AND_EXTENSIONS.md
    └── PRESENTATION_GUIDE.md
```

## Recommended demo flow (3–5 minutes)

1. Show the four statistics on Dashboard and top matches.
2. Navigate to **My Profile**, select `PyTorch`, `Docker`, `LLMs`, and `FastAPI`, and save; demonstrate changed rankings.
3. Use **Explore Jobs** to search `AI` or filter `Remote`; open a job's details and explain the score breakdown.
4. Save a job and open **Saved Jobs**.
5. Choose **AI Engineer** under **Skill Gap Analysis**, then generate a roadmap.
6. Tick a few tasks, reload the page to prove persistence, and export the learning plan.

## Basic browser compatibility

Modern Chrome, Edge, Firefox and Safari with JavaScript and `localStorage` enabled. The app is responsive on mobile and desktop. The course-resource URLs require internet only when **you click** those links.

## Developer notes

The code uses semantic HTML, CSS custom properties, ES6 JavaScript, delegated event listeners, and basic browser APIs (`Blob`, `URL.createObjectURL`, `localStorage`). No dependencies, frameworks or build steps. Editing the code is allowed; for production, split it into modules, use a real backend and datasets with appropriate licenses, implement privacy controls, and evaluate a validated recommendation model. See `docs/API_AND_EXTENSIONS.md`.

## Limitations / responsible use

This is an **educational prototype**, not a live recruitment platform. No actual job applications are submitted, no PDF/DOCX resume upload or deep NLP parsing is provided, and no claims are made about authentic employers, vacancies, or offer likelihood. Synthetic data and heuristic outputs must be clearly labeled in any academic report.
