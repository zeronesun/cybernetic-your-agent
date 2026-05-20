# Prolog: Warum KI alles Wissen lernt, aber immer noch nicht "dich versteht"

Hast du so etwas schon einmal erlebt:

Du arbeitest schon seit dutzenden Malen mit einem KI-Assistenten. Du sagst ihm immer wieder "Keine Zusammenfassung als Schluss", "Schreibe zuerst Tests, dann die Implementierung", "Liste zuerst Risiken auf, dann sprich über den Nutzen". Jedes Mal stimmt es zu. Jede neue Sitzung, alles zurück auf Null. Das nächste Mal sendest du dieselbe Aufgabe, es begeht enthusiastisch denselben Fehler wieder und wartet darauf, dass du es erneut korrigierst.

**Das Problem liegt nicht daran, dass die KI nicht schlau genug ist.** Ihre Modellparameter könnten millionenfach sein. Sie hat fast alle öffentlich zugänglichen Texte seit Menschengedenken gelesen. Jedes Wort, das du ihr sagst, "versteht" sie. Aber sie kann es sich nicht merken — nicht die Informationen selbst, sondern **was dir wichtig ist, was bei dir als Fehler gilt, was für eine Lieferung als qualifiziert gilt**.

Der Mainstream-Ansatz zur Lösung dieses Problems lautet: weiter unterrichten. Schreib längere Prompts. Organisiere detailliertere Regeldokumente. Mach ein komplexes RAG-Wissenssystem. Füge bei jedem KI-Fehler eine weitere Regel hinzu, bis die System-Prompts auf zehntausende Token angewachsen sind, die Regeln beginnen sich zu widersprechen, und du selbst nicht mehr weißt, wie viele Anforderungen du tatsächlich geschrieben hast.

**Dieses Tutorial geht einen entgegengesetzten Weg.**

Wir unterrichten die KI nicht mit neuem Wissen. Wir **nutzen die härteste System-Engineering-Theorie des 20. Jahrhunderts, um die Architektur der Erinnerung und Fähigkeiten der KI neu zu gestalten**.

Der Name dieser Theorie klingt fern — Qian Xuesens "Engineering Cybernetics". Aber du musst kein Ingenieur sein und musst keine Mathematik verstehen. Du musst nur vier Konzepte verstehen und sie Schritt für Schritt wie diesem Tutorial auf deinem KI-Agenten deployen: **Feedforward** (vermeide Fehler, bevor sie passieren), **Integral Control** (einmalige Beschwerde ändert nichts, zweimalige Beschwerde ändert systematisch), **Hierarchical Separation** (Prinzipien und Schritte gründlich trennen), **Self-Monitoring** (automatische Qualitätsprüfung vor der Lieferung).

Diese vier Konzepte, plus eine periodische geschlossene Reflexion, ermöglichen es deinem Agenten, sich von einem "Tool, das jedes Mal erneut unterrichtet werden muss", in einen **kollaborativen Motor zu verwandeln, der aktiv Fehler vermeidet, nicht wild schwingt und sich stetig an deine Prinzipien anpasst**.

Dieser Ansatz ist nicht im stillen Kabinett entstanden.

Er begann mit einer Notiz. In dieser Notiz hat ein Benutzer versucht, die Kernideen von Qian Xuesens Engineering Cybernetics an seinen Hermes Agenten zu "füttern", um Erinnerungen und Fähigkeitsschichten zu organisieren, damit der Agent nach dieser Logik während der Arbeit entsprechende Fähigkeiten auslöst. Die Kommentare waren voll mit "wozu machst du das", "nachdem du es probiert hast, funktioniert es wirklich".

Dieses Tutorial ist die Systematisierung dieses Ehrgeizes aus dieser Notiz, kombiniert mit unzähligen nachfolgenden Testläufen und Architektur-Deduktionen, **zu einem vollständigen, reproduzierbaren, für allgemeine Agentenplattformen gerichteten praktischen Plan**. Wir gehen vom Satz "Destillierung des menschlichen Denkmodells" bis zur vollständigen Architektur aus, die Agenten zur selbst- Evolution durch vier Cybernetik-Konzepte antreiben kann.

