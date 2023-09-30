# Erste Schritte

```tip
Vorne weg ein paar [heitere Worte](../articles/ct.2006-02.003_editorial_cc-by-sa.pdf) zur Motivation und eine [Einführung](../articles/ct.2006-02.130-135_spielgefaehrten_cc-by-sa.pdf) in das Projekt.
```

Das ct-Bot- und ct-Sim-Projekt läuft schon eine ganze Weile und folglich gibt es auch eine ganze Menge an Dokumentation, Artikeln, FAQs und so weiter. Damit der Einstieg etwas leichter wird, haben wir hier ein paar nützliche Tipps und Literaturhinweise gesammelt.

## Allgemeine Infos

Zum Projekt gibt es viel Dokumentation, hier ein paar generelle Anlaufadressen:

1. Die [Projektseite www.ct-bot.de](../README.md)
1. Die [Liste der c't-Artikel](2_ct-articles.md)
1. Die <a href="https://github.com/Nightwalker-87/ct-bot-doku/blob/master/doc/wiki_main.md" target="_blank">Projektdokumentation</a>
1. Die <a href="https://www.heise.de/ct/artikel/c-t-Bot-und-c-t-Sim-284119.html" target="_blank">ehemalige, offizielle Projektseite</a> des c't-Magazins (nicht mehr gepflegt, somit zum Teil veraltete Inhalte)
1. Die Liste an <a href="https://www.heise.de/ct/artikel/FAQ-fuer-c-t-Bot-und-c-t-SIM-291940.html" target="_blank">FAQs für ct-Bot und ct-Sim</a> (nicht mehr gepflegt, somit zum Teil veraltete Inhalte)
1. Das <a href="https://www.heise.de/forum/c-t/Kommentare-zu-c-t-Artikeln/c-t-Bot-und-c-t-Sim/forum-23074/" target="_blank">Heise Forum</a> (nicht mehr aktiv, somit zum Teil veraltete Inhalte)
1. Das <a href="https://www.heise.de/ct/Aeltere-c-t-Projekte-4274377.html" target="_blank">Archiv der ehemaligen Mailingliste</a> enthält noch den ein oder anderen Schatz an Informationen, die allerdings nicht mehr aktuell sein müssen.

## Support

1. Direkter Kontakt im [Chat](../README.md#community-und-support)
1. Das <a href="https://www.ctbot.de" target="_blank">Forum</a>

## Testen/Spielen ohne Geld für Hardware auszugeben

Wer (noch) keinen realen Bot besitzt und erstmal in das Projekt reinschauen will, kann mit dem <a href="https://www.heise.de/ct/artikel/c-t-Bot-und-c-t-Sim-284119.html?seite=3" target="_blank">Simulator</a> spielen. Folgendes sollte man für den Einstieg beachten:

1. Toolchain [installieren](../installation/1_installation-allgemein.md)
1. ct-Bot- und ct-Sim-Code aus dem [Repository](../repository/1_git-eclipse.md) laden
1. ct-Bot compilieren [Bot compilieren, Simulator starten und ct-Bot starten](../installation/1_installation-allgemein.md#ct-sim-und-virtuelle-bots-aus-eclipse-starten)
1. Fernbedienung öffnen und Wandfolger (Taste 5) starten

Nun hat man einen virtuellen Bot im Simulator. Möchte man dem Bot eigene Kunststückchen beibringen, kommt man um die [Installation der Toolchain](../installation/1_installation-allgemein.md) nicht herum. Wie man den Bot verwendet und programmiert ist in den folgenden [Artikeln](2_ct-articles.md) ausführlich beschrieben:

1. **Einsteiger-Tutorial zu ct-Bot und ct-Sim: <a href="../articles/make.2012-01.100_ct-bot-programmieren-leicht-gemacht_cc-by-nc-sa.pdf" target="_blank">c’t-Bot: Programmieren leicht gemacht</a>**. *Benjamin Benz*. c’t Hardware Hacks 1, 2012. CC BY-NC-SA 4.0.
1. **Idee des ct-Sim: <a href="../articles/ct.2006-02.130-135_spielgefaehrten_cc-by-sa.pdf" target="_blank">Spielgefährten</a>** -- Roboter für Löter, Simulator für Soft-Werker. *Thorsten Thiele, Benjamin Benz, Carl Thiede*. c't 2, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290274" target="_blank">html-Version</a>.
1. **Interna des ct-Sim: <a href="../articles/ct.2006-05.224-230_draengelnde-spielgefaehrten_cc-by-sa.pdf" target="_blank">Drängelnde Spielgefährten</a>** -- Kollisionen und Sensoren für den c't-Sim, neues Verhalten für den c't-Bot. *Peter König, Lasse Schwarten, Benjamin Benz*. c't 5, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290334" target="_blank">html-Version</a>.
1. **Programmierung des (virtuellen) ct-Bot: <a href="../articles/ct.2006-07.218-222_hohe-schule_cc-by-sa.pdf" target="_blank">Hohe Schule</a>** -- c't-Bots bewältigen komplexe Aufgaben. *Christoph Grimmer*. c't 7, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290392" target="_blank">html-Version</a>.
1. **Tutorial für die Programmierung von Verhalten: <a href="../articles/ct.2006-10.236-239_ausgang-gesucht_cc-by-sa.pdf" target="_blank">Ausgang gesucht!</a>** -- Komplexe Verhalten für den c't-Bot selbst entwickelt. *Torsten Evers*. c't 10, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290460" target="_blank">html-Version</a>.
1. **Eigene Welten für den ct-Sim: <a href="../articles/ct.2006-11.214-217_genesis_cc-by-sa.pdf" target="_blank">Genesis</a>** -- c't-Sim: Weltenbau und Netzwerkzuschauer. *Benjamin Benz*. c't 11, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290480" target="_blank">html-Version</a>.
1. **Kartographie für den ct-Bot: <a href="../articles/ct.2006-19.198-205_an-der-naechsten-ecke-links_cc-by-sa.pdf" target="_blank">An der nächsten Ecke links...</a>** -- Karten bauen (nicht nur) mit dem c't-Bot. *Andreas Birk*. c't 19, 2006. CC BY-SA 4.0. <a href="https://heise.de/-290662" target="_blank">html-Version</a>.

## Weitere externe Dokumentation

1. Eine Bachelorarbeit zur <a href="http://users.informatik.haw-hamburg.de/~kvl/teske/bachelor_teske.pdf" target="_blank">Entwicklung einer Bibliothek als Basis für die Programmierung und Steuerung des ct-Bots</a> der HAW Hamburg.
1. Eine Diplomarbeit zur <a href="https://www.db-thueringen.de/servlets/MCRFileNodeServlet/dbt_derivate_00013826/Schmidt_Diplom_ct-Bot.pdf" target="_blank"> Konzeption und Umsetzung eines Remote Engineering Praktikums für mobile Roboter</a> der TU Ilmenau.

## Ausblick

Für alle, die einen ct-Bot besitzen, geht es nun mit der <a href="https://github.com/Nightwalker-87/ct-bot-doku/blob/master/doc/wiki_main.md#ct-bot" target="_blank">Hardware-Dokumentation</a> weiter, insbesondere mit der <a href="https://github.com/Nightwalker-87/ct-bot-doku/blob/master/doc/wiki_pages_deprecated/ct-bot_assembly.md#aufbauanleitung-für-den-ct-bot" target="_blank">Aufbauanleitung</a>.

Beim Überprüfen des eigenen Hardwareaufbaus hilft das <a href="https://github.com/tsandmann/ct-bot-doku/blob/master/_tmp_materialpool/hardware/ct-bot_messprotokoll.pdf" target="_blank">ct-Bot Messprotokoll</a>, mit dem sich elektrische Messwerte systematisch <a href="https://github.com/tsandmann/ct-bot-doku/blob/master/_tmp_materialpool/hardware/ct-bot_messprotokoll.odt" target="_blank">erfassen</a> und mit Beispieldaten vergleichen lassen.

---

<a href="https://creativecommons.org/licenses/by-sa/4.0/" target="_blank"><img src="images/license.svg" alt="License: CC BY-SA 4.0" style="left;margin-left:0;margin-right:1em;" /></a><br>
Autoren: Benjamin Benz, <a href="https://github.com/tsandmann" target="_blank" style="color:#3c454e;">Timo Sandmann</a> \| Stand: 30.09.2023
