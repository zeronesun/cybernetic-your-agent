
2. Wenn kumuliert ≥ Threshold (standardmäßig 2 Mal), und noch nicht abgesunken, führt Agent automatisch das Absinken aus:
   - Diese Regel wird in das entsprechende L2, L3 oder Skill geschrieben.
   - Der Status "Ist-abgesunken" aktualisiert.
   - Bestätige bei dir: "'Schluss-KI-Zusammenfassung' ist jetzt 2 Mal aufgetreten, ich habe es in L2 Ästhetische Prinzipien gesunken, ist das OK?".
3. Wenn kumultiert = 1, mache nur diese Korrektur, ändere keine langfristige Regel.

**Warum-Threshold auf 2**:
- 1 Mal ist Rauschen: Vielleicht nur, weil du schlechte Laune hast, oder eine bestimmte Szene nicht passt.
- 2 Mal ist Signal: Kontinuierliche gleichartige Feedback zweimal zeigen, das ist wahrscheinlich deine stabile Präferenz.
- Du kannst es nach deinem Stil auf 3 anpassen, aber ich empfehle, von 2 zu starten.

### 3.2.4 Wie man überprüft, ob es bereits wirkt

- Du gibst absichtlich Feedbacksgleicher Typ zweimal (z.B. sagst zweimal "Schluss zu langwierig"), beobachte ob Agent nach dem zweiten Mal aktiv vorschlägt, die langfristige Regel zu ändern.
- Du gibst ein zufälliges Feedback (sagst ein Mal "ich mag diese Metapher nicht"), beobachte ob Agent因此而 nicht den gesamten Stil ändert.

**Integralsteuerung-Ziel ist nicht, Agent "sturhaft" zu machen, sondern ihm stabile Präferenz-Erfassungsfähigkeit zu geben — das, was gehört werden sollte, nicht漏 das, was ignoriert werden sollte, nicht übermäßig.**

---

## 3.3 Hierarchische Zerlegung — Strategie und Ausführung werden彻底 getrennt

### 3.3.1 Prinzip-Erklärung

Eines der Kernelemente von Qian Xuesens System-Denken ist **Hierarchische Steuerung**. Ein komplexes System muss in verschiedene Schichten zerlegt werden: obere Schicht legt Strategie, Ziel, Zwang fest; untere Schicht macht Ausführung, Anpassung, Feedback. Zwischen Ober- und Unterschicht werden Informationen nur über klare Schnittstellen übertragen, die interne Implementierung ist gegenseitig unsichtbar.

Wenn diese Trennung gebrochen wird — obere Schicht beginnt, Ausführungsdetails zu kontrollieren, untere Schicht Strategie selbst zu bestimmen — System gerät in Chaos: Ändert man一处, das全局 schwingt, ändert man一处,全局震荡.

### 3.3.2 Warum KI-Agent hierarchische Zerlegung braucht

Erinnerung und Fähigkeiten des Agenten sind natürlich容易陷入 folgende几种混淆:

- **Erinnerungsschwellen**: 用户的原则（"hasst AI-Schluss"）und konkrete Ausführungsschritte（"nach dem Schreiben nach '总而言之' suchen und löschen"）sind vermischt. Erinnerung speichert sowohl "warum" als auch "wie", Volumen EXPLODIERT, Abruf Schwierigkeiten.
- **Fähigkeitssteifigkeit**: Fähigkeiten ist hartcodiertet mit einer Präferenz aus einem Gespräch, aber diese Präferenz könnte temporär sein. Nächstes Mal, wenn man es verwendet, ist die Fähigkeit bereits veraltet, und du weißt nicht, warum es so macht.
- **Änderungskosten hoch**: Um einen Ausgabestil zu ändern, musst du einzeiligen Suchen in dicht gepackter Erinnerung und Fähigkeiten, nicht wissend, welches das Prinzip ist, das ändern sollte, welches das historische Protein ist, das irrelevant ist.

Hierarchische Zerlegung 设置一个不可逾越的边界: **Prinzipien in Erinnerung, Schritte in Fähigkeiten.**

