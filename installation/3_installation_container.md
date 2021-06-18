# Fertige Container-Images zur Entwicklung

```warning
Diese Anleitung befindet sich aktuell noch im Aufbau. Bei Fragen oder Unklarheiten hilft der [Support](../README.md#community-und-support) weiter.
```

## Installation

### Datenverzeichnis anlegen

Es wird ein Datenverzeichnis auf dem Host benötigt, in dem die Quelltext von ct-Bot und ct-Sim sowie die Einstellungen des Eclipse-Workspaces aufbewahrt werden. Im Folgenden wird dafür ein Unterverzeichnis `ctbot-data` angelegt und verwendet. Dort werden auch die Start-Skripte abgelegt, so dass der lokale Pfad zu diesem Datenverzeichnis jeweils einfach `.` ist.

```shell
mkdir ctbot-data && cd ctbot-data
```

```tip
Hat man eigenen Änderungen am Code vorgenommen, sollte man das Datenverzeichnis (hier `ctbot-data`) in sein Backup einschließen. Die komplette Installation inkl. IDE und Toolchains hingegen liegt im Container-Image und kann jederzeit wieder (im Ursprungszustand) heruntergeladen werden.
```

### Eclipse-Entwicklungsumgebung

```shell
wget https://github.com/tsandmann/ctbot-container/raw/master/run_eclipse.sh
chmod +x run_eclipse.sh
./run_eclipse.sh PATH_TO_DATADIR [VERSION]
# ./run_eclipse.sh . 2021-06
```

Als `VERSION` kann auch `latest` verwendet werden, um die aktuellste Version zu starten:
```shell
./run_eclipse.sh . latest
```

```note
Die Größe dieses Images beträgt ca. 1,4 GB.
```

```tip
Wurde Eclipse (oder die Eclipse-Einstellungen) "kaputtgespielt", kann die ganze Umgebung problemlos wieder auf die Ausgangswerte zurückgesetzt werden, siehe [Eclipse-Workspace bereinigen](#eclipse-workspace-bereinigen).
```

### Eclipse-Entwicklungsumgebung inkl. Raspberry-Pi-Toolchain

```shell
wget https://github.com/tsandmann/ctbot-container/raw/master/run_eclipse-rpi.sh
chmod +x run_eclipse-rpi.sh
./run_eclipse-rpi.sh PATH_TO_DATADIR [VERSION]
# ./run_eclipse-rpi.sh . latest
```

```note
Diese Variante wird nur benötigt, wenn der ct-Bot eine Raspberry-Pi-Erweiterung hat. Durch die zusätzliche Toolchain für den Raspberry Pi ist das Image ca. 2,5 GB groß.
```

### Standalone ct-Sim

```tip
Die ct-Sim-Images sind nützlich, falls nur der ct-Sim benötigt wird (z.B. wenn die Tools für die ct-Bot-Programmierung eh schon vorhanden sind), die Installation einer kompatiblen Java-Laufzeitumgebung aber vermieden werden soll oder nicht möglich ist. Die Größe dieser Images beträgt knapp 600 MB.
```

#### Release-Version

```shell
wget https://github.com/tsandmann/ctbot-container/raw/master/run_ctsim.sh
chmod +x run_ctsim.sh
./run_ctsim.sh PATH_TO_DATADIR [VERSION]
# ./run_ctsim.sh . 2.28
```

Als `VERSION` kann auch `latest` verwendet werden, um die aktuellste Version zu starten:
```shell
./run_ctsim.sh . latest
```

#### Entwicklungsversion

```shell
wget https://github.com/tsandmann/ctbot-container/raw/master/run_ctsim-dev.sh
chmod +x run_ctsim-dev.sh
./run_ctsim-dev.sh PATH_TO_DATADIR
# ./run_ctsim-dev.sh .
```

## Verwendung

### Ins Datenverzeichnis wechseln

```shell
cd ctbot-data
```

### Eclipse-Entwicklungsumgebung starten

```shell
./run_eclipse.sh PATH_TO_DATADIR [VERSION]
# ./run_eclipse.sh . 2021-06
```

oder 

```shell
./run_eclipse-rpi.sh PATH_TO_DATADIR [VERSION]
# ./run_eclipse-rpi.sh . 2021-06
```

Als `VERSION` kann jeweils auch `latest` verwendet werden, um die aktuellste Version zu starten, also z.B.:
```shell
./run_eclipse.sh . latest
```

### Eclipse-Workspace bereinigen

