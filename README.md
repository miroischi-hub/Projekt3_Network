# Projekt 3 – Automatisiertes Backup-System

## Kurzbeschreibung

In diesem Projekt soll ein automatisiertes Backup- und Restore-System für mehrere Debian-Server aufgebaut werden.

Für die Datensicherung wird **BorgBackup** eingesetzt. Die Backups werden über SSH auf einem zentralen Backup-Server gespeichert. Die Installation und Konfiguration der Systeme wird mit **Ansible** automatisiert.

Der Schwerpunkt liegt auf:

* automatisierten Backups
* zentraler Speicherung
* Verschlüsselung
* Backup-Rotation
* Wiederherstellung
* Überprüfung der Datenintegrität
* Automatisierung mit Ansible

## Dokumentation

Die detaillierte Projektspezifikation befindet sich im Verzeichnis `docs/`.

* [Projektbeschreibung](docs/01-projektbeschreibung.md)
* [Architektur](docs/02-architektur.md)
* [Anforderungen](docs/03-anforderungen.md)
* [Backupstrategie](docs/04-backupstrategie.md)
* [Testkonzept](docs/05-testkonzept.md)
* [Abgrenzung](docs/06-abgrenzung.md)
