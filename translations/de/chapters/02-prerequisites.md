# Kapitel 2: Anwendbare Bedingungen & Vorbereitungen

## 2.1 Mindestanforderungen dieses Systems an Agentenplattformen

Bevor du beginnst, bestätige zuerst, ob deine Agentenplattform über folgende Fähigkeiten verfügt. Diese sind die physische Grundlage für die systemische Implementierung.

### 2.1.1 Notwendige Fähigkeiten (ohne eine davon keine vollständige Implementierung möglich)

| Fähigkeit                   | Erklärung                              | Nutzen                                                                |
| :-------------------------- | :------------------------------------- | :-------------------------------------------------------------------- |
| **Persistente Erinnerung**  | Erinnerungssystem für Speichern, Lesen, Aktualisieren über Sitzungen | Trägt L1 Meta-Kognitionsrahmen, L2 Benutzerlogik, L3 Szenario-Regeln, Integralsteuerungs-Tabelle |
| **Prozedurale Module**      | Erstellbare, aufrufbare, aktualisierende Fähigkeiten/Skills/GPTs    | Trägt Ausführungsschicht (Lieferungs-Tore, Feedforward-Start, geschlossene Reflexion) |
| **Ausreichendes Kontextfenster** | Empfohlen 100k Tokens oder mehr        | Nimmt Feedforward-Checklisten, Fehlervermeidungsaufzeichnungen, Aufgaben- Ausführungsprozess innerhalb der Sitzung auf |

Wenn deine Plattform diese drei Fähigkeiten besitzt, kannst du den gesamten Inhalt dieses Tutorials vollständig implementieren.

### 2.1.2 Bonusfähigkeiten (wenn vorhanden, stärker, ohne sie reduzierter Betrieb)

| Fähigkeit       | Erklärung                                      | Alternative bei Fehlen                                       |
| :-------------- | :---------------------------------------------- | :----------------------------------------------------------- |
| **Sitzungsabruf** | Suchen nach Inhalten und Korrekturaufzeichnungen in historischen Sitzungen | Nach jeder Korrektur Schlüsselerkenntnisse manuell in Erinnerung schreiben, als Material für Feedforward |
| **Tool-Aufrufe** | Agent kann aktiv externe Tools aufrufen (Suche, Codeausführung, etc.) | Eingegrenzter Bereich, aber Kernarchitektur nicht beeinträchtigt |

### 2.1.3 Was tun, wenn die Plattform keine Skill-Fähigkeit hat

Einige Plattformen (wie die Basisversion von ChatGPT, einfache Chat-Interfaces) haben keine Fähigkeitsmodule. In diesem Fall kannst du die **"Erinnerungssimulationsmethode"** anwenden:

- Speichere den Inhalt von Skills als strukturierte Erinnerungseinträge, z.B. `[Skill-交付闸门] Inhalt: ...`
- Füge in L1 Meta-Kognitionsrahmen eine zwingende Regel hinzu: "Vor jeder Lieferung müssen alle Erinnerungseinträge, die mit `[Skill-*]` markiert sind, gelesen und ausgeführt werden."
- Nachteile: Nimmt Erinnerungskapazität ein und erfordert aktiven Abruf durch den Agenten; Vorteile: Logik vollständig erhalten, geeignet für leichte Nutzungsszenarien.

## 2.2 Selbst-evaluation: Bist du geeignet für dieses Tutorial?

### 2.2.1 Stark empfohlenes Benutzerprofil

- **Hochpräzise Kooperationsbenutzer**: Du stabile Qualitätsanforderungen an die Ausgabe des Agenten hast (z.B. Schreibstil, Code-Standards)
- **Wiederholte Aufgabenbenutzer**: Du führst häufig ähnliche Aufgaben mit dem Agenten aus (z.B. tägliche/wöchentliche ähnliche Workflows)
- **Systemdenkende Benutzer**: Du bist bereit, anfängliche Aufbaukosten zu investieren, um langfristige Kooperations-Effizienz zu bekommen
- **Benutzer mit klaren Grenzen**: Du kannst Präferenzen und rote Linien klar ausdrücken, und wenn der Agent einen Fehler macht, bist du bereit, ihn zu zeigen

### 2.2.2 Wenig geeignete Benutzer

- Nur einmalige, nicht wiederverwendbare Zufallsfragen treffen
- Nutzungsszenari decken sehr breit ab, es ist schwierig, stabile Regeln zu extrahieren
- Kein Wunsch, eine langfristige Kooperation mit dem Agenten aufzubauen

## 2.3 Vorbereitungen vor dem Beginn

