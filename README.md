# Thinking Ledger

A private personal system for thinking and managing life, published as a claude.ai artifact:
https://claude.ai/artifact/7yyWxMhb4AaPh9SmTiHULG

`thinking-ledger.html` is the page source. Republish it to the same artifact URL after editing.

## Tabs

- **Home**: today's schedule, today's tasks, deadlines for the next 14 days, active projects with their next action, courses with their next assignment or exam, and a "Waiting on you" list (unwritten journal, weekly review, projects with no next action, ideas missing an opposing view or a "what would change my mind", decisions due for review, hobby "next time" notes).
- **Work**: Inbox and projects (next actions, deadlines); Studies (courses, current topic, assignments and exams, each course linked to its Google Classroom calendar).
- **Week**: weekly schedule merged with Google Calendar and Classroom due dates. Schedule items, tasks, assessments and project deadlines can also be created in Google Calendar.
- **Journal**: one intention, what happened, what I learned, an open question, energy 1 to 5.
- **Hobbies**: sessions with time, what I worked on, what I noticed, what to try next.
- **Think**: idea ledger (confidence, perspectives for and against from named sources, what would change my mind, revision history); decision journal (reasoning before the outcome, Brier score for calibration); weekly review with Claude's notes.

## Data

Stored in the artifact's database, readable and writable only by the owner.

| Collection | Contents |
| --- | --- |
| `tasks` | title, due, star, done, doneAt, projectId, courseId, gcalId |
| `projects` | name, outcome, deadline, status, notes, gcalId |
| `courses` | name, code, who, topics, status, calendarId (Classroom calendar) |
| `assessments` | title, courseId, kind, due, weight, status, result, gcalId |
| `events` | weekly or one-off schedule items, gcalId |
| `entries` | one per day (id `YYYY-MM-DD`): focus, log, learned, question, energy |
| `hobbies`, `sessions` | hobbies and logged sessions |
| `ideas`, `decisions` | idea ledger and decision journal |
| `reviews` | one per ISO week (id `YYYY-Www`): own reflections plus `claudeNotes` |
| `settings/gcal` | Google Calendar ids shown on the page |
| `cache/gcal` | copy of the next 15 days of calendar items, refreshed when the page is open, read by the routines |

## Routines

- **Evening nudge**, daily at 20:56 IST: open and overdue tasks, deadlines in the next 3 days, tomorrow's first commitment, journal reminder, decisions due. Read-only.
- **Weekly review**, Sundays at 18:47 IST: writes `claudeNotes` into `reviews/<week>`.

Routines cannot hold a Google Calendar connection in this account, so they read `cache/gcal` instead of the calendar itself.
