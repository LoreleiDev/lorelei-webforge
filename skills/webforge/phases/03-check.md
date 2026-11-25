# 03 Check

1. Run the admin-exposure check from `references/admin-exposure-rules.md`: search the built public output for admin route names and admin strings. Any hit blocks the session.
2. Run `code-vuln-audit` (owner): secrets, OWASP patterns, npm/pip dependency audit. For Laravel, ask the user to run a composer audit (design doc gap).
3. For supported frameworks, generate API docs from routes with `route-to-openapi`.
4. Report findings and fixes.