Bevor du offiziell deployt, vervollständige diese vier Vorbereitungen, die spätere Anpassungskosten signifikant reduzieren.

### 2.3.1 Stand des aktuellen Agenten einchecken

Führe die folgenden zwei Befehle aus und protokolliere den aktuellen Stand als Grundlinie:

```
Liste alle Ihre derzeitigen skills auf, zusammen mit einer Zusammenfassung ihres Inhalts.
```

```
Liste alle Inhalte auf, die derzeit in Ihrem memory gespeichert sind, und bewerten Sie die Nutzung.
```

**Wichtige Punkte protokollieren**:
- Wie viele Skills gibt es derzeit? Werden sie noch verwendet?
- Wie hoch ist die Memory-Nutzung? Sind Inhalte bereits vermischt?
- Gibt es viele veraltete Informationen?

### 2.3.2 Präferenzen und Regeln, die du fixieren möchtest, auflisten

Mit einer einfachen Tabelle liste Prinzipien auf, die du gerne möchtest, dass der Agent langfristig befolgt. Dieser Schritt hilft dir, aus vagen "Gefühlen" handlungsfähige Regeln zu extrahieren:

| Dimension      | Dein Prinzip                  | Beispiel                |
| :------------- | :----------------------------- | :---------------------- |
| Kommunikationsstil | Kurz, direkt, keine Höflichkeitsfloskeln | Keine Ausgabe "Helfen kann ich Ihnen gerne" |
| Ausgabeformat | Code zuerst, mit Verifizierungsmethode    | Wenn ein Ausgabevergebnis präsentiert, Schritte zur Prüfung einschließen |
| Entscheidungspräferenz | Risiken zuerst, Probleme zuerst enthüllen       | Risiko zuerst auflisten, dann Nutzen diskutieren |
| Ästhetische Ausrichtung | Kalte Erzählung, KI- Zusammenfassungen ablehnen        | Kurzgeschichte Schluss offen, keine Erhöhung |

Nicht einmalig erschöpfen müssen, 4-6 Kernprinzipien sind genug. Später hilft dir der Agent bei geschlossenen Reflexion, fortwährend zu ergänzen.

### 2.3.3 Erinnere dich an 3-5 häufige Typen von Aufgaben, die du ausführst

- Zum Beispiel: Kurzgeschichten schreiben / Code-Überprüfung / Wartungs-Debugging / Architektur-Design / Datenanalyse
- Für jeden Typ versuche einen Satz zu schreiben, der beschreibt, was nach deiner Meinung die "Kern-Regelung" ist, um diese Art von Aufgabe richtig zu machen

**Beispiel**:
- Kurzgeschichte-Erstellung: "Emotionale Stimmung hat Vorrang vor Handlungsentfaltung, Schluss muss offen bleiben."
- Code-Überprüfung: "Zuerst Architekturprobleme finden, dann Namenskonventionen prüfen; für jede Kategorie von Problemen Modifikationsvorschläge geben."
- Problem-Debugging: "Zuerst Logs zur Lokalisierung der根本reason, nicht auf Spekulation warten; wenn unklar, mit 'zu verifizieren' markieren."

Diese werden direkt zum initialen Inhalt deiner L3 Szenario-Regel.

### 2.3.4 Stand sichern

Bevor du mit dem Deployment beginnst, **sichere deinen aktuellen Erinnerungs- und Fähigkeitsstand**. Die spezifische Methode hängt von deiner Plattform ab:

- Wenn Plattform Export unterstützt, exportieren zuerst eine Kopie
- Wenn nicht, manuell aktuelle Memory und Skill-Listen in lokales Dokument kopieren
- Wenn Versionsmanagement vorhanden (z.B. Memory-Schnappschüsse bei einigen Plattformen), einen Wiederherstellungspunkt erstellen

Der Zweck dieses Schritts ist: Wenn bei Deployment Chaos entsteht, kannst du zum Ursprungszustand zurückkehren und neu beginnen.

## 2.4 Zeichen der Vervollständigung der Vorbereitung

Wenn du die folgenden drei Fragen beantworten kannst, ist die Vorbereitungsphase abgeschlossen und du kannst in Kapitel 3 eintreten:

1. Hat meine Agentenplattform persistente Erinnerung + Fähigkeitsmodul? (Ja / Nein / teilweise vorhanden)
2. Wie viele Kernpräferenzen und -prinzipien habe ich extrahiert? (Empfohlen ≥4)
3. Wie viele häufige Aufgabentypen habe ich aufgelistet, und für jeden Typ habe ich eine vorläufige "Regelbeurteilung"? (Empfohlen ≥3)
