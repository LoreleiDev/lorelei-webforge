# 04 Ship

1. Read `references/dependencies.md`.
2. CI/CD templates (owner): use `pipeline-blueprint`; pin versions in generated pipelines (design doc gap).
3. Load test (owner): `http-load-profiler` — staging only, with explicit user approval.
4. Deep pre-release audit (owner): Cloudflare `security-audit` — manual, once per release; needs a sandbox that blocks network access; findings stay `needs_validation` without one.
