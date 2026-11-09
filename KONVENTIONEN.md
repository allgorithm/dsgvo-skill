# Skill-Architektur: Konventionen für neue Familien

Verbindlich für alle künftigen Skill-Familien (z. B. EU AI Act, NIS-2, DSA). Änderungen nur hier dokumentieren.

## Beschluss 1: Flache Auflösung — keine Verschachtelung

Skills liegen flach als `<name>/SKILL.md` (Loader: `os.path.join(SKILL_DIR, name, "SKILL.md")` in `agent-ollama.sh`). Pfade mit `/` würden zwar auflösen, aber die Katalog-Discovery scannt flach. Ordnung entsteht über Naming (Beschluss 2) und Registry (Beschluss 3), nicht über Ordnerbäume.

## Beschluss 2: Familien-Prefix `<familie>-<thema>`

- Fach-Skills: `<familie>-<thema>` — Beispiele: `dsgvo-betroffenenrechte`; künftig z. B. `aiact-transparenz`, `nis2-meldung`.
- Facade je Familie: `<familie>/` — mit Material darunter: `<familie>/_references/` (Karten, Index-README) und `<familie>/_build/` (Extraktion, Testkatalog). Nicht in der Wurzel.
- Suffixe kurz, klein, Bindestrich, ohne Umlaute (Loader- und Shell-sicher).

## Beschluss 3: Registry-Pflicht

Jeder neue Skill trägt sich an zwei Stellen ein, sonst existiert er nicht: Zeile in `INDEX.md` (Tabelle) + Eintrag in `FAMILIES.md` (genau eine Familie je Skill).

## Beschluss 4: Format-Standard je SKILL.md

- Frontmatter: `name`, `description` (Einsatz + „Verwenden bei …"), `keywords`, `not-for`, `updated`.
- Proxy-Block ab Zeile 1 des Bodys: Disclaimer, Fail-Closed (kein Anker keine Aussage; Unsicherheit aussprechen), Quellenzeile — Grenzen vor Fachwissen.
- Budgets: `SKILL.md` 40–80 Zeilen, Karte ≤25, Registry-Dateien ≤40. Zu groß → Inhalt nach `_references/`.

## Beschluss 5: Karten-Skelett (Template Method + Interpreter)

Feste Grammatik: `Kern / Pflichten / Ausnahmen / Fristen / Prüfung` — jede Aussage mit Artikel-/Absatzbezug, Imperative statt Prosa. Voll = alle Blöcke; kompakt = `Kern + Pflichten`.
## Beschluss 6: Kombinationsbudget (Decorator)

Maximal 3 Kontextschichten pro Anfrage (1 Fassade/Fach-Skill + bis zu 2 Karten bzw. 2 Skills). Erlaubte Skill-Kombis stehen in der Fassade; darüber hinaus: „Frage aufteilen."

## Checkliste: Neue Familie in 6 Schritten

1. Fassade `<familie>/SKILL.md` (Routing-Tabelle, Proxy-Block, Budget).
2. Fach-Skills `<familie>-<thema>/SKILL.md` (40–80 Zeilen, Karten-Auswahl mit Pfaden).
3. Material nach `<familie>/_references/` (Karten im Skelett, `README.md`-Index).
4. Registrieren: `INDEX.md` + `FAMILIES.md`.
5. Testkatalog + Runner nach `<familie>/_build/` ( analog `dsgvo/_build/`).
6. Stichproben gegen Primärquelle; Quelle im Proxy-Block jeder Karte.
