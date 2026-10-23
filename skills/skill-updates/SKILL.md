---
name: skill-updates
description: Prüft auf Zuruf, ob für installierte Claude-Code-Plugin-Skills neuere Versionen vorliegen, und installiert gefundene Updates nach Bestätigung. Nutze diesen Skill immer, wenn jemand wissen will, ob seine Skills/Plugins aktuell sind oder sie aktualisieren möchte - auch bei Formulierungen wie "gibt es updates für meine skills", "sind meine skills aktuell", "prüf auf updates", "skill updates", "plugins aktualisieren", "update meine skills", "skills auf den neuesten stand bringen". Betrifft GitHub-Plugin-Skills (z. B. marketing-skills, superpowers, ui-ux-pro-max).
---

# Skill-Updates prüfen und anwenden

Dieser Skill prüft auf Zuruf, ob für installierte Plugin-Skills neuere Versionen bereitstehen, und wendet Updates nach Bestätigung an.

Der Skill ist bewusst ohne externes Skript und ohne feste Pfade gebaut, damit er auf jedem Rechner (Windows, Mac, Linux) ohne Zusatzinstallation funktioniert. Du führst die Prüfung selbst aus, indem du die Konfigurationsdateien liest und Versionen vergleichst.

Antworte in der Sprache der Nutzerin oder des Nutzers und halte die Ausgabe kurz und ohne Fachjargon.

## Wo die Daten liegen

Das Plugin-Verzeichnis von Claude Code liegt standardmäßig unter `~/.claude/plugins` (Heimatverzeichnis). Falls die Umgebungsvariable `CLAUDE_CONFIG_DIR` gesetzt ist, gilt stattdessen `$CLAUDE_CONFIG_DIR/plugins`. Ermittle den Heimatpfad betriebssystem-unabhängig.

Relevante Dateien:
- `<plugins>/installed_plugins.json` - was installiert ist, je Eintrag Schlüssel `"<plugin>@<marketplace>"` mit `version` und `gitCommitSha`.
- `<plugins>/marketplaces/<marketplace>/.claude-plugin/marketplace.json` - der aktuelle Stand im jeweiligen Marketplace (Claude Code frischt diese Klone beim Start auf).

## Ablauf

### 1. Installierte Plugins einlesen

Lies `installed_plugins.json` und gehe die Einträge unter `plugins` durch. Für jeden Eintrag `"<plugin>@<marketplace>"`:
- Merke dir die installierte `version` (erstes Element des Wert-Arrays).
- **Überspringe** Einträge, deren `version` eine reine Hex-Zeichenkette ohne Punkt ist (z. B. `465f09344424`). Das sind die offiziellen Anthropic-Plugins (z. B. code-review, skill-creator); die verwaltet Claude Code selbst und ihr Stand lässt sich lokal nicht sauber ablesen. Echte Versionsnummern enthalten Punkte (z. B. `2.13.0`).

### 2. Aktuelle Version je Plugin ermitteln

Öffne für jedes verbleibende Plugin die `marketplace.json` seines Marketplace und finde dort den Plugin-Eintrag mit passendem `name`:
- Hat der Eintrag ein Feld `version`, ist das die aktuelle Version.
- Fehlt `version` und die Quelle (`source`) ist ein lokaler Pfad (beginnt mit `.`, z. B. `"./"`), steht die Version in der `plugin.json` des Plugins: unter `<marketplace>/<source>/.claude-plugin/plugin.json` (sonst `<marketplace>/<source>/plugin.json`), Feld `version`.
- Lässt sich keine Version ermitteln, überspringe das Plugin still.

### 3. Vergleichen und melden

Vergleiche installierte mit aktueller Version.
- Weichen sie ab → Update verfügbar.
- Sind alle geprüften Plugins gleich → sag klar, dass alles aktuell ist. Fertig.

Bei gefundenen Updates nenne pro Plugin kurz Name, installierte und neue Version. Frage dann, ob du die Updates jetzt installieren sollst.

### 4. Updates anwenden (nur nach Bestätigung)

Erst nach Zustimmung führe für jedes gefundene Update den passenden Befehl aus:

```
claude plugin update <plugin>@<marketplace>
```

Berichte ehrlich, was zurückkommt (aktualisiert, oder bereits aktuell). Weise am Ende darauf hin, dass die Aktualisierungen erst nach einem **Neustart von Claude Code** greifen.

## Nicht abgedeckt

- **Offizielle Anthropic-Plugins**: verwaltet Claude Code selbst (siehe Schritt 1).
- **Reine Ordner-Skills** (ohne Marketplace) und **claude.ai-synchronisierte Skills**: Erstere haben keine Update-Quelle zum Prüfen, Letztere aktualisieren sich automatisch.
