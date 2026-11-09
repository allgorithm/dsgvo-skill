# Skill-Index (Repo `dsgvo-skill`)

Einstieg: Name, Datei, Einsatz je Skill. Gelesen wird danach nur die `SKILL.md` der passenden Skills; Artikel-Karten unter `dsgvo/_references/` erst bei Bedarf nachgeladen.

## Skill-Auswahl (Facade)

- **Jede DSGVO-Frage:** `dsgvo` (Wegweiser) zuerst — leitet in Fach-Skills und Karten.
- **Unsicher, welcher Skill?** Vollständige Tabelle unten; Familien: `FAMILIES.md`; geteilte Begriffe: `FACTS.md`.

## Vollständige Tabelle

| Skill | Datei | Einsatz |
| :--- | :--- | :--- |
| `dsgvo` | `dsgvo/SKILL.md` | DSGVO-Wegweiser: Anliegen → Fach-Skill/Karte, Kombinationsregeln |
| `dsgvo-grundsaetze` | `dsgvo-grundsaetze/SKILL.md` | Art. 5, 24, 25, 35, 36, 40–43: Grundsätze, Design, DSFA, Nachweis |
| `dsgvo-einwilligung` | `dsgvo-einwilligung/SKILL.md` | Art. 6–10, 22: Rechtsgrundlagen, Einwilligung, Kategorien, Profiling |
| `dsgvo-betroffenenrechte` | `dsgvo-betroffenenrechte/SKILL.md` | Art. 11–23, 77–81: Auskunft bis Klage, Fristen |
| `dsgvo-auftragsverarbeitung` | `dsgvo-auftragsverarbeitung/SKILL.md` | Art. 26–29, 31: AVV, Subprozessoren, Gemeinsame, Vertreter |
| `dsgvo-verzeichnisse` | `dsgvo-verzeichnisse/SKILL.md` | Art. 30: Verzeichnis der Verarbeitungstätigkeiten |
| `dsgvo-sicherheit-tom` | `dsgvo-sicherheit-tom/SKILL.md` | Art. 32, 37–39: TOM, Sicherheit, Datenschutzbeauftragter |
| `dsgvo-datenpannen` | `dsgvo-datenpannen/SKILL.md` | Art. 33/34: Meldung 72h, Benachrichtigung, Zustands-Automat |
| `dsgvo-drittländer` | `dsgvo-drittländer/SKILL.md` | Art. 44–50: Transfers, SCC, BCR, Ausnahmen |

## Konventionen

- Größenbudgets: `SKILL.md` 40–80 Zeilen, Artikelkarte ≤25 Zeilen, Registry-Datei ≤40 Zeilen.
- Skills kombinierbar via `ai --skill a --skill b` — Decorator-Budget ≤3.
- DSGVO-Karten: `dsgvo/_references/artikel-NN.md` für Artikel 1–99, Index in `dsgvo/_references/README.md`.
- **Neue Familien** (z. B. EU AI Act, NIS-2): Naming `<familie>-<thema>`, Facade `<familie>/`, Material darunter — verbindlich in `KONVENTIONEN.md`.
