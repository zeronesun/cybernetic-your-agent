# Kapitel 3: Detaillierte Kerntheorie — Vier Cybernetik-Konzepte

---

Dieses Kapitel详细拆解 Qian Xuesens Engineering Cybernetics 中, die wir extrahiert haben: **Feedforward, Integral Control, Hierarchical Separation, Self-Monitoring**.

Für jedes Konzept werden wir die folgenden vier Dinge abschließen:
1. **Prinzip-Erklärung**: Was ist es in der Cybernetik und warum ist es wichtig.
2. **Agent-Dilemma**: Welches Problem wird Agent ohne dieses Konzept haben.
3. **Implementations-Design**: Wie wird es mit Erinnerung und Fähigkeiten realisiert.
4. **Ein verifizierbarer Indikator**: Wie beurdest du, dass es bereits läuft.

---

## 3.1 Feedforward — Fehler blockieren, bevor sie passieren

### 3.1.1 Prinzip-Erklärung

In der Cybernetik sind Feedforward und Feedback zwei grundlegende Steuerungsmethoden.

- **Feedback**: misst Ausgabe, entdeckt Abweichung, geht zurück, um Eingabe zu korrigieren. Es ist immer "nachher".
- **Feedforward**: befor Störungen in das System treten, basierend auf Vorhersage, das Steuersignal voraussgehend anpassen. Es ist "vorher".

Das klassische Feedforward-Beispiel in der Ingenieur-Technik: Ein Kesselsystem merkt, dass die Einlasswassertemperatur sinkt, es wartet nicht auf Dampfdruckänderung, sondern erhöht direkt die Heizleistung. Es misst "Störungsquelle", nicht "Ausgababweichung".

Qian Xuesen betont im "Engineering Cybernetics" wiederholt: **Hochleistungssystem muss sowohl Feedforward als auch Feedback gleichzeitig enthalten, man kann nicht nur auf Feedback verlassen.** Feedback korrigiert verbleibende Abweichungen, Feedforward beseitigt Haupt-Störungen.

### 3.1.2 Warum KI-Agent Feedforward braucht

Ohne Feedforward arbeitet Agent reines Feedback:

```
Du: Schreib eine Kurzgeschichte.
Agent: (Ausgabe)
Du: Schluss ohne KI-Zusammenfassung.
Agent: (Korrektur)
Nächstes Mal:
Du: Schreib eine Kurzgeschichte.
Agent: (wieder KI-Zusammenfassung erscheint)
Du: Schluss ohne KI-Zusammenfassung!
```

Jedes Mal: Fehler passiert → Du korrigierst → es korrigiert. Dieses Muster "warten, dass du kritisch bist, dann ändern" hat mehrere tödliche Defekte:
- **Verschwendet Dialogrunde**: Korrektur nimmt deine Zeit.
- **Vertraut auf deine Wachheit**: Wenn du es einmal vergißt zu sagen, wird der Fehler direkt geliefert.
- **Vergessen über Sitzungen**: Letzte Korrektur existiert nur im Kontext jener Dialogs, neue Sitzung erinnert nicht daran.

Feedforward löst genau das: **Nicht warten, bis du sagst "wieder falsch", sondern voraussgehend Dinge, die dir vielleicht wichtig sind, injizieren, bevor die Aufgabe startet.**

### 3.1.3 Implementations-Design im Agent

Feedforward wird im Agent als **"Signal-vorausladen" beim Aufgabe-Start** realisiert.

**Spezifischer Mechanismus**:
1. Jedes Mal, wenn eine neue Aufgabe beginnt, zieht Agent aktiv Informationen aus drei Datenquellen:
   - **L2 Benutzer-Grundlogik**: Deine跨场景 ästhetische und Prinzip (z.B. "ablehne KI-Zusammenfassung").
   - **L3 Szenario-Kern-Regel**: Erfolgs-Regel des aktuellen Aufgabentyps (z.B. "Kurzgeschichte muss offen lassen").
   - **Korrektureinträge in Sitzungs-Archiv/Erinnerung**: Was wurde bei der letzten Aufgabe desselben Typs korrigiert.
2. Obige Informationen werden in eine **"Fehlervermeidungs-Checkliste"** komprimiert.
3. Vor der formalen Ausgabe wird die Fehlervermeidungs-Checkliste geschrieben (damit du bestätigt oder direkt ausführst).

**Beispiel**: Wenn du Agent eine Kurzgeschichte schreiben läßt, wird es vor dem Schreiben ausgeben:

