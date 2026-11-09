---
name: dsgvo-grundsaetze
description: "Verarbeitungsgrundsätze der DSGVO: Rechtmäßigkeit, Zweckbindung, Datenminimierung, Richtigkeit, Speicherbegrenzung, Integrität/Vertraulichkeit (Art. 5), Verantwortung und Rechenschaftspflicht (Art. 24), Datenschutz durch Technikgestaltung und datenschutzfreundliche Voreinstellungen (Art. 25), DSFA (Art. 35/36), Verhaltensregeln und Zertifizierung (Art. 40–43). Verwenden bei Prinzipien- und Konformitätsfragen."
keywords: [dsgvo, grundsätze, art. 5, zweckbindung, datenminimierung, privacy by design, art. 25, dsfa, folgenabschätzung, art. 35, rechenschaftspflicht, verhaltensregeln, zertifizierung]
not-for: [einwilligungsbedingungen im detail, betroffenenrechte im einzelnen]
updated: "2026-11-09"
---

# DSGVO-Grundsätze, Verantwortung & Nachweis

**Grenzen (Proxy):** Kein Ersatz für Rechtsberatung. Keine Aussage ohne Artikelbezug (Art. N Abs. X lit. Y). Bei Unsicherheit: Unsicherheit aussprechen. Original: VO (EU) 2016/679, 27.04.2016. Begriffe: `FACTS.md`.

## Kernregeln

- Verarbeite personenbezogene Daten nur nach den Grundsätzen des Art. 5 Abs. 1 lit. a–f: rechtmäßig/fair/transparent; zweckgebunden; datenminimal; richtig; speicherbegrenzt; integer und vertraulich. Der Verantwortliche weist die Einhaltung nach (Rechenschaftspflicht, Art. 5 Abs. 2).
- Rechtsgrundlage vor jeder Verarbeitung festlegen (Art. 6) — Details im Skill `dsgvo-einwilligung`.
- Implementiere TOM, die Konformität sicherstellen und deren Nachweis erbringen — risikobasiert, regelmäßig überprüft (Art. 24 Abs. 1).
- Berücksichtige Datenschutz bereits bei der Mittelwahl (Privacy by Design, Art. 25 Abs. 1) und stelle datenschutzfreundliche Voreinstellungen sicher: nur nötige Datenmenge, Umfang, Speicherfrist und Zugänglichkeit (Art. 25 Abs. 2).
- Führe vorab eine DSFA durch, wenn Art, Umfang, Umstände und Zwecke ein hohes Risiko begründen — insbesondere Profiling mit Rechtswirkung, umfangreiche Art.-9-/Art.-10-Daten, systematische flächendeckende Überwachung (Art. 35 Abs. 1, 3); DSFA-Inhalt: Art. 35 Abs. 7 lit. a–d; DSB-Rat einholen (Art. 35 Abs. 2); fortlaufend überprüfen (Art. 35 Abs. 11).
- Liegt das hohe Risiko trotz DSFA vor und wird nicht eingedämmt: vorherige Konsultation der Aufsichtsbehörde (Art. 36 Abs. 1) — Fristen: Empfehlung bis zu acht Wochen, Verlängerung um sechs Wochen (Art. 36 Abs. 2).
- Nutze Verhaltensregeln (Art. 40) und Zertifizierung (Art. 42, drei Jahre) als Nachweis geeigneter Garantien — Überwachung durch akkreditierte Stellen (Art. 41, 43).

## Karten-Auswahl (Tiefe nachladen)

- Grundsätze einzeln prüfen → `dsgvo/_references/artikel-05.md`
- TOM-Verantwortung, Nachweis → `artikel-24.md`
- Privacy by Design / Voreinstellungen → `artikel-25.md`
- DSFA Pflichtfälle und Inhalt → `artikel-35.md`
- Vorherige Konsultation → `artikel-36.md`
- Verhaltensregeln → `artikel-40.md`; Überwachungsstelle → `artikel-41.md`
- Zertifizierung → `artikel-42.md`; Zertifizierungsstellen → `artikel-43.md`

## Prüfung

- Prüfe: Ist für die Verarbeitung eine Rechtsgrundlage benannt und dokumentiert?
- Prüfe jede Verarbeitung gegen Art. 5 Abs. 1 lit. a–f und die Nachweisführung gegen Art. 5 Abs. 2.
- Prüfe: Liegt ein Art.-35-Abs.-3-Fall vor oder ein hohes Risiko? Dann DSFA vorab, DSB beteiligt.
- Prüfe Voreinstellungen: Werden ohne Eingreifen des Nutzers nur nötige Daten verarbeitet (Art. 25 Abs. 2)?

## Kombinationen

- Mit `dsgvo-einwilligung` bei Rechtsgrundlagen-Fragen (Budget beachten: ≤3 Schichten).
- Mit Karten `artikel-06.md`/`artikel-32.md` bei Abwägung Rechtmäßigkeit vs. Sicherheit.