### 3.3.3 Implementations-Design im Agent

Die Kernregel ist nur eine:

> **Erinnerung speichert nur "warum" und "welche Regel", Fähigkeiten speichern nur "wie zu machen".**

Spezifisch表现为:

| Informationstyp                     | Zuweisung      | Beispiel                             |
| :---------------------------------- | :-------------- | :----------------------------------- |
| Ästhetische Tendenz（hasst AI-Schluss） | Erinnerung L2   | Benutzer prefers kalte Erzählung, lehntusammenfassende Schluss ab |
| Aufgaben-Regel（Kurzgeschichte首先定调）   | Erinnerung L3   | Kurzgeschichte-Erstellung Kernregel: Emotionale Stimmung zuerst |
| Ausführungsschritte（nach Schreiben通过闸门检查） | Fähigkeiten     | delivery_gate 五关检查清单       |
| Ein spezifisches Korrektureintrag   | Archiv/Abruf   | 2025-05-10 Benutzer sagt Schluss zu langwierig        |

**Forcierte Regel in Ausführung**:
- Jedes Mal bei geschlossener Reflexion muss Agent aktiv scannen:
  - In Erinnerung gibt es Ausführungsschritte? Wenn ja,则在技能之间转移。
  - In Fähigkeiten gibt es Prinzip-Inhalt? Wenn ja,则在记忆之间转移.
- Jedes Mal bei Speichern neuer Erinnerung muss Agent zuerst beurteilen, zu welcher Kategorie Informationen gehört, dann Speicherort bestimmen.

### 3.3.4 Wie man überprüft, ob es bereits wirkt

- Du öffnest Erinnerung des Agenten,发现 sie ist klare Partitionierung: Prinzipien, Regeln, Szenario-Abbild — keine vermischte Schritte.
- Du öffnest Fähigkeiten des Agenten,发现 sie hat nur Checklisten "was tun, was prüfen", keine Erklärungen "weil Benutzer etwas mag, deshalb so tun".
- Wenn du eine ästhetische Regel änderst（z.B. "jetzt kann gelegentlich metaphorisches Vokabular verwendet werden"）, musst du nur一条 Erinnerung ändern, braucht nicht irgendwelche Fähigkeiten zu berühren.

**Hierarchische Zerlegungs-Ziel ist, Erinnerung von "Kuchenteig" zu "Datenbank" zu machen, 让 jede Information eine einzige Zuweisung und bestimmte Änderungspfad hat.**

---

## 3.4 Selbstüberwachung — Vor der Lieferung, zuerst durch eigenes Tor

### 3.4.1 Prinzip-Erklärung

Jedes Steuermuss 最后必需有一个 **Feedback回路** 闭合。在工程系统里，这意味着: System misst seine eigener Ausgabe, vergleicht mit erwartetem Wert, erzeugt Fehler-Signal zu korrigieren. Für Agent ist dieser "Feedback-Schleife" du — Benutzer — zur Überprüfung der Ausgabe und Korrektur. Wenn Sie es aber können, bevor es zu dir geliefert wird,让 Agent selbst zuerst eine Runde diese Schleife laufen, das bedeutet, eine Automatisierungs-Qualitätsprüfung hinzufügen. Das ist **Selbstüberwachung**: System内建一个Qualitätsdauer, bringt Vorprüfung seiner eigener Ausgabe, nur durch Vorprüfung kann geliefert werden.

### 3.4.2 Warum KI-Agent Selbstüberwachung braucht

Die häufigsten Lieferungsprobleme des Agent:
- **Harte Anforderungen ausgelassen**: Du verlangst reiner Text, es gibt interlinierte, interne Version mit Kommentaren.
- **KI-Spuren zu schwer**: "总而言之" "值得关注" "als ein KI" diese Floskeln siehst du 厌烦.
- **Struktur unvollständig**: 说好的 drei Teile, es schreibt zwei und stopped.
- **Lieferung nicht rein**: Datei带着 review notes, interne Markierungen, du musst manuell bereinigen.

