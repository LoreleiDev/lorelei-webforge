# WebForge

WebForge is a router skill for fullstack website projects: it asks first (what you are building, stack, visual direction, languages, auth and hosting), then runs four phases in order — Design (visual direction, tokens), Build (minimal code), Check (security gate, admin-exposure rules) and Ship (CI/CD, load test, release audit). External skills do the work; WebForge owns the order, the gates and the revision loops.

## Install

```
npx skills add LoreleiDev/webforge
```

## Dependencies

WebForge calls other people's skills (it does not copy them). Full list, source URLs, licenses, install commands and per-phase fallbacks: [references/dependencies.md](references/dependencies.md).

| Phase | Owner skills |
|---|---|
| Design | `ui-ux-pro-max`, `frontend-design` |
| Build | `ponytail`, `test-driven-dev` |
| Check | `code-vuln-audit` + WebForge admin-exposure check |
| Ship | `pipeline-blueprint`, `http-load-profiler` |

WebForge never installs a dependency by itself: when one is missing it tells you what is needed and asks first.

## First run

On first activation in a project, WebForge asks questions one at a time — what you are building and who uses it, stack, visual direction, languages, auth and roles, hosting target. Answers are saved to `webforge.config.md` in the project root so the questions are not repeated.

## Agents

Tested with the `npx skills` CLI (`opencode` was detected during a `npx skills add` verification run). The format is a plain `SKILL.md`, so any agent that reads that format can install it.

## License

MIT — see [LICENSE](LICENSE).

## Notes

skills.sh lists skills through install telemetry; a new repo may not appear right away.
