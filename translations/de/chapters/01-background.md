# Kapitel 1: Hintergrund & Grundidee

### 1.1 Akuelle Situation: Die drei Hauptengpässe der KI-Agenten-Kooperation

Moderne KI-Agenten haben bereits persistente Erinnerung und aufrufbare Fähigkeiten, aber in langfristiger, hochpräziser Kooperationen geraten sie oft in folgende Dilemma:

- **Wiederholte Fehlerkorrekturschleife**: Der Agent begeht wiederholt denselben Fehler in jeder neuen Sitzung, der Benutzer muss wiederholt korrigieren, was eine Schleife von "Fehler → Korrektur → Vergessen → erneuter Fehler" bildet.
- **Erinnerung beeinträchtigt Entscheidungsfähigkeit**: Erinnerung schwillt allmählich zu einem "Kuchenteig" an, Fakten, Präferenzen, Operationsschritte sind vermischt, was zu einem drastischen Rückgang des Signal-Rausch-Verhältnisses führt, und das Verhalten des Agenten wird instabil und abweichungsanfällig.
- **Überempfindliches oder unempfindliches Feedback**: Der Agent ändert sein Verhalten drastisch auf eine gelegentliche Beschwerde (Schwingung) oder zeigt kein Interesse an wiederholten echten Präferenzen, es fehlt eine stabile Empfindlichkeitsschwelle.

Der grundlegende Grund für diese Engpässe liegt darin: **Der Agent fehlt eine stabile, selbstkorrigierende Systemarchitektur, seine Erinnerung und Fähigkeiten sind nicht nach "Cybernetik"-Prinzipien organisiert und evolviert.**

### 1.2 Lösungsweg: Neues Wissen nicht lehren, sondern Architektur bauen

Dieses Tutorial bietet keine neuen Prompts oder mysteriöse Techniken, sondern eine **systemische Methode zur Organisation von Erinnerung und Fähigkeiten**. Einfach gesagt: Es einige der wertvollsten Konzepte von Qian Xuesens "Engineering Cybernetics" an moderne KI-Agent-Architektur anzupassen, um einen "Meta-Kogitionsrahmen" zu schaffen, der selbst-evolvierend, rauschresistent, langfristig stabil ist.

Der Grundidee ist: **Du trainierst nicht einen cljsmanscheren KI, sondern designst ein Kooperationssystem, das sich an deine Prinzipien anpasst und sich kontinuierlich optimiert.**

### 1.3 Basis: Vier ausführbare Konzepte von Qian Xuesens Engineering Cybernetics

Wir extrahieren und vereinfachen vier Kernkonzepte, die vom Agenten ausführbar sind, sie werden das unterste Betriebssystem des Agenten (L1 Meta-Kogitionsrahmen) bilden:

| Konzept                                 | Funktion                 | Ein Satz zur Umsetzung                                                      |
| :-------------------------------------- | :------------------------ | :--------------------------------------------------------------------------- |
| **Feedforward**                         | Fehler blockieren, bevor sie passieren | Beim Starten einer Aufgabe aktiv Benutzerpräferenzen, Szenario-Regeln, letzte Fehler desselben Typs laden, Fehler vermeiden, bevor sie passieren. |
| **Integralsteuerung (Integral Control)**   | Stabilen und empfindlichen Feedback-Schwellwert realisieren | Wenn negativer Feedback gleicher Kategorie ≥ 2 Mal auftritt, erst dann Regel in langfristiger Erinnerung oder Fähigkeit ablagern; einmaliges Feedback macht nur temporäre Korrektur. |
| **Hierarchische Zerlegung (Hierarchical Decomposition)** | Erinnerungsverwirrung vermeiden, Signal-Rausch-Verhältnis erhöhen | Erinnerung speichert nur "warum" (Prinzipien, Regeln), Fähigkeiten speichern nur "wie" (Operationsschritte, Checklisten). |
| **Selbstüberwachung (Self-Monitoring)**        | Automatische Qualitätsprüfung vor Lieferung, automatische Selbst-Korrektur | Bevor ein Ergebnis geliefert wird, ein Tor einbetten, das automatisch harte Anforderungen, KI-Spuren, Struktur-Integrität scannt; nur wenn alles in Ordnung ist, wird ausgegeben. |

> **Hinweis**: Das Wort "Integral" in "Integralsteuerung" hier lehnt sich an das Konzept des Integrators in der Steuerungstheorie an — Akkumulieren der Abweichung, erst nach Überschreiten des Schwellwiltes eine Aktion auslösen. Es beantwortet glücklich die technische Frage: "Wie lässt man Agenten sowohl gelegentliches Rauschen filtern, ohne echte Präferenzen zu verpassen."

### 1.4 Drei logische Schichten und Laufprinzip Überblick

