<!-- MGD-HEADER -->
<p align="center"><a href="https://Michael-Gahn.de"><img src="assets/mgd-logo.png" alt="Michael Gahn DESIGN" width="48"></a></p>

<p align="center"><img src="assets/banner.svg" alt="Fragenkatalog" width="100%"></p>

<p align="center">
  <img alt="Lizenz" src="https://img.shields.io/github/license/MichaelGahnDESIGN/Fragenkatalog-Skill?label=Lizenz">
  <a href="https://github.com/MichaelGahnDESIGN/Fragenkatalog-Skill/releases/latest"><img alt="Release" src="https://img.shields.io/github/v/release/MichaelGahnDESIGN/Fragenkatalog-Skill?label=Release"></a>
  <img alt="Sprache" src="https://img.shields.io/badge/Sprache-HTML-2f6fed">
  <a href="https://Michael-Gahn.de"><img alt="by Michael Gahn DESIGN" src="https://img.shields.io/badge/by-Michael%20Gahn%20DESIGN-cd1616"></a>
</p>
<!-- /MGD-HEADER -->

# Fragenkatalog-Skill

Ein wiederverwendbarer Skill für **Claude Code** und **ChatGPT Codex**, der für ein beliebiges
Projekt (Spiel, App, Website, Buch, Business-Plan, Produktdesign, Marketingkampagne, ...) einen
strukturierten, durchsuchbaren **Fragenkatalog** erzeugt: alle wichtigen Design- und
Konzeptfragen an einem Ort, zu jeder Frage sofort eine KI-Antwort aus einer frei wählbaren
Experten-Perspektive, und ein eigenes Feld für die endgültige Entscheidung des Projektinhabers.

> [!TIP]
> Ergebnis ist eine einzige self-contained HTML-Datei — kein Server, kein CDN, keine
> Abhängigkeiten. Einfach im Browser öffnen, filtern, durchsuchen, bearbeiten.

## Das Problem

Design-Fragen für ein Projekt bleiben oft unstrukturiert in Chat-Verläufen verstreut: mal fragt
man die KI "was hältst du von X", mal notiert man sich etwas in einem Dokument, mal vergisst man
die Frage komplett wieder. Es fehlt:

- ein **durchsuchbares Nachschlagewerk** aller offenen und beantworteten Fragen,
- eine klare **Trennung** zwischen dem, was die KI aus einer Experten-Perspektive vorschlägt, und
  dem, was der Projektinhaber tatsächlich entschieden hat,
- ein **Fortschritts-Tracking**, wie viele Fragen schon final beantwortet sind.

Der Fragenkatalog-Skill löst das mit einer einzigen HTML-Datei, die als lebendiges Dokument im
Projekt-Repo mitwächst.

## Installation

### 👤 Für Entwickler — Claude Code

```bash
git clone https://github.com/MichaelGahnDESIGN/Fragenkatalog-Skill.git
cp -r Fragenkatalog-Skill/.claude/commands/fragenkatalog.md <dein-projekt>/.claude/commands/
cp -r Fragenkatalog-Skill/SKILL.md <dein-projekt>/.claude/skills/fragenkatalog/SKILL.md
cp -r Fragenkatalog-Skill/templates <dein-projekt>/.claude/skills/fragenkatalog/templates
```

Danach in Claude Code:

```
/fragenkatalog setup
```

### 👤 Für Entwickler — ChatGPT Codex

```bash
git clone https://github.com/MichaelGahnDESIGN/Fragenkatalog-Skill.git
cp -r Fragenkatalog-Skill/.codex/commands/fragenkatalog.md <dein-projekt>/.codex/commands/
cp -r Fragenkatalog-Skill/SKILL.md <dein-projekt>/.codex/skills/fragenkatalog/SKILL.md
cp -r Fragenkatalog-Skill/templates <dein-projekt>/.codex/skills/fragenkatalog/templates
```

Danach im Codex-Prompt:

```
fragenkatalog setup
```

> [!NOTE]
> Beide Wrapper-Dateien greifen auf dieselbe `SKILL.md` zurück — die eigentliche Logik lebt nur
> dort. Detaillierte Installationsschritte inkl. Ordnerstruktur siehe [wiki/Setup.md](wiki/Setup.md).

### 🤖 Für KI-Agenten

Lies vor jedem Aufruf `SKILL.md` vollständig — sie ist die einzige verbindliche Spezifikation für
Verhalten, Datenmodell (`fragenkatalog.json`), Konfiguration (`.fragenkatalog-config`) und
HTML-Export-Struktur. Die Wrapper-Dateien unter `.claude/commands/` und `.codex/commands/`
duplizieren keine Logik.

