# Expense Logger (IS218 Creative Project)

A small web app where college students log their expenses and see a private monthly dashboard.
This is a **non-game** creative project (allowed without prior approval).

- **Research site:** https://anasanchezbs.github.io/IS218-ExpenseLogger/
- **Career research site:** link will be added when the Portfolio Plan site is published
- **Stage:** Review 1 (Plan). No app code yet; later work isn't due early.

## Concept comparison
| | Expense logger (chosen) | Study-session tracker |
|---|---|---|
| Useful interaction | Log an expense | Log a study session |
| Dashboard | Monthly total + totals by category | Hours per course |
| Hard part | Exact money math, private financial data | Time zones, durations |

I chose the expense logger because money data gives clearer, more meaningful tests and fits my Business & Information Systems major.

## Audience
College students on a tight budget.

## Finished flow
Account (sign up / log in) → log an expense → expense saved → private dashboard (monthly total, category totals, history) → account update (change email/password, delete account and all data).

## Stack
Python 3, FastAPI, PostgreSQL, SQLAlchemy, Pydantic, pytest, HTML templates. Docker Compose and GitHub Actions if the course uses them.

## User stories
1. As a new student, I want to create an account with my email and a password so my spending stays private.
2. As a student, I want to log an expense (amount, category, date, note) in under 30 seconds so I keep doing it.
3. As a student, I want my expenses saved so they're still there when I log back in.
4. As a student, I want a dashboard with this month's total and totals by category so I can see where my money goes.
5. As a student, I want to change my email or password, or delete my account and data, so I stay in control.

## Architecture
```
Browser (HTML forms, dashboard)
   → FastAPI routes (/auth, /expenses, /dashboard, /account)
   → Services (login check, totals, CategorySuggester)
   → PostgreSQL (users, expenses)
```
- Money stored as Python `Decimal` / Postgres `NUMERIC(10,2)`, never float.
- Server takes the user from the login token and filters every query by it. Another user's expense returns 404.
- Passwords hashed with Argon2 (`pwdlib`).

## Uncertain creative experiment
Auto-suggest a category from the expense note, using the **Strategy pattern**: a keyword-based suggester vs. a history-based suggester.
Success check (planned): at least 15 of 20 sample expenses guessed correctly.

## Planned tests
- Student A can't read student B's expense (404)
- Password stored as a hash, not plain text
- $0.10 + $0.20 → dashboard shows exactly $0.30
- Negative or zero amount rejected
- Deleting an account deletes its expenses

## AI assistance
Claude (Anthropic) helped draft this plan and the research site on November 12, 2026. Verification steps are listed on the research site.
