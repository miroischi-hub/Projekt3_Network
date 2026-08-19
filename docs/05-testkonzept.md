# Testkonzept

Die Anforderungen des Projekts werden durch definierte Tests überprüft.

## Test 1 – Automatisierte Installation

**Ziel:** BorgBackup kann mit Ansible bereitgestellt werden.

**Durchführung:**

1. Neue Debian-VM bereitstellen.
2. VM zum Ansible-Inventar hinzufügen.
3. Playbook ausführen.
4. Installation und Konfiguration überprüfen.

**Erwartetes Resultat:**

BorgBackup ist installiert und die benötigte Konfiguration wurde
automatisch erstellt.

---

## Test 2 – Backup erstellen

**Ziel:** Ein Client kann Daten auf dem Backup-Server sichern.

**Durchführung:**

1. Testdateien unter `/srv/data/` erstellen.
2. Backup ausführen.
3. Borg-Archiv auflisten.
4. Inhalt überprüfen.

**Erwartetes Resultat:**

Alle definierten Testdateien befinden sich im Backup.

---

## Test 3 – Automatisches Backup

**Ziel:** Ein Backup wird ohne manuellen Eingriff erstellt.

**Durchführung:**

1. Neue Testdatei erstellen.
2. Automatischen Backup-Lauf abwarten.
3. Vorhandene Borg-Archive überprüfen.

**Erwartetes Resultat:**

Ein neues Backup wurde automatisch erstellt und enthält die Testdatei.

---

## Test 4 – Verschlüsselung

**Ziel:** Die Backup-Daten sind vor unberechtigtem Zugriff geschützt.

**Durchführung:**

Es wird versucht, ohne die erforderlichen Zugangsdaten auf die
gesicherten Inhalte zuzugreifen.

**Erwartetes Resultat:**

Die Inhalte können nicht gelesen werden.

---

## Test 5 – Rotation

**Ziel:** Nicht mehr benötigte Backupstände werden entfernt.

**Durchführung:**

1. Mehrere Backupstände vorbereiten.
2. Borg-Rotation ausführen.
3. Verbleibende Archive auflisten.
4. Resultat mit der definierten Aufbewahrungsstrategie vergleichen.

**Erwartetes Resultat:**

Es bleiben nur die vorgesehenen täglichen, wöchentlichen und
monatlichen Backups erhalten.

---

## Test 6 – Restore und Integrität

**Ziel:** Eine Datei kann vollständig wiederhergestellt werden.

**Durchführung:**

1. Testdatei erstellen.
2. SHA-256-Prüfsumme berechnen.
3. Backup erstellen.
4. Originaldatei löschen.
5. Datei aus dem Backup wiederherstellen.
6. SHA-256-Prüfsumme erneut berechnen.
7. Prüfsummen vergleichen.

Beispiel:

    sha256sum /srv/data/testfiles/test.txt

**Erwartetes Resultat:**

Die Prüfsumme der wiederhergestellten Datei entspricht der Prüfsumme
der ursprünglichen Datei.

---

## Test 7 – Neuer Client

**Ziel:** Ein weiterer Debian-Client kann automatisiert hinzugefügt
werden.

**Durchführung:**

1. Neue Debian-VM bereitstellen.
2. Client zum Ansible-Inventar hinzufügen.
3. Playbook ausführen.
4. Testdaten erstellen.
5. Backup durchführen.

**Erwartetes Resultat:**

Der neue Client kann erfolgreich ein Backup auf dem zentralen
Backup-Server erstellen.
