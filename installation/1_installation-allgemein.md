# Installationsanleitung für ct-Bot und ct-Sim

```tip
Wer auf seinem (Linux-)System podman oder docker installiert hat, kann alternativ zur manuellen Installation wie in dieser Anleitung beschrieben auch fertige Container-Images verwenden, die bereits alle Tools für die ct-Bot-Entwicklung mitbringen. Eine entsprechende Anleitung ist unter [Fertige Container-Images zur Entwicklung](3_installation_container.md) zu finden.
```

## I. Entwicklungsumgebung und Java-Laufzeit

### 1. Java installieren
    
* **Linux**: Java SE 8 **JDK** (OpenJDK) am besten über die Paketverwaltung installieren, empfohlen für ct-Sim ist **Version 1.8**.
    * Debian 10: 
    ```shell
    sudo apt-get install --no-install-recommends apt-transport-https ca-certificates wget dirmngr gnupg software-properties-common fontconfig
    wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -
    sudo add-apt-repository https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
    sudo apt-get update
    sudo apt-get install adoptopenjdk-8-hotspot
    ```
    ```warning
    Unter Debian 11 ist die Darstellung des ct-Sim fehlerhaft, z.B. wird die Welt zu dunkel angezeigt. Die Ursache hierfür ist derzeit unbekannt, vermutlich ein Java3D-Problem.
    ```

    * Debian 12: 
    ```shell
    sudo apt-get install --no-install-recommends apt-transport-https ca-certificates wget dirmngr gnupg software-properties-common fontconfig mesa-utils libgl1-mesa-glx libgl1-mesa-dri
    wget -qO - https://repos.azul.com/azul-repo.key | sudo gpg --dearmor -o /usr/share/keyrings/azul.gpg
    echo "deb [signed-by=/usr/share/keyrings/azul.gpg] https://repos.azul.com/zulu/deb stable main" | sudo tee -a /etc/apt/sources.list.d/zulu.list
    sudo apt-get update
    sudo apt-get install zulu8-jdk
    ```

    * RHEL/Rocky 8/9, Fedora:
    ```shell
    sudo dnf install java-1.8.0-openjdk libXxf86vm mesa-libGL mesa-dri-drivers
    ```
* **macOS**: 
    * Java SE 8 **JDK** (OpenJDK) [herunterladen](https://adoptium.net/?variant=openjdk8) und installieren. *Getestete Version: jdk8u332-b09*.
    * Alternativ kann unter macOS auch der Paketmanager [Homebrew](https://brew.sh) verwendet werden:
    ```shell
    brew tap adoptopenjdk/openjdk
    brew install adoptopenjdk8
    ```

* **Windows 10/11**: 
    * Java SE 8 **JDK** (OpenJDK) [herunterladen](https://adoptium.net/?variant=openjdk8) und installieren. *Getestete Version: jdk8u332-b09*.

```warning
Teilweise funktionert auch ein (Open) JDK in Version 11, das beispielsweise bei Debian in den offiziellen Paketquellen enthalten ist. Allerdings kann Java 11 zu [Problemen](https://bugs.launchpad.net/ubuntu/+source/openjdk-lts/+bug/1838740) mit Java3D führen, daher wird das ältere Java 8 (1.8) empfohlen und in dieser Anleitung verwendet.
```

### 2. Eclipse installieren
[Eclipse](https://de.wikipedia.org/wiki/Eclipse_(IDE)) herunterladen und installieren, siehe [Anleitung zur Einrichtung von Eclipse](2_installation-eclipse.md). *Getestete Version: Eclipse 2022‑03*.

```note
Alternativ kann auch [Visual Studio Code](https://de.wikipedia.org/wiki/Visual_Studio_Code) (VSCode) als IDE verwendet werden, zur Installation siehe [Anleitung zur Einrichtung von Visual Studio Code und PlatformIO](https://docs.platformio.org/en/latest/integration/ide/vscode.html#installation). Schritt III. entfällt dann ebenfalls, weil [PlatformIO](https://docs.platformio.org/en/latest/index.html) als Buildsystem verwendet wird.
```

## II. Compiler für simulierte Bots (x86)

* **Linux**: gcc Toolchain über die Paketverwaltung installieren:
  * Debian 10/11/12:
  ```shell
  sudo apt-get install build-essential manpages-dev git
  ```
  * RHEL/Rocky 8/9, Fedora:
  ```shell
  sudo dnf groupinstall "Development Tools"
  sudo dnf install gcc-c++
  ```
* **macOS**: [Xcode](https://itunes.apple.com/de/app/xcode/id497799835?mt=12) installieren, im Terminal `xcode-select --install` ausführen, um die Command Line Tools zu installieren.
* **Windows 10/11**:
  1. msys2 installieren (siehe auch [msys2 Installationsanleitung](http://msys2.github.io)):
     1. Installer [hier](http://msys2.github.io) herunterladen (`msys2-x86_64-*.exe`) und ausführen.
     1. Als Installationsordner `C:\msys64` verwenden (wie gehen hier von der 64-Bit Version aus).
  1. gcc von msys2 installieren:
     1. *MSYS2 MSYS Shell* starten.
     1. `pacman -Suy` ausführen, um msys2 zu aktualisieren.
     1. `pacman -S --needed base-devel mingw-w64-x86_64-toolchain make` ausführen, um gcc Toolchain zu installieren.
  1. Path-Einträge in Eclipse ergänzen:
     1. In Eclipse `Window` -> `Preferences` -> `C/C++` -> `Build` -> `Environment` öffnen.
     1. Dann `Select...` -> `Path` -> `Edit...` auswählen.
     1. Am **Anfang** `C:\msys64\usr\bin;C:\msys64\mingw64\bin;` hinzufügen.
  1. Für VSCode oder Commanline-Builds die systemweiten Path-Einträge ergänzen:
     1. Siehe <a href="https://bodo-schoenfeld.de/umgebungsvariablen-in-windows-10-bearbeiten/" target="_blank">Umgebungsvariablen in Windows 10 bearbeiten</a> zum Bearbeiten
     1. Für die Variable `Path` die folgenden Einträge hinzufügen: `C:\msys64\usr\bin` und `C:\msys64\mingw64\bin`

## III. Compiler und Tools für reale Bots (ATmega)

```note
Dieser Schritt ist nicht erforderlich, wenn Visual Studio Code als IDE mit PlatformIO verwendet wird, die nötigen Tools werden in diesem Fall automatisch eingerichtet.
```

* **Linux**: 
  * Debian 10/11/12:
    ```shell
    sudo apt-get install gcc-avr avr-libc avrdude
    ```
  * Fedora:
    ```shell
    sudo dnf install avr-gcc-c++ avr-libc avr-libc-doc avrdude
    ```
  * RHEL/Rocky 8/9: **AVR Toolchain for Linux** von [hier](https://www.microchip.com/mplab/avr-support/avr-and-arm-toolchains-c-compilers) (**8-bit** Version) herunterladen und z.B. nach `/usr/local/` entpacken. *Getestete Version: 3.7.0*.
* **macOS**: **AVR Toolchain for Darwin** [herunterladen](https://www.microchip.com/mplab/avr-support/avr-and-arm-toolchains-c-compilers) (**8-bit** Version) und entpacken nach `/usr/local/`. *Getestete Version: 3.7.0*.
* **Windows 10/11**: **AVR Toolchain for Windows** [herunterladen](https://www.microchip.com/mplab/avr-support/avr-and-arm-toolchains-c-compilers) und installieren. Das Installationsprogramm sollte man dabei explizit als Administrator ausführen (via Kontextmenü), sonst schlägt der Installer einen komischen Installationsort vor anstatt höhere Rechte anzufordern. *Getestete Version: 3.7.0*.

* Den Pfad zum avr-gcc (Unterverzeichnis `bin`) in Eclipse zum **PATH** hinzufügen, falls die Toolchain nicht über einen (Linux-) Paketmanager installiert wurde:
   1. In Eclipse `Window` -> `Preferences` -> `C/C++` -> `Build` -> `Environment` öffnen.
   1. Dann `Select...` -> `Path` -> `Edit...` auswählen.
   1. Am **Ende** `;C:\Program Files (x86)\avr8-gnu-toolchain\bin` (Windows) bzw. `:/usr/local/avr8-gnu-toolchain-linux_x86/bin` (Linux) oder `:/usr/local/avr8-gnu-toolchain-darwin_x86_64/bin` (macOS) hinzufügen.

## IV. Code für Bot und Sim importieren

Der Code steht im GIT-Repository zur Verfügung, siehe [Import des Codes von GitHub in Eclipse](../repository/1_git-eclipse.md) oder [Import des Codes von GitHub in VSCode](../repository/2_git-vsc.md).

## V. Installation Testen und nächste Schritte

```tip
Evtl. bekommt man in Eclipse Warnings ähnlich der Folgenden angezeigt: *Program "arm-linux-gnueabihf-g++" not found in PATH* Diese kann man ignorieren, wenn man das zugehörige Target nicht braucht (z.B. Build für Raspberry Pi im Falle von arm-linux-gnueabihf). Um die Warnings zu entfernen kann man die nicht benötigten Configurations in den Projekteinstellungen unter `C/C++ Build` -> `Manage Configurations...` löschen.
```

### ct-Sim und virtuelle Bots starten

1. ct-Sim starten. Hierzu gibt es drei Möglichkeiten:
    * Fertiges ct-Sim Release als jar-Archiv *ct-Sim.jar* <a href="https://github.com/tsandmann/ct-sim/releases" target="_blank">hier</a> herunterladen und von der Kommandozeile mit `java -jar ct-Sim.jar` starten.

      ```note
      Sind mehrere Java-Versionen auf dem System installiert, muss `java` durch den vollen Pfad zur Java-Version 8 ersetzt werden, z.B. `/usr/lib/jvm/java-1.8.0/bin/java`.
      ```

      ```tip
      Dies ist die bevorzugte Methode, wenn der Simulator nicht weiterentwickelt werden soll. Der Sourcecode ist dann nicht erforderlich, daher muss das git-Repository *ct-sim* nicht geladen werden.
      ```
    * In **Eclipse** klickt man die Datei `ctSim/controller/Main.java` rechts an und wählt `Run As` -> `Application`.

      ```tip
      Nach dem ersten Run startet `Strg + F11` die zuletzt ausgeführte Datei.
      ```
    * Von der **Kommandozeile** aus wechselt man in das Verzeichnis, in dem Eclipse das ct-Sim-Projekt aufhebt (ein Unterverzeichnis des Eclipse-Workspace, den man bei der Eclipse-Installation angegeben hat). Um den Simulator zu starten, ruft man dort `java ctSim.controller.Main` auf.

    ```danger
    ct-Sim ist unter macOS derzeit nicht lauffähig, weil Java3D nicht korrekt unter macOS funktioniert.
    ```

1. Falls nicht schon geschehen, den Code des ct-Bot compilieren: ct-Bot-Projekt markieren und `Project` -> `Clean` wählen.
1. ct-Bot starten:
    * In Eclipse: Im ct-Bot-Projekt die Datei `Debug-Linux_Mac/ct-Bot` (Linux und macOS) bzw. `Debug-W32\ct-Bot.exe` doppelt anklicken.
    * Auf der Kommandozeile: Wechsel in das Verzeichnis, in dem Eclipse das ct-Bot-Projekt aufhebt, und die genannte Datei ausführen.

```tip
Die Datei `ct-Bot.exe` bzw. `ct-Bot` beendet sich zügig wieder, wenn sie keinen Simulator findet, der auf ihren Versuch einer TCP/IP-Verbindung antwortet. Daher ist die Reihenfolge "zuerst Sim, dann Bot" wichtig.
```

## VI. Compiler für Raspberry Pi (optional)

### Für Raspberry Pi 2

* **Linux** (x86_64):
  1. Toolchain verfügbar auf [GitHub](https://github.com/tsandmann/arm-toolchain-linux):
    ```shell 
    sudo git clone --depth=1 https://github.com/tsandmann/arm-toolchain-linux.git /usr/local/arm-unknown-linux-gnueabihf
    ```
* **macOS** (x86_64):
  1. Toolchain verfügbar auf [GitHub](https://github.com/tsandmann/arm-toolchain-mac):
    ```shell
    sudo git clone --depth=1 https://github.com/tsandmann/arm-toolchain-mac.git /usr/local/arm-unknown-linux-gnueabihf
    ```
* **Windows 10/11**:
  1. Linaro Toolchain `gcc-linaro-7.1.1-2017.05-i686-mingw32_arm-linux-gnueabihf.tar.xz` von [hier](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/arm-linux-gnueabihf/) herunterladen.
  1. Das Archiv nach `C:\Program Files (x86)\arm-linux-gnueabihf` entpacken.
* Den Pfad zum arm-gcc (Unterverzeichnis `bin`) anschließend ebenfalls in Eclipse zum **PATH** hinzufügen:
   1. PATH-Einträge erweitern um `C:\Program Files (x86)\arm-linux-gnueabihf\bin` (Windows) bzw. `/usr/local/arm-unknown-linux-gnueabihf/bin` (Linux / macOS) in Eclipse.
   1. In Eclipse `Window` -> `Preferences` -> `C/C++` -> `Build` -> `Environment` öffnen.
   1. Dann `Select...` -> `Path` -> `Edit...` auswählen.
   1. Am Ende `;C:\Program Files (x86)\arm-linux-gnueabihf\bin` (Windows) bzw. `:/usr/local/arm-unknown-linux-gnueabihf/bin` (Linux / macOS) hinzufügen.

### Für Raspberry Pi 3

* **Linux** (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/armv8l-toolchain-linux):
    ```shell
    sudo git clone --depth=1 https://github.com/tsandmann/armv8l-toolchain-linux.git /usr/local/armv8l-unknown-linux-gnueabihf
    ```
* **macOS** (x86_64):
  1. Toolchain verfügbar auf [Github](https://github.com/tsandmann/armv8l-toolchain-mac):
    ```shell
    sudo git clone --depth=1 https://github.com/tsandmann/armv8l-toolchain-mac.git /usr/local/armv8l-unknown-linux-gnueabihf
    ```
* **Windows 10/11**:
  1. Linaro Toolchain `gcc-linaro-7.1.1-2017.05-i686-mingw32_armv8l-linux-gnueabihf.tar.xz` von [hier](https://releases.linaro.org/components/toolchain/binaries/7.1-2017.05/armv8l-linux-gnueabihf/) herunterladen.
  1. Das Archive nach `C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf` entpacken.
* Den Pfad zum arm-gcc (Unterverzeichnis `bin`) anschließend ebenfalls in Eclipse zum **PATH** hinzufügen:
   1. PATH-Einträge erweitern um `C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf\bin` (Windows) bzw. `/usr/local/armv8l-unknown-linux-gnueabihf/bin` (Linux / macOS) in Eclipse.
   1. In Eclipse `Window` -> `Preferences` -> `C/C++` -> `Build` -> `Environment` öffnen.
   1. Dann `Select...` -> `Path` -> `Edit...` auswählen.
   1. Am Ende `;C:\Program Files (x86)\armv8l-unknown-linux-gnueabihf\bin` (Windows) bzw. `:/usr/local/armv8l-unknown-linux-gnueabihf/bin` (Linux / macOS) hinzufügen.

---

<a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank"><img src="images/license.svg" alt="License: CC BY-SA 4.0" style="left;margin-left:0;margin-right:1em;" /></a><br>
Autor: <a href="https://github.com/tsandmann" target="_blank" style="color:#3c454e;">Timo Sandmann</a> \| Stand: 15.10.2023