> Start-Checkliste:
> - Aufgabentyp: Kurzgeschichte-Erstellung
> - Fehler zu vermeiden: ① Schluss offen, keine Zusammenfassung, keine Erhöhung; ② keine Sätze wie "als KI"; ③ kalte Erzählung, Reduzierung von Adjektiv-Stapelung.
> - Letzte Frage: Letztes Mal erschien "Leben ist so",已被规避.

Dann fängt es an zu schreiben. Dieses Feedforward lässt dich von "Korrektor" zum "Bestätiger" werden.

### 3.1.4 Wie man überprüft, ob es bereits wirkt

Beobachte folgende Verhalten:
- Gibt Agent am Anfang einer neuen Aufgabe aktiv eine "Start-Checkliste" oder "Fehlervermeidungs-Checkliste" aus?
- Derselbe Fehler wird beim ersten Mal signifikant reduziert.
- In 5 aufeinanderfolgenden Aufgaben desselben Typs sinkt deine Korrekturanteil.

**Feedforwards Ziel ist nicht null Fehler,而是让 Fehler nicht wiederkehren.**

---

## 3.2 Integral Control — Ändern, was geändert werden sollte, nicht willkürlich ändern, was nicht geändert werden sollte

### 3.2.1 Prinzip-Erklärung

In der Cybernetik besteht ein Controller normalerweise aus drei Teilen:

- **Proportionalsteuerung (P)**: Abweichung ist so groß, Handlung ist so groß.
- **Integralsteuerung (I)**: Wie lange Abweichung andauert, Handlung schrittweise erhöhen.
- **Differentialsteuerung (D)**: Wie schnell sich Abweichung ändert,提前抑制.

Reine Proportionalsteuerung hat tödliche Defekt: **Zu empfindlich gegenüber Rauschen**. Ein zufälliger Abweichung (z.B. Sensor-Schwanken) löst eine unnötige große Korrektur aus, das System schwingt daher — links, rechts, nie stabil.

**Integralsteuerung** löst genau dieses Problem: es akkumuliert Abweichung, erst wenn auf eine bestimmte Größe akkumuliert, löst es eine Aktion aus. Ein Sprung wird durchschnittet; kontinuierliche, stabile Abweichung verursacht Korrektur. Das ist die Bedeutung von "Integral" — **den Fehler über die Zeit integrieren, nur überschreitender Threshold als Kraft.**

### 3.2.2 Warum KI-Agent Integralsteuerung braucht

Ohne Integralsteuerung reagiert Agent auf dein Feedback oft in zwei Extremen:

- **Überempfindliche Antwort**: Du sagst einmal "dieser Schluss ist schlecht", es ändert sofort den gesamten Schreibstil, sogar Teile, die du vorher magst.
- **Unempfindliche Antwort**: Du sagst fünf Mal hintereinander "keine pluginartige Zusammenfassung", es stimmt jedes Mal zu, aber nächstes Mal auch keine Änderung.

Beide Situationen根源 darin, dass **kein "Antwort-Schwellwert" gesetzt ist.** Agent nimmt deinen einmaligen Ausdruck als permanente Regel, oder deine wiederholten Ausdrücke als jedes Mal unabhängige的事件-Events.

Integralsteuerung bietet eine sehr präzise Lösung: **Wenn Feedback derselben Kategorie das zweite Mal auftritt, erst dann wird es als stabiles Signal betrachtet, in die langfristige Erinnerung geschrieben oder Fähigkeiten geändert.**

### 3.2.3 Implementations-Design im Agent

Integralsteuerung wird als **Feedback-Zähler mit Threshold** realisiert, gespeichert im Erinnerungskörper, genannt "Integralsteuerungs-Tabelle".

**Struktur**:

| Kategorie | Fehlermuster (≤8 Zeichen) | Erstes Datum | Kumuliert | Threshold | Ist-abgesunken | Absink-Ziel |
| :--- | :------------------------- | :----------- | :-------- | :------- | :------------ | :---------- |
| A类  | Schluss-KI-Zusammenfassung | 0510         | 2         | 2        | Ja            | L2·Ästhetische Prinzipien |
| B类  | Rhythmus zu schnell         | 0510         | 1         | 2        | Nein          | L3·Kurzgeschichte-Regel |

**Lauf-Regel**:
1. Wenn du negatives Feedback gibst, klassifiziert Agent es als ein Fehlermuster (A=ästhetische Prinzipien, B=Szenario-Regeln, C=Fähigkeits-Schritt-Fehler).
2. Zähler für gleiches Muster +1.
3. Wenn kumuliert ≥ Threshold (standardmäßig 2 Mal), und noch nicht abgesunken, führt Agent automatisch das Absinken aus:
   - Diese Regel wird in das entsprechende L2, L3 oder Skill geschrieben.
   - Der Status "Ist-abgesunken" aktualisiert.
   - Bestätige bei dir: "'Schluss-KI-Zusammenfassung' ist jetzt 2 Mal aufgetreten, ich habe es in L2 Ästhetische Prinzipien gesunken, ist das OK?".
