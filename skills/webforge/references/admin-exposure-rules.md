# Admin exposure rules

From the design doc, section 10.

- Public UI never contains an admin link, button, menu item, icon, or text hint. The admin affordance must not exist on public pages.
- The admin entry is an unlinked route. Protection is authentication plus role checks on the server. Hiding it is not the protection.
- No admin route names in public HTML, JS bundles, sitemap.xml, robots.txt, source maps, or comments.
- Check step: after each session, search the built public output for admin route names and admin strings. Any hit blocks the session.
