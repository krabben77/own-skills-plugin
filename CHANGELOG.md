# Ändringslogg

Senast ändrat: 2026-11-27

Format: senaste överst. Varje version listar vad som lagts till, ändrats och
åtgärdats. Skriv in en rad här för varje ändring som merges. Källa och
granskning av intagna skills: se `KALLOR.md`.

## 0.2.0 – 2026-11-27 (PR #1, väntar på merge)

### Tillagt
- **`github-guide`**: egen skill om GitHub och git per app (moln, lokal,
  chatt), arbetsflöde för nya repon, felsökning, officiella länkar och en
  hinderlogg som fylls på efterhand (`references/niclas-setup.md`,
  `references/lankar.md`).
- **Sju skills från superpowers v7.0.2** (commit `22f0b46`, MIT): `writing-skills`,
  `executing-plans`, `subagent-driven-development`,
  `dispatching-parallel-agents`, `requesting-code-review`,
  `receiving-code-review`, `using-git-worktrees`. Totalt 14 skills.
- `KALLOR.md`: källa, version, skriptgranskning (7 skript lästa rad för rad,
  inget använder nätet) och alla ändringar mot originalet.
- `docs/specs/2026-11-27-egen-bas-design.md` (godkänd) och
  `docs/plans/2026-11-27-egen-bas-plan.md`.
- README: vägvalet "egen bas, inte fork" med de bortvalda alternativen (B, C,
  riktig fork) så att de kan tas fram senare.
- Den här filen.

### Ändrat
- Hänvisningar `superpowers:` → `own-skills:` på 43 ställen, även i de sex
  tidigare skillsen. Före: trasiga hänvisningar.
- `plugin.json`: version 0.2.0, ny beskrivning.
- `executing-plans/SKILL.md` och `writing-skills/SKILL.md`: borttagna
  hänvisningar till `using-superpowers`, som vi inte har.
- `writing-skills/references/flowcharts.md`: pekar inte längre på
  `render-graphs.js`; visa flödesscheman som mermaid i stället.
- `using-git-worktrees/SKILL.md` steg 2: **frågar dig först** innan något
  `npm install`, `pip install`, `cargo build` eller liknande körs.

### Borttaget
- `writing-skills/render-graphs.js` (behövs inte, kräver Node och Graphviz).

### Säkerhet
- **`brainstorming/scripts/server.cjs`**: den visuella följeslagaren hämtade en
  logotyp från `primeradiant.com` med versionsnumret i adressen, om inte en
  telemetri-variabel var satt. Nu hämtas den aldrig. Verifierat: originalet gör
  anropet utan inställning, vår version gör det inte.
  Bieffekt: märkningen i hörnet visar "vunknown" som version (utseende, ingen
  funktion).

### Ej medtaget
- `using-superpowers` (samma jobb som `hooks/session-start`) och
  `diagnosing-superpowers`.

## 0.1.0 – 2026-11-12

### Tillagt
- Sex skills från superpowers, kopierade oförändrade: `brainstorming`,
  `test-driven-development`, `systematic-debugging`,
  `verification-before-completion`, `writing-plans`,
  `finishing-a-development-branch`.
- `hooks/hooks.json` och `hooks/session-start`: påminner vid varje sessionsstart
  om att använda en skill när någon passar.
- `.claude-plugin/plugin.json`, `LICENSE` (MIT, © Jesse Vincent), `README.md`.