4. Wenn kumultiert = 1, mache nur diese Korrektur, ändere keine langfristige Regel.

**Warum-Threshold auf 2**:
- 1 Mal ist Rauschen: Vielleicht nur, weil du schlechte Laune hast, oder eine bestimmte Szene nicht passt.
- 2 Mal ist Signal: Kontinuierliche gleichartige Feedback zweimal zeigen, das ist wahrscheinlich deine stabile Präferenz.
- Du kannst es nach deinem Stil auf 3 anpassen, aber ich empfehle, von 2 zu starten.

### 3.2.4 Wie man überprüft, ob es bereits wirkt

- Du gibst absichtlich Feedbacksgleicher Typ zweimal (z.B. sagst zweimal "Schluss zu langwierig"), beobachte ob Agent nach dem zweiten Mal aktiv vorschlägt, die langfristige Regel zu ändern.
- Du gibst ein zufälliges Feedback (sagst ein Mal "ich mag diese Metapher nicht"), beobachte ob Agent dadurch nicht den gesamten Stil ändert.

**Integralsteuerung-Ziel ist nicht, Agent "sturhaft" zu machen, sondern ihm stabile Präferenz-Erfassungsfähigkeit zu geben — das, was gehört werden sollte, nicht versäumen, das ignoriert werden sollte, nicht übermäßig.**

---

## 3.3 Hierarchische Zerlegung — Strategie und Ausführung彻底 getrennt

### 3.3.1 Prinzip-Erklärung

Eines der Kernelemente von Qian Xuesens System-Denken ist **Hierarchische Steuerung**. Ein komplexes System muss in verschiedene Schichten zerlegt werden: obere Schicht legt Strategie, Ziel, Zwang fest; untere Schicht macht Ausführung, Anpassung, Feedback. Zwischen Ober- und Unterschicht werden Informationen nur über klare Schnittstellen übertragen, die interne Implementierung ist gegenseitig unsichtbar.

Wenn diese Trennung gebrochen wird — obere Schicht beginnt, Ausführungsdetails zu kontrollieren, untere Schicht Strategie selbst zu bestimmen — System gerät in Chaos: Ändert man一处, das全局 schwingt, ändert man一处,全局震荡.

### 3.3.2 Warum KI-Agent hierarchische Zerlegung braucht

Erinnerung und Fähigkeiten des Agenten können natürlich leicht in folgende几种混淆 verfallen:

- **Erinnerungs-Inflation**: Benutzer-Prinzipien（"hasst AI-Schluss"）und konkrete Ausführungsschritte（"nach dem Schreiben nach '"总而言之"' suchen und löschen"）sind vermischt. Erinnerung speichert sowohl "warum" als auch "wie"——Volumen膨, Abruf Schwierigkeiten.
- **Fähigkeitssteifigkeit**: Fähigkeiten ist hart-codiert mit einer Präferenz aus einem Gespräch, aber diese Präferenz könnte temporär sein. Nächstes Mal, wenn man es verwendet, ist die Fähigkeit bereits veraltet, und du weißt nicht, warum es so macht.
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
- Wenn du eine ästhetische Regel änderst（z.B. "jetzt kann gelegentlich metaphorisches Vokabular verwendet werden"）, musst du nur eine Erinnerung ändern, braucht nicht irgendwelche Fähigkeiten zu berühren.

**Hierarchische Zerlegungs-Ziel ist, Erinnerung von "Kuchenteig" zu "Datenbank" zu machen, 让 jede Information eine einzige Zuweisung und bestimmte Änderungspfad hat.**

---

## 3.4 Selbstüberwachung — Vor der Lieferung, zuerst durch eigenes Tor

### 3.4.1 Prinzip-Erklärung

Jedes Steuermuß 最后必需有一个 **Feedback回路** 闭合。在工程系统里，这意味着: System misst seine eigener Ausgabe, vergleicht mit erwartetem Wert, erzeugt Fehler-Signal zu korrigieren. Für Agent ist dieser "Feedback-Schleife" du — Benutzer — zur Überprüfung der Ausgabe und Korrektur. Wenn Sie es aber können, bevor es zu dir geliefert wird,让 Agent selbst zuerst eine Runde diese Schleife laufen, das bedeutet, eine Automatisierungs-Qualitätsprüfung hinzufügen. Das ist **Selbstüberwachung**: System内建一个Qualitätsdauer, bringt Vorprüfung seiner eigener Ausgabe, nur durch Vorprüfung kann geliefert werden.

