# Projekt 3 – Projektspezifikation

## Automatisiertes Backup-System mit BorgBackup und Ansible

**Kurs:** Netzwerkbetriebssysteme  
**Projekt:** Projekt 3  
**Thema:** Backup und Automatisierung

---

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

---

## 2. Projektziele

Das Hauptziel ist der Aufbau einer zentralen Backup-Infrastruktur für mehrere Debian-Systeme.

Folgende Ziele sollen erreicht werden:

1. BorgBackup wird auf den benötigten Systemen mit Ansible installiert.
2. Die Backup-Clients können Daten auf einen zentralen Backup-Server sichern.
3. Die Kommunikation zwischen Client und Backup-Server erfolgt über SSH.
4. Die Backups werden verschlüsselt gespeichert.
5. Backups werden automatisch und regelmässig ausgeführt.
6. Alte Backups werden anhand einer definierten Aufbewahrungsstrategie automatisch entfernt.
7. Einzelne Dateien können aus einem Backup wiederhergestellt werden.
8. Die Integrität wiederhergestellter Dateien kann überprüft werden.
9. Neue Debian-Clients können über das Ansible-Inventar in das Backup-System aufgenommen werden.

---

## 3. Architektur

Für das Projekt werden mehrere Debian-VMs verwendet.

Geplant sind:

- 1 Ansible Control Node
- 1 zentraler Backup-Server
- 3 Debian Backup-Clients

### Architekturdiagramm

```text
                       +---------------------+
                       | Ansible Control Node|
                       |                     |
                       | Playbooks           |
                       | Inventory           |
                       +----------+----------+
                                  |
                              Ansible / SSH
                                  |
               +------------------+------------------+
               |                  |                  |
               v                  v                  v
        +-------------+    +-------------+    +-------------+
        | Debian      |    | Debian      |    | Debian      |
        | Client 01   |    | Client 02   |    | Client 03   |
        |             |    |             |    |             |
        | Testdaten   |    | Testdaten   |    | Testdaten   |
        +------+------+    +------+------+    +------+------+
               |                  |                  |
               +------------------+------------------+
                                  |
                             Borg / SSH
                                  |
                                  v
                        +-------------------+
                        |   Backup Server   |
                        |      Debian       |
                        |                   |
                        | Borg Repositories |
                        +-------------------+
```

### Komponenten

#### Ansible Control Node

Der Ansible Control Node soll die zentrale Konfiguration der Infrastruktur übernehmen.

Von diesem System aus werden die Ansible-Playbooks ausgeführt.

#### Backup-Clients

Die Debian-Clients enthalten die Daten, die gesichert werden sollen.

Jeder Client soll definierte Verzeichnisse über BorgBackup auf den Backup-Server sichern.

#### Backup-Server

Der Backup-Server stellt den zentralen Speicherort für die Borg-Repositories bereit.

Die Backup-Daten werden getrennt von den ursprünglichen Daten der Clients gespeichert.

---

## 4. Automatisierung mit Ansible

Die Installation und Konfiguration soll soweit möglich automatisiert erfolgen.

Ansible soll mindestens folgende Aufgaben übernehmen:

- Installation von BorgBackup
- Erstellung benötigter Benutzer
- Erstellung benötigter Verzeichnisse
- Konfiguration der SSH-Kommunikation
- Vorbereitung der Borg-Repositories
- Bereitstellung der Backup-Konfiguration
- Einrichtung der automatischen Backup-Ausführung
- Konfiguration der Backup-Rotation

Ein neuer Backup-Client soll durch einen Eintrag im Ansible-Inventar und die anschliessende Ausführung des Playbooks in die Backup-Infrastruktur aufgenommen werden können.

Dadurch soll vermieden werden, jeden Client vollständig von Hand konfigurieren zu müssen.

---

## 5. Zu sichernde Daten

Für die Umsetzung werden definierte Testdaten verwendet.

Ein mögliches Verzeichnis auf den Clients ist:

```text
/srv/data/
├── documents/
├── configuration/
└── testfiles/
```

Diese Verzeichnisse sollen durch BorgBackup gesichert werden.

Für die Tests können unterschiedliche Dateien erstellt werden, beispielsweise:

- Textdateien
- Konfigurationsdateien
- grössere Binärdateien
- mehrere Verzeichnisse und Unterverzeichnisse

---

## 6. Backup-Strategie

Die Backups sollen automatisch in regelmässigen Abständen durchgeführt werden.

Als Aufbewahrungsstrategie ist vorgesehen:

| Backup-Typ | Aufbewahrung |
|---|---:|
| Täglich | 7 |
| Wöchentlich | 4 |
| Monatlich | 3 |

Somit sollen beispielsweise die letzten sieben täglichen, vier wöchentlichen und drei monatlichen Backupstände erhalten bleiben.

Ältere, nicht mehr benötigte Backupstände sollen automatisch entfernt werden.

Die konkrete Strategie kann während der Umsetzung angepasst werden, sofern die Änderung technisch begründet und dokumentiert wird.

---

## 7. Sicherheit

Die Backup-Infrastruktur soll grundlegende Sicherheitsanforderungen erfüllen.

Dazu gehören:

- Übertragung der Backups über SSH
- Authentifizierung mittels SSH-Schlüsseln
- verschlüsselte Borg-Repositories
- Zugriff auf die Backup-Daten nur durch vorgesehene Benutzer
- keine unverschlüsselte Speicherung der Backup-Daten

Damit soll verhindert werden, dass ein nicht autorisierter Benutzer ohne die benötigten Zugangsdaten auf die gesicherten Inhalte zugreifen kann.

---

## 8. Testkonzept

Die Projektziele sollen mit definierten Tests überprüft werden.

### 8.1 Automatisierte Installation