Wurde Eclipse (oder die Eclipse-Einstellungen) "kaputtgespielt", kann die ganze Umgebung wieder auf die Ausgangswerte zurückgesetzt werden (im Normalbetrieb nicht erforderlich):

```warning
Alle eigenen Eclipse-Einstellungen werden dabei gelöscht! Änderungen am Sourcecode der Projekte bleiben natürlich erhalten.
```

```shell
rm -rf .metadata
```

### Standalone ct-Sim starten

```shell
./run_ctsim.sh PATH_TO_DATADIR [VERSION]
# ./run_ctsim.sh . 2.28
```

Als `VERSION` kann auch `latest` verwendet werden, um die aktuellste Version zu starten:
```shell
./run_ctsim.sh . latest
```

### Weitere Features für Fortgeschrittene

#### Eigene Parameter

Hängt man an das Start-Skript weitere Parameter an, werden diese direkt an den `run`-Aufruf des Containers weitergereicht. So lassen sich z.B. weitere Verzeichnisse in den Container mounten, Programmier- bzw. USB-2-Bot-Adapter im Container verfügbar machen oder Ports forwarden.

Beispiele:
* USB-2-Bot-Adapter verwenden: `./run_eclipse.sh . 2021-06 --device=/dev/ttyUSB0`
* ct-Sim-Port forwarden: `./run_eclipse.sh . 2021-06 -p 10001:10001`

#### Benutzer im Container

Im Container wird der Benutzer `developer` mit der UID `1000` verwendet, das Passwort ist auf `ct-bot` gesetzt. Der Benutzer ist Mitglied der Gruppen `dialout` und `sudo`.

#### Persistente Container

Die Start-Skripte starten die Container mit der Option `--rm`, so dass sie nach dem Beenden automatisch entfernt werden. Somit erhält man bei jedem Start ein "frisches" System, Änderungen gelten nur für die Laufzeit des Containers. Entfernt man die `--rm`-Option im Start-Skript, erhält man einen persistenten Container, in man Änderungen auch in das Image committen kann. Dabei bietet es sich an, mit `--name` dem Container einen Namen zuzuweisen. Für weitere Informationen siehe <a href="http://docs.podman.io" target="_blank">Podman-Dokumentation</a> bzw. <a href="https://docs.docker.com" target="_blank">Docker-Dokumentation</a>.

### Container-Images aktualisieren

```shell
podman pull IMAGE_REPO:VERSION
# podman pull docker.io/tsandmann/ctbot-eclipse:2021-06
```
oder
```shell
docker pull IMAGE_REPO:VERSION
# docker pull docker.io/tsandmann/ctbot-eclipse:2021-06
```

Um die neueste verfügbare Version zu laden:
```shell
podman pull IMAGE_REPO:latest
# podman pull docker.io/tsandmann/ctbot-eclipse:latest
```

### Alte Container-Images aufräumen

```shell
podman image prune
```
oder
```shell
docker image prune
```

### Container-Images bauen

```shell
git clone https://github.com/tsandmann/ctbot-container.git
cd ctbot-container

./build_eclipse.sh VERSION 
# ./build_eclipse.sh 2021-06

./build_eclipse-rpi.sh VERSION
# ./build_eclipse-rpi.sh 2021-06

./build_ctsim.sh VERSION
# ./build_ctsim.sh 2.28
```

## Quellen

* Dockerfiles, Build- und Start-Skripte im <a href="https://github.com/tsandmann/ctbot-container" target="_blank">Github-Repository</a>

* Container-Images in der <a href="https://registry.hub.docker.com/u/tsandmann" target="_blank">Docker Hub Registry</a>
  * <a href="https://registry.hub.docker.com/r/tsandmann/ctbot-eclipse" target="_blank">Eclipse-Image</a>
  * <a href="https://registry.hub.docker.com/r/tsandmann/ctbot-eclipse-rpi" target="_blank">Eclipse-RPi-Image</a>
  * <a href="https://registry.hub.docker.com/r/tsandmann/ctsim" target="_blank">ct-Sim Standalone</a>
  * <a href="https://registry.hub.docker.com/r/tsandmann/ctsim-dev" target="_blank">ct-Sim Standalone Entwicklungsversion</a>

---

<a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank"><img src="images/license.svg" alt="License: CC BY-SA 4.0" style="left;margin-left:0;margin-right:1em;" /></a><br>
Autor: <a href="https://github.com/tsandmann" target="_blank" style="color:#3c454e;">Timo Sandmann</a> \| Stand: 18.06.2021