### 3.4.2 Warum KI-Agent Selbstüberwachung braucht

Die häufigsten Lieferungsprobleme des Agent:
- **Harte Anforderungen ausgelassen**: Du verlangst reiner Text, es gibt interlinierte, interne Version mit Kommentaren.
- **KI-Spuren zu schwer**: "总而言之" "值得关注" "als ein KI" 这些 Floskel 你看 厌烦.
- **Struktur unvollständig**: 说好的 drei Teile, 它写到 zwei und stopped.
- **Lieferung nicht rein**: Datei 带着 review notes, 内部 Markierungen, 你你得 manuell bereinigen.

Diese Probleme, wenn du es nicht prüfst und direkt zu dir schickst, du prüfst und dann musst eine Runde Dialog verschwenden zur Korrektur. Selbstüberwachung ist, diese Runde Dialog-Prüfungskosten von dir auf den Agenten selbst zu transferieren.

### 3.4.3 Implementations-Design im Agent

Selbstüberwachung implementiert als **Lieferungs-Vor-Tor-Fähigkeit（delivery_gate）**. Bevor der Agent eine final Ergebnis ausgibt, muss er diese Fähigkeit laufen, Summe prüfen.

**Tor-Prüfungsinhalt（fünf Phase)**:

| Phase   | Priorität      | Prüfungs-Inhalt                                     | Nicht-durch-Vorgang           |
| :------- | :------------- | :-------------------------------------------------- | :------------------------------ |
| Phase 1 | P0 Härte-Block | Harte Anforderungen prüfen: Wortanzahl, Format, forbiddens, must-include | Forcierte Korrektur, erneutes Tor |
| Phase 2 | P0 Härte-Block | Fakt-Genauigkeit: Code-Logik, Daten-Referenz, Dateinamen/Pfad          | Unbestimmte markiert "zu verifizieren" |
| Phase 3 | P1 Hohe Priorität | KI-Spuren: Floskel, Moral-Zusammenfassung, sudden Erhöhung             | Forcierte Löschung             |
| Phase 4 | P1 Hohe Priorität | Struktur-Integrität: Logik-Schließung, notwendige Schritte nicht fehlen | Ergänzen                   |
| Phase 5 | P2 Optimierungs-Vorschlag | Lieferungsreinheit: Kommentaren entfernen, review notes, Markierungen          | Reinigen                 |

**Lauf-Schritte**:
1. Aufgabe fertig, bereit zu liefern.
2. Agent Intern ruft `delivery_gate` auf.
3. Summe scannen, durch/nicht-durch Protokollieren.
4. Alle durch → finalen Ergebnis Ausgabe.
5. Jeder nicht durch → automatische Korrektur → erneutes Tor → bis alle durch.

### 3.4.4 Wie man überprüft, ob es bereits wirkt

- Agent liefert, du prüfst: Gibt es noch KI-Floskel? Überflüssige Kommentaren? Format完全符合要求?
- Vor der Lieferung, hat Agent in reasoning oder中omialaus输出 eine Prüfung implementiert (wie "Selbstprüfung im Gang: P0 Härte-Block durch, P1 KI-Spur ein Ort gefunden, 已经 gel).

**Selbstüberwachungs-Ziel:让你拿到手的 Lieferung ist bereits "rein", du musst nur bestätigen, brauchst nicht mehr als Qualitätsprüfer fungieren.**

---

## 3.5 Kooperations-Verhältnis der vier Konzepte

Die vier Konzepte sind nicht没有互相独立的零件, 而是 四个 Phase einer System-Lauf:

1. **Vor Aufgabenbeginn**: Feedforward injiziert Signal, 提前 markiert坑.
2. **Während Aufgaben-Ausführung**: Hierarchische Zerlegung gewährleistet, dass信息流 rein — obere Schicht Richtung gibt, untere Schritt gibt Ausführung.
3. **Bei Benutzer-Feedback**: Integralsteuerung bestimmt, ob Feedback zu langfristiger Regel 加 wird.
4. **Vor Aufgaben-Lieferung**: Selbstüberwachung fungiert als letzte Feedback-Schleife, blockt unqualifizierte Ausgabe.

Und bei **periodischer Reflexion**, Agent nimmt diese vier als Standard, um alle Erinnerungen und Fähigkeiten zu auditieren,完成 selbst-Evolution. Das wird下一章将展开的系统架构全景。

---

**下一章, wir werden diese vier Konzepte auf konkrete Erinnerungs- und Fähigkeits-Struktur des Agenten abbilden, zeigen完整 System-Architektur-Design und信息fließ zwischen 各层.**

