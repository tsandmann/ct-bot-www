# Verwendung von Visual Studio Code

## Code compilieren

1. Mit Strg + Alt + T die Taskauswahl öffnen und `PlatformIO` wählen:

    <img src="images/build-vsc-01.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

### Für MCU

1. `PlatformIO: Build` baut die Standardkonfiguration (ATmega 1284P):

    <img src="images/build-vsc-02.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

1. Das Ergebnis ist anschließend in der Konsolenausgabe unten zu sehen:

    <img src="images/build-vsc-03.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

### Für PC

1. Zuerst die Projekt-Umgebung auf `native` umstellen, dazu unten in der Statusleiste auf `Switch PlatformIO Project Environment` klicken und in der Auswahlliste `env:native` auswählen:

    <img src="images/build-vsc-04.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

1. Dann mit Strg + Alt + T die Taskauswahl öffnen und `PlatformIO` -> `PlatformIO: Build (native)` wählen:

    <img src="images/build-vsc-05.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

1. Das Ergebnis ist anschließend in der Konsolenausgabe unten zu sehen:

    <img src="images/build-vsc-06.png" width="1000" style="display:block;margin-left:0;margin-right:auto;">

```tip
Um den simulierten Bot zu starten, auf einer Konsole ins Verzeichnis des ct-Bot-Projekts wechseln und `.pio/build/native/program` aufrufen.
```

## Firmware flashen

```danger
ToDo: Beschreibung der Programmieradapter-Einstellung und des Flashvorgangs
```

## Remote-Entwicklung

### SSH

```danger
ToDo: Beschreibung der Möglichkeiten zur Entwicklung auf einem Remote-System über SSH.
```

### WSL

```danger
ToDo: Beschreibung der Möglichkeiten zur Entwicklung unter Windows mit WSL.
```

---

<a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank"><img src="images/license.svg" alt="License: CC BY-SA 4.0" style="left;margin-left:0;margin-right:1em;" /></a><br>
Autor: <a href="https://github.com/tsandmann" target="_blank" style="color:#3c454e;">Timo Sandmann</a> \| Stand: 20.12.2020
