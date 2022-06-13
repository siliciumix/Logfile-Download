# Logfile Download

Dieses Python Skript liest die Logfiles aus einem Pythovoltaik Speicher eines Herstellers aus Leipzig aus. Falls auf euerem Rechner noch kein Python3 installiert, ist bitte erst die *README_Python_install.md* lesen.

Bei GitHub seid ihr schon gelandet und habt die README Datei gefunden. Jetzt müsst ihr nur noch das ganze auf euren Computer herunterladen. 

Dazu einfach oben rechts den grünen Butten der mit *Code* beschriftet ist anklicken. Es öffnet sich ein kleines Fenster und dort klickt ihr auf Download ZIP. Nach dem der Download abgeschlossen ist kann die Datei enpackt werden.

Bei mir sieht das dann so aus. 
**C:\Users\galli\Downloads\Logfile-Download-main\Logfile-Download-main**

Jetzt könnt ihr das Verzeichnis **Logfile-Download-main** in dem alle nötigen Dateien enthalten sind an eine beliebige Stelle verschieben wie z.B. **C:\Program Files**


### Konfiguration anpassen

Jetzt müssen noch ein paar kleinigkeiten in der **config.ini** angepasst werden.


Der Aufbau der Datei sieht so aus:
```
[conf]
ipAddress = 192.168.178.27
tag = 0
monat = 0
jahr = 0
pfad = logfiles
append = no
```
**ipAddress:**
Ist die IP-Adresse des Stromspeichers. Diese kann auf dem Display des Speichers abgelesen werden.

**tag, monat und jahr:**
Vor dem ersten Start wenn ihr noch keine Logfiles aus dem Speicher herunter geladen habt tragt ihr hier am besten das Datum der Inbetriebnahme ein.
Wenn alles Logfiles heruntergeladen sind und man auf dem aktuellen Stand ist kann man die Werte: tag, monat, jahr mit einer 0 angeben. Das ist für den Zeitgesteuerten aufruf des Skripts gedacht.
Dabei wird nur das Logfile des aktuellen Tages heruntergeladen. Am besten man ruft das Skript jeden Tag um 23:59 Uhr auf. Dann hat man immer das Vollständige Logfile für diesen Tag.

**pfad:**
Hier am besten alles so lassen wie es voreingestellt ist. Die Logfeils werden dann beim Ausführen des Skripts automatisch in einen Ordner namens **logfiles** unterhalb des ausführenden Verzeichnisses.
Das Verzeichnis muss nicht erstellt werden das passiert bei bedarf automatisch.

**append:** 
Mit diesem Parameter kann eingestellt werden ob für jeden Tag eine eigene Datei erstellt wird oder ob alles in eine Datei geschrieben wird. Ist in den Parametern **tag, monat oder jahr** eine **0** eingetragen ist diese funktion gesperrt und es werden immer alle Logfiles in einzelne Dateien geschrieben.

Mögliche Parameter sind **yes** und **no**

Jetzt ist unsere **config.ini** für den eigenen Zweck Konfiguriert und wir sollten es jetzt mal ausführen.

Dazu klicken wir mit der rechten Maustaste auf die Datei *LogfileDownload.py* und anschließend auf **Öffnen mit >** ein neues Fenster erscheint und dort klicken wir **Python** an. Ein Terminal-Fenster öffnet sich. Jetzt werden alle Logfiles nach vorgabe der **config.ini** heruntergeladen.

Ein weiterer Weg wäre die PowerShell zu öffnen und in das Verzeichnis zu wechsel in dem sich das Skript befindet wechseln. Als dritten Weg kann man aus dem Datei-Explorer heraus ein Terminal-Fenster öffnen. Dazu müssen wir in dem Verzeichnis sein in dem das Skript liegt. Dann mit der rechten Maustaste in einem freien Bereich klicken. In dem erscheinenden Fenster klicken wir auf **In Terminal öffnen**

Jetzt können wir das Skript mit dem Befehl: **python3 LogfileDownload.py** starten.

#### Zeitsteuerung unter Linux

Wie schon erwähnt benutze ich unter Linux einen Cronjob um die Zeitsteuerung zu verwirklichen. Dazu muss man nur in die **crontab** mittels 

```
crontab -e
```

einsteigen. 

Folgende Eintragungen haben sich als praktikabel erwiesen.

XXXX Beschreibt den Speicherort eures Skriptes. Also ersetzt das XXXX durch euren Speicherort.

Bei mir ist es z.B.

**/home/pi/pvanlage**

```
# Schreibt um 23:59 Uhr das Logfile auf die Speicherkarte
59 23 * * * /usr/bin/python3 XXXX/LogfileDownload.py

# Schreibt zu jedem vollen Stunden das Logfile auf die Speicherkarte
0 * * * * /usr/bin/python3 XXXX/LogfileDownload.py
```