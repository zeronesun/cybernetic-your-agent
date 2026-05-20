[English](README_EN.md) | [简体中文](README.md) | [繁體中文](README_ZH_TW.md) | [한국어](README_KO.md) | [Deutsch](README_DE.md)

# Training AI Agents mit Qian Xuesens Engineering Cybernetics

> Lehre dem KI nicht neues Wissen. Verwende **Feedforward, Integralsteuerung, hierarchische Zerlegung und Selbstüberwachung** — vier Konzepte — um die Erinnerungs- und Fähigkeitsarchitektur des Agenten umzugestalten, ihn von einem passiven Werkzeug zu einem selbstkorrigierenden und Evolution-fördernden Kollaborationsmotor zu verwandeln.

---

## Was ist das?

Ein vollständiges, reproduzierbares, praktisches Tutorial.

Es adaptiert die Kernelemente von Qian Xuesens *Engineering Cybernetics* für moderne KI-Agentenplattformen（Hermes, Claude mit MCP, custom GPTs等等）。Ohne neue Prompt-Inhalte hinzuzufügen oder neue Modelle einzuführen, nutzt es **Architektur-Neugestaltung**, um den Agenten zu machen:

- 🎯 **Feedforward für Fehlervermeidung** — lädt proaktiv deine Präferenzen und historischen Lektionen, bevor die Aufgabe beginnt
- 🔧 **Integralsteuerung zur Schwingungsvermeidung** — eine einmalige Beschwerde wird nur времен korrigiert; dieselbe Rückmeldung zweimal triggert eine systematische Änderung
- 🧹 **Hierarchische Zerlegung** — Erinnerung speichert nur das "Warum"; Fähigkeiten speichern nur das "Wie"; nie gemischt
- 🚦 **Selbstüberwachungs-Lieferungstor** — ein fünffach-Prüfungsqualitätstor läuft vor jeder Ausgabe; unqualifizierte Ergebnisse werden nie geliefert
- 🔄 **Geschlossener Evolution-Schleife** — sage "Start" einmal pro Woche und der Agent überwacht und optimiert sich automatisch selbst

---

## Schnellstart

Senden sie diesen Befehl an Ihren Agenten; er wird das volle Training automatisch abschließen (≈ 40 Minuten):

```
Trainiere mich nach github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md.每步确定后完成闭环测试。
```

**Anforderungen**: Ihr Agent muss GitHub zugreifen, in die Erinnerung schreiben und Fähigkeiten erstellen können. Wenn nicht erfüllt, folgen Sie den manuellen Schritt unten.

1. Stellen Sie sicher, dass Ihre Agentenplattform hat: **persistente Erinnerung** + **Fähigkeiten / prozedurale Module**
2. Lesen Sie das Tutorial（Reihenfolge ist empfohlen, oder zumindest第一章 ounderstand）
3. Gehen Sie zu [Chapter 5](chapters/05-deployment.md), kopieren Sie die Anweisungen und deployen Sie Schritt für Schritt (≈ 1 Stunde)
4. [Chapter 6](chapters/06-daily-usage.md) sagt Ihnen, wie man täglich mit ihm arbeitet und wie man überprüft, ob es funktioniert

---

## Tutorial-Struktur

| Chapter  | Datei                                                         | Ein-Satz-Zusammenfassung                                 |
| :------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| Preface  | [`PREFACE.md`](PREFACE.md)                                   | Warum KI alles Wissen lernt aber immmer noch nicht "dich versteht" |
| Chapter 1 | [`chapters/01-background.md`](chapters/01-background.md)     | Hintergrund und Kernphilosophie                       |
| Chapter 2 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | Voraussetzungen und Vorbereitung                        |
| Chapter 3 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md)   | Vier Cybernetik-Konzepte im Detail (Feedforward / Integral / Zerlegung / Selbstüberwachung) |
| Chapter 4 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | Systemarchitektur im Detail (dreischichtige Erinnerung + Fähigkeitsschicht + Datenfluss) |
| Chapter 5 | [`chapters/05-deployment.md`](chapters/05-deployment.md)     | Praktischer Leitfaden (Schritt-für-Schritt-Deploy-Anleitungen, die Sie direkt kopieren können) |
| Chapter 6 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md)   | Tägliche Nutzung und Überprüfung                        |
| Chapter 7 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | Fehlersuche + Multi-Agent / Neue-Theorie-Erweiterungen |
| Epilogue | [`EPILOGUE.md`](EPILOGUE.md)                                 | Nach dem Deploy: Bedeutung und zukünftige Richtung     |

### Datei-Benennungs-Hinweis

Root-Verzeichnis und Kapiteldateinamen verwenden Englisch für plattformübergreifende und Toolchain-Kompatibilität. Abbildung von chinesischen Quelldateinamen zu GitHub-Namen:

