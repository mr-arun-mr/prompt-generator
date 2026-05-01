# Prompt Generator

A zero-installation, single-file tool that turns your professional profile into ready-to-paste AI prompts. Fill in a form, copy the generated prompt, paste it into **Claude** or **ChatGPT**, and get a polished post, caption, or cover letter — tailored to your background, tone, and platform.

No accounts. No API keys. No data sent anywhere. Works by opening one HTML file in any browser.

---

## How it works

1. **Load your profile** — pick your `profiles/*.json` file (or paste JSON directly)
2. **Select a template** — LinkedIn post, cover letter, or Instagram caption
3. **Fill in the details** — pre-filled where possible from your profile
4. **Copy the prompt** — paste it into Claude or ChatGPT to generate the final content

---

## Features

- **9 templates** covering LinkedIn (7 types), job cover letters, and Instagram captions
- **Profile-driven** — your name, role, skills, and experience are woven into every prompt automatically
- **Hashtag chip selector** — auto-suggested from your profile's skill categories, individually toggleable
- **Per-template config** — tone, length, hashtag count, CTA, and emoji options adapt to each template type
- **Multiple users** — each user keeps their own `profiles/*.json`; skill categories are fully user-defined
- **Zero installation** — open `linkedin-prompt-generator.html` directly in any browser; works offline
- **No external dependencies** — all CSS and JS are inline in a single HTML file

---

## Platform support

| Platform | Status |
|---|---|
| Chrome / Edge (desktop) | Full |
| Firefox (desktop) | Full |
| Safari (macOS) | Full |
| iOS Safari (iPhone / iPad) | Full |
| Android Chrome | Full |

Works via `file://` protocol — no local server required.
Safe-area padding ensures the sticky Generate button clears the iPhone home indicator.
Input font sizes are 16px to prevent iOS Safari auto-zoom on tap.

---

## Templates

| Key | Name | Platform | Description |
|---|---|---|---|
| `new-job` | New Job / Career Milestone | LinkedIn | Announce a new role or career move |
| `achievement` | Technical Achievement | LinkedIn | Share a project win or delivery impact |
| `award` | Award & Recognition | LinkedIn | Celebrate an award or commendation |
| `insight` | Tech Insight | LinkedIn | Share a thought leadership opinion |
| `learning` | Learning & Certification | LinkedIn | Announce a cert or course completion |
| `ai-news` | AI & Industry News | LinkedIn | Comment on a trending AI or tech story |
| `general` | General Update | LinkedIn | Share any professional update |
| `cover-letter` | Cover Letter | Job application | Full cover letter body mapped to JD requirements |
| `instagram` | Instagram Caption | Instagram | Engaging caption with optional emoji and hashtags |

---

## Quick start

1. Download or clone this repository
2. Open `linkedin-prompt-generator.html` in your browser
3. Click **Load Profile JSON** and select `profiles/arun.json` (or any example profile)
4. Pick a template, fill in the fields, and click **Generate Prompt**
5. Copy the prompt and paste it into [Claude](https://claude.ai) or [ChatGPT](https://chat.openai.com)

---

## Profile schema

Profiles are plain JSON files stored in `profiles/`. Key top-level fields:

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✓ | Full name |
| `title` | string | ✓ | Professional title |
| `location` | string | — | City, Country |
| `summary` | string | ✓ | 2–3 sentence professional summary |
| `yearsExperience` | number | ✓ | Total years of experience |
| `domain` | string | — | Industry domain (e.g. Fintech, SaaS) |
| `primarySkillCategories` | string[] | — | Category keys to prioritise for hashtag suggestions |
| `currentRole` | object | ✓ | See below |
| `experience` | array | — | Previous roles (same shape as `currentRole`) |
| `skills` | object | ✓ | Skill categories — any key names you choose |
| `certifications` | array | — | `{ title, issuer, shortName }` |
| `awards` | array | — | `{ title, issuer, date }` |
| `education` | array | — | `{ degree, field, institution, location, period }` |

**`currentRole` shape:**
```json
{
  "title": "Senior Engineer",
  "company": "Acme Corp",
  "client": null,
  "domain": "Fintech",
  "startDate": "Jan 2024",
  "endDate": null,
  "location": "London, UK",
  "highlights": ["Achievement 1", "Achievement 2"],
  "technologies": ["Java", "Kubernetes", "PostgreSQL"]
}
```

**`skills` shape** — category names are fully user-defined:
```json
{
  "languages":     ["Python", "Go", "SQL"],
  "frameworks":    ["FastAPI", "React"],
  "cloud":         ["AWS", "GCP"],
  "aiTools":       ["GitHub Copilot", "Claude"],
  "methodologies": ["Agile", "DataOps"]
}
```

Set `primarySkillCategories` to control which categories drive hashtag suggestions and the skills summary in prompts. If omitted, all categories are used in insertion order.

---

## Example profiles

| File | Persona | Domain |
|---|---|---|
| `profiles/arun.json` | Arun Madathil Rajan — Senior Java Engineer, 13 yrs | Banking / Fintech |
| `profiles/example-data-engineer.json` | Priya Sharma — Senior Data Engineer | Data & Analytics |
| `profiles/example-frontend.json` | Sofia Reyes — Senior Frontend Engineer | SaaS |
| `profiles/example-it-helpdesk.json` | Jordan Mitchell — IT Support Analyst | IT Service Management |
| `profiles/example-fresher.json` | Arjun Menon — CS Graduate / Intern | Software Engineering |
| `profiles/template.json` | Blank starter template | — |

---

## Creating your own profile

1. Copy `profiles/template.json` and rename it (e.g. `profiles/yourname.json`)
2. Fill in your details — fields set to `null` are optional and can be removed
3. Define your own skill category names under `"skills"` — use whatever makes sense for your stack
4. Set `"primarySkillCategories"` to a list of your most important category keys
5. Open `linkedin-prompt-generator.html`, click **Load Profile JSON**, and select your file

---

## Skill categories and hashtags

Skill category names are completely user-defined. A Java backend engineer might use `"backend"`, `"cloud"`, `"devops"`. A data engineer might use `"dataEngineering"`, `"languages"`, `"cloud"`. A frontend engineer might use `"frameworks"`, `"testing"`, `"devops"`.

The app reads `profile.primarySkillCategories` (or all category keys in order) to generate hashtag chip suggestions. Chips are individually toggleable before generating a prompt. The Instagram template allows up to 28 hashtag chips; LinkedIn templates show up to 14.

The `aiTools` category name is a convention used by the **AI & Industry News** template to prefill the AI tools field — but it is not required. If missing, the field is left blank for manual entry.
