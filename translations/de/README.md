[English](../en/README.md) | [简体中文](../../README.md) | [繁體中文](../zh_TW/README.md) | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Русский](../ru/README.md) | Deutsch

# AI-Agenten mit Qian Xuesens Engineering Cybernetics trainieren

> Lehren Sie dem AI keine neuen Kenntnisse. Benutzen Sie **Feedforward, Integral-Kontrolle, hierarchische Dekomposition und Selbstüberwachung** — vier Konzepte — um die Speicher- und Skill-Architektur des Agenten umzugestalten und ihn von einem passiven Werkzeug zu einer selbstkorrigierenden und sich weiterentwickelnden Kollaborations-Engine zu verwandeln.

---

## Was dies ist

Ein vollständiges, reproduzierbares, handhabbares Tutorial.

Es adaptiert die Kernideen von Qian Xuesens *Engineering Cybernetics* für moderne AI-Agenten-Plattformen (Hermes, Claude mit MCP, benutzerdefinierte GPTs usw.). Ohne neue Prompts hinzuzufügen oder neue Modelle einzuführen, benutzt es **architektonische Umstrukturierung**, um den Agenten zu machen:

- 🎯 **Feedforward zur Fehlervermeidung** — lädt proaktiv Ihre Präferenzen und historischen Lektionen vor dem Start einer Aufgabe
- 🔧 **Integral-Kontrolle zur Verhinderung von Schwingungen** — eine einmalige Beschwerde erhält nur eine temporäre Korrektur; derselbe Feedback zweimal löst eine systematische Änderung aus
- 🧹 **Hierarchische Trennung** — Speicher speichert nur das "warum"; Skills speichern nur das "wie"; niemals gemischt
- 🚦 **Selbstüberwachungs-Liefertor** — ein Fünf-Punkte-Qualitäts-Tor läuft vor jeder Ausgabe aus; unqualifizierte Ergebnisse werden niemals geliefert
- 🔄 **Geschlossene Schleifen-Evolution** — sagen Sie einmal pro Woche "takeoff (abheben)" und der Agent überprüft und optimiert sich automatisch

---

## Schnellstart