| Lokaler Dateiname (Chinesisch)           | GitHub-Dateiname              |
| :---------------------------------- | :---------------------------- |
| 序章：为什么 AI…md                  | `PREFACE.md`                  |
| 第一章：背景与核心理念.md           | `chapters/01-background.md`   |
| 第二章：适用条件与准备工作.md       | `chapters/02-prerequisites.md`|
| 第三章：核心理论详解.md             | `chapters/03-core-theory.md`  |
| 第四章：系统架构详解.md             | `chapters/04-architecture.md` |
| 第五章：实操指南.md                 | `chapters/05-deployment.md`   |
| 第六章：日常使用与验证.md           | `chapters/06-daily-usage.md`  |
| 第七章：常见问题与延伸思考.md       | `chapters/07-faq-extensions.md`|
| 结尾：架构之后.md                   | `EPILOGUE.md`                 |

Überschriften und Text innerhalb von Dateien bleiben Chinesisch. Das `translations/` Verzeichnis ist für Übersetzungen in andere Sprache reserviert (z.B. `en/`, `de/`, `ja/`).

### Ergänzende Dateien

| Datei                                                         | Beschreibung                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | Reine Extraktion aller Kapitel-5-Befehle (keine Erklärungen, für schnelle Ausführung) |
| [`examples/`](examples/)                                     | L2/L3-Beispiel, Integralsteuerungs-Tabelle Beispiel, Ausgabebeispiel bei tief Reflexion |
| [`CONTRIBUTING.md`](CONTRIBUTING.md)                         | Beitrag-Leitfaden                                           |
| [`LICENSE`](LICENSE)                                         | Open-Source-Lizenz                                          |

---

## Unterstützte Plattformen

- ✅ **Hermes 3** (vollständige native Unterstützung, alle Anleitungen funktionieren nahtlos)
- ✅ **Claude (mit MCP)** (kleine Syntax-Tweaks für Werkzeug-Aufrufe; Kernarchitektur vollständig anwendbar)
- ✅ **Custom GPTs** (Verwende Knowledge-Dateien um Erinnerung zu simulieren, Aktionen um Fähigkeiten zu simulieren)
- 🔸 Andere Agentenplattformen mit **persistenter Erinnerung + Fähigkeit / prozedurale Module**
- 🔸 Plattformen ohne eine Fähigkeits-Feature (können im degradierten Modus laufen, siehe [Kapitel 7 §7.1](chapters/07-faq-extensions.md))

---

## Auf einen Blick: Vorher vs Nachher

| Dimension        | Vorher                                     | Nachher                                      |
| :--------------- | :----------------------------------------- | :------------------------------------------- |
| Aufgabenbeginn       | Du gibst das Bedarfe; der Agent beginnt direkt  | Agent gibt erst eine Fehlervermeidungs-Checkliste und Risiko-Evaluierung aus; du bestätigst |
| Wiederholte Fehler | Korrigiere jedes Mal; derselbe Fehler scheint wieder | Automatisch sinkt in Regeln nach dem zweiten Auftreten; passiert nicht dritten Mal |
| Erinnerungs-Signal-zu-Rauschen | Prinzipien, Schritte, Beispiele alle gemischt | Dreischichtige Trennung; Prinzipien und Schritte haben各自的 Ort |
| Ausgabequalität   | Du prüfst, findest Floskeln / Format-Probleme, dann fragst du nach Korrektur | Agent läuft sein eigenes Fünf-hal-Prüfung-qualitätstor; liefert nicht bis es besteht |
| System-Evolution | Gelegentlich geändert basierend auf Intuition    | Sage "Start" wöchentlich; automatische Prüfung und auto-Optimierung |

---

## Kernphilosophie

> **Was du machst ist nicht Prompt-Engineering. Es ist Architektur Engineering.**
>
> Du lehrst dem Agenten nicht neues Wissen. Du nutzt Systemtechnik-Denken um eine interne Architektur zu entwerfen, die stabil läuft und kontinuierliche Entwicklung ermöglicht.

Für mehr Hintergrund und Vertiefung, siehe die [Preface](PREFACE.md) und [Kapitel 1](chapters/01-background.md).

---

## Projektname

**Cybernetic Your Agent** — cybernetische Gene in deinen Agenten injizieren.

Wir lehren KI nicht neues Wissen. Wir nutzen die vier Konzepte aus Qian Xuesens Engineering Cybernetics — Feedforward, Integralsteuerung, hierarchische Zerlegung und Selbstüberwachung — um die Erinnerungs- und Fähigkeitsarchitektur des Agenten umzugestalten. Der Agent geht vom Verstehen von Befehlen zum Verstehen *deines Urteilslogik* — wirklich *dein* Agent werden.

---

## Lizenz

Dieses Projekt ist lizenziert unter der [MIT License](LICENSE).

---

## Danksagungen

- Qian Xuesens *Engineering Cybernetics* — die theoretische Fundierung dieses Tutorials
- Der ursprüngliche Notizen-Autor, der zuerst die Idee von "Agenten-Erinnerung mit Cybernetik organisieren" vorgeschlagen hat und alle, die getestet und Feedback im Kommentarbereich gegeben haben
- Jeder, der geholfen hat, die Architektur in frühen Versionen zu testen und zu verbessern

---

## Star-Historie

<a href="https://www.star-history.com/?repos=zeronesun%2Fcybernetic-your-agent&type=date&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=zeronesun/cybernetic-your-agent&type=date&legend=bottom-right" />
 </picture>
</a>
