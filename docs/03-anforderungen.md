# Anforderungen

Das Backup-System soll folgende Anforderungen erfüllen.

## Funktionale Anforderungen

### Installation

BorgBackup soll mit Ansible auf den benötigten Systemen installiert und
konfiguriert werden können.

### Zentrales Backup

Mehrere Debian-Clients sollen ihre Daten auf einem zentralen
Backup-Server sichern können.

### Automatische Backups

Die Backups sollen regelmässig und ohne manuellen Eingriff ausgeführt
werden.

### Verschlüsselung

Die Borg-Repositories sollen verschlüsselt sein. Ohne die benötigten
Zugangsdaten sollen die gesicherten Inhalte nicht lesbar sein.

### Rotation

Alte Backups sollen automatisch anhand einer definierten
Aufbewahrungsstrategie entfernt werden.

### Restore

Einzelne Dateien sollen aus einem vorhandenen Backup wiederhergestellt
werden können.

### Datenintegrität

Nach einem Restore soll überprüft werden können, ob die
wiederhergestellte Datei mit dem Original übereinstimmt.

Dafür wird SHA-256 verwendet.

### Erweiterbarkeit

Ein neuer Debian-Client soll durch einen Eintrag im Ansible-Inventar
und die Ausführung des entsprechenden Playbooks in das Backup-System
aufgenommen werden können.

## Automatisierung

Ansible soll mindestens folgende Aufgaben übernehmen:

- Installation von BorgBackup
- Erstellung benötigter Benutzer
- Erstellung benötigter Verzeichnisse
- SSH-Konfiguration
- Vorbereitung der Backup-Repositories
- Bereitstellung der Backup-Konfiguration
- Einrichtung automatischer Backups
- Konfiguration der Backup-Rotation
