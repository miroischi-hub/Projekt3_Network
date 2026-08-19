# Backupstrategie

## Zu sichernde Daten

Für das Projekt werden definierte Testdaten verwendet.

Beispiel:

/srv/data/
├── documents/
├── configuration/
└── testfiles/

Diese Verzeichnisse werden mit BorgBackup gesichert.

## Aufbewahrung

Folgende Aufbewahrungsstrategie ist vorgesehen:

| Typ | Anzahl |
| --- | ---: |
| Tägliche Backups | 7 |
| Wöchentliche Backups | 4 |
| Monatliche Backups | 3 |

Nicht mehr benötigte Backupstände sollen automatisch entfernt werden.

Die genaue Strategie kann während der Umsetzung angepasst werden,
sofern die Änderung begründet und dokumentiert wird.

## Sicherheit

Die Backup-Infrastruktur soll folgende Sicherheitsanforderungen
erfüllen:

- Übertragung über SSH
- Authentifizierung mittels SSH-Schlüsseln
- verschlüsselte Borg-Repositories
- Zugriff nur für vorgesehene Benutzer
- keine unverschlüsselte Speicherung der Backup-Daten
