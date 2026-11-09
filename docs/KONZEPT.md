# Architektur-Konzept: Rechtswissen als lokale KI-Skills

Stand: 2026-11-09 · Status: umgesetzt und getestet (DSGVO, 99 Artikel) · Gilt für: alle künftigen Skill-Familien (EU AI Act, NIS-2, DSA …)

## 1. Ausgangslage: das Problem

Die Datenschutz-Grundverordnung als Wissensquelle: **88 Seiten, 99 Artikel, über 60.000 Tokens** Fließtext. Wer sie einem kleinen lokalen Sprachmodell (7B) „einfach als PDF übergibt", scheitert an vier harten Fakten:

1. **Das Fenster:** 60k+ Tokens passen nicht ins Kontextfenster eines 7B-Modells — der Volltext ist gar nicht ladbar.
2. **Die Genauigkeit:** Rechtstext ist halluzinationskritisch. Eine erfundene Paragrafen-Nummer ist bei Compliance-Fragen kein Makel, sondern ein Schaden (falsche Meldung, verpasste Frist, unzulässige Verarbeitung).
3. **Die Struktur:** Eine PDF hat kein Routing, keine Einstiege, keine Verhaltensregeln. Das Modell muss selbst raten, welche Artikel gemeint sind — aus 88 Seiten.
4. **Die Pflege:** Verarbeitung personenbezogener Daten in der Cloud erzeugt Auftragsverarbeitungspflichten. Lokale Verarbeitung ist datenschutzrechtlich der sauberste Weg — aber nur, wenn die Qualität trotzdem stimmt.

Merksatz: *Ein 7B-Modell ist ein starker Textarbeiter in einem kleinen Arbeitszimmer. Wer ihm ein Bibliotheksgebäude (PDF) auf den Tisch stellt, statt die drei richtigen Karteikarten, bekommt Bauchgefühl statt Antwort.*

## 2. Designziele (Leitplanken)

| # | Ziel | Konsequenz |
| :--- | :--- | :--- |
| 1 | **Prüfbarkeit** | Jede Aussage trägt Artikel-, Absatz- und Literatürbezeichnung (Art. N Abs. X lit. Y) |
| 2 | **Fail-Closed** | Keine Aussage ohne Anker; bei Unsicherheit wird Unsicherheit ausgesprochen, nie geraten |
| 3 | **Token-Budget** | Pro Anfrage ≈ 1,5–3k Tokens Kontext — Platz für Frage und Antwort bleibt |
| 4 | **Lokal & offline** | Keine Cloud, keine Kundendaten im Prompt — Verarbeitung ohne AVV-Kette |
| 5 | **Skalierbarkeit** | Gleiche Struktur für weitere Verordnungen (Familien), keine Sonderlösungen |
| 6 | **Eine Wahrheitsquelle** | Jeder Fakt einmal gepflegt (Flyweight), Änderungen ohne Doppelung |

## 3. Angewandte Strukturen (Patterns)

GoF-Muster, übertragen von Laufzeit- auf Wissensarchitektur. Maßstab war nicht elegante Kopplung, sondern: *Was kostet es an Tokens pro Anfrage, und hilft es dem kleinen Modell, korrekt zu antworten?*

| Pattern | Umsetzung | Gelöstes Problem |
| :--- | :--- | :--- |
| **Adapter** (Registry) | `FAMILIES.md` + Routing-Tabelle in der Fassade | Anliegen (Usersprache) → Skill-ID wird zur Nachschlagetabelle statt Modell-Intuition; Fehlselektion praktisch ausgeschlossen |
| **Facade** | `dsgvo/SKILL.md` (39 Zeilen) | Einstieg ohne 99 Artikel zu kennen; verhindert Fehlstarts |
| **Proxy** (Schutzschicht) | Zeilen 1–5 jeder Skill-Datei und -Karte: Disclaimer, Fail-Closed, Quelle | Das Modell liest seine Grenzen, bevor es Fachwissen sieht — Halluzinationsabwehr im Kontext selbst |
| **Strategy** | 8 Fach-Skills à 36–47 Zeilen | Nur die für die Frage nötige Strategie wird geladen; klein, austauschbar, einzeln testbar |
| **Decorator** | `ai --skill a --skill b`, Budget ≤3 | Kontexte schichtbar (Mechanik existierte bereits); das Budget verhindert, dass ab ~4 Schichten das Modell Prioritäten verwässert |
| **Flyweight** | `FACTS.md` (Art.-4-Begriffe) + geteilte Karten (z. B. Art. 32 in drei Skills) | Keine doppelte Pflege, garantiert konsistente Antworten, kleineres Gesamtvolumen |
| **Template Method** | Festes Karten-Skelett | Ein Format, einmal gelernt: das Modell liest komprimiert, Befolgungsquote steigt |
| **Interpreter** | Mikro-Grammatik: `Kern / Pflichten / Ausnahmen / Fristen / Prüfung` in Imperativen mit Anker | Gesetzesfließtext wird ausführbare Checkliste statt Interpretationsaufgabe |
| **State** | `dsgvo-datenpannen` als 3-Zustands-Automat | „Vorfall erkannt → 72h-Meldefrist läuft → dokumentiert abgeschlossen": Fristen und Übergänge als kleiner Regelsatz, der im Ernstfall nicht verloren geht |

