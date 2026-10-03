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
- **Pushing to `main` updates the live app within 1-2 minutes.** Always show Maria the changes (a summary and the diff) and ask before pushing. Never push without a clear yes.
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
- Show changes and ask before pushing.
- Keep explanations simple; avoid jargon, or explain it when used.
