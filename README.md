# dsgvo-skill

Die DSGVO (VO (EU) 2016/679, dt. Fassung 27.04.2016) als KI-Skills für kleine lokale Sprachmodelle (7B). Statt 88 Gesetzesseiten in den Kontext zu laden: Fassade + 8 Fach-Skills + 99 verdichtete Artikel-Karten — jede Antwort mit Artikel-, Absatz- und Literatürbezeichnung, fail-closed („Keine Aussage ohne Artikelbezug").

## Inhalt

- `dsgvo/` — Wegweiser (Routing, Kombinationsbudget ≤3, Disclaimer)
- `dsgvo-<thema>/` — 8 Fach-Skills (Grundsätze, Einwilligung, Betroffenenrechte, Auftragsverarbeitung, Verzeichnisse, Sicherheit/TOM, Datenpannen, Drittländer)
- `dsgvo/_references/artikel-01.md … artikel-99.md` — Artikel-Karten im festen Skelett (Kern/Pflichten/Ausnahmen/Fristen/Prüfung), Index in `dsgvo/_references/README.md`
- `INDEX.md`, `FAMILIES.md`, `FACTS.md` — Registry (Flyweight: Begriffe aus Art. 4 zentral)
- `KONVENTIONEN.md` — Architektur-Standard für weitere Skill-Familien

## Nutzung

Voraussetzung: lokaler Ollama-Assistent, der `--skill <name>` aus einem Skills-Verzeichnis lädt (z. B. `ai` aus dem `ollama-local`-Setup).

**Variante A — direkt aus dem Repo** (alle Pfade relativ zum Repo-Wurzel):

```bash
cd dsgvo-skill
ai --skill dsgvo-betroffenenrechte dsgvo/_references/artikel-17.md \
  "Kunde verlangt Löschung — wann müssen wir löschen, wann nicht?"
```

**Variante B — als Skill-Installation** (Fach-Skills nach `~/.agents/skills` verlinken):

```bash
cd dsgvo-skill
for d in dsgvo dsgvo-*; do ln -sfn "$(pwd)/$d" "$HOME/.agents/skills/$d"; done
ai --skill dsgvo-datenpannen dsgvo/_references/artikel-33.md "Datenleck — bis wann melden, was gehört in die Meldung?"
```

Karten werden als Dateipfad-Argument übergeben — rufen Sie `ai` dafür aus dem Repo-Wurzelverzeichnis auf (Variante A) oder passen Sie die Pfade an Ihre Installation an.

## Regeln für Antworten

- Jede Aussage mit Artikelbezug (Art. N Abs. X lit. Y).
- Bei Unsicherheit: Unsicherheit aussprechen, nichts erfinden.
- Maximal 3 Kontextschichten pro Anfrage (1 Skill + bis zu 2 Karten).
- Quelle der Artikeltexte: EUR-Lex CELEX 32016R0679 (© Europäische Union, Weiterverwendung erlaubt); Karten sind verdichtete, stichprobenkontrollierte Regeltexte — kein Ersatz für Rechtsberatung.
