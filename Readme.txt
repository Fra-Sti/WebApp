
ÜBERSICHT

Diese Vorlage zeigt die aktuellen Messwerte mit Trends, sowie historische Daten, in übersichtlicher Art und Weise auf allen Displaygrößen vom Smartphone bis hin zum PC an. 

Zur Schonung des FLASH Speichers, bzw. der SD Karte, werden keine Dateien oder Diagramme lokal gespeichert. Die html Dateien werden als ftp Dienst periodisch geladen, befüllt und auf den eigenen Web-Server übertragen. Alternativ kann selbstverständlich der Web-Server der Meteobridge verwendet werden. Die Diagramme sind als Link eingebunden und werden von dem Server der Meteobridge auf Anfrage bereitgestellt. 

Sind die Seiten einmal konfiguriert, ist relativ wenig Pflegeaufwand zu betreiben. Es müssen lediglich alle 3 Monate einige Daten aus einer Email in die Jahreszeiten-Tabelle eingefügt werden und 1x jährlich sind die Tabellen um ein neues Jahr zu erweitern. Ein einfacher Texteditor reicht hierfür völlig aus.

Nachstehende Auflistung gibt einen Überblick der Inhalte:

   - index.html ist die Startseite auf der die aktuellen Werte in Kacheln an-
     gezeigt wird*

   - tthb.metachart zur Darstellung der letzten 24h in Minutenauflösung in 
     einer der Kacheln

   - page1.html beinhaltet das Impressum*

   - page2.html beinhaltet die Tabellen mit den Monatsstatistiken**

   - page3.html beinhaltet die Tabellen mit den Statistiken zu den Jahreszeiten**

   - page4.html stellt die Tageswerte des aktuellen Jahres grafisch dar*

   - Klimadiagramm.chart definiert das Diagramm der Tagesdaten in page4.html

   - monthly.mail sendet am Ende eines Monats eine Zusammenfassung der Monatswerte.
     Am Ende einer Saison werden die Statistikdaten der letzten Saison hinzugefügt.

   - Der Ordner "assets" beinhaltet alle Scripte zur Ausführung der WebSeite.

* Einmalige Konfiguration notwendig
** Quartalsweise pflege notwendig


EINSTELLUNGEN

Die Diagramme werden lokal auf der Meteobridge erzeugt. Dazu muß der Remote-Zugriff eingerichtet sein und die IP der Meteobridge in den html-Dateien angepasst werden. Hierzu ist in index.html und page4.html der Link "https://admin.meteobridge.com/xyz/..." durch den Link zur eigenen Station zu ersetzen. Dieser ist im Reiter "Graphiken" der Meteobridge abrufbar.


Zusätzlich sind nachstehende Dateien anzupassen. Am einfachsten gelingt dies mit der Suche im Editor:

   - index.html: An 3 Stellen ist "ORT" durch die Bezeichnung der Wetterstation zu ersetzen.

   - page1.html: die Platzhalter NAME, STRASSE, ORT, TEL und EMAIL sind jeweils 1x durch
     die eigenen Daten zu ersetzen.

   - page2.html: Diese Seite enthält drei Tabellen mit den Monatswerten der letzten Jahre. 
     Jeder der Tabellenzeilen ist in einem Block definiert. Durch hinzufügen oder ent-
     fernen von Blöcken lässt sich die Tabelle anpassen. Die Struktur wird schnell er-
     sichtlich, wenn man nach den Kommentaren sucht. Sie beginnen alle mit der Zeichenkette
     "<!--". Anfang und Ende von Tabellen und Tabellenzeilen sind eindeutig beschriftet.

     Um die Last der Meteobridge gering zu halten, sind historische Werte als Zahl eingetragen.
     Die Monate des aktuellen Jahres werden hingegen durch die Meteobridge befüllt. Beispiel:
     [sol0rad-avg@202011: ] für die mittlere Solarstrahlung im Nov 2020.

     Nach Ablauf eines Jahres ist die Tabelle um eine Zeile für das Folgejahr zu ergänzen. 
     Am einfachsten wird hierzu der letzte Block dupliziert und angepasst.

   - page3.html: Der Aufbau der Tabellen ist analog zu page2.html. Leider bietet die Meteo-
     bridge keine Möglichkeit zum Ausführen von Diensten am Ende einer Saison. Daher müssen 
     saisonale Daten manuell alle 3 Monate eingegeben werden. Zur Vereinfachung werden sie 
     monatlich per Email zugestellt, so dass keine eigenen Berechnungen erforderlich sind.

   - robots.txt und sitemap.xml: www.MEINE_SEITE.de ist durch die eigene DOMAIN zu ersetzen


Alle Dateien in diesem Unterverzeichnis "meteobridge" müssen nach Anpassung auf die Meteobridge in den Ordner data/templates kopiert werden. Die Dateien im Verzeichnis "webspace" sind im Root der WEB-Domain abzulegen. Wird der Web-Servers der Meteobridge verwendet, ist dies der Ordner "data/html".


METEOBRIDGE EINRICHTEN

Der externe Zugriff muss im Reiter "System" erlaubt sein. Zudem müssen die Dienste "Email" und "ftp" konfiguriert sein. Anschließend sind folgende Dienste anzulegen:

   - ftp, periodisch: Alle x Minuten die Datei index.html ausführen und unter dem gleichen
     Namen im Hauptverzeichnis (/index.html) ablegen

   - ftp, periodisch: Vor Monatswechsel die Dateien page2.html und page3.html aufrufen und
     ebenfalls unter dem gleichen Namen im Hauptverzeichnis ablegen. Hierzu sind 2 ftp Jobs
     zu erstellen. 

   - Email, periodisch: Nach Monatswechsel das template monthly.mail and die eigene
     Adresse senden.

Wird der Web-Server der Meteobridge verwendet, müssen anstelle der ftp Jobs html Jobs angelegt werden. Die Dateien sind dann alle in Verzeichnis "data/html" abzulegen.

Anschließend die Einstellungen speichern und die ftp Jobs einmalig manuell starten (Test), um die Seiten auf dem Web-Server verfügbar zu machen.

Viel Spaß
Frank
