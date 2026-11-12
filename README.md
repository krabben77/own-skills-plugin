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

Ingen `hooks/` och ingen `using-superpowers`-bootstrap här ännu — skills
måste anropas explicit (`/skill-namn` eller att modellen själv känner igen
situationen) tills en egen SessionStart-hook eller motsvarande läggs till.

## Nästa beslut

- Döpa om pluginet och fylla i author/homepage i plugin.json
- Bestämma om skills ska trimmas/anpassas efter eget arbetssätt eller
  behållas orörda
- Lägga till en egen `hooks/hooks.json` om auto-trigger vid sessionsstart
  önskas

## Attribution

Innehållet i `skills/` är kopierat från [obra/superpowers](https://github.com/obra/superpowers)
(MIT-licens, © Jesse Vincent). `LICENSE` är därför bibehållen oförändrad.
