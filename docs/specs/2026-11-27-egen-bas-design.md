# Design: egen bas av superpowers-skills

Senast ändrat: 2026-11-27 · Status: utkast, väntar på Niclas godkännande

## Syfte och varför

Niclas vill ha en egen, generisk bas att arbeta med som nybörjare i
kommande projekt, lokalt och i molnet. Basen ska vara hel och fungerande nu
och anpassas efterhand. Den är också övningsmaterial för att lära sig bygga
egna plugins.

## Mål

- Alla användbara superpowers-skills finns i `own-skills`.
- Hänvisningar mellan skills fungerar (`own-skills:<namn>`).
- Varje fil som tas in är granskad; skript lästa rad för rad.
- Det går att se varifrån allt kommer och vad som ändrats.

## Icke-mål

- Ingen översättning eller omskrivning nu (alternativ B, se README).
- Ingen fork, inget upplägg för automatiska uppdateringar.
- Inga nya egna skills utöver `github-guide`.

## Anti-mål (misslyckande även om det tekniskt fungerar)

- Något kommer in ogranskat, eller ett skript som gör något oklart.
- Arbetsflödet bryts: en skill pekar på en som inte finns.

## Begränsningar

- Källa: `krabben77/superpowers`, commit `22f0b46` (v7.0.2), MIT-licens.
- `LICENSE` behålls oförändrad.
- Arbete på grenen `claude/awesome-davinci-2o7o3d`, samma PR som
  `github-guide`. Niclas mergar.

## Vägval

Se README, avsnittet "Vägval 2026-11-27". Valt: A.

## Hur (beslutat)

1. Kopiera de sju skillsen med alla filer.
2. Granska de skript som följer med: `executing-plans/scripts/*` (2),
   `subagent-driven-development/scripts/*` (4), `writing-skills/render-graphs.js`.
   Resultat per skript i `KALLOR.md`: vad det gör, nätverk/skrivning
   utanför projektet ja/nej, taget med ja/nej.
3. Byt `superpowers:` mot `own-skills:` i alla skills, även de sex
   befintliga. Hänvisningar till skills vi inte har (`using-superpowers`,
   `diagnosing-superpowers`) ändras eller tas bort.
4. Uppdatera README-strukturen och `plugin.json` (beskrivning, version 0.2.0).
5. Verifiera: inga `superpowers:`-hänvisningar kvar; varje `own-skills:X`
   pekar på en befintlig mapp; frontmatter i varje `SKILL.md` går att läsa.

## Lämnas till byggaren

- Exakt formulering där en hänvisning till en borttagen skill måste ändras.
- Om ett skript visar sig oklart: ta inte med det, notera i `KALLOR.md`,
  och justera skillens text så den fungerar utan.