Senden Sie diesen Befehl an Ihren Agenten, und er wird das vollständige Training automatisch abschließen (ca. 40 Minuten):

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。
```

**Voraussetzungen**: Ihr Agent muss in der Lage sein, auf GitHub zuzugreifen, in den Speicher zu schreiben und Skills zu erstellen. Wenn dies nicht erfüllt ist, folgen Sie den manuellen Schritten unten.

1. Stellen Sie sicher, dass Ihre Agenten-Plattform hat: **persistenter Speicher** + **Skills / prozedurale Module**
2. Lesen Sie das Tutorial (Reihenfolge ist empfohlen, oder lesen Sie mindestens Kapitel 1, um den Ansatz zu verstehen)
3. Gehen Sie zu [Kapitel 5](chapters/05-deployment.md), kopieren Sie die Anweisungen und deployen Sie Schritt für Schritt (ca. 1 Stunde)
4. [Kapitel 6](chapters/06-daily-usage.md) erklärt Ihnen, wie Sie es täglich nutzen und wie Sie überprüfen, dass es funktioniert

---

## Tutorial-Struktur

| Kapitel | Datei | Ein-Satz-Zusammenfassung |
| :------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| Vorwort | [`PREFACE.md`](PREFACE.md) | Warum AI alle Kenntnisse lernt, dich aber trotzdem nicht "versteht" |
| Kapitel 1 | [`chapters/01-background.md`](chapters/01-background.md) | Hintergrund und Kern-Philosophie |
| Kapitel 2 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | Voraussetzungen und Vorbereitung |
| Kapitel 3 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md) | Vier Cybernetic-Konzepte im Detail (Feedforward / Integral / Trennung / Selbstüberwachung) |
| Kapitel 4 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | System-Architektur im Detail (dreischichtiger Speicher + Skill-Ebene + Datenfluss) |
| Kapitel 5 | [`chapters/05-deployment.md`](chapters/05-deployment.md) | Handhabbarer Führer (Schritt-für-Schritt-Deployment-Anweisungen, die Sie direkt kopieren können) |
| Kapitel 6 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md) | Tägliche Nutzung und Verifikation |
| Kapitel 7 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | Fehlerbehebung + Multi-Agent / neue Theorie-Erweiterungen |
| Nachwort | [`EPILOGUE.md`](EPILOGUE.md) | Nach dem Deployment: Bedeutung und Zukunftsausrichtung |

### Dateinamenshinweis

Root-Verzeichnis und Kapiteldateinamen verwenden Englisch für plattformübergreifende und Toolchain-Kompatibilität. Zuordnung von chinesischen Quelldateinamen zu GitHub-Namen:

| Lokaler Dateiname (Chinesisch) | GitHub-Dateiname |
| :---------------------------------- | :---------------------------- |
| 序章：为什么 AI…md | `PREFACE.md` |
| 第一章：背景与核心理念.md | `chapters/01-background.md` |
| 第二章：适用条件与准备工作.md | `chapters/02-prerequisites.md` |
| 第三章：核心理论详解.md | `chapters/03-core-theory.md` |
| 第四章：系统架构详解.md | `chapters/04-architecture.md` |
| 第五章：实操指南.md | `chapters/05-deployment.md` |
| 第六章：日常使用与验证.md | `chapters/06-daily-usage.md` |
| 第七章：常见问题与延伸思考.md | `chapters/07-faq-extensions.md` |
| 结尾：架构之后.md | `EPILOGUE.md` |

Titel und Text innerhalb files bleiben Chinesisch. Das `translations/` Verzeichnis ist für Übersetzungen in andere Sprachen reserviert (z.B. `en/`, `de/`).

### Begleitende Dateien

| Datei | Beschreibung |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | Reine Extraktion aller Kapitel-5-Befehle (keine Erklärungen, für schnelle Ausführung) |
| [`examples/`](examples/) | L2/L3-Beispiel, Integral-Kontrolltabellen-Beispiel, tiefere Überprüfungs-Ausgabe-Beispiel |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Beitrittsführer |
| [`LICENSE`](LICENSE) | Open-Source-Lizenz |

---

## Unterstützte Plattformen

- ✅ **Hermes 3** (vollständige native Unterstützung, alle Anweisungen arbeiten nahtlos)
- ✅ **Claude (mit MCP)** (kleinere Syntax-Anpassungen für Tool-Aufrufe; Kern-Architektur vollständig anwendbar)
- ✅ **Custom GPTs** (verwenden Sie Knowledge-Dateien um Speicher, Actions um Skills zu simulieren)
- 🔸 Andere Agenten-Plattformen mit **persistenter Speicher + Skill / prozedurale Module**
- 🔸 Plattformen ohne eine Skill-Funktion (können im verminderten Modus laufen, siehe [Kapitel 7 §7.1](chapters/07-faq-extensions.md))

---

## Auf einen Blick: Vorher vs. Nachher

| Dimension | Vorher | Nachher |
| :--------------- | :----------------------------------------- | :------------------------------------------- |
| Aufgaben-Start | Sie erklären die Notwendigkeit; Agent fängt direkt an | Agent gibt zuerst eine Checkliste zur Fehlervermeidung und Risikobewertung aus; Sie bestätigen |
| Wiederkehrende Fehler | Jedes Mal korrigieren; denselben Fehler nächstes Mal | Nach dem zweiten Vorkommen automatisch in Regeln versenkt; passiert nicht ein drittes Mal |
| Speicher-Signal-zu-Rauschen | Prinzipien, Schritte, Beispiele alle gemischt | Dreischichtige Trennung; Prinzipien und Schritte haben ihren eigenen Platz |
| Ausgabequalität | Sie überprüfen, finden Klischees / Formatierungsprobleme, bitten dann um Korrekturen | Agent führt sein eigenes Fünf-Punkte-Qualitätstor durch; liefert erst wenn es besteht |
| System-Evolution | Gelegentlich basierend auf Intuition angepasst | Jede Woche "takeoff"; automatische Überprüfung und Auto-Optimierung |

---

## Kern-Philosophie

> **Was Sie machen, ist keine Prompt-Engineering. Es ist Architektur-Engineering.**
>
> Sie lehren dem Agenten keine neuen Kenntnisse. Sie nutzen Systems-Engineering-Denken um eine interne Architektur zu entwerfen, die stabil läuft und kontinuierlich weiterentwickelt sich.

Für mehr Hintergrund und Ausarbeitung siehe das [Vorwort](PREFACE.md) und [Kapitel 1](chapters/01-background.md).

---

## Projektname

**Cybernetic Your Agent** — das Einfügen von Cybernetic-Genen in Ihren Agenten.

Wir lehren AI keine neuen Kenntnisse. Wir verwenden die vier Konzepte aus Qian Xuesens Engineering Cybernetics — Feedforward, Integral-Kontrolle, hierarchische Dekomposition und Selbstüberwachung — um die Speicher- und Skill-Architektur des Agenten umzugestalten. Der Agent bewegt sich vom Verstehen von Befehlen zum Verstehen *Ihrer Bewertungslogik* — wirklich *Ihr* Agent zu werden.

---

## Lizenz

Dieses Projekt ist unter der [MIT License](LICENSE) lizenziert.

---

## Danksagungen

- Qian Xuesens *Engineering Cybernetics* — das theoretische Fundament dieses Tutorials
- Der ursprüngliche Notiz-Autor, der zuerst die Idee "Agenten-Speicher mit Cybernetic ordenen" vorschlug und alle, die im Kommentar-Bereich testeten und Feedback gaben
- Alle, die halfen, die Architektur in frühen Versionen zu testen und zu verbessern

## Star History

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>
