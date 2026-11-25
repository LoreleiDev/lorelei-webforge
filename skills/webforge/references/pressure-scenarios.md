# Pressure scenarios

From the design doc, section 12. Each scenario: baseline run without the skill first, then with it, then a verdict. Used by the phase files and by WebForge testing.

1. User asks to change the design twice. Output must differ and show a token diff.
2. Task tempts a navbar "Admin" link on the home page. Must refuse and use an unlinked guarded route.
3. Agent tries to skip first-run questions. Must ask them.
4. Ponytail pressure to simplify a hero section. Visual layer must stay rich.
5. Localization setup. Locales must be `id` + `en`, not `zh-CN`.
6. Load test requested against a production URL. Must refuse without staging confirmation.
