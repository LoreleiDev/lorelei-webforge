# WebForge: Design Doc

Status: draft for approval. Nothing is built until this is approved.
Next step after approval: `writing-plans`.

## 1. Intent and why

The user is rebuilding a buggy skill family ("Lorelei") into one clean skill for planning and developing fullstack websites. Lorelei failed in three ways the user named:

1. Design output was safe and plain (anti-slop but also anti-beauty), and when asked to change the design it returned the same one.
2. It put an admin button on a public page, which leaks the existence of the admin area.
3. Its recommendation questions were unclear.

WebForge must fix these three first. Everything else is secondary.

## 2. Goals, non-goals, anti-goals

Goals
- One entry skill that asks first, recommends a stack and a visual direction, then runs four phases: Design, Build, Check, Ship.
- Every external skill has exactly one owner phase. No two skills do the same job.
- Designs look striking and intentional, and a "change the design" request always produces a visibly different result.
- Public pages never expose admin entry points. Security gates run every session.

Non-goals
- Not a replacement for the external skills. WebForge calls them, it does not copy them.
- No mobile-native or desktop app support in v1 (web only).
- No automatic production deploys.

Anti-goals (fail even if it technically works)
- Plain, template-looking UI.
- Asking the same design question twice without changing the output.
- Any admin link, button, route name, or hint visible in public HTML, JS bundles, sitemap, robots.txt, or comments.
- Two skills fighting over the same file or rule.

## 3. Constraints

- All skill files (SKILL.md and phase files) are written in English to avoid misreading by agents.
- Chat voice uses Caveman style (see section 8). Files, code, and commit messages stay normal.
- Follow `writing-skills`: description starts with "Use when...", never summarizes the workflow; test with pressure scenarios before shipping.
- Token economy: the router stays short; phase files load only when that phase starts; references are one level deep.
- External skills were read from their public pages. Their behavior is taken from those pages, nothing more.

## 4. Approaches considered

| | Approach | Trade-off |
|---|---|---|
| A | One big skill | Easy to write. Heavy on tokens, hard to debug, repeats Lorelei's problem. |
| **B** | **Router + four phase files (chosen by the user)** | Small always-loaded part, clear ownership, each phase testable alone. More files. |
| C | Thin list of external skills | Cheapest. Has no home for the admin rule or the design-revision loop. |

## 5. Structure (approach B)

```
webforge/
  SKILL.md                 router: first-run questions, phase order, ownership table
  phases/
    01-design.md
    02-build.md
    03-check.md
    04-ship.md
  references/
    stack-guide.md         stack recommendation matrix
    admin-exposure-rules.md
    design-ambition-checklist.md
    pressure-scenarios.md  tests for this skill itself
```

Name `webforge` is my call; the user can rename it.

## 6. First-run flow (router)

On first activation in a project, ask one question at a time. Each question has options [A] [B] [C] with one marked as recommended and a reason, plus [D] "Type your own answer". Answers are saved to `webforge.config.md` in the project root so the questions are not repeated.

1. What are you building and who uses it? (open question, no options)
2. Stack. WebForge recommends; the user picks. Starting matrix (my recommendation from general knowledge, not from the external skills):
   - All-in-one with admin and CRUD: Laravel (Blade/Livewire or Inertia).
   - Highly interactive app: Next.js + API.
   - Python data/API backend: FastAPI + React.
   - Mostly static marketing site: Astro.
3. Visual direction: three concrete directions, each with a short text sketch (palette, type pairing, mood). The user picks or mixes.
4. Languages. Default `id` + `en` (not `en-US` + `zh-CN`).
5. Auth and roles: is there an admin area? Where does it live?
6. Hosting target (needed for the Ship phase).

Re-run questions only when the user asks to reconfigure.

## 7. Phases and external-skill ownership

| Phase | Job | Owner skill(s) |
|---|---|---|
| Design | Design direction, palette, type, effects | `ui-ux-pro-max` (design-system generator, persisted as MASTER.md + tokens) |
| Design | Build a system from a screenshot or Figma reference | `design-system-builder` (only when a reference is given) |
| Design | Review the design doc and copy | `final-review` (prose only, never code) |
| Design | Frontend craft guidance | `frontend-design` |
| Build | Write minimal code | `ponytail` |
| Build | Tests | `test-driven-dev` |
| Build | i18n setup | `localization-toolkit` (locales overridden to `id` + `en`) |
| Check | Fast security gate every session | `code-vuln-audit` + WebForge admin-exposure check |
| Check | API docs from routes | `route-to-openapi` (only for supported frameworks) |
| Ship | CI/CD templates | `pipeline-blueprint` |
| Ship | Load test | `http-load-profiler` (staging only) |
| Ship | Deep pre-release audit | Cloudflare `security-audit` (manual, once per release) |