## Erste Schritte

```
/fragenkatalog setup
  → Projektname, -typ, Plattform(en), Experten-Perspektive, Speicherpfad, Sprache

/fragenkatalog generate 50
  → 50 Fragen in sinnvollen Kategorien, sofort aus der gewählten Perspektive beantwortet
    (inkl. automatischer "Recht"-Kategorie, siehe unten)

/fragenkatalog export
  → docs/Fragenkatalog.html geschrieben — im Browser öffnen und loslegen
```

## Alle Befehle

| Befehl | Beschreibung |
|---|---|
| `/fragenkatalog-setup` | Interaktive Ersteinrichtung (Projekt, Plattform, Perspektive, Pfad, Sprache) |
| `/fragenkatalog-generate [anzahl]` | Initiale Fragenliste generieren + sofort beantworten |
| `/fragenkatalog-add-category <name>` | Neue Kategorie mit 5–30 Fragen hinzufügen |
| `/fragenkatalog-add-question <kategorie> <frage>` | Einzelne Frage manuell hinzufügen |
| `/fragenkatalog-answer <id-oder-suchtext>` | Bestehende Frage (neu) beantworten |
| `/fragenkatalog-export` | Finale self-contained HTML bauen/aktualisieren |
| `/fragenkatalog-import <pfad>` | Bestehende JSON/Markdown-Fragenliste importieren |
| `/fragenkatalog-stats` | Fortschrittsübersicht anzeigen |
| `/fragenkatalog-pfad <pfad>` | Speicherort der HTML ändern |
| `/fragenkatalog-perspektive <beschreibung>` | Experten-Perspektive ändern |

Details und Beispiele zu jedem Befehl: [wiki/Befehle.md](wiki/Befehle.md).

## HTML-Struktur / Datenmodell

Kanonisches Zwischenformat (liegt als `fragenkatalog.json` neben der Konfiguration und wird 1:1
in die HTML eingebettet):

```json
{
  "id": 1,
  "category": "Kern-Loop",
  "question": "Was ist die zentrale Spielhandlung, die der Spieler alle 30–60 Sekunden wiederholt?",
  "kiAnswer": "Baue einen klaren Ressourcen-Sammeln → Craften → Verbessern-Loop ...",
  "userAnswer": ""
}
```

Die exportierte HTML ist reines Vanilla-HTML/CSS/JS ohne CDN und ohne Framework
(`templates/Fragenkatalog.template.html`), mit Kategorie-Filter, Volltextsuche, Edit-Modus,
Modal-Dialog zum Bearbeiten/Hinzufügen/Löschen, localStorage-Persistenz und JSON-Import/-Export.
Technische Details: [wiki/HTML-Format.md](wiki/HTML-Format.md).

## Experten-Perspektiven

Die KI-Antwort in jeder Frage wird aus einer frei wählbaren Experten-Perspektive formuliert —
erkennbar am Präfix-Emoji (Default `💙`). Beispiele:

- "Blizzard Entertainment Lead Game Designer" (Spiele)
- "Naughty Dog Narrative Director" (Story-getriebene Spiele)
- "Y Combinator Partner" (Startups/Business-Pläne)
- "Erfahrener Verlagslektor" (Bücher/Romane)

Die Perspektive ist frei wählbar und jederzeit über `/fragenkatalog-perspektive` änderbar. Mehr
Beispiele und Formulierungstipps: [wiki/Experten-Perspektiven.md](wiki/Experten-Perspektiven.md).

## Rechtliche Fragen

> [!WARNING]
> Der Fragenkatalog-Skill ersetzt **keine Anwaltsleistung**. Die Kategorie "Recht" liefert
> ausschließlich allgemeine Orientierung zur eigenen Recherche.

Jeder generierte Katalog enthält standardmäßig eine Kategorie **"Recht"** mit projekttypischen
Rechercheragen (z. B. Jugendschutz, DSGVO, Urheberrecht, Plattform-Richtlinien, AGB/Impressum —
je nach Projekttyp). Anders als bei Design-Fragen antwortet die KI hier nicht aus einer frei
gewählten Kreativ-Persona, sondern mit einem eigenen Präfix (`⚖️` statt `💙`) und einem
**Pflicht-Disclaimer**, der jeder Antwort angehängt wird:

