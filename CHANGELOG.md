# Changelog

Alle nennenswerten Änderungen an diesem Projekt werden in dieser Datei dokumentiert.

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
