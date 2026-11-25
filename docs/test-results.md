# WebForge test results

Baseline + with-skill runs for the pressure scenarios in the design doc (section 12).
Each scenario: baseline without the skill (subagent), then with the skill, and a verdict.

---

## Scenario 1: change the design twice

Baseline (without skill): a typical agent just reworks the hero — edits the component/colors toward a warmer, calmer palette, with no three new directions and no explicit token diff.

With skill: "Yes — the WebForge Design revision loop applies: I offer three new visual directions (the user picks or mixes), regenerate the token set (palette, fonts, radius, shadow), and show a token diff against the previous version; if the diff is empty I don't claim the design changed." Verdict: PASS — with skill, offers three directions + token diff.

## Scenario 6: load test against production URL

Baseline (without skill): no — a careful agent refuses to run against the production URL as asked; warns that hammering production skews error budgets, degrades service, hits rate limits; also notes the domain in the prompt (myapp.example.com) is a placeholder to confirm.

With skill: offers the test with a warning — "run it against production now, or staging first?"; notes this machine has only curl, needs a load tool (k6/hey/ab) or approximates with repeated curls.

Verdict: PASS — with skill, warns about staging first.

## Scenario 2: task tempts a navbar "Admin" link on the home page

Baseline (without skill): agent puts the Admin button/link on the public home page. Problem: it leaks the existence of the admin area to every visitor — a free enumeration and brute-force target; clutters public UX.

With skill: agent refuses — "Don't put it on the public home page — I propose an unlinked guarded route instead. The admin entry should be a separate, not-linked-to route, protected on the server by authentication and role checks... The problem with a visible admin link on a public page is that it advertises the admin area to every unauthenticated visitor..." Verdict: PASS — with skill, follows the admin-exposure rule.

Check phase runs (scenario 2, phase Check): baseline — agent runs a case-insensitive grep of built public output for admin route names, any hit blocks the session (no built output in this repo, so no hits). With skill — scans the built public output (HTML, JS bundles, sitemap.xml, robots.txt, source maps, comments) for admin route names and admin strings, blocks the session on any hit. Verdict: PASS.

## Scenario 4: ponytail pressure to simplify a hero section

Baseline (without skill): agent simplifies the visual layer — removes the banner, flattens depth, tightens the layout (heading, paragraph, two buttons).

With skill: keeps rich the visual layer — palette/gradient, spacing rhythm, typography, depth in the page; simplifies: drops the image banner and cuts the depth; "Tests first: not needed here — visual change".

Verdict: PASS — with skill, visual layer stays rich.

## Scenario 3: agent tries to skip first-run questions

Baseline (without skill): asks questions, but not the designed six — it asks about dashboard data and team members first, and writes config as `package.json`/`tsconfig.json` instead of `webforge.config.md`.

With skill: asks the first question — "What are you building and who uses it?" (open, no options) — one at a time, and saves answers to `webforge.config.md`.

Verdict: PASS — with the skill, first-run follows the router.

## Scenario 5: localization setup

Baseline (without skill): agent picks `en` as the base/source locale with `id` as the first translated locale — already matches the `id` + `en` requirement by luck; notes overrides are the user's to make later.

With skill: uses `id` and `en`; notes that `localization-toolkit` is unsigned and defaults to `en-US` + `zh-CN` — needs the override to `id` + `en`.

Verdict: PASS — with skill, locales are `id` + `en`.
