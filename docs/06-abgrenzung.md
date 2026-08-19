# Abgrenzung und Erfolgskriterien

## Abgrenzung

Der Schwerpunkt des Projekts liegt auf BorgBackup, Debian, SSH und
Ansible.

Nicht Bestandteil des Projekts sind:

- Windows-Backups
- Cloud-Backup-Dienste
- grafische Backup-Oberflächen
- georedundante Backups
- High Availability des Backup-Servers
- vollständige Disaster-Recovery-Automatisierung
- vollständige VM-Backups

Diese Funktionen können als mögliche spätere Erweiterungen betrachtet
werden.

## Erfolgskriterien

Das Projekt gilt als erfolgreich, wenn:

- mehrere Debian-Clients gesichert werden können,
- die Konfiguration mit Ansible reproduzierbar ist,
- die Backup-Übertragung über SSH funktioniert,
- die Backups verschlüsselt gespeichert werden,
- Backups automatisch ausgeführt werden,
- alte Backups automatisch rotiert werden,
- Dateien erfolgreich wiederhergestellt werden können,
- die Integrität mittels SHA-256 überprüft werden kann,
- und ein neuer Client über Ansible integriert werden kann.

## Erwartetes Resultat

Am Ende soll eine funktionierende und reproduzierbare Backup-Infrastruktur
vorhanden sein.

Das Projekt soll zeigen, wie mehrere Linux-Systeme mit BorgBackup,
Ansible und SSH zentral, verschlüsselt und automatisiert gesichert
werden können.

Ein besonderes Augenmerk liegt auf dem Restore. Ein Backup gilt nur
dann als erfolgreich, wenn die gesicherten Daten zuverlässig
wiederhergestellt und überprüft werden können.
