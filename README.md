# skill-updates (Claude Code Marketplace)

Ein kleiner Claude-Code-Skill, der auf Zuruf prüft, ob für installierte
Plugin-Skills neuere Versionen vorliegen, und sie nach Bestätigung installiert.
Funktioniert auf Windows, Mac und Linux ohne Zusatzinstallation.

## Installieren

In Claude Code zwei Befehle ausführen (ersetze `DEIN-NAME/DEIN-REPO` durch die
Adresse dieses Repositorys, z. B. `maxmuster/skill-updates`):

```
claude plugin marketplace add DEIN-NAME/DEIN-REPO
claude plugin install skill-updates@skill-updates
```

Danach Claude Code neu starten.

## Verwenden

Sag Claude Code einfach z. B. „gibt es Updates für meine Skills?" oder
„bring meine Skills auf den neuesten Stand". Der Skill listet gefundene Updates
auf und installiert sie erst nach deiner Bestätigung.

## Umfang

Geprüft werden Plugin-Skills aus GitHub-Marketplaces mit erkennbarer
Versionsnummer. Offizielle Anthropic-Plugins verwaltet Claude Code selbst; reine
Ordner-Skills und claude.ai-synchronisierte Skills werden nicht geprüft.
