# Skill-Familien (Factory-Registry)

Jeder Skill in diesem Repo liegt in **genau einer** Familie. Der Agent wählt die Familie (Strategy), die Registry liefert den Skill-Satz.

| Skill | Familie | Kurzzweck |
| :--- | :--- | :--- |
| `dsgvo` | DSGVO-Wissen | Wegweiser: Anliegen → Fach-Skill/Karte |
| `dsgvo-grundsaetze` | DSGVO-Wissen | Grundsätze, Verantwortung, Design, DSFA |
| `dsgvo-einwilligung` | DSGVO-Wissen | Rechtsgrundlagen, Einwilligung, Profiling |
| `dsgvo-betroffenenrechte` | DSGVO-Wissen | Rechte, Fristen, Rechtsbehelfe |
| `dsgvo-auftragsverarbeitung` | DSGVO-Wissen | AVV, Subprozessoren, Gemeinsame |
| `dsgvo-verzeichnisse` | DSGVO-Wissen | Verzeichnis der Verarbeitungstätigkeiten |
| `dsgvo-sicherheit-tom` | DSGVO-Wissen | TOM, Sicherheit, DSB |
| `dsgvo-datenpannen` | DSGVO-Wissen | Meldung, Benachrichtigung, Dokumentation |
| `dsgvo-drittländer` | DSGVO-Wissen | Drittlandübermittlungen, SCC/BCR |

Routing-Regel: Das Anliegen bestimmt die Familie; innerhalb von DSGVO-Wissen entscheidet der Wegweiser (`dsgvo`) über den Fach-Skill. Geteilte Begriffe in `FACTS.md`, Kombinationsbudget im Wegweiser.

Konvention für künftige Familien (Naming, Material, Registry-Pflicht): `KONVENTIONEN.md`. Neue Fach-Skills bekommen den Familien-Prefix `<familie>-<thema>`.
