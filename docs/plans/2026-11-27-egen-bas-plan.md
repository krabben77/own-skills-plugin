# Egen bas: genomförandeplan

Senast ändrat: 2026-11-27

> **För den som genomför:** använd `own-skills:executing-plans` (inline) eller
> `own-skills:subagent-driven-development`. Stegen har kryssrutor.

**Mål:** Ta in sju superpowers-skills i `own-skills`, granskade och med fungerande hänvisningar.

**Arkitektur:** Kopiera skillmapparna oförändrade från källan, granska varje skript, byt prefix i hänvisningarna, dokumentera källan. Ingen ny logik.

**Tekniker:** Markdown, bash (`grep`, `diff`, `python3` för frontmatter-kontroll).

**Spec:** `docs/specs/2026-11-27-egen-bas-design.md`

## Globala krav

- Källa: `/home/user/krabben77/superpowers`, commit `22f0b46` (v7.0.2), MIT. Kontrollera med `git -C /home/user/krabben77/superpowers rev-parse --short HEAD`.
- De sju skillsen: `writing-skills`, `executing-plans`, `subagent-driven-development`, `dispatching-parallel-agents`, `requesting-code-review`, `receiving-code-review`, `using-git-worktrees`.
- Tas inte med: `using-superpowers`, `diagnosing-superpowers`.
- `LICENSE` oförändrad. Inga modellnamn i filer eller commit-meddelanden.
- Arbeta på grenen `claude/awesome-davinci-2o7o3d` i `/home/user/own-skills-plugin`.
- Skript som inte förstås eller inte behövs tas inte med. Skills förblir på engelska.

## Granskningsfokus

1. Skript som skriver eller raderar utanför projektmappen. Förväntat: ingen sådan, annars tas skriptet inte med.
2. Skript som använder nätverk (`curl`, `wget`, `nc`, `http`). Förväntat: inget, annars tas det inte med.
3. Hänvisning till en skill vi inte har (`using-superpowers`, `diagnosing-superpowers`). Förväntat: ändrad eller borttagen, aldrig trasig.
4. En skill som anropar ett skript som uteslöts. Förväntat: skillens text fungerar utan skriptet.
5. Ett befintligt skillnamn som skrivs över av kopieringen. Förväntat: de sex befintliga är oförändrade förutom prefixbytet.

---

### Uppgift 1: Kopiera och granska skript

**Filer:**
- Skapa: `skills/<de sju>/` (kopia av källan)
- Skapa: `KALLOR.md`

**Producerar:** `KALLOR.md` med en rad per skript (vad det gör, nätverk ja/nej, skriver utanför projektet ja/nej, taget med ja/nej). Uppgift 2 läser den för att veta vilka skript som finns kvar.

- [ ] **Steg 1: Kopiera de sju mapparna** med `cp -r` från `/home/user/krabben77/superpowers/skills/<namn>` till `skills/`. Kontrollera: `diff -rq` mot källan visar inga skillnader.
- [ ] **Steg 2: Lista skripten.** Kör `find skills -type f \( -name '*.sh' -o -name '*.js' -o -path '*/scripts/*' \)`. Förväntat: 7 nya skript, `executing-plans/scripts/task-done`, `executing-plans/scripts/task-start`, `subagent-driven-development/scripts/{review-package,sdd-repo,sdd-workspace,task-brief}` och `writing-skills/render-graphs.js`. Avvikelse från de sju: stanna och rapportera.
- [ ] **Steg 3: Läs varje skript hela, rad för rad.** Sök även mekaniskt: `grep -nE 'curl|wget|nc |http|ssh|rm -rf|eval|base64|/etc|~/\.|\$HOME' <skript>`. Bedöm per skript mot granskningsfokus 1 och 2.
- [ ] **Steg 4: Skriv `KALLOR.md`:** källa (repo, commit `22f0b46`, version, licens), tabell över skripten, lista över skills som inte togs med och varför, datum överst. Skript som inte klarar granskningen tas bort från `skills/` och noteras.
- [ ] **Steg 5: Committa.** `git add skills KALLOR.md && git commit -m "Ta in sju superpowers-skills och granska skript"`.

### Uppgift 2: Laga hänvisningar

**Filer:**
- Ändra: alla `SKILL.md` och `.md`-filer under `skills/` som innehåller `superpowers:`

**Konsumerar:** den slutliga skriptlistan i `KALLOR.md`.

- [ ] **Steg 1: Mät före.** `grep -rho 'superpowers:[a-z-]*' skills | sort | uniq -c`. Spara utfallet till rapporten.
- [ ] **Steg 2: Byt prefix** `superpowers:` till `own-skills:` för de skills vi har: `sed -i` med en regel per skillnamn (inte en bred ersättning), så att `using-superpowers` och `diagnosing-superpowers` inte råkar bytas.
- [ ] **Steg 3: Åtgärda hänvisningar till skills vi inte har.** `grep -rn 'using-superpowers\|diagnosing-superpowers' skills`. Ändra eller ta bort meningen så att texten fortfarande är sammanhängande, och notera varje ändring i `KALLOR.md` under "Ändringar mot källan".
- [ ] **Steg 4: Åtgärda anrop till skript som uteslöts** (granskningsfokus 4) på samma sätt.
- [ ] **Steg 5: Kontrollera.** `grep -rn 'superpowers:' skills` ska ge noll träffar. Alla `own-skills:X` ska peka på en befintlig mapp:
  `grep -rho 'own-skills:[a-z-]*' skills | sort -u | sed 's/own-skills://' | while read n; do [ -d skills/$n ] || echo "SAKNAS: $n"; done` ska inte skriva ut något.
- [ ] **Steg 6: Committa.** `git commit -am "Byt superpowers: mot own-skills: i hänvisningar"`.

### Uppgift 3: Manifest, README och slutkontroll

**Filer:**
- Ändra: `.claude-plugin/plugin.json`
- Ändra: `README.md`

- [ ] **Steg 1: `plugin.json`:** `version` till `0.2.0`, `description` uppdaterad till att tala om alla skills (14 st inklusive `github-guide`).
- [ ] **Steg 2: README:** lägg de sju skillsen i strukturlistan med en rad vardera, hänvisa till `KALLOR.md`, och flytta designen från "utkast" till "godkänd 2026-11-27" i `docs/specs/2026-11-27-egen-bas-design.md`.
- [ ] **Steg 3: Slutkontroll** (kör allt, visa utfallet):
  - `python3 -c` som läser frontmatter i varje `skills/*/SKILL.md` och skriver ut `name` (ska stämma med mappnamnet, 14 st).
  - `python3 -c "import json;json.load(open('.claude-plugin/plugin.json'))"` utan fel.
  - `git status --short` är tom efter commit.
  - `diff -rq` mot källan för de sex ursprungliga skillsen visar bara prefixbytet (granskningsfokus 5).
- [ ] **Steg 4: Committa och pusha.** `git commit -am "Uppdatera manifest och README för egen bas v0.2.0"` och `git -c push.negotiate=true push`. PR #1 uppdateras av pushen.

## Egen granskning mot spec

- Täckning: intag (U1), skriptgranskning (U1), hänvisningar (U2), KALLOR/README/plugin.json (U1, U3), verifiering (U2 steg 5, U3 steg 3). Inget saknas.
- Proportion: planen är kort eftersom arbetet är kopiering och kontroll, inte kod.
- Test: kontrollerna är kommandon med förväntat utfall, inte enhetstester, eftersom det inte finns någon programkod att testa.
