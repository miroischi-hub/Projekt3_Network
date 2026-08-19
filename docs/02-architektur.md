# Architektur

## Systeme

Für das Projekt sind folgende Debian-VMs vorgesehen:

- 1 Ansible Control Node
- 1 Backup-Server
- 3 Backup-Clients

## Aufbau

<img width="1527" height="654" alt="Unbenannt" src="https://github.com/user-attachments/assets/24a52198-dee0-47f2-be78-ffb4a4567693" />

## Ansible Control Node

Der Ansible Control Node übernimmt die zentrale Konfiguration der
Infrastruktur. Von diesem System werden die Ansible-Playbooks ausgeführt.

## Backup-Clients

Die Clients enthalten die zu sichernden Daten. Definierte Verzeichnisse
werden mit BorgBackup auf den zentralen Backup-Server übertragen.

## Backup-Server

Der Backup-Server stellt die Borg-Repositories bereit. Die Sicherungen
werden dadurch getrennt von den Originaldaten der Clients gespeichert.

## Kommunikation

Ansible verwendet SSH zur Administration der Systeme.

Auch die Übertragung der Backups zwischen den Clients und dem
Backup-Server erfolgt über SSH.
