# Meal Rota

Family meal planner PWA: one Lunch and one Tea per day for the whole family, with an optional adults-only slot, on a rotating 4-week template (Weeks A–D). Replaces the older `Meal-planner` repo and reuses its meal bank.

Live: https://bengalebg23.github.io/MealRota/

## How Ben works
- Ben works from his phone. He asks for changes in chat and Claude pushes them straight to the deploy branch. There's no local build and no pull-request review.
- Pushing to `main` deploys via GitHub Pages within a minute or two.
- The repo is **public**. Never commit secrets, API keys meant to stay private, family photos or personal data.

## Every release
- Bump `APP_VERSION` and the `<title>` in `index.html` and `CACHE` in `sw.js` together, to the same version.
- Keep `HANDOFF.md` up to date (version, what changed, open threads) if the repo has one.
- After pushing, give Ben the live URL and the new version number so he can check it on his phone.

## Code rules
- Single-file app: keep HTML, CSS and JS in `index.html`. No build step, bundler or npm packages.
- Pin exact CDN versions (no `@latest` or floating majors). A floating Babel major broke an app before.
- Self-review before pushing: duplicate `const`/`let` in one scope, variable shadowing inside loops, unclosed template literals, undefined references.
- Defer re-renders triggered inside click handlers with `setTimeout(..., 0)` to avoid detached-node bugs from bubbled events.
- Don't swallow Firebase errors with a bare `console.warn`. Surface them so permission problems are visible.
- UK English in all user-facing text.
- Bulk Firebase writes: use direct awaited `set()` calls. Debounced save helpers only keep the last write in a tight loop.
- Never let a fresh or cleared device overwrite cloud data on first load. Read the cloud first, merge, then write.

## This app
- Firebase project `meal-planner-f5ba2` (europe-west1), shared with the old Meal-planner app. Check what the old app reads before changing data shapes.
- No in-app Claude or AI chat feature. Ben decided against it because of API cost.
