---
name: dsgvo-datenpannen
description: "Datenpannen (Verletzungen des Schutzes personenbezogener Daten) nach DSGVO: Meldung an die Aufsichtsbehörde binnen 72 Stunden (Art. 33), Benachrichtigung der betroffenen Person bei hohem Risiko (Art. 34), Inhalte, Ausnahmen, Dokumentationspflicht — als 3-Zustands-Automat. Verwenden bei Sicherheitsvorfällen, Leaks und Meldefristen."
keywords: [dsgvo, datenpanne, breach, art. 33, art. 34, 72 stunden, meldung, benachrichtigung, sicherheitsvorfall, leak, dokumentation]
not-for: [präventive tom-gestaltung, betroffenenrechte außerhalb von pannen]
updated: "2026-11-09"
---

# DSGVO: Datenpannen — Meldung & Benachrichtigung (Zustands-Automat)

**Grenzen (Proxy):** Kein Ersatz für Rechtsberatung. Keine Aussage ohne Artikelbezug. Bei Unsicherheit aussprechen — bei Pannen gilt: lieber melden als schweigen. Original: VO (EU) 2016/679, 27.04.2016.

## Zustände und Übergänge (State)

1. **Vorfall erkannt** → sofort beurteilen: Risiko für Rechte und Freiheiten? Dokumentation beginnen (Art. 33 Abs. 5).
2. **Meldung läuft (72h)** → an die nach Art. 51 zuständige Aufsichtsbehörde, unverzüglich und möglichst binnen 72 Stunden nach Bekanntwerden; spätere Meldung nur mit Begründung (Art. 33 Abs. 1). Auftragsverarbeiter meldet unverzüglich dem Verantwortlichen (Art. 33 Abs. 2).
3. **Abgeschlossen/dokumentiert** → Benachrichtigung der Betroffenen geprüft und ggf. versendet; Panne vollständig dokumentiert; Aufsichtsbehörde hat Zugriff auf die Dokumentation.

## Kernregeln

- Meldung an die Behörde entfällt nur, wenn die Panne voraussichtlich zu keinem Risiko führt (Art. 33 Abs. 1).
- Melde-Inhalt (Art. 33 Abs. 3 lit. a–d): Art der Verletzung mit Kategorien und ungefährer Zahl betroffener Personen und Datensätze (lit. a); Kontakt DSB/Anlaufstelle (lit. b); wahrscheinliche Folgen (lit. c); ergriffene/vorgeschlagene Maßnahmen zur Behebung und Abmilderung (lit. d). Nicht sofort verfügbar → schrittweise ohne unangemessene Verzögerung (Art. 33 Abs. 4).
- Benachrichtigung der betroffenen Person (Art. 34 Abs. 1–2): unverzüglich bei voraussichtlich hohem Risiko, in klarer und einfacher Sprache, mit den Angaben nach Art. 33 Abs. 3 lit. b–d.
- Keine Benachrichtigung bei: TOM haben Daten für Unbefugte unzugänglich gemacht, etwa Verschlüsselung (lit. a); Folgemaßnahmen haben das hohe Risiko beseitigt (lit. b); unverhältnismäßiger Aufwand → dann öffentliche Bekanntmachung (lit. c) (Art. 34 Abs. 3).
- Die Aufsichtsbehörde kann die Nachholung der Benachrichtigung verlangen oder Ausnahmen feststellen (Art. 34 Abs. 4).
- Jede Panne dokumentieren: Fakten, Auswirkungen, Abhilfemaßnahmen — Überprüfung durch die Behörde muss möglich sein (Art. 33 Abs. 5).

## Karten-Auswahl (Tiefe nachladen)

- Meldung an die Behörde, 72h, Inhalte, Dokumentation → `dsgvo/_references/artikel-33.md`
- Benachrichtigung Betroffener, Ausnahmen → `artikel-34.md`
- Wirksamkeit der TOM prüfen (Verschlüsselung etc.) → `artikel-32.md` (via `dsgvo-sicherheit-tom`)
- Behördenzusammenarbeit während des Vorfalls → `artikel-31.md`

## Prüfung (pro Vorfall)

- Prüfe: Risiko vorhanden → Meldungspflicht (Art. 33 Abs. 1)?
- Prüfe: 72 Stunden ab Bekanntwerden — Frist dokumentiert?
- Prüfe: Meldung vollständig nach lit. a–d, Lücken schrittweise nachgeliefert?
- Prüfe: Hohes Risiko → Benachrichtigung der Betroffenen oder Ausnahme lit. a–c belegt (Art. 34)?
- Prüfe: Vollständige Dokumentation mit Fakten, Auswirkungen, Maßnahmen (Art. 33 Abs. 5)?

## Kombinationen

- Mit `dsgvo-sicherheit-tom` (TOM-Bewertung: Verschlüsselung als Ausnahmegrund, Art. 34 Abs. 3 lit. a).
- Mit `dsgvo-auftragsverarbeitung` bei Vorfällen beim Auftragsverarbeiter (Meldung an den Verantwortlichen, Art. 33 Abs. 2).
- Mit Bußgeld-Karten `artikel-82.md`/`artikel-83.md` bei der Bewertung von Folgen.
