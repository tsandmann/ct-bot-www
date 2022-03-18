# Willkommen bei ct-Bot und ct-Sim

<img src="images/ctbot.png" title="ct-Bot ohne Kabel von Peter Recktenwald, CC BY-SA 3.0" style="float: right; margin-left:2em; height: 200px;" />

ct-Bot und ct-Sim gehören zusammen und sind ein Roboterprojekt, das von der Zeitschrift c't Anfang des Jahres 2006 gestartet und in einer Reihe von 16 Artikeln beschrieben wurde. Das Ziel des ct-Bots war und ist dabei, möglichst Vielen den Zugang zu dem spannenden Thema der Robotik zu eröffnen. Das Projekt besteht aus zwei Teilen: Dem eigentlichen Roboter ct-Bot und dem dazu passenden Simulator ct-Sim.

Seit Projektstart ist um das Projekt eine Community entstanden, welche das Projekt weiterhin pflegt auch nach dem Erscheinen des letzten c't-Artikels im Jahr 2011. Derzeit bemüht sich ein Kreis aus Projektbegeisterten um eine Neuorganisation des Projekts. So sind der Quelltext und die gesamte Dokumentation auf die GitHub-Plattform umgezogen, mit dem Ziel den Projektumfang und das entstandene Wissen auch langfristig zu erhalten und frei zugänglich zu machen. In Absprache mit dem Heise Verlag, als ursprünglicher Initiator des Projekts, wurde die Projektdokumentation inzwischen größtenteils unter die <a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank">CC-BY-SA-Lizenz</a> gestellt. Die zusammengetragenen Inhalte werden derzeit neu aufbereitet und aktualisiert. Darüber hinaus gibt es Pläne und erste Ansätze für eine aktualisierte Version des ct-Bots auf der Basis zeitgemäßer Hard- und Software.

# Community und Support

## Chat/Instant Messenger

* <a href="https://de.wikipedia.org/wiki/Matrix_%28Kommunikationsprotokoll%29" target="_blank">Matrix</a> (bspw. mit dem Client <a href="https://element.io" target="_blank">Element</a>, frei, föderal)
  * <a href="https://app.element.io/#/room/%23ctbot:matrix.org" target="_blank">Direktzugang zum ct-Bot-Channel</a> über die Web-App von Element
  * <a href="https://app.element.io/#/room/%23ct-Bot-news:matrix.org" target="_blank">Direktzugang zum News-Channel</a> über die Web-App von Element
* <a href="https://de.wikipedia.org/wiki/Slack_%28Software%29" target="_blank">Slack</a> (proprietär, zentralisiert)
  * <a href="https://ct-bot-slack.herokuapp.com" target="_blank">Registrierung zum ct-Bot-Workspace</a>

```tip
Da Matrix und Slack synchronisiert sind, zeigen sie dieselben Inhalte und können nach persönlicher Präferenz gewählt werden.
```

## Forum

Unter <a href="https://www.ctbot.de" target="_blank">www.ctbot.de</a> ist das Community-Forum zum ct-Bot und zu verwandten Themen zu finden. Es besteht bereits seit der Anfangszeit des Projekts und enthält somit nicht nur Support zum ct-Bot sowie aktuelle Diskussionen zur Zukunft des Projekts, sondern auch die zugehörige Historie.

# Anleitungen und Dokumentation

## <a href="https://github.com/Nightwalker-87/ct-bot-doku/blob/master/doc/wiki_main.md" target="_blank">Projektdokumentation</a>

Derzeit befindet sich die Projektdokumentation in Überarbeitung (siehe auch <a href="https://www.ctbot.de/viewtopic.php?f=34&t=1219" target="_blank">Diskussion im Forum</a>). Im Zuge dieser werden sowohl sämtliche Informationen des ehemaligen Trac-Wikis als auch des Community-Wikis in eine gemeinsame Projektdokumentation portiert. Temporär sind die Inhalte des ehemaligen Trac-Wikis von Heise zusätzlich als <a href="https://github.com/tsandmann/ct-bot-doku/tree/master/_tmp_trac_wiki_export" target="_blank">Archiv</a> verfügbar. Außerdem existiert noch ein Community-Wiki, dessen noch nicht portierte Inhalte unter <a href="https://wiki.ctbot.de" target="_blank">wiki.ctbot.de</a> verfügbar bleiben. 

