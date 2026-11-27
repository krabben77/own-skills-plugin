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
  github-guide/                 eget: GitHub/git för Niclas, per app, hinderlogg
```

`hooks/hooks.json` kör `hooks/session-start` vid varje sessionsstart
(startup/clear/compact). Skriptet injicerar en kort, strikt text som säger
åt modellen att den MÅSTE använda en skill om den rimligen kan passa,
innan den svarar eller agerar — samma mekanism som superpowers'
`using-superpowers`, men utan separat meta-skill-fil att hålla i synk.
Claude Code-specifikt: filen heter `session-start` utan `.sh`-ändelse för
att undvika Claude Codes auto-bash-wrapping av `.sh`-kommandon på Windows.

## Vägval 2026-11-27: egen bas, inte fork

**Syfte.** Pluginet är Niclas egen bas: en generisk brygga för en nybörjare
som bygger och fixar projekt, lokalt och i molnet. Det anpassas efterhand när
riktiga projekt visar behov. Inget laddas ner från community utan granskning
(virusrisk). En riktig fork av superpowers är överkurs tills vidare.

**Valt: A. Ta in, laga, anpassa efterhand.**
- Ta in de sju användbara skills som saknas, oförändrade: `writing-skills`,
  `executing-plans`, `subagent-driven-development`,
  `dispatching-parallel-agents`, `requesting-code-review`,
  `receiving-code-review`, `using-git-worktrees`.
- Läs varje skript rad för rad före intag. Det som inte förstås eller behövs
  tas inte med.
- Laga hänvisningar `superpowers:` → `own-skills:` (ett 60-tal ställen,
  trasiga redan i dag).
- Notera källa, version och granskning i `KALLOR.md`.
- Ändra en skill först när ett verkligt projekt visar ett behov.
- Skills förblir på engelska: de är instruktioner till Claude. Svaren till
  Niclas är på svenska via hans inställningar.

**Bortvalt, kan tas fram vid behov:**
- **B. Skriva om allt direkt till svenska och nybörjarnivå.** Personligast
  direkt, men mycket arbete nu, bygger på gissade behov och riskerar att
  tappa det som gör skillsen bra. Passar när några projekt visat vad som
  behövs.
- **C. Bara några få nu, resten senare.** Mindre att granska, men
  arbetsflödena blir halva (planering pekar på utförande som saknas).
- **Riktig fork med två lager** (superpowers orörd + eget lager ovanpå).
  Gör uppdateringar från originalet enkla. Värt när Niclas vill ta in nya
  superpowers-versioner regelbundet.

**Tas inte med:** `using-superpowers` (samma jobb som vår
`hooks/session-start`) och `diagnosing-superpowers` (felsöker superpowers
själv).

Design: `docs/specs/2026-11-27-egen-bas-design.md`.

## Nästa beslut

- Döpa om pluginet och fylla i author/homepage i plugin.json

## Attribution

Innehållet i `skills/` är kopierat från [obra/superpowers](https://github.com/obra/superpowers)
(MIT-licens, © Jesse Vincent). `LICENSE` är därför bibehållen oförändrad.
