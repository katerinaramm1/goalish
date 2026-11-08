# Goalish — MVP Product Requirements Specification (v0.1)

**Product vision:** A free, minimal, browser-based challenge planner for creators and indie builders. Convert big numerical goals into a series of actions, track self-reported progress, and share milestones.

**Primary personas:** Independent creator pursuing audience growth; indie builder launching a side project; freelancer pursuing a revenue target; publisher with a content challenge.

**Success statement:** In under two minutes, a first-time user can create a goal, understand their next practical actions, and share their challenge card without creating an account.

## Scope

### In scope (v0.1)

- P0: Create goal with template, title, username, current value, target value, and future deadline.
- P0: Templates: social follower growth, revenue, product launch, content publishing, and custom.
- P0: Generate six predefined actions with suggested dates spread across the challenge duration.
- P0: View all saved challenges with goal progress and task completion count.
- P0: Update current progress and toggle individual actions complete/incomplete.
- P0: Store and reload challenges locally; allow delete with confirmation.
- P0: Export and import JSON backup (import replaces currently stored data after confirmation).
- P0: Generate PNG share card with username, title, progress and goal deadline. Clearly label self-reported status.
- P1: Export tasks as `.ics` calendar events with reminder alarm; calendar behavior is dependent on calendar provider.
- P1: Open X intent page with prefilled text.
- P1: Responsive desktop/mobile, keyboard-accessible form, high contrast text, safe HTML escaping.

### Out of scope (v0.1)

Account signup, backend, cross-device sync, AI API, actual push/email reminders, direct posting to social accounts, automatic follower/revenue verification, linked multi-target goals, public leaderboards, payments, goal/task editing after creation.

## Screen inventory

1. **Home / New Challenge:** Header; value proposition; category selector; username; title; starting/target metrics; deadline; create action.
2. **My Challenges:** Repeated cards; numerical progress bar; due date; generated action list; toggle completion; update progress; delete; card/calendar/share actions.
3. **Backup:** Export/import JSON.
4. **Future detail screen (v0.2):** Task editor and multiple metrics, not included in current code.

## Data schema

```json
{
  "id": "uuid",
  "category": "followers | revenue | launch | content | custom",
  "title": "Reach 10000 followers on X",
  "username": "@example",
  "start": "2026-11-06",
  "deadline": "2026-12-31",
  "initial": 2000,
  "current": 2500,
  "target": 10000,
  "tasks": [
    {"id":"0","text":"Define your audience and three content themes","done":false,"due":"2026-11-15"}
  ],
  "createdAt": "2026-11-06T12:00:00.000Z"
}
```

Storage key: `goalish.challenges.v1`. JSON backup shape: `{ "app": "goalish", "version": 1, "exportedAt": "...", "goals": [...] }`.

## Calculation rules

- Goal progress: `clamp(round(current / target * 100), 0, 100)`; goal achieved when `current >= target`.
- Task completion: number of checked tasks divided by number of tasks, independent from goal metric.
- Suggested due dates: evenly distributed between creation day and deadline; they are non-binding suggestions.
- Current and target numbers must be finite; current >= 0; target > 0; deadline cannot be earlier than local today.

## Acceptance criteria / manual test matrix

| ID | Scenario | Expected result |
|---|---|---|
| AC-01 | Create follower goal with valid values and future deadline | Challenge appears with six relevant actions |
| AC-02 | Refresh the page | Saved challenge and tasks remain |
| AC-03 | Change current number to 50% of target | Progress bar shows 50% |
| AC-04 | Mark one task complete | Action displays checked state, count increases, survives reload |
| AC-05 | Reach or exceed target | Challenge shows target reached; card includes `I DID IT!` |
| AC-06 | Export share card | PNG with title, username, deadline, progress and self-report disclaimer downloads |
| AC-07 | Export calendar | Valid iCalendar `.ics` file downloads with dated milestones |
| AC-08 | Click share on X | X compose page opens with challenge text; no automatic posting |
| AC-09 | Export JSON; delete challenge; import JSON | Challenge is restored after confirmation |
| AC-10 | Enter negative current value, zero target, or past deadline | Form prevents creating invalid goal |
| AC-11 | Delete a challenge | Confirmation is shown; canceled deletion does not remove data |
| AC-12 | Open on narrow mobile viewport | Form and challenge cards stack without horizontal overflow |
| AC-13 | Try an HTML-like title | Text is displayed as text, not executed as code |
| AC-14 | Disable/clear browser storage | App warns about storage; export strategy documented |

## Non-functional requirements

- No third-party calls, tracker, cookie banner requirement from app itself, or mandatory login.
- Avoid exposing private goal data in query strings; share only after explicit user click.
- Works on modern browsers with JS, Canvas, localStorage, and download support; some features degrade in private browsing.
- Graceful no-data state and basic input validation.
- Targeted low-cost hosting: GitHub Pages, $0 base cost for typical personal usage within its limits.

## Version 0.2 roadmap

- Combine multiple target metrics into one challenge (e.g. $10K revenue AND 10K X followers).
- Add/edit/reorder custom tasks; user-selected hours per week; smarter timeframe estimates.
- Progress history, weekly reviews, overdue/reschedule workflow.
- Card templates for 1:1, 4:5, 16:9 formats; reusable social snippets.
- Optional shareable public challenge page requires explicit consent and backend.

## Implementation milestones

**Milestone A (included now):** Static frontend, form, deterministic templates, stored progress.

**Milestone B (included now):** Calendar export, social share, image card, backup/restore.

**Milestone C (before public launch):** Browser testing (Chrome/Firefox/Safari/mobile), accessibility audit, refine design/copy, automated tests, favicon, privacy page, choose name and license.

**Milestone D (post validation):** Optional backend and AI only if user demand supports maintenance costs.

## Potential privacy/security risks

- Browser-only data is not synchronized and can be deleted by user/browser; visible warnings and backup export mitigate this.
- Imported JSON is untrusted input; validate entries and escape on output; add size and type limits (implemented) and schema evolution plan.
- Users can misstate achievements; label all cards as self-reported.
- Future public pages, remote analytics, or integrations will require consent, clear privacy terms, and abuse prevention.

## Analytics (Goalish v0.1)

- GoatCounter is integrated for aggregate web-traffic analytics. No goal data is sent.
- Display site-wide total visits in the footer using GoatCounter's public `TOTAL` counter.
- Enable public visitor counts in GoatCounter settings.
- Retain explicit disclosure of the analytics integration on the goal-creation screen.
