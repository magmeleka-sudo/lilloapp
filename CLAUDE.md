# Our budget (lilloapp)

A household budget web app shared by Maria and her husband Jack.

## About the user
- Maria is not a developer. Explain things simply, step by step, in plain language.

## How the app is built
- The whole app is a single file: `index.html` (HTML, CSS and JavaScript together, no build step).
- Tabs: Overview, Expenses, Budget, Reports, Year. Money is in GBP (£).
- It loads the Supabase JavaScript library from a CDN and talks to Supabase directly from the browser.
- Supabase connection is in the "Supabase connection" section near the bottom of `index.html` (`SUPABASE_URL`, `SUPABASE_KEY`).

## Hosting and publishing
- Hosted with GitHub Pages at https://magmeleka-sudo.github.io/lilloapp/
- Repository: https://github.com/magmeleka-sudo/lilloapp (public), branch `main`.
- **Pushing to `main` updates the live app within 1-2 minutes.**
- Push rule (agreed with Maria on 2026-10-03):
  - **Safe changes: push without asking**, then tell Maria afterwards what changed. Safe means display-only tweaks that do not change any figure or behaviour: wording and labels, colours, fonts, spacing, small layout fixes, typos. Check the page loads with no errors first.
  - **Everything else: show the changes and ask for a clear yes before pushing.** This includes anything touching money figures, totals, savings or budget calculations, categories, sign-in, reading or writing the database, new features or tabs, and removing anything.
  - If unsure whether a change is safe, ask.
  - Every push is saved in git history, so a bad update can be rolled back.
- GitHub account to use: the PERSONAL account `magmeleka-sudo`, not her work account.

## Data (Supabase)
- Project id: `wsvqbkwokaahtztidspw`, region Frankfurt.
- The app uses the **publishable key only**. Never put a secret or `service_role` key in the code (the repo is public).
- Tables: `members`, `app_settings`, `month_budgets`, `transactions`.
- All four are protected by row-level security (RLS): only the two emails listed in `members` can access them.
- Sign-in is email and password. The two users are Maria and Jack.

## Database changes
- If a change needs a new table or column, write the SQL for Maria to run in the Supabase SQL Editor and explain in simple terms what it does.
- Never write SQL that deletes or overwrites existing data (no DROP, TRUNCATE, or DELETE without a clear request). Keep RLS on for any new table.

## Working agreements
- Follow the push rule above: ask before pushing anything that is not a safe display-only change.
- Preview with real data: serve index.html on localhost and let Maria sign in herself in the Browser pane. Never enter her password. Anything saved there writes to her real database.
- Display names: `CAT_LABELS` in index.html maps stored category names to display names (the "10%" category shows as "God’s Shares"). The stored name is unchanged.
- Savings are split equally between Savings – Maria and Savings – Jack in every month. `POTS_SAVINGS_ALL_TO_JACK` in index.html is a list of months (e.g. `['2026-10']`) where all savings go to Jack instead; it is empty now (October 2026 was switched back to an equal split on request). The Insights > Pots tab keeps running totals from October 2026 (`POTS_START`).
- Category merges (read-time only, stored data unchanged): Council tax counts under Bills; Clothes – Maria/Jack count under Pocket money – Maria/Jack (`CAT_MERGE`). Some categories are hidden from the add/scan/import pick lists (`PICK_HIDDEN`).
- Add expenses screen (Scan or import): type one in, scan a receipt, bank screenshot, CSV/paste. Photos are read on the device with Tesseract.js; nothing is uploaded.
- Keep explanations simple; avoid jargon, or explain it when used.
