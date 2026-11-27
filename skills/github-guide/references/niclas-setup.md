# Niclas GitHub-setup och behov

Senast ändrat: 2026-11-27

Fylls på efterhand. Nya rader läggs överst i varje avsnitt, med datum.
Skriv bara hit efter Niclas ok.

## Konto och åtkomst

- GitHub-konto: `krabben77` (även organisationen `krabben77-Inc`).
- Anthropics GitHub-plugin i claude.ai: tillagd och ansluten (observerat 2026-11-27).
- Claude-appen på GitHub: når minst de repon `list_repos` visar (46 st 2026-11-27).
  Okänt om den har "alla repon" eller "valda repon".
- `gh` på egen dator: inte installerat/testat (2026-11-27).

## Beslut

- 2026-11-27: Nya repon skapas av Niclas på github.com/new (alternativ B).
  Lokalt `gh` och GitHubs eget MCP-plugin valdes bort tills vidare.
- 2026-11-27: Denna skill ligger i `own-skills-plugin`.

## Behov

- Automatisera allt han inte behöver kunna i förväg.
- Arbetar ofta från mobilen (claude.ai). Pluginkort syns inte där: svara i text.

## Hinderlogg

| Datum | Hinder | Orsak | Lösning |
|---|---|---|---|
| 2026-11-27 | Molnsession kunde inte skapa `test-repo` | `create_repository` spärrat i molnsessioner; `gh` bara för sökning | Skapa på github.com/new, sedan `add_repo` |
| 2026-11-27 | Anthropics GitHub-plugin kan inte skapa repon | Pluginet läser bara filer | Se ovan |