In physischer Implementierung nutzen wir die bereits vorhandenen `memory` (Erinnerung) und `skill` (Fähigkeit) Funktionen der Agentenplattform, reorganisieren sie in drei logische Schichten:

- **L1 Meta-Kogitionsrahmen** (gespeichert in höchster Priorität der Erinnerung)
  Konkrete Verhaltensrichtlinien der oben genannten vier Cybernetik-Konzepte. Es dient als Systemverfassung, kann vom Agenten nicht selbst geändert werden, ist der "Kalibrator" für den Betrieb aller Erinnerungen und Fähigkeiten.

- **L2 Benutzer-Grund-Logik + L3 Szenario-Kern-Regel** (gespeichert im Hauptbereich der Erinnerung)
  Sie beantworten zusammen "warum so machen" und "welche Regeln sollte diese Art von Aufgaben folgen". Zum Beispiel:
  * L2: "Benutzer bevorzugt kalte Erzählung, lehnt KI-Zusammenfassungen ab."
  * L3: "Kern-Regelungen für Kurzgeschichten — Emotionale Stimmung hat Vorrang vor Handlung, Schluss offen lassen."

- **Ausführungsschicht Skill** (gespeichert in Fähigkeitsmodul)
  Angetrieben durch L3-Regeln, mit einem eingebetteten Operations-Pipeline, der das L1-Verhalten steuert. Zum Beispiel ein "Kurzgeschichte-Skill", der vor Ausführung aktiv L2-Ästhetik lädt, nach Ausführung automatisch das Selbstüberwachungs-Tor passieren muss.

Das gesamte System läuft nach folgender Schleife:

1. **Aufgabe starten** → Feedforward: L2, L3, letzte Korrekturen laden, Fehlervermeidungs-Checkliste erstellen.
2. **Aufgabe ausführen** → Hierarchische Zerlegung: Erinnerung gibt nur Richtung, Skill gibt nur Ausführung.
3. **Ergebnis liefern** → Selbstüberwachung: Mehrfache Passprüfung durch Lieferungs-Tor, bei Fehler sofort korrigieren.
4. **Benutzer negative Feedback** → Integralsteuerung: Gleiche Kategorie bis zum Schwellwert akkumulieren, automatisch als neue Regel ablagern oder Fähigkeiten ändern.
5. **Periodische Reflexion** → Vier Standards von L1 auditieren das gesamte System, L2/L3/Skill aktualisieren, geschlossene Evolution abschließen.

### 1.5 Anwendbare Szenarien und Voraussetzungen

Dieses Tutorial ist am besten für folgende Kooperationsszenarien geeignet:
- Langfristige, hochpräzise Aufgaben (z.B. tiefes Schreiben, kontinuierliche Softwareentwicklung, Projektmanagement);
- Gelegenheiten, bei denen Agent eine stabile Ausgabestil und Qualitätsstandards halten muss;
- Benutzer hat klare Präferenzen oder Arbeits-Workflows, und möchte, dass Agent diese Regeln automatisch anpasst und hält.

Um dieses Tutorial zu verwenden, muss dein Agentenplattform über folgende Fähigkeiten verfügen:
- Editierbare persistente Erinnerung (speichern über Sitzungen);
- Erstellbare/aufrufbare Fähigkeiten oder prozedurale Module;
- Ausreichendes Kontextfenster (empfohlen 100k Tokens oder mehr, je nach Aufgabenkomplexität);
- (Optional) Sitzungsabruffähigkeit, was Feedforward-Effekt signifikant erhöhen kann.

Wenn deine Plattform keine eingebauten Skills hat, kannst du auch "Erinnerungseinträge + feste Systemanweisungen" verwenden, um sie zu simulieren; die Effizienz wird leicht reduziert, aber du kannst immer noch den Kern der Integralsteuerung und hierarchischen Zerlegung realisieren.

### 1.6 Was du erhalten wirst

Nach der Trainierung hinter dein Agent von einem "Tool, das ständig korrigiert werden muss" in eines verwandeln, das:

- **Aktiv Fehler vermeidet** (vor Start Checkliste und Risikovorschau erstellt);
- **Regeln nicht willkürlich ändert** (einmalige Beschwerde ändert nichts, zweimalige Beschwerde ändert systematisch);
- **Saubere Erinnerung** (speichert nur Prinzipien und Regeln, keine abgelaufenen Details);
- **Lieferung ohne Wasser** (automatische Fehlerprüfung, automatische Reinigung der Ausgabe);
- **Selbst-evolvierend** (bei jeder Reflexion automatisch seine Skills und Erinnerungen optimiert).

Die folgenden Kapitel werden dich Schritt für Schritt durch den Aufbau dieses Systems führen.