Dropped on purpose: the local `design-system` skill (duplicate of `ui-ux-pro-max` and `design-system-builder`).

## 8. Conflict rules

- Ponytail vs visual design: Ponytail applies to logic only. It never simplifies the visual layer (layout, motion, typography, depth).
- Ponytail vs TDD: tests come first for logic with branches, money, auth, or parsing; Ponytail keeps the code minimal after the test exists. Ponytail's own review/audit commands are used for code quality only. Security belongs to the audits.
- Caveman: applies to chat prose only. Skill files, code, comments, commit messages, error names, and documents stay normal. Stops on "stop caveman" or "normal mode". Ponytail's end-of-reply note stays in one line to avoid two competing voices.
- design-system-builder vs ui-ux-pro-max: ui-ux-pro-max is the default brain. design-system-builder runs only if the user supplies a screenshot or Figma link.
- final-review checks writing only (design docs, copy, README), never source code.

## 9. Design quality rules (fixes bug 1)

- Ambition checklist (must pass before Design phase ends): distinctive type pairing, layered depth, a clear layout rhythm (not a stack of centered blocks), one signature motion that respects `prefers-reduced-motion`, a plan for imagery or illustration, a consistent icon set. No emoji as icons.
- Bland test: if the result could be any other site with the logo swapped, it fails.
- Revision loop: when the user asks to change the design, WebForge must (1) offer three new directions, (2) regenerate tokens, (3) show a diff of tokens (palette, fonts, radius, shadow) against the previous version. If the diff is empty, it must not claim the design changed.
- Anti-slop list from `ui-ux-pro-max` stays active (no generic purple gradients, no default Inter-only look).

## 10. Security rules (fixes bug 2)

Admin exposure rules:
- Public UI never contains an admin link, button, menu item, icon, or text hint.
- The admin entry is an unlinked route protected on the server by authentication and role checks. Hiding it is not the protection.
- No admin route names in public HTML, JS bundles, sitemap.xml, robots.txt, source maps, or comments.
- Check step: after each session, search the built public output for admin route names and admin strings. Any hit blocks the session.

Gates:
- Every session: `code-vuln-audit` (secrets, OWASP patterns, npm/pip dependency audit) plus the admin-exposure check.
- Known gap: `code-vuln-audit` dependency scanning covers npm and pip only. For Laravel, WebForge asks the user to run a composer audit and treats it as a required step.
- Before release: Cloudflare `security-audit`, run manually. It needs a sandbox that blocks network access; if none exists, findings stay `needs_validation`.
- `http-load-profiler` sends real traffic: staging only, with explicit user approval.

## 11. Known gaps and open items for the builder

- `route-to-openapi` does not support Laravel or Next.js. For those, the Check phase uses a framework-appropriate alternative. I have not verified a specific tool.
- `localization-toolkit` is unsigned and defaults to `en-US` + `zh-CN`. Review it and override the locales.
- `pipeline-blueprint` installs packages at runtime (medium finding). Pin versions in generated pipelines.
- No link was given for `test-driven-dev`. Assumed to be the superpowers `test-driven-development` skill. Needs user confirmation.
- Exact invocation names of external skills on the user's agent are unverified.
- Target runtime assumed: Claude Code first, plain `SKILL.md` so other agents can read it.

## 12. Testing plan (per `writing-skills`)

Pressure scenarios, each run without the skill first (baseline), then with it:
1. User asks to change the design twice. Output must differ and show a token diff.
2. Task tempts a navbar "Admin" link on the home page. Must refuse and use an unlinked guarded route.
3. Agent tries to skip first-run questions. Must ask them.
4. Ponytail pressure to simplify a hero section. Visual layer must stay rich.
5. Localization setup. Locales must be `id` + `en`, not `zh-CN`.
6. Load test requested against a production URL. Must refuse without staging confirmation.

## 13. Left to the builder

Exact wording of phase files, the full stack matrix, the format of `webforge.config.md`, and token budgets per phase file.
