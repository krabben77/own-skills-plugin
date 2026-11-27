# Källor och granskning

Senast ändrat: 2026-11-27

## Källa

- Repo: `krabben77/superpowers` (fork av `obra/superpowers`)
- Commit: `22f0b46`, version 7.0.2, 2026-11-03
- Licens: MIT, © Jesse Vincent. `LICENSE` är oförändrad.
- Intaget 2026-11-27 följer `docs/specs/2026-11-27-egen-bas-design.md`.

## Vad som togs in

Sju skills, kopierade med alla filer och verifierade identiska med källan
innan någon ändring: `writing-skills`, `executing-plans`,
`subagent-driven-development`, `dispatching-parallel-agents`,
`requesting-code-review`, `receiving-code-review`, `using-git-worktrees`.

## Skriptgranskning (varje skript läst hela, rad för rad)

Metod: läst i sin helhet, samt sökt efter `curl`, `wget`, `nc`, `http`,
`ssh`, `rm -rf`, `eval`, `base64`, `sudo`, `chmod`, `npm`, `pip`, `fetch`,
`child_process`, `/etc`, `$HOME`. Inga CR-tecken (dolda radslut).

| Skript | Vad det gör | Nätverk | Skriver utanför projektet | Taget med |
|---|---|---|---|---|
| `executing-plans/scripts/task-start` | Hämtar en uppgifts text ur planen, skriver ner nuvarande commit (BASE) | Nej | Nej | Ja |
| `executing-plans/scripts/task-done` | Kör den testkommando som anropet anger, loggar utfallet, skriver en rad i framstegsloggen om testet lyckas | Nej | Nej | Ja |
| `subagent-driven-development/scripts/sdd-repo` | Skriver ut git-projektets rotmapp, stoppar utanför ett git-projekt | Nej | Nej | Ja |
| `subagent-driven-development/scripts/sdd-workspace` | Skapar arbetsmappen `.superpowers/sdd/<plan>/` i projektet, med egen `.gitignore` (`*`) | Nej | Nej | Ja |
| `subagent-driven-development/scripts/task-brief` | Klipper ut en uppgift ur planen till en fil i arbetsmappen; tar bara bort sin egen halvfärdiga utfil vid fel | Nej | Nej | Ja |
| `subagent-driven-development/scripts/review-package` | Samlar commit-lista och diff mellan två commits i en fil i arbetsmappen | Nej | Nej | Ja |
| `writing-skills/render-graphs.js` | Ritar flödesscheman till SVG med Node och Graphviz | Nej | Skriver `diagrams/` bredvid skillen | **Nej, borttaget** (behövs inte, kräver extra program) |

Att veta: `task-done` kör det testkommando som den som anropar skriptet
anger. Det är avsikten, men det betyder att skriptet är lika säkert som
kommandot som ges.

## Ändringar mot källan

- `writing-skills/render-graphs.js` borttaget. Meningen i
  `writing-skills/references/flowcharts.md` som pekade på det ersatt med
  "visa flödesschemat som mermaid-diagram i svaret".
- Hänvisningar `superpowers:` → `own-skills:` (se commit "Byt superpowers: mot own-skills:").
- `using-git-worktrees/SKILL.md` steg 2: fråga först före installationer.
- `brainstorming/scripts/server.cjs`: logotypen hämtas aldrig (se fyndet nedan).

## Texter som kunde ladda ner eller radera (beslut 2026-11-27)

- `using-git-worktrees/SKILL.md` steg 2 körde automatiskt `npm install`,
  `pip install`, `poetry install`, `cargo build` och `go mod download`
  (kod från tredje part). **Ändrat:** Claude frågar Niclas först och väntar på ja.
- `subagent-driven-development/references/final-review.md` raderar arbetsmappen
  `.superpowers/sdd/<plan>` med `rm -rf`. **Orört:** mappen ligger i projektet
  och är tillfällig.

## Inte medtaget

- `using-superpowers`: samma jobb som `hooks/session-start`.
- `diagnosing-superpowers`: felsöker superpowers själv.

## Fler ändringar mot källan (hänvisningar)

- `executing-plans/SKILL.md`: meningen som pekade på
  `../using-superpowers/references/` borttagen (skillen finns inte hos oss).
- `writing-skills/SKILL.md`: länkarna till `using-superpowers/references/codex-tools.md`
  och `gemini-tools.md` ersatta med "skills ligger i `skills/<namn>/SKILL.md`".
- Sökvägar som `docs/superpowers/plans/` och `.superpowers/sdd/` är orörda. De är
  mappnamn i användarens projekt, inte hänvisningar till pluginet.

## Fynd i en tidigare befintlig skill: `brainstorming` (åtgärdat)

Hittat 2026-11-27 under granskningen.

- `skills/brainstorming/scripts/server.cjs` (den visuella följeslagaren, en lokal
  webbserver, bara om Niclas tackat ja) hämtade en logotyp från
  `https://primeradiant.com/brand/superpowers-visual-brainstorming-logo.png?v=<version>`
  om inte `SUPERPOWERS_DISABLE_TELEMETRY` eller `DISABLE_TELEMETRY` var satt.
  Det är en förfrågan ut på nätet med versionsnumret.
- **Ändrat:** `SUPERPOWERS_TELEMETRY_DISABLED = true` (en rad plus kommentar), så
  logotypen aldrig hämtas oavsett inställning.
- **Verifierat:** servern startad med originalfilen och med vår, sidan hämtad
  med giltig nyckel. Original: `<img src="https://primeradiant.com/...logo.png?v=7.0.2">`.
  Vår: ingen `<img>` och ingen `primeradiant` i sidan. Märkningen visar
  "vunknown" som version (utseende, ingen funktion).
- Övrigt i `brainstorming`: inga andra utgående anrop (länken till GitHub är en
  klickbar adress, WebSocket går till den egna datorn).

