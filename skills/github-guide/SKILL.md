---
name: github-guide
description: This skill should be used when Niclas asks about GitHub or git, e.g. "skapa ett repo", "nytt repo", "varför syns inte repot", "kan du pusha", "hur gör jag en PR", "koppla GitHub", "gh", "GitHub-plugin", or when a GitHub step (clone, push, pull request, repo access) fails. Holds what Claude can and cannot do on GitHub per app, the proven workflows, official links, and Niclas own GitHub setup and needs, which grow over time.
---

# GitHub-guide

Senast ändrat: 2026-11-27

Niclas är nybörjare på git och GitHub. Målet är att Claude sköter allt han
inte behöver kunna, och förklarar kort varför när något kräver hans hand.
Niclas fattar alla beslut. Skrivregeln gäller (beskriv, vänta på ok, utför,
rapportera).

## Gör först

1. Läs `references/niclas-setup.md`: hans konto, val och tidigare hinder.
2. Kontrollera miljön innan svar: vilka repon sessionen har
   (`list_repos`), om en dator är kopplad, vilken app som används.
   En direkt observation vinner över dokumentationen.
3. Svara utifrån tabellen nedan. Fakta om produkterna kontrolleras mot
   länkarna i `references/lankar.md` när de kan ha ändrats.

## Vad Claude kan göra, per app

| Uppgift | Molnsession (claude.ai/code, mobil) | Lokal Claude Code (Desktop "Local", terminal) | Chatt/Projects |
|---|---|---|---|
| Skapa nytt repo | Nej. `create_repository` är spärrat; `gh` bara för sökning | Ja, med `gh repo create` om `gh` är installerat och inloggat | Nej |
| Läsa/ändra kod, commit, push till gren, PR | Ja, i repon kopplade till sessionen | Ja | Nej (bara läsa filer) |
| Lägga till ett befintligt repo i sessionen | Ja, `add_repo`, om Claude-appen har åtkomst | Ej relevant | Välj i bilaga/projekt |
| Push till `main`, force-push, radera gren | Kräver Niclas ok; proxyn nekar radering | Kräver ok | Nej |

Anthropics GitHub-plugin (connector) i claude.ai: läser filer och ger
repoval i Claude Code. Kan inte skapa repon, issues eller PR själv.
Ska behållas: det är det som ger molnsessioner åtkomst.

## Arbetsflöde: nytt repo (Niclas val 2026-11-27: alternativ B)

1. Niclas öppnar `https://github.com/new?name=NAMN&visibility=private&owner=@me`
   (fyll i NAMN åt honom).
2. Kryssa i **Add a README**, annars är repot tomt och kan inte klonas.
3. Om Claude-appen bara har valda repon: lägg till det nya på
   `https://github.com/apps/claude/installations/select_target`.
   Det är det vanligaste skälet till att ett nytt repo inte syns.
4. Claude kör `add_repo` i pågående session, eller Niclas väljer repot
   när en ny session startas.

## Arbetsflöde: vanligt kodarbete i molnet

- Arbeta på sessionens `claude/`-gren. Commit, push, öppna utkast-PR.
- Förklara PR enkelt: "ett förslag på ändring som du godkänner på GitHub".
- Merge görs av Niclas, aldrig av Claude.

## När något går fel

Säg i en rad vilket steg som föll (klona, läsa, pusha, PR), sedan åtgärden:

- Repo syns inte / 403 → Claude-appen saknar åtkomst till repot (steg 3 ovan),
  eller GitHub är inte kopplat: `https://claude.ai/connect-github`.
- Push nekad → bara grenar kan pushas; `main` kräver ok.
- `gh pr` / `gh issue` misslyckas i molnet → GraphQL är blockerat; använd
  GitHub-verktygen (`mcp__github__*`).

Registrera varje nytt hinder och lösning i `references/niclas-setup.md`
(med datum) efter Niclas ok.

## Lär inte ut i onödan

Niclas behöver inte lära sig: grenar, commits, rebase, merge-konflikter,
`.gitignore`, PR-mallar. Claude sköter dem och nämner bara resultatet.
Han behöver känna till: github.com/new, Claude-appens repoåtkomst,
att godkänna (merga) en PR.

## Resurser

- **`references/niclas-setup.md`** – konto, val, inställningar, hinderlogg.
  Fylls på efterhand.
- **`references/lankar.md`** – officiella länkar: GitHub, git, Claude Code.
