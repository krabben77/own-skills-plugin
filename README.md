# own-skills

Minimal Claude Code-plugin med de sex mest återanvändbara skills från
`obra/superpowers` (MIT-licens), kopierade rakt av utan harness-beroenden.

## Struktur

```
.claude-plugin/plugin.json   manifest (namn, version)
skills/
  brainstorming/               kravställning innan byggande
  test-driven-development/     skriv test först
  systematic-debugging/        root cause före fix
  verification-before-completion/   bevis före påstående om klart
  writing-plans/                plan för flerstegsuppgifter
  finishing-a-development-branch/   verifiera -> välj integrationsväg -> städa
```

`hooks/hooks.json` kör `hooks/session-start` vid varje sessionsstart
(startup/clear/compact). Skriptet injicerar en kort, strikt text som säger
åt modellen att den MÅSTE använda en skill om den rimligen kan passa,
innan den svarar eller agerar — samma mekanism som superpowers'
`using-superpowers`, men utan separat meta-skill-fil att hålla i synk.
Claude Code-specifikt: filen heter `session-start` utan `.sh`-ändelse för
att undvika Claude Codes auto-bash-wrapping av `.sh`-kommandon på Windows.

## Nästa beslut

- Döpa om pluginet och fylla i author/homepage i plugin.json
- Bestämma om skills ska trimmas/anpassas efter eget arbetssätt eller
  behållas orörda

## Attribution

Innehållet i `skills/` är kopierat från [obra/superpowers](https://github.com/obra/superpowers)
(MIT-licens, © Jesse Vincent). `LICENSE` är därför bibehållen oförändrad.