**Verworfen, mit Grund:** Composite und Chain of Responsibility (Token-O(n) pro Anfrage — im kleinen Fenster ruinös); Bridge, Visitor, Memento, Observer (kein Anker in statischem Wissen — ihre Substanz lebt besser in Template Method, Interpreter und der Versionsregel).

## 4. Die Lösung im Detail

**Dreistufiger Zugriff (2-Ebenen-Modell plus Registry):**

```
Anfrage
  → 1. Fassade (Routing-Tabelle, Disclaimer, Kombinationsbudget)
  → 2. Fach-Skill (Kernregeln mit Ankern, Karten-Auswahl, Prüf-Block)
  → 3. Artikel-Karte (≤25 Zeilen, Festformat, für Tiefe gezielt nachgeladen)
```

**Effizienzrechnung pro typischer Anfrage:**

```
Routing (~40 Z.) + 1–2 Skills (≤80 Z.) + 0–2 Karten (≤50 Z.)
≈ 120–170 Zeilen ≈ 1,5–3k Tokens   —  vs.  Volltext ≈ 60k+ Tokens (nicht ladbar)
```

**Fail-Closed-Block (steht an erster Stelle jeder Datei):** *Kein Ersatz für Rechtsberatung. Keine Aussage ohne Artikelbezug. Bei Unsicherheit: Unsicherheit aussprechen, nichts erfinden.*

**Qualitätssicherung in der Pipeline:** Die Extraktion aus dem Amtsblatt fand reale Fehler und reparierte sie reproduzierbar: neun umgebrochene Artikeltitel, vier Fußnoten-Einschübe, drei versehentlich verworfene Textzeilen (Seiten-Furniture-Filter) und einen Glyphfehler der Druckvorlage (Art. 15 Abs. 4: „Absatz 1b" statt „Absatz 3"). Eine rohe PDF-Übergabe hätte diese Fehler 1:1 in Antworten übertragen.

**Multi-Familien-Verwaltung:** `KONVENTIONEN.md` legt verbindlich fest: flache Auflösung (keine Ordnerbäume — die Katalog-Discovery scannt flach), Familien-Prefix `<familie>-<thema>`, Material unter der Fassade (`<familie>/_references/`), Registry-Pflicht, Budgets. Ein Repo = eine Familie; die globale Registry in `~/.agents/skills` ist die operative Summe.

## 5. Was das konkret löst — Belege aus dem Testkatalog

- **Mit Karte geladen:** Antworten sauber geankert. Beispiele aus Live-Tests: Löschfrage → Art. 17 Abs. 1 lit. a–f mit Ausnahmen Abs. 3; Datenpanne → 72h (Art. 33 Abs. 1) mit Meldeinhalt lit. a–d; AVV → Art. 28 Abs. 3 lit. a–h.
- **Halluzinations-Falle:** „Zitiere Art. 33 Abs. 7" (existiert nicht) wurde **nicht** erfunden — das Modell verweigerte das Zitat statt ein Fiktat zu liefern. Der Proxy-Block funktioniert.
- **Ehrliche Schwäche:** Skill-only-Abwägungsfragen (Einwilligung vs. berechtigtes Interesse) bleiben auf dem 7B-Modell dünn — zwei Skill-Iterationen konnten einen Parametrier-Bias des Modells nicht vollständig neutralisieren. Konsequenz: Für solche Fälle ist die Pflicht-Karte hinterlegt (`artikel-06.md`). Das Verfahren „Skill + Karte" ist der verlässliche Pfad; der Katalog dokumentiert beides.
- **Regel:** Fehler werden an Karte oder Skill adressiert, nie durch „Biegen" der Regel im Gesetz.

