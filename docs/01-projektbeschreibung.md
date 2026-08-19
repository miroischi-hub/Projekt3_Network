## 1. Projektbeschreibung

Im Rahmen dieses Projekts soll ein automatisiertes Backup- und Restore-System für mehrere Debian-Server geplant und umgesetzt werden.

Für die Datensicherung wird **BorgBackup** verwendet. Die Backups werden von mehreren Debian-Clients auf einem zentralen Backup-Server gespeichert.

Die Installation und Konfiguration der beteiligten Systeme soll mit **Ansible** automatisiert werden. Dadurch soll die Backup-Infrastruktur reproduzierbar aufgebaut und um weitere Clients erweitert werden können.

Neben der Erstellung von Backups werden insbesondere folgende Themen untersucht und umgesetzt:

- Automatisierung mit Ansible
- Backup über das Netzwerk
- SSH-Kommunikation
- Verschlüsselung der Backups
- Automatische Durchführung von Backups
- Aufbewahrung und Rotation alter Backups
- Wiederherstellung von Daten
- Überprüfung der Datenintegrität

Das Ziel besteht somit nicht nur darin, BorgBackup zu installieren, sondern ein automatisiertes, reproduzierbares und überprüfbares Backup-System aufzubauen.
