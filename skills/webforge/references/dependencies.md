# Dependencies

External skills WebForge calls. Each skill has exactly one owner phase (design doc section 7). WebForge never auto-installs a dependency: when one is missing, it tells the user and asks first.

Licenses verified with `gh repo view` on 2026-11-25 (all MIT). Skills whose source is not in the design doc: `final-review` and `localization-toolkit` — no dedicated repo was verified, marked "unverified" below. WebForge calls them by name per the design doc.

## Build phase

| Skill | Source | License | Install | Fallback (design doc gaps) |
|---|---|---|---|---|
| ponytail | https://github.com/DietrichGebert/ponytail | MIT | `npx skills add DietrichGebert/ponytail` | No fallback — write minimal code yourself. |
| test-driven-dev | https://github.com/obra/superpowers | MIT | `npx skills add obra/superpowers` | Write the test first and watch it fail; fix code until it passes. |
| localization-toolkit | unverified | unverified | unverified | Fallback: set up locales with the app's framework (`id` + `en`). |

## Check phase

| Skill | Source | License | Install | Fallback (design doc gaps) |
|---|---|---|---|---|
| code-vuln-audit | https://github.com/zebbern/claude-code-guide | MIT | `npx skills add zebbern/claude-code-guide` | Run `npm audit` (or pip-equivalent) manually with the app's tooling. |
| route-to-openapi | https://github.com/zebbern/claude-code-guide | MIT | `npx skills add zebbern/claude-code-guide` | Only supported for some frameworks; for others use the framework's built-in schema generators. |

## Ship phase

| Skill | Source | License | Install | Fallback (design doc gaps) |
|---|---|---|---|---|
| pipeline-blueprint | https://github.com/JantonioFC/skillsbank | MIT | `npx skills add JantonioFC/skillsbank` | Copy CI configs from the repo's workflows; ask for a concrete template. |
| http-load-profiler | unverified | unverified | unverified | Ask the user to run a load test manually (staging only). |
| security-audit (Cloudflare) | https://github.com/cloudflare/security-audit-skill | MIT | `npx skills add cloudflare/security-audit-skill` | Manual review in the Cloudflare dashboard. |

## Design phase

| Skill | Source | License | Install | Fallback (design doc gaps) |
|---|---|---|---|---|
| ui-ux-pro-max | https://github.com/nextlevelbuilder/ui-ux-pro-max-skill | MIT | `npx skills add nextlevelbuilder/ui-ux-pro-max-skill` | Follow the project's design system defaults; keep type/color off generic sets. |
| frontend-design | unverified | unverified | unverified | Design from the Design-phase doc and tokens; use the framework's design system. |
| design-system-builder | https://github.com/signerlabs/design-system-builder-skills | MIT | `npx skills add signerlabs/design-system-builder-skills` | Only when the user supplies a screenshot or Figma reference; otherwise reuse the ui-ux-pro-max tokens. |
| final-review | unverified | unverified | unverified | Fallback: read `docs/DESIGN.md` and `docs/DESIGN-TOKENS.md` carefully once and rewrite anything that reads like filler. |

## Used by WebForge (no phase owner)

| Skill | Source | License | Install | Use |
|---|---|---|---|---|
| caveman | unverified | unverified | unverified | WebForge chat voice per design doc section 8: chat prose gets Caveman, files/code stay normal. |
