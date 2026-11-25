# 01 Design

Produce: `docs/DESIGN.md` (design doc) and `docs/DESIGN-TOKENS.md` (token set).

Owners: `ui-ux-pro-max` (default brain, persisted as MASTER.md + tokens), `frontend-design` (frontend craft guidance), `final-review` (prose only, never code).

Steps:

1. Read `references/design-ambition-checklist.md` and `references/admin-exposure-rules.md`.
2. If the brief is vague, ask one question at a time until you have enough.
3. Offer three visual directions (see the router for the direction style). The user picks or mixes.
4. Write the design doc headings and the token set. Pass the ambition checklist and the bland test (swap the logo — the site must still look distinctive).
5. Admin exposure: no admin link, button, menu item, icon or text hint on the public pages. The admin entry is an unlinked route, guarded by authentication and role checks on the server.
6. When the user later asks to change the design, run the revision loop from the checklist (three new directions, regenerate tokens, show the token diff).
