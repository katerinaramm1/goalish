# Goalish ↗

**Big goals. Small steps. Real progress.**

Goalish is a free, privacy-first browser app for creators, indie builders, and entrepreneurs. Turn an ambitious goal into a practical checklist, track your progress, and download a personalized challenge card to share.

## Try it locally

Open `index.html` in a modern browser. No installation, accounts, database, API keys, or build tools required.

## Publish on GitHub Pages

1. Create a public repository, e.g. `goalish`.
2. Upload `index.html` (and optionally this README and REQUIREMENTS.md) to the repository root.
3. In **Settings → Pages**, select **Deploy from a branch**, choose `main` and `/ (root)`, and save.
4. After deployment, open `https://YOUR-USERNAME.github.io/goalish/`.
5. On GitHub Pages, test that a challenge persists after a page reload, download a PNG card and `.ics` calendar file, and export a backup.

If deploying in an organization or private repository, review GitHub Pages eligibility and permissions for that account.

## What's included in version 0.1

- Responsive, minimalist layout
- Five goal templates: followers, revenue, product launch, content, custom
- Six suggested actionable steps per challenge with evenly spaced suggested dates
- Multiple local challenges (maximum 30)
- Numeric progress and checklist completion
- PNG image cards for goals and achievements (Canvas API)
- Calendar `.ics` export with reminders (calendar app behavior varies)
- X prefilled text sharing (attach downloaded card manually)
- LocalStorage persistence and JSON import/export (also accepts legacy Stepwise backup files)
- Basic accessible form labels, progress semantics and status messages

## Important limitations

- All progress is self-reported. The app does not confirm revenue, follower counts or completed projects.
- Planner templates are deterministic, not AI advice; dates are suggestions, not predictions.
- No cross-device sync. Browser clearing/private browsing may erase local progress. Export backups regularly.
- An exported calendar file is a snapshot. Editing a goal later does **not** automatically modify existing calendar entries.
- `.ics` reminders depend on the importing calendar application's support and settings.
- X intent shares text, not the image. The user downloads and manually attaches the card.
- Version 0.1 supports one numeric goal per challenge. For the example `$10k AND 10k followers`, create two separate challenges. Linked multi-target challenges are planned for version 0.2.
- No network requests or tracking scripts are included in this starter.

## Suggested backlog

1. Custom editable tasks with add/remove/reorder and due date updates.
2. Linked multi-target challenges and visual dashboard.
3. Better card styles, aspect ratios and custom themes.
4. Search/filter and archived challenges.
5. Automated tests and accessibility checks.
6. Optional cloud sync and AI planning only after privacy and cost review.

## Developer notes

The entire proof of concept is in `index.html` to simplify GitHub Pages deployment. For ongoing development, split CSS and JavaScript into separate files and add linting, tests, and a deployment workflow. No third-party dependencies are required.

## Privacy

Data is stored using the browser's localStorage under `goalish.challenges.v1`; only you control exported backup files. Sharing to X opens X's website when the user chooses the share button.

## License

No license is supplied by default. Add an open-source license (such as MIT) only if you wish to give others permission to reuse and redistribute your code.

## Visitor analytics and footer count

The app includes the GoatCounter tracking script for `https://goalish.goatcounter.com/count` and displays site-wide total visits in the footer.

In GoatCounter, open **Settings → Allow adding visitor counts on your website** and enable it; otherwise the footer cannot show the number. GoatCounter may cache the count for up to four hours. The public counter reports visits according to your GoatCounter session settings; it is not a verified count of distinct people.

Goals are kept locally; GoatCounter receives ordinary website usage events, not goal text or user-entered challenge data.
