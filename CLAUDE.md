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
- Push rule (updated by Maria on 2026-10-03: "push it always"): **push app changes to `main` without asking first**, then tell Maria afterwards, in plain language, what changed and what to check.
  - Before every push: test the change in a local preview, check there are no console errors, and re-check any figures by hand. Never push a change that fails these checks.
  - Still ask first (do not just do it) for: anything that deletes or overwrites her real data, anything saved into her real Supabase data beyond what she asked for, any SQL, and anything that stores a secret or key in the code.
  - Every push is saved in git history, so a bad update can be rolled back. If a pushed change turns out wrong, fix it quickly and say so plainly.
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
- Display names: `CAT_LABELS` in index.html maps stored category names to display names (the "10%" category shows as "God’s Shares", Grocery as "Groceries", Transportation as "Transport", Misc as "Other"; always use `catLabel()` for any category name shown to the user, including downloads and messages). The stored name is unchanged.
- Language: Maria is in the UK, so all wording must be British English (spelling such as "recategorise", "colour", "tick", £ amounts, DD/MM dates, "Log in" / "Log out").
- Savings are one category, "House savings" (Savings – Maria and Savings – Jack were combined on request, so savings are no longer split). The Insights > Pots tab keeps running totals from October 2026 (`POTS_START`).
- Category merges (read-time only, stored data unchanged, `CAT_MERGE`): Council tax counts under Bills; Clothes – Maria/Jack count under Pocket money – Maria/Jack; Savings – Maria/Jack count under House savings. Some categories are hidden from the add/scan/import pick lists (`PICK_HIDDEN`).
- The app started in October 2026 (`APP_START`): months before that have zero budget and income (read-time rule in `budgetFor`). A month can still be given its own figures.
- Budget tab has three views: 12 months (editable table, current month highlighted, saves only per-month differences from the default), Default budget, and One month.
- Savings tab (next to Insights): forecast per quarter from October 2026 for Travel savings, Investing – Maria, Investing – Jack, House savings and Loan (`SAV_POTS`). A month that has ended uses its actual figure; later months use the budget. An "Actual" figure shows under the forecast as soon as there is spending ("Actual so far" while the month runs, final when it ends); House savings has no actual until the month ends. The quarter table shows running totals since October 2026 (each row accumulates all earlier quarters); the month-by-month table shows what each single month adds.
- Add expenses screen (Scan or import): type one in, scan a receipt, bank screenshot, CSV/paste. Photos are read on the device with Tesseract.js; nothing is uploaded.
- Keep explanations simple; avoid jargon, or explain it when used.
