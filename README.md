# Farming Simulator 25 – Pelican/Pterodactyl Egg

Ein Egg für einen FS25 Dedicated Server mit dem Docker-Image
[`toetje585/arch-fs25server:latest`](https://github.com/wine-gameservers/arch-fs25server).

## Funktionen

- FS25-Installation und Lizenzaktivierung über noVNC
- Wine 11 und Headless-Audio-Konfiguration
- automatische DLC-Reihenfolge mit manueller Eingabe der Produktschlüssel
- freie Game-, Web- und noVNC-Ports
- persistente Mods, Savegames, DLCs und Lizenzdaten
- Kartenwahl über das GIANTS-Webinterface

## Installation

1. [`egg-farming-simulator-25.json`](./egg-farming-simulator-25.json) im
   Pelican-/Pterodactyl-Adminbereich importieren.
2. Ports zuweisen:
   - primär: `10823` TCP/UDP – Spielport
   - zusätzlich: `7999` TCP – GIANTS-Webinterface
   - zusätzlich: `6080` TCP – noVNC
3. FS25-IMG/ZIP/EXE nach `/home/container/installer` hochladen.
4. Server starten und noVNC öffnen:

   ```text
   http://SERVER-IP:6080/vnc.html?resize=remote&autoconnect=1
   ```

5. **FS25 installieren / aktivieren** öffnen und den Server-Key eingeben.

Eine separate GIANTS-Serverlizenz ist erforderlich. Die Steam-Version stellt
keinen passenden Server-Key bereit.

## DLCs

DLC-Installer als `FarmingSimulator25_*.exe`, `.img`, `.iso` oder `.zip` nach
`/home/container/dlc` hochladen und im Panel setzen:

```text
AUTO_INSTALL_DLC=true
```

Die Installer öffnen sich nacheinander in noVNC. Bereits installierte DLCs
werden übersprungen; die Produktschlüssel werden weiterhin manuell eingegeben.

## Mods und Savegames

```text
Mods:      /home/container/config/FarmingSimulator2025/mods
Savegames: /home/container/config/FarmingSimulator2025/savegame1
DLCs:      /home/container/config/FarmingSimulator2025/pdlc
Logs:      /home/container/logs
```

Mods als ZIP hochladen und nicht entpacken.

## Kartenwahl

`SERVER_MAP` leer lassen, wenn die Karte im GIANTS-Webinterface ausgewählt
werden soll. Die dort gespeicherte `mapID` und `mapFilename` bleiben über
Containerneustarts erhalten. Ein Wert in `SERVER_MAP` erzwingt diese Karte.

## Hinweis

Dieses Projekt ist nicht mit GIANTS Software verbunden. Spiel und DLCs müssen
regulär über GIANTS bezogen und für den Server aktiviert werden.