Du benötigst kein bestimmtes Modell. Du benötigt kein Hermes. Du benötigst nur eine moderne Agentenplattform mit **persistenter Erinnerung** und **Fähigkeiten/Prozedur-Module** und die Geduld, bereit zu sein, ein oder zwei Stunden zu investieren, um ein System mit langfristiger Rendite aufzubauen.

## Was dieses Buch nicht ist

**Dies ist keine Prompt-Sammlung.** Du findest hier keine "50 Prompts, um das Schreiben der KI besser zu machen". Wir kümmern uns um Architektur, Systeme, wie man die Organisation der Prompts selbst kontrollierbar und evolvierbar macht.

**Dies ist keine akademische Arbeit.** Unsere Zitate zur Engineering Cybernetics sind hochgradig technisch und stark vereinfacht. Qian Xuesens System ist weit tiefer und breiter als das, was wir hier darstellen. Wir haben nur vier Konzepte genommen, die direkten Wert für die Architekturplanung von Agenten haben, und machen eines: **sie in ausführbare Befehle für Agenten verwandeln.**

**Dies ist keine einmalige Umgestaltung.** Der Kern dieses Systems ist "geschlossene Evolution" — Deployment ist nur der Beginn, nicht das Ziel. Du sagst einmal pro Woche "Start" (Take off), und der Agent führt gemäß Cybernetik-Standards eine Selbstprüfung durch, nähert sich kontinuierlich deinen wahren Präferenzen.

## Wem dieses Buch nützt

Wenn du eine der folgenden Bedingungen erfüllst, könnte dir dieses Buch nützlich sein:

- Du hast einen häufig zusammenarbeitenden KI-Agenten, aber jede neue Sitzung ist wie das erneute Kennenlernen seines.
- Du hast es über, immer wieder denselben Fehler zu korrigieren, und hoffst, dass eine Korrektur als langfristige Regel abgelagert wird.
- Du bist neugierig auf "System-Engineering-Denken auf KI anzuwenden".
- Du bist nicht zufrieden, KI nur als Antwort-Tool zu nutzen, und möchtest sie zu einem Kollaborator mit stabiler Persönlichkeit und selbst-korrigierender Fähigkeit verwandeln.

Wenn du KI nur gelegentlich zum Chatten oder Frage nach einmaligen Dingen nutzt, könnte die Architektur dieses Buches für dich zu schwer sein. Du kannst die ersten drei Kapitel lesen, um die Idee zu verstehen, die folgenden praktischen Schritte musst du nicht vollständig deployen.

## Wie man dieses Buch verwendet

Dieses Buch hat sieben Kapitel, organisiert nach dem Pfad "Warum → Was → Wie baut man → Wie benutzt man → Wie repariert man":

- **Kapitel 1 bis Kapitel 4** sind theoretische Grundlage und Architekturplanung. Wenn du nach dem Lesen denkst "Dieser Ansatz gefällt mir", dann gehe zum praktischen Einsatz.
- **Kapitel 5** ist das reine Befehls-Kapitel. Du kannst direkt die Befehle kopieren und ihrem Agenten senden, um Schritt für Schritt das Deployment abzuschließen.
- **Kapitel 6** lehrt dir, wie man es täglich verwendet und wie man überprüft, ob das System normal läuft.
- **Kapitel 7** ist zur Fehlerbehebung und erweiterter Reflexion; bei Problemen kannst du jederzeit hierhin zurückkehren.

Wenn du die Agentenplattform Hermes (oder ähnliche Fähigkeitssammlung) verwendest, kannst du fast nahtlos alle Schritte ausführen. Wenn deine Plattform Fähigkeiten hat, die abweichen, bietet Kapitel 7, Abschnitt 7.1 einen reduzierten Adaptionsplan.

## Bevor wir beginnen, sei eine Sache klar

Das Deployen dieses Systems erfordert von dir eine Stunde. Die Rendite ist: Von nun an wird der Agent bei jeder Kooperation aktiv deine Präferenzen erinnern, aktiv bekannte Fehler vermeiden, vor der Lieferung selbst-Qualitätscontroll durchführen und bei wöchentlichen Reflexionen sein Verhalten automatisch optimieren.

**Dies lässt KI nicht "stärker" werden. Es lässt sie "dich verstehen".**

Der Unterschied zwischen beiden ist der Unterschied zwischen hundert Prompts und einer Architektur.

Jetzt fangen wir an. Kapitel 1: Hintergrund & Grundidee.