> "Dies ist keine Rechtsberatung, sondern eine allgemeine Orientierung zur Recherche. Für
> verbindliche Aussagen einen Anwalt/Fachberater für [Rechtsgebiet, Land] konsultieren."

Die Rechts-Kategorie wird bei `/fragenkatalog-setup` standardmäßig aktiviert und kann dort explizit
abgewählt werden. Details, Beispielfragen und das Antwort-Format:
[wiki/Rechtliche-Fragen.md](wiki/Rechtliche-Fragen.md).

## Wiki

| Seite | Inhalt |
|---|---|
| [Home](wiki/Home.md) | Einstieg, Konzept-Übersicht, Schnellreferenz |
| [Befehle](wiki/Befehle.md) | Jeder Slash-Befehl im Detail mit Beispiel-Ein-/Ausgabe |
| [HTML-Format](wiki/HTML-Format.md) | Technische Struktur der erzeugten HTML/des Datenmodells |
| [Experten-Perspektiven](wiki/Experten-Perspektiven.md) | Wie man gute Perspektiven-Prompts formuliert |
| [Rechtliche Fragen](wiki/Rechtliche-Fragen.md) | Disclaimer-Konzept, Beispielfragen, Antwortformat |
| [Setup](wiki/Setup.md) | Detaillierte Installationsanleitung für Claude Code und Codex |
| [Beispielprojekt](wiki/Beispielprojekt.md) | Durchgespieltes Mini-Beispiel "Sternenfänger" |
| [Verwandte MGD-Skills](wiki/Verwandte-Skills.md) | MGD_DEV_SKILL, MGD_Todo_SKILL, MGD_Living-Documentation und der automatische Begleit-Skills-Check |

## Grenzen

- **Kein Multiplayer-Sync**: Die HTML-Datei nutzt Browser-`localStorage` — Änderungen bleiben
  lokal im jeweiligen Browser. Für Team-Nutzung: Datei nach Bearbeitung exportieren
  (`/fragenkatalog-export` bzw. der Export-Button in der HTML) und im Repo committen.
- **Merge-Konflikte bei gleichzeitiger Bearbeitung**: Bearbeiten mehrere Personen parallel dieselbe
  `fragenkatalog.json`, sind klassische Merge-Konflikte möglich — es gibt keine automatische
  Konfliktauflösung.
- **KI-Antworten sind Vorschläge, keine Garantien** — das gilt für Design-Antworten ebenso wie,
  mit noch größerer Deutlichkeit, für die Rechts-Kategorie (siehe oben).

## Verwandte MGD-Projekte

Der Fragenkatalog-Skill ist Teil einer Familie von vier zusammengehörigen KI-Agenten-Skills für
Claude Code und ChatGPT Codex, die im selben Projekt oft gemeinsam sinnvoll sind:

| Projekt | Beschreibung | Mögliche Integration |
|---|---|---|
| [MGD_DEV_SKILL](https://github.com/MichaelGahnDESIGN/MGD_DEV_SKILL) | Release/Sync/Backup/Cleanup/Tests/Wissensdokumentation für das Projekt | Der Fragenkatalog-Stand wird vor einem Release Teil der Projekt-Wissensdokumentation |
| [MGD_Todo_SKILL](https://github.com/MichaelGahnDESIGN/MGD_Todo_SKILL) | Todo-Verwaltung als Skill für Claude Code/Codex, gleiches Namensschema und gleicher Aufbau | Unbeantwortete Fragen (leeres `userAnswer`) lassen sich als Todos exportieren, um sie gezielt abzuarbeiten |
| [MGD_Living-Documentation](https://github.com/MichaelGahnDESIGN/MGD_Living-Documentation) | Lebendige Projektdokumentation (Entscheidungen, offene Punkte, Risiken, Testnachweise) als HTML+Markdown | Unbeantwortete Fragen lassen sich als offene Punkte in die Living Documentation übernehmen |

> [!TIP]
> `/fragenkatalog-setup` prüft bei der Ersteinrichtung aktiv, ob diese drei Begleit-Skills im
> Projekt oder global bereits installiert sind, und bietet fehlende Skills zur Mitinstallation an
> (siehe `SKILL.md`, Abschnitt "Begleit-Skills-Check").

## Lizenz

MIT License, Copyright (c) 2026 Michael Gahn DESIGN — siehe [LICENSE](LICENSE).

Impressum: siehe Profil [MichaelGahnDESIGN](https://github.com/MichaelGahnDESIGN).

---

Entwickelt von Michael Gahn DESIGN — gepflegt mit Claude Code & ChatGPT Codex.