**Ziel:**  
BorgBackup und die benötigte Konfiguration können mit Ansible bereitgestellt werden.

**Test:**  
Das Ansible-Playbook wird auf einem neu installierten Debian-Client ausgeführt.

**Erwartetes Resultat:**  
BorgBackup ist installiert und der Client verfügt über die benötigte Backup-Konfiguration.

---

### 8.2 Backup-Erstellung

**Ziel:**  
Ein Client kann seine Daten auf dem Backup-Server sichern.

**Test:**

1. Testdateien unter `/srv/data/` erstellen.
2. Backup ausführen.
3. Inhalt des erstellten Borg-Archivs anzeigen.
4. Überprüfen, ob die Testdateien vorhanden sind.

**Erwartetes Resultat:**  
Alle definierten Testdateien befinden sich im Backup.

---

### 8.3 Automatische Backup-Ausführung

**Ziel:**  
Backups werden ohne manuellen Eingriff ausgeführt.

**Test:**

1. Automatische Backup-Ausführung konfigurieren.
2. Eine neue Testdatei erstellen.
3. Den nächsten automatischen Backup-Lauf abwarten.
4. Borg-Archive auf dem Backup-Server überprüfen.

**Erwartetes Resultat:**  
Ein neues Backup wurde automatisch erstellt und enthält die neue Testdatei.

---

### 8.4 Verschlüsselung

**Ziel:**  
Die gespeicherten Backups sind verschlüsselt.

**Test:**  
Es wird versucht, ohne die erforderlichen Zugangsdaten auf das Borg-Repository und dessen gesicherte Inhalte zuzugreifen.

**Erwartetes Resultat:**  
Die gesicherten Inhalte können ohne die benötigten Zugangsdaten nicht gelesen werden.

---

### 8.5 Backup-Rotation

**Ziel:**  
Alte Backupstände werden anhand der definierten Aufbewahrungsstrategie entfernt.

**Test:**

1. Mehrere Backupstände erstellen bzw. für den Rotationstest vorbereiten.
2. Rotation mit Borg ausführen.
3. Verbleibende Archive auflisten.
4. Archive mit der definierten Aufbewahrungsstrategie vergleichen.

**Erwartetes Resultat:**  
Es bleiben nur die Backupstände erhalten, die laut Aufbewahrungsstrategie benötigt werden.

---

### 8.6 Restore-Test

**Ziel:**  
Eine gesicherte Datei kann vollständig wiederhergestellt werden.

**Test:**

1. Eine Testdatei erstellen.
2. SHA-256-Prüfsumme der Datei berechnen und speichern.
3. Backup durchführen.
4. Originaldatei löschen.
5. Datei aus dem Borg-Backup wiederherstellen.
6. SHA-256-Prüfsumme der wiederhergestellten Datei berechnen.
7. Beide Prüfsummen vergleichen.

Beispiel:

```bash
sha256sum /srv/data/testfiles/test.txt
```

**Erwartetes Resultat:**  
Die SHA-256-Prüfsumme der wiederhergestellten Datei entspricht der Prüfsumme der ursprünglichen Datei.

Damit wird nachgewiesen, dass die Datei korrekt wiederhergestellt wurde.

---

### 8.7 Integration eines neuen Clients

**Ziel:**  
Die Backup-Infrastruktur kann um einen weiteren Debian-Client erweitert werden.

**Test:**

1. Neue Debian-VM bereitstellen.
2. VM zum Ansible-Inventar hinzufügen.
3. Ansible-Playbook ausführen.
4. Testdaten auf dem neuen Client erstellen.
5. Backup durchführen.
6. Borg-Archiv überprüfen.

**Erwartetes Resultat:**  
Der neue Client ist korrekt konfiguriert und kann seine Daten auf dem Backup-Server sichern.

---

## 9. Abgrenzung

Der Schwerpunkt des Projekts liegt auf BorgBackup, Linux und der Automatisierung mit Ansible.

Folgende Themen sind nicht Bestandteil des geplanten Projektumfangs:

- Backups von Windows-Systemen
- Cloud-Backup-Dienste
- grafische Backup-Oberflächen
- georedundante Backup-Systeme
- High-Availability des Backup-Servers
- vollständige Disaster-Recovery-Automatisierung
- Backups kompletter virtueller Maschinen

Diese Funktionen könnten später als Erweiterungen umgesetzt werden.

---

## 10. Erfolgskriterien

Das Projekt gilt als erfolgreich umgesetzt, wenn folgende Kriterien erfüllt sind:

- Mehrere Debian-Clients können Daten auf den zentralen Backup-Server sichern.
- Die Installation und Konfiguration kann mit Ansible reproduziert werden.
- Die Backup-Übertragung funktioniert über SSH.
- Backups werden verschlüsselt gespeichert.
- Backups können automatisch ausgeführt werden.
- Alte Backupstände werden nach einer definierten Strategie rotiert.
- Einzelne Dateien können wiederhergestellt werden.
- Die Integrität einer wiederhergestellten Datei kann mittels SHA-256 überprüft werden.
- Ein zusätzlicher Debian-Client kann über Ansible in die Infrastruktur integriert werden.

---

## 11. Erwartetes Resultat

Am Ende des Projekts soll eine funktionierende und reproduzierbare Backup-Infrastruktur vorhanden sein.

Durch die Kombination von **BorgBackup**, **SSH**, **Debian** und **Ansible** soll gezeigt werden, wie Backups mehrerer Linux-Systeme zentral, verschlüsselt und automatisiert durchgeführt werden können.

Neben der eigentlichen Datensicherung liegt ein Schwerpunkt auf der Wiederherstellung. Ein Backup gilt erst dann als erfolgreich, wenn die gesicherten Daten zuverlässig wiederhergestellt und auf ihre Integrität überprüft werden können.