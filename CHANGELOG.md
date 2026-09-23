# Changelog

Alle nennenswerten Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

## Unreleased

- `SKILL.md`: `/fragenkatalog-setup` prüft jetzt einmalig aktiv (per konkretem Datei-/Ordner-Check,
  projekt-lokal und global, Claude Code und Codex) auf die drei Begleit-Skills MGD_DEV_SKILL,
  MGD_Todo_SKILL und MGD_Living-Documentation und bietet fehlende Skills zur Mitinstallation an
  (git clone + Kopieren gemäß deren dokumentierter Zielstruktur; bei fehlendem Netzzugriff nur als
  Anleitung).
- `README.md`: Abschnitt "Verwandte MGD-Projekte" um MGD_DEV_SKILL und MGD_Living-Documentation
  ergänzt (bisher nur MGD_Todo_SKILL) sowie Hinweis auf den automatischen Begleit-Skills-Check.
- `wiki/Verwandte-Skills.md` (neu): Übersicht der drei Begleit-Skills und ihres Zusammenspiels mit
  dem Fragenkatalog, verlinkt von `wiki/Home.md` und `README.md`.

## 1.0.0 - Initial Release

- `SKILL.md`: vollständige Spezifikation aller Befehle (`setup`, `generate`, `add-category`,
  `add-question`, `answer`, `export`, `import`, `stats`, `pfad`, `perspektive`) inkl.
  kanonischem Datenmodell (`{category, question, kiAnswer, userAnswer}`).
- `templates/Fragenkatalog.template.html`: funktionsfähige, self-contained Start-Vorlage —
  Kategorie-Filter, Volltextsuche, Edit-Modus mit Modal, localStorage-Persistenz,
  JSON-Import/-Export, XSS-sicheres Rendering, keine externen Abhängigkeiten.
- Slash-Command-Wrapper für Claude Code (`.claude/commands/fragenkatalog.md`) und ChatGPT Codex
  (`.codex/commands/fragenkatalog.md`).
- Ausführliches `README.md` mit Installationsanleitung, Befehlsübersicht, Datenmodell-Erklärung
  und Konzept der Experten-Perspektiven.
- Wiki-Inhalte unter `wiki/` (Home, Befehle, HTML-Format, Experten-Perspektiven, Setup,
  Beispielprojekt).
- `LICENSE` (MIT, Michael Gahn DESIGN).