Diese Probleme, wenn du es nicht prüfst und direkt zu dir schickst, du prüft und dann musst eine Runde Dialog verschwenden zur Korrektur. Selbstüberwachung ist, diese Runde Dialog-Prüfungskosten von dir auf den Agenten selbst zu transferieren.

### 3.4.3 Implementations-Design im Agent

Selbstüberwachung implementiert als **Lieferungs-Vor-Tor-Fähigkeit（delivery_gate）**. Bevor der Agent eine final Ergebnis ausgibt, muss er diese Fähigkeit laufen, Summe prüfen.

**Tor-Prüfungsinhalt（ fünf Phase)**:

| Phase   | Priorität      | Prüfungs-Inhalt                                     | Nicht- durch-Vorgang           |
| :------- | :------------- | :-------------------------------------------------- | :------------------------------ |
| Phase 1 | P0 Härte-Block | Harte Anforderungen prüfen: Wortanzahl, Format, forbidden, must-include | Forcierte Korrektur, erneutes Tor |
| Phase 2 | P0 Härte-Block | Fakt-Genauigkeit: Code-Logik, Daten-Referenz, Dateinamen/Pfad          | Unbestimmte markiert "zu verifizieren" |
| Phase 3 | P1 Hohe Priorität | KI-Spuren: Floskel, Moral-Zusammenfassung, sudden Erhöhung             | Forcierte Löschung             |
| Phase 4 | P1 Hohe Priorität | Struktur-Integrität: Logik-Schließung, notwendige Schritte nicht fehlen | Ergänzen                   |
| Phase 5 | P2 Optimierungs-Vorschlag | Lieferungsreinheit: Kommentaren entfernen, review notes, Markierungen          | Reinigen                 |

**Lauf-Schritte**:
1. Aufgabe fertig, bereit zu liefern.
2. Agent Intern ruft `delivery_gate` auf.
3. Summe scannen, durch/nicht-durch Protokollieren.
4. Alle durch → finale Ergebnis Ausgabe.
5. Jeder nicht durch → automatische Korrektur → erneutes Tor → bis alle durch.

### 3.4.4 Wie man überprüft, ob es bereits wirkt

- Agent liefert, du prüfst: Gibt es noch KI-Floskel? Überflüssige Kommentaren? Format完全符合要求?
- Vor der Lieferung, hat Agent in reasoning oder中间输出 eine Prüfung implementiert (wie "Selbstprüfung im Gange: P0 Härte-Block durch, P1 KI-Spur ein Ort gefunden, bereits gel").

**Selbstüberwachungs-Ziel:让你拿到手的 Lieferung ist bereits "rein", du musst nur bestätigen, brauchst nicht mehr als Qualitätsprüfer fungieren.**

---

## 3.5 Kooperations-Verhältnis der vier Konzepte

Die vier Konzepte sind nicht没有互相独立的零件, sondern是四个 Phase einer System-Lauf:

1. **Vor Aufgabenbeginn**: Feedforward injiziert Signal, заранее markiert坑.
2. **Während Aufgaben-Ausführung**: Hierarchische Zerlegung gewährleistet, dass信息流 rein — obere Schicht Richtung gibt, untere Schritt gibt Ausführung.
3. **Bei Benutzer-Feedback**: Integralsteuerung bestimmt, ob Feedback zu langfristiger Regel erhöht wird.
4. **Vor Aufgaben-Lieferung**: Selbstüberwachung fungiert als letzte Feedback-Schleife, blockt unqualifizierte Ausgabe.

Und bei **periodischer Reflexion**, Agent nimmt diese vier als Standard, um alle Erinnerungen und Fähigkeiten zu auditieren,完成 selbst-Evolution. Das wird下一章将展开的系统架构全景。

---

**下一章, wir werden diese vier Konzepte auf konkrete Erinnerungs- und Fähigkeits-Struktur des Agenten abbilden, zeigen完整 System-Architektur-Design und信息fliess zwischen各层.**
