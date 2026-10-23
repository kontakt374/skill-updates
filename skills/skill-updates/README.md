# skill-updates

Ein kleiner Claude-Code-Skill, der auf Zuruf prüft, ob für deine installierten
Plugin-Skills neuere Versionen vorliegen, und sie nach Bestätigung installiert.

Funktioniert auf Windows, Mac und Linux und braucht keine Zusatzinstallation –
die Prüfung macht Claude selbst, indem es die Plugin-Konfiguration liest und die
Versionen vergleicht.

## Verwenden

Sag Claude Code einfach z. B.:
- „gibt es Updates für meine Skills?"
- „prüf mal, ob meine Plugins aktuell sind"
- „bring meine Skills auf den neuesten Stand"

Claude listet gefundene Updates auf und installiert sie erst, wenn du zustimmst.
Nach einem Update einmal Claude Code neu starten.

## Installieren

**Claude Code (CLI, VS Code, Desktop):** Lege den Ordner `skill-updates` in dein
Skills-Verzeichnis:
- nur für dich: `~/.claude/skills/skill-updates/`
- für ein bestimmtes Projekt: `<projekt>/.claude/skills/skill-updates/`

Danach Claude Code neu starten. Fertig – der Skill meldet sich von selbst, wenn
er zum Anliegen passt.

**claude.ai:** Diese Ordner-Variante ist für Claude Code gedacht. Für claude.ai
kann der Ordner als `.skill`-Datei (ZIP) über „Skills → Skill hochladen"
eingespielt werden.

## Umfang

Geprüft werden Plugin-Skills aus GitHub-Marketplaces mit erkennbarer
Versionsnummer. Offizielle Anthropic-Plugins verwaltet Claude Code selbst; reine
Ordner-Skills und claude.ai-synchronisierte Skills werden nicht geprüft.
