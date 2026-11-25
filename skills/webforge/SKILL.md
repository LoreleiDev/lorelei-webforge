---
name: webforge
description: Use when building, rebuilding or redesigning a fullstack website, choosing a stack, defining UI direction, or adding security gates.
---

# WebForge

WebForge runs four phases in order. Load the phase file when its phase starts.

Phases:

1. Design — `phases/01-design.md`
2. Build — `phases/02-build.md`
3. Check — `phases/03-check.md`
4. Ship — `phases/04-ship.md`

## First run

On first activation, if `webforge.config.md` does not exist in the project root, ask one question at a time. Question 1 is open (no options); each of the other questions has options [A] [B] [C] with one marked recommended with a reason, plus [D] "Type your own answer". Save each answer to `webforge.config.md` as it is given. Questions, in order:

1. What are you building and who uses it?
2. Stack. WebForge recommends; the user picks. See `references/stack-guide.md`.
3. Visual direction: three concrete directions, each with a short text sketch (palette, type pairing, mood). The user picks or mixes.
4. Languages. Default `id` + `en`.
5. Auth and roles: is there an admin area? Where does it live?
6. Hosting target (needed for the Ship phase).

Re-run questions only when the user asks to reconfigure.

## Owners

| Phase | Owner skills |
|---|---|
| Design | `ui-ux-pro-max`, `frontend-design` |
| Build | `ponytail`, `test-driven-dev` |
| Check | `code-vuln-audit` + WebForge admin-exposure check |
| Ship | `pipeline-blueprint`, `http-load-profiler` |

Full list, install commands and per-phase owners: `references/dependencies.md`.