## 6. Warum diese Architektur — aktuell und künftig dringend

### Warum jetzt

1. **Regulierungsflut:** DSGVO, EU AI Act, NIS-2, DSA, Data Act, CRA — jede Verordnung bringt hunderte Artikel. Compliance-Wissen wächst schneller als jede Personaldecke. Drei reale Treiber: 72-Stunden-Meldefristen unter Ransomware-Druck (BSI 2025: 950 Angriffe, 72 % mit Datenleak), Cookie-Banner als Abmahn-Kostenfalle (BGH I ZR 186/17, 27.3.2025), Beschwerde-Flut (BfDI 2025: +36 %).
2. **Lokal-KI-Boom:** 7B-Modelle laufen auf jedem Rechner — aber „dumm im Kontext". Der Engpass ist nicht Modellqualität, sondern **Wissensarchitektur**. Dieses Konzept ist genau der Hebel: kleines Modell + gute Struktur schlägt großes Modell + schlechte Struktur bei Regelwerksfragen.
3. **Recht folgt Architektur:** Lokale Verarbeitung entfernt Cloud-AVV-Ketten; gleichzeitig verlangt das Gesetz Präzision (Artikelbezug, Fristen). Die Struktur erfüllt beides gleichzeitig.

### Warum künftig

4. **Modell-Immunität:** Das Wissen liegt in Dateien, nicht im Modell. Das Modell ist austauschbar — heute 7B, morgen 14B — ohne Retraining, ohne Verlust. Bessere Modelle machen die Struktur wertvoller, nicht überflüssig: Sie nutzen den gleichen kleinen, geankerten Kontext nur noch besser.
5. **Änderungsmanagement:** Neue VO-Version, neue Rechtsprechung = Diff auf wenige Karten, nicht Neuauflage. Die Wahrheitsquelle pro Fakt (Flyweight) garantiert, dass eine Korrektur überall wirkt.
6. **Agenten-Ökosysteme:** Mehrere Werkzeuge (lokale Modelle, Coding-Agenten, Assistenten) teilen denselben Wissens-Container. Die Skills sind werkzeugneutral — ein Standard-Format für reguliertes Wissen.
7. **Determinismus schlägt Ähnlichkeit:** Vektorsuche/RAG liefert plausible Ausschnitte mit Wahrscheinlichkeit; Regelwerke verlangen jedoch *vollständige, geankerte* Antworten. Feste Routing-Tabellen und Skelette geben dem kleinen Modell das richtige, nicht das ähnlichste Material — der entscheidende Unterschied bei Fristen und Bußgeld-Tabellen.

## 7. Grenzen (ehrliche Einordnung)

- Kein Ersatz für Rechtsberatung; die Struktur sichert Anker und Unsicherheit, nicht die Auslegung im Einzelfall.
- Modell-Bias bleibt ein Restrisiko (Beispiel: veralteter Kenntnisstand zu Angemessenheitsbeschlüssen — deshalb die „Stand prüfen"-Regel in der Fassade).
- Skill-only ist bei Abwägungsfragen schwächer als Skill + Karte — das Budget ist bewusst Disziplin, nicht Komfort.
- Die genutzte PDF-Fassung enthielt die Anhänge I/II nicht; das ist im Karten-Index vermerkt (Fail-Closed statt Auffüllen).

## Verweise

- `KONVENTIONEN.md` — verbindlicher Architektur-Standard (Beschlüsse 1–6, Checkliste)
- `INDEX.md` / `FAMILIES.md` / `FACTS.md` — Registry (Adapter/Factory/Flyweight)
- `dsgvo/SKILL.md` — Fassade; `dsgvo/_references/README.md` — Karten-Index
- Testkatalog und Runner liegen in der Arbeitskopie unter `~/.agents/skills/dsgvo/_build/` (bewusst nicht im Distributions-Repo)