Ein paar grundlegende Informationen und Anleitungen für Neueinsteiger sind direkt hier auf der Projektwebseite
zu finden, das Menü links gruppiert sie in chronologischer Reihenfolge als Empfehlung für Einsteiger. Einen guten Überblick über das gesamte Projekt geben außerdem die [c't-Artikel](first-steps/2_ct-articles.md).

```tip
Um mal direkt auszuprobieren, wie das Ganze so geht (auch ohne Geld auszugeben), helfen die [ersten Schritte](first-steps/1_first-steps.md) weiter.
```

Für detaillierte Dokumentationen inkl. technischer Details, Spezifikationen und Erläuterung sei auf das <a href="https://github.com/Nightwalker-87/ct-bot-doku" target="_blank">Dokumentationsprojekt</a> verwiesen, dort werden derzeit die im Laufe der Zeit seit Projektbeginn entstandenen Dokumentationen neu aufbereitet.

## Alte Projektdokumentation

* Die <a href="https://www.heise.de/ct/artikel/c-t-Bot-und-c-t-Sim-284119.html" target="_blank">ehemalige, offizielle Projektseite</a> des c't-Magazins von Heise wird nicht mehr gepflegt und enthält somit zum Teil auch veraltete Inhalte.
* Die Liste an <a href="https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html" target="_blank">FAQs für ct-Bot und ct-Sim</a> wird nicht mehr gepflegt und enthält somit zum Teil auch veraltete Inhalte.
* Das <a href="https://www.heise.de/ct/newsletter/archiv/ct-bot-entwickler/" target="_blank">Archiv der ehemaligen Mailingliste</a> enthält noch den ein oder anderen Schatz an Informationen, die allerdings auch nicht mehr aktuell sein müssen.

# Source Code

Der Quellcode des Projekts ist unter GPL lizensiert und in Git-Repositories auf GitHub verfügbar. Für den ct-Bot ist er in C geschrieben -- sowohl für den realen ct-Bot als auch einen Virtuellen im Simulator. So lassen sich komplexe Verhaltensmuster für den Bot zunächst am PC testen. Der in Java geschriebene Simulator ct-Sim kommuniziert mit mehreren virtuellen Robotern, gaukelt ihnen eine Umgebung vor und liefert Sensorwerte zurück.

Das Software-Framework des ct-Bot erfüllt sehr unterschiedliche Anforderungen:

* Die Programmierung des Roboters soll möglichst einfach sein, indem von der Komplexität der typischen Mikrocontroller-Programmierung wie Interrupts, I/O-Ports, Timer, PID-Regler abstrahiert wird.
* Alle Sensorwerte stehen als globale Variablen zur Verfügung, die automatisch aktualisiert werden. Einfache Funktionen ermöglichen den Zugriff auf die Aktuatoren.
* Der Source Code ist plattformunabhängig, sodass er sowohl im Simulator auf einem PC als auch dem realen Bot läuft, ohne dass man ihn manuell anpassen muss.
* Einmal entwickelte Unterprogramme (im Framework *Verhalten* genannt), von ganz rudimentären wie `bot_turn()` bis zu komplexen wie `bot_solve_maze()`, lassen sich weiterverwenden und in andere Routinen einbauen.

## Offizielle Code-Repositories

* <a href="https://github.com/tsandmann/ct-bot" target="_blank">ct-Bot</a> Code-Repository auf GitHub
* <a href="https://github.com/tsandmann/ct-sim" target="_blank">ct-Sim</a> Code-Repository auf GitHub

## Weitere Repositories

* <a href="https://github.com/tsandmann/ct-bot-hw" target="_blank">ct-bot-hw</a> enthält alles zur Hardware des ct-Bots:
  * Im Ordner <a href="https://github.com/tsandmann/ct-bot-hw/tree/master/v1" target="_blank">v1</a> finden sich die Design-Dateien des originalen ct-Bots und die gehörigen Datenblätter.
  * Im Ordner <a href="https://github.com/tsandmann/ct-bot-hw/tree/master/v2" target="_blank">v2</a> ist die Entwicklung einer neuen Hardware-Revision des ct-Bots zu finden, die derzeit in Planung ist.
* <a href="https://github.com/tsandmann/ctbot-atmega" target="_blank">ctbot-atmega</a> enthält eine vollständige Neuentwicklung in C++ einer reduzierten Basis-Firmware für die Grundfunktionalität eines realen ct-Bots. Nähere Informationen finden sich in der <a href="https://github.com/tsandmann/ctbot-atmega/blob/master/README.md" target="_blank">Readme-Datei</a>.
* <a href="https://github.com/tsandmann/ctbot-teensy" target="_blank">ctbot-teensy</a> enthält eine vollständige Neuentwicklung des Frameworks in C++ für einen realen Bot, der mit einem Teensy 4.1 ARM-Mikrocontroller ausgestattet ist. Nähere Informationen finden sich in der <a href="https://github.com/tsandmann/ctbot-teensy/blob/master/README.md" target="_blank">Readme-Datei</a>.
* <a href="https://github.com/tsandmann/ctbot-viewer" target="_blank">ctbot-viewer</a> enthält einen neu entwickelten Remote-Viewer für den ct-Bot, derzeit noch im Beta-Stadium. Nähere Informationen finden sich in der <a href="https://github.com/tsandmann/ctbot-viewer/blob/master/README.md" target="_blank">Readme-Datei</a>.

---

<a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank"><img src="images/license.svg" alt="License: CC BY-SA 4.0" style="left;margin-left:0;margin-right:1em;" /></a><br>
Autoren: Benjamin Benz, <a href="https://github.com/tsandmann" target="_blank" style="color:#3c454e;">Timo Sandmann</a> \| Bild: *ct-Bot ohne Kabel* von <a href="https://github.com/robotfreak" target="_blank" style="color:#3c454e;">Peter Recktenwald</a> (CC BY-SA 3.0) \| Stand: 18.03.2022
