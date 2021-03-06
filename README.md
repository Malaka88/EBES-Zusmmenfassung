# Netzwerk

## OSI

![OSI Schichtenmodel mit Beispielen](img/OSI_Modell.png)

## Topologien

**Bus:**

![Bustopologie](img/Bustopologie.png)

* Anzahl zerstörter Verbindungen = 1 (nur Ausgefallener Knoten ist betroffen)
* minimalem Aufwand beim Anschluss neuer Knoten
* zunehmende Kollision bei Überlastung

| Eigenschaft                    | Wert                                   |
| ------------------------------ | -------------------------------------- |
| Anschlüsse                     | 1                                      |
| Anzahl zerstörter Verbindungen | 1 (nur Ausgefallener Knoten Betroffen) |
| max. Entfernung                | n-1                                    |

**Ring**

![Ringtopologie](img/Ringtopologie.png)

* einfach und kostengünstig

| Eigenschaft                    | Wert          |
| ------------------------------ | ------------- |
| Anschlüsse                     | 2             |
| Anzahl zerstörter Verbindungen | 2             |
| max. Entfernung                | $\frac{n}{2}$ |

**Kette**

* einfach und kostengünstig

| Eigenschaft                    | Wert  |
| ------------------------------ | ----- |
| Anschlüsse                     | 2     |
| Anzahl zerstörter Verbindungen | 1     |
| max. Entfernung                | $n-1$ |

**Barrel Shifter:**

* Erweiterung des Rings um zusätzliche Verbindungen
* Überspringen eines oder mehrerer Knoten möglich
* Anzahl von Anschlüssen einer Station wird erhöht
* verringert max. Entfernung
* erhöht die Redundanz durch alternative Wege

| Eigenschaft                    | Wert                     |
| ------------------------------ | ------------------------ |
| Anschlüsse                     |                          |
| Anzahl zerstörter Verbindungen | $2 \cdot log_{2}(n) - 1$ |
| max. Entfernung                |                          |

**Baumtopologie:**

* geeignet für Broadcastartige Kommunikation (von der Wurzel aus)
* Engpass ist der Pfad über die Wurzel

| Eigenschaft                    | Wert     |
| ------------------------------ | -------- |
| Anschlüsse                     |          |
| Anzahl zerstörter Verbindungen | 1        |
| max. Entfernung                | $log(n)$ |

**Sterntopologie**

![Sterntopologie](img/Sterntopologie.png)

* Spezialfall eines einstufigen Baums
* Große Anzahl von Anschlüssen an der Zentralstation
* Hauptlast liegt auf der Zentralstation
* Zentralstation = Single Point of Failuer (Ausfall = Totalausfall)
* Anschluss neuer Knoten sorgt für höhere Last auf der Zentralstation

| Eigenschaft                    | Wert                   |
| ------------------------------ | ---------------------- |
| Anschlüsse                     | 1 (Zentralstation = n) |
| Anzahl zerstörter Verbindungen | 1                      |
| max. Entfernung                | 2                      |

**2D-Gitter:**

* Jeder Knoten ist mit 4 Nachbarn verbunden
* leicht Skalierbar

| Eigenschaft                    | Wert               |
| ------------------------------ | ------------------ |
| Anschlüsse                     |                    |
| Anzahl zerstörter Verbindungen | 2 (beim Eckknoten) |
| max. Entfernung                | $\sqrt{n}$         |

**3D-Torus:**

* 6 Anschlüsse pro Station

| Eigenschaft                    | Wert                      |
| ------------------------------ | ------------------------- |
| Anschlüsse                     | 6                         |
| Anzahl zerstörter Verbindungen | $2 \cdot n^{\frac{2}{3}}$ |
| max. Entfernung                | $\sqrt{3}{n}$             |

  

**Vollvermascht:**

* Jede Station ist mit jeder Station verbunden
* sehr hoher Hardwareaufwand
* nur bei kleiner Anzahl von Stationen realisierbar

| Eigenschaft                    | Wert  |
| ------------------------------ | ----- |
| Anschlüsse                     | n     |
| Anzahl zerstörter Verbindungen | $n-1$ |
| max. Entfernung                | 1     |

## Routing

### Dijkstra-Algorithmus

* Gerichteter, Kantenbewerteter Graph
* Algorithmus zur Bestimmung des kürzesten Wegs zwischen zwei Punkten
* Gewichtung nicht von den Hops abhängig sondern nur von den Wegekosten

## Leitungscodierung

* **selbsttaktende Leitungscodes** 
  * ermöglichen Taktrückgewinnung aus dem Datenstrom
  * wird bei der **synchronen seriellen** Datenübertragung benötigt (alle Rechnernetze inkl. Sensor-Aktuator- und Feldbusse)
  * setzt einen regelmäßigen Wechsel zwischen 0 und 1 Pegel voraus
  * Sicherstellung von Signalen die keine zu langen Eins- bzw. Nullfolgen ohne Flankenwechsel haben
  * Takt kann aus den Flanken rekonstruiert werden
* **gleichstromfreie Leitungscodes**
  * Leitungscodes ohne Gleichanteil im Signal
  * Datenübertragung über Stromversorgungsleitung möglich, sofern eine Gleichspannung als Energieversorgung verwendet wird.
  * Senke kann durch Tiefpass den Gleichanteil der Energieversorgung und durch einen Hochpass das Datensignal herausfiltern.

### (Unipolarer) NRZ-Codierung (Non Return to Zero)

| Eigenschaften       | Wert                                                         |
| ------------------- | ------------------------------------------------------------ |
| Taktrückgewinnung   | nicht gegeben                                                |
| Gleichstromfreiheit | nein                                                         |
| Logische 1          | High-Pegel (+1)                                              |
| Logische 0          | Low-Pegel (0)                                                |
| Pegelwechsel        | Bei jedem wechsel von logischer 1 und 0                      |
| Anwendungsbereich   | asynchrone Übertragung, bei der Synchronisation durch Rahmendaten erfolgt |

### (Bipolarer) NRZ-Codierung (Non Return to Zero)

| Eigenschaften       | Wert                                                         |
| ------------------- | ------------------------------------------------------------ |
| Taktrückgewinnung   | nicht gegeben                                                |
| Gleichstromfreiheit | nein                                                         |
| Logische 1          | High-Pegel (+1)                                              |
| Logische 0          | Low-Pegel (-1)                                               |
| Pegelwechsel        | Bei jedem wechsel von logischer 1 und 0                      |
| Anwendungsbereich   | asynchrone Übertragung, bei der Synchronisation durch Rahmendaten erfolgt |

### NRZI-Codierung (Non Return to Zero Inverted)

| Eigenschaften          | Wert                   |
| ---------------------- | ---------------------- |
| Taktrückgewinnung      | nicht gegeben          |
| Gleichstromfreiheit    | nein                   |
| Logische 1             | wechsel des Pegels     |
| Logische 0             | beibehalten des Pegels |
| Pegelwechsel           | bei jeder logischen 1  |
| Bandbreitenanforderung | NRZ                    |

### RZ-Codierung (Return to Zero)

| Eigenschaften          | Wert                                    |
| ---------------------- | --------------------------------------- |
| Taktrückgewinnung      | möglich                                 |
| Gleichstromfreiheit    | nein                                    |
| Logische 1             | Heigh-Pegel (+1)                        |
| Logische 0             | Low-Pegel (-1)                          |
| Pegelwechsel           | nach halber Taktperiode zurück auf Null |
| Bandbreitenanforderung | 2 * NRZ                                 |

### Unipolare RZ-Codierung

| Eigenschaften          | Wert                                    |
| ---------------------- | --------------------------------------- |
| Taktrückgewinnung      | nicht gegeben                           |
| Gleichstromfreiheit    | nein                                    |
| Logische 1             | Heigh-Pegel (+1)                        |
| Logische 0             | Low-Pegel (0)                           |
| Pegelwechsel           | nach halber Taktperiode zurück auf Null |
| Bandbreitenanforderung | 2 * NRZ                                 |

### Bipolare RZ-Codierung

| Eigenschaften          | Wert                                        |
| ---------------------- | ------------------------------------------- |
| Taktrückgewinnung      | nicht gegeben                               |
| Gleichstromfreiheit    | ja                                          |
| Logische 1             | Pegel = +1 und -1 im wechsel (alternierend) |
| Logische 0             | 0-Pegel                                     |
| Pegelwechsel           | bei jeder logischen 1                       |
| Bandbreitenanforderung |                                             |

### Manchester-Codierung (IEEE 802.3)

| Eigenschaften          | Wert                                       |
| ---------------------- | ------------------------------------------ |
| Taktrückgewinnung      | Ja                                         |
| Gleichstromfreiheit    | nur bei Verwendung eines Bipolaren Signals |
| Logische 1             | steigende Flanke                           |
| Logische 0             | fallende Flanke                            |
| Pegelwechsel           | zu beginn und zur Mitte des Takts          |
| Bandbreitenanforderung | 2 * NRZ                                    |
| Anwendung              | Teil des Ethernet-Standards                |

### Differential-Manchester-Codierung

| Eigenschaften       | Wert                           |
| ------------------- | ------------------------------ |
| Taktrückgewinnung   | Ja                             |
| Gleichstromfreiheit |                                |
| Logische 1          | kein Flankenwechsel Taktanfang |
| Logische 0          | Flankenwechsel Taktanfang      |
| Pegelwechsel        | zur Taktmitte                  |
| Anwendung           | Tokenring                      |

### AMI (Alternate Mark Inversion Code)

| Eigenschaften       | Wert                             |
| ------------------- | -------------------------------- |
| Taktrückgewinnung   | Ja                               |
| Gleichstromfreiheit | Ja                               |
| Logische 1          | Pegel = +1 und -1 (alternierend) |
| Logische 0          | 0-Pegel                          |
| Pegelwechsel        | im Takt                          |
| Anwendung           |                                  |

### 4B/5B-Codierung

* Blöcke aus 4 Bit werden zu 5 Bit kodiert
* Es folgen nie mehr als 3 Nullen aufeinander
* die 5 Bit werden **NRZI** Codiert zur Vermeidung zu langer 1-Folgen

| Eigenschaften          | Wert                       |
| ---------------------- | -------------------------- |
| Taktrückgewinnung      | Ja                         |
| Gleichstromfreiheit    |                            |
| Bandbreitenanforderung | 1,25 NRZ                   |
| Anwendung              | FDDI (100MBit/s Tokenring) |

## Medien Zugangskontrolle (MAC-Teilschicht)

### Aloha-Verfahren

* Medienzugriffsverfahren nach zufälligen Strategien
* Einsatz in einem funkbasierten Forschungsnetz auf Hawaii
* **alle sende** bereiten Teilnehmer senden **sofort** (ohne Erlaubnis und ohne Prüfung ob das Medium belegt ist)
* gleichzeitiges Senden von Teilnehmern führt zur Überlagerung und Verfälchung der Daten -> Empfänger erkennt die Daten nicht mehr
* Einführung von Quittungssignalen zur quittierung des korrekten Empfangs
* Bei ausbleiben der Quittung wird die Sendung wiederholt
* Mehrfaches versenden belastet den Kanal zusätzlich
* selbst bei geringer Kanalbelegung ist die Anzahl der Kollisionen ausreichend das die Übertragung merklich verzögert wird
* Einsatz nur bei einer Kanalbelegung unter 20%

### CSMA-Protokoll (Cerrier Sense Multiple Access)

* Sendewillige **Station hört **den Kanals vor dem Senden **ab** -> Übertragung beginnt bei freiem Kanal
* Erhebliche Kollisionsreduktion gegenüber Aloha
* Quittungsbasiertes Verfahren (Quittieren des korrekten Empfangs)

#### CSMA/CD (CD = collision detect)

* **Kollisionserkennung**
* Bei frei werdendem Kanal **Sendet der Teilnehmer** und **liest gleichzeitig** auf dem Kanal mit
* Sind gesendetes und abgehörtes Signal gleich, erhält der Teilnehmer nach einer Abitrierungszeit bis zum Ende der Übertragung seines Rahmes den Bus
* Durch gleichzeitiges Senden und Lesen kann eine Kollision schnell erkannt werden
* Übertragung wird bei Kollision direkt abgebrochen und sendet ein **Störsignal** (**jam-Signal**)
* Dieses **Störsignal** lässt auch alle anderen Teilnehmer die gerade Senden die Übertragung abbrechen
* Keine Quittierung des Empfangs erforderlich!

#### CSMA/CA (CA = collision avoidance)

* **Kollisionsvermeidung**
* 

# Bussysteme

## **LIN** (Local Interconnect Network)

* geringe Anforderungen gegenüber CAN
* kostengünstig
* geringe Datenrate
* Einsatz: Sitze, Türen, Dach, Klimaanlage, Steuereinheiten (Motorsteuerung)

| Eigenschaft        | Wert                                      |
| ------------------ | ----------------------------------------- |
| Übertragungsmedium |                                           |
| Übertragungsrate   | 1-20 kbit/s                               |
| Teilnehmer         | max. 16 Knoten                            |
| Daten/Nachricht:   | 1-8 Byte (ab Version 2.0 oder höher)      |
| Busmanagement:     | Master/Slave (Zeitslots, deterministisch) |
| Einsatzgebiet      | KFZ (Sitze, Türen, Dach, Klimaanlagen)    |

## **CAN** (Controller Area Network)

* vernetzung komplexer Controller und Steuergeräte
* Echtzeitfähig (verbesserung in TTCAN)
* preisgünstig aufgrund von hoher Stückzahl
* max. Übertragungsrate in der Praxis effektiv 500kBit/s
* max. Teilnehmer kann durch Aufteilung in Segmenten erhöht werden

| Eigenschaft           | Wert                                              |
| --------------------- | ------------------------------------------------- |
| Übertragungsmedium    | verdrillte Zweidrahtleitung                       |
| Übertragungsrate      | 10kbit/s (bei wenigen Kilometern) - 1MBit/s (40m) |
| Teilnehmer            | max. 32 Knoten                                    |
| Daten/Nachricht:      | max. 8 Byte                                       |
| Busmanagement:        | serieller Multi-Master-Bus                        |
| Buszugriffsverfahren: | CSMA/CA                                           |
| Einsatzgebiet         | KFZ, Haushaltsgeräte, Medizintechnik              |

## LON (Local Operating Network)

* 

| Eigenschaft           | Wert                                                       |
| --------------------- | ---------------------------------------------------------- |
| Übertragungsmedium    | verdrillte Zweidrahtleitung und Funk                              |
| Übertragungsrate      | 4,9 kBit/s (Funk 49 MHZ) - 1.25 MBit/s (Zweidraht 500m)    |
| Teilnehmer            | max. 32000 (127 Endpunkte pro Subnetz, 255 Subnetze)       |
| Daten/Nachricht:      |                                                            |
| Busmanagement:        |                                                            |
| Buszugriffsverfahren: | CSMA/CD                                                    |
| Einsatzgebiet         | verteilte industrieelle Anendungen, Gebäudeautomatisierung |

## EIB** (European Installation Bus)

* spezifiziert durch die EIBA (EIB Assoziation)
* über zwei Ebenen hierarchisch unterteilt.
* durch Koppler wird die Last des Gesamtnetzes verringert (ähnlich Router und Switches)
* Aufmodulierung des Datensignals auf 28-V Gleichspannung

| Eigenschaft           | Wert                                                        |
| --------------------- | ----------------------------------------------------------- |
| Übertragungsmedium    |                                                             |
| Übertragungsrate      | 9600 Bit/s                                                  |
| Teilnehmer            | max. 11500 (12 Linien zu je 64 Teilnehmern in 15 Bereichen) |
| Daten/Nachricht:      | UART-Zeichen (23 Zeichen pro Nachricht)                     |
| Busmanagement:        |                                                             |
| Buszugriffsverfahren: | CSMA/CA                                                     |
| Einsatzgebiet         | Gebäudeautomatisierung Zweckbau und Privat                  |

## **Profibus** (Process Field Bus)

* 

| Eigenschaft           | Wert                                              |
| --------------------- | ------------------------------------------------- |
| Übertragungsmedium    |                        |
| Übertragungsrate      |  |
| Teilnehmer            |   |
| Daten/Nachricht:      |  |
| Busmanagement:        |  |
| Buszugriffsverfahren: |   |
| Einsatzgebiet         |   |

## **FlexRay** 

* 

| Eigenschaft           | Wert                                              |
| --------------------- | ------------------------------------------------- |
| Übertragungsmedium    |                        |
| Übertragungsrate      |  |
| Teilnehmer            |   |
| Daten/Nachricht:      |  |
| Busmanagement:        |  |
| Buszugriffsverfahren: |   |
| Einsatzgebiet         |   |

## **MOST** (Media Oriented System Transport)

* 

| Eigenschaft           | Wert                                              |
| --------------------- | ------------------------------------------------- |
| Übertragungsmedium    |                        |
| Übertragungsrate      |  |
| Teilnehmer            |   |
| Daten/Nachricht:      |  |
| Busmanagement:        |  |
| Buszugriffsverfahren: |   |
| Einsatzgebiet         |   |

# Echtzeitsysteme

> Echtzeitsysteme sind also Systeme, die korrekte Reaktionen innerhalb einer definierten Zeitspanne produzieren müssen. Falls die Reaktionen diese Zeitlimits überschreiten, führt dies zu Leistungseinbußen und/oder Fehlfunktionen.

## Unterteilung

* **harte Echtzeitsysteme**

  * Katastrophale Folgen beim Verpassen einer Deadline

  * Deadline muss zwingend eingehalten werden

  * bsp. flight control system (Flugzeugsteuerung)

  * > Zeitliche Bindung die vom System stets erfüllt werden muss, da eine auch nur gelegentliche Verletzung erhebliche Folgen nach sich ziehen würde.

* **weiche Echtzeitsysteme**

  * Einhaltung von Deadlines wichtig aber nicht notwendig zur korrekten funktionsweise.
  * zeitliche Bedingung bei der gelegentliche Verletzungen tolerierbar sind
  * bsp. Multimediasysteme (Darstellung 25fps -> verletzung meist tollerierbar)

* **oberen Zeitschranken** -> maximal erlaubte Zeitspanne

  * Mindestgeschwindigkeit des Systems oder Teilen wird vorrausgesetzt
  * erreichung durch konstruktive Maßnahmen (aufwändig)

* **untere Zeitschranke** -> minimale dauer einer Phase

  * anforderung kann durch warten erfüllt werden

* **beidseitige Zeitschranken**

## Unterscheidung

* **Ereignis gesteuert** (event triggered)
  * Auslösung eines Interrupts bei auftreten eines Ereignisses (der Umgebung)
  * resultiert in kurzen Reaktionszeiten
  * anfällig bei der Verarbeitung vieler gleichzeitiger Ereignissen (sogennante **event showers**)
* **Zeit gesteuert** (time triggered)
  * Auslösung durch periodische Zeitgeber
  * Aktives abfragen von Sensoren durch das Steuergerät (Polling)
  * ggf. puffern kurzer Signale
  * planbares zeitliches Verhalten sämtlicher Systemaktivitäten
  * Prüfbar ob Echtzeitanforderungen eingehalten werden können.

## Systemeinteilung

Bei einer Büroanwendung handelt es sich um ein rein **transformationelles** oder **interaktives** System, bei einem eingebetteten System dagegen um ein **reaktives** System. 

### Reaktive Systeme

* müssen ständig mit ihrer Umgebung interagieren
* Geschwindigkeit und Art und Weise wird durch die Umgebung vorgegeben

### Interaktive Systeme

* kommunizieren mit ihrem Benutzer
* bestimmen die Art und Weise sowie Geschwindigkeit der Interaktion selbst

### Transformationelle Systeme

* führen keine Kommunikation mit der Umgebung

## Echtzeitbetriebssysteme

> Ein **Betriebssystem** nach **DIN44300 sind die Programme eines digitalen Rechensystems, die zusammen mit den Eigenschaften dieser Rechenanlage die Basis der möglichen Betriebsarten des digitalen Rechensystems bilden und die insbesondere die Abwicklung von Programmen steuern und überwachen.

| Komponente               | Beispiele                                                    |
| ------------------------ | ------------------------------------------------------------ |
| **Prozess-Verwaltung**   | Kreieren und Terminieren von Applikations- und System-Prozessen, Suspendieren und Reaktivieren von Prozessen, Prozess-Synchronisation und Kommunikation, Deadlock-Behandlung |
| **Speicher-Verwaltung**  | „Buchführung“ über freie und belegte Hauptspeicherbereiche, Kommunikation mit den in der Hierarchie angrenzenden Speichermedien, Dynamische Allokation und Deallokation von Hauptspeicher, Speicherschutz und Zugriffskontrolle |
| **Prozessor-Verwaltung** | Multiprogramming, Dispatching, Zuteilungsalgorithmen (Scheduling), Vorrangunterbrechung (Interrupt, Preemption) |
| **Geräte-Verwaltung**    |                                                              |
| **Datei-Verwaltung**     | Datei-Konzepte, -Attribute und -Operationen, Zugriffs-Methoden, Verzeichnis-Strukturen und Implementierungen, Allokations-Methoden |

>Definition (**Echtzeitbetrieb**, DIN 44300) (engl. **Real Time Operating System**, kurz: **RTOS**) ist ein Betrieb eines Rechensystems, bei dem Programme zur Verarbeitung anfallender Daten ständig betriebsbereit sind derart, dass die Verarbeitungsergebnisse innerhalb einer vorgegebenen Zeitspanne verfügbar sind. Die Daten können je nach Anwendungsfall nach einer zeitlich zufälligen Verteilung oder zu vorbestimmten Zeitpunkten anfallen.

**Anforderungen:**

* deterministisches zeitliches Verhalten -> Reihenfolge der Verarbeitungsschritte liegt eindeutig und wiederholbar fest
* Bearbeitung vieler externer Ereignisse mithilfe eines Unterbrechungskonzepts
* definierte Antwortzeiten einer Unterbrechung
* schnelle Reaktion -> geringer Overhead bei direkten Zugriffen oder Kontextwechsel
* Multitaskingfähigkeit (Vergabe des Prozessors an andere Prozesse bei Interrupts oder Timerablauf)
* prioritätsgesteuerter anlauf von Programmen
* effiziente und schnelle Interprozesskommunikation
* Einsatz in Systemen mit begrenzten Ressourcen (durch Skalierbarkeit)
* Lastunabhängigkeit muss garantiert sein
* Verwendung von Standardschnittstellen
* Kommunikation mit nicht Echtzeitsystemen
* Verfügbarkeit für verschiedene Prozessorarchitekturen
* optimierte Werkzeuge zur Entwicklung von Echtzeitanwendungen

### Task

* ist ein Ausführbares Programm inkl. aller dazu gahöriger aktueller Werte, Register, Variablen und Betriebsmittel (Speicher, I/O, Signale, usw.)
* Organisation in der **Task Control Block** (**TCB**) oder **Process Control Block** (**PCB**) Tabelle
* Der **PCB** enthält die Prozessinformationen sowie CPU- und Systemkontext für den jeweiligen Task.
* Die Prozessinformationen definieren den **Prozesszustand** (erzeugt, lauffähig, laufend, suspendiert, terminiert) sowie die **Prozesspriarität** (hoch, mittel, niedrig)

### Scheduler

* Zuordnung der Ausführungsreihenfolge von Prozessen bzw. Tasks (genannt Schedule)
  * Entscheidet anhand der Prozesspriarität welchem Lauffähigen Programm die CPU zugeordnet wird.
* zentrale Instanz eines Echtzeitbetriebssystems
* **zulässig** (feasible) wenn **alle Zeitbedingungen aller Tasks** im System **erfüllt sind** (keine Deadlines werden überschritten)
* **schedulebar** heißen Systeme, die für jede mögliche Aktivierungssequenz einen zulässigen Schedule besitzen
* **präemptives** (unterbrechendes) **Sheduling**:
  * von den meisten Echtzeitsystemen unterstützt
  * Tasks mit höherer Priorität unterbrechen laufende Tasks mit niedrigerer Priorität
* **kooperative Scheduling**:
  * Tasks geben freiwillig (zu einem ihm passenden Zeitpunkt) die CPU ab
* **Dispatcher** (Verteiler, operative Komponente):
  * zuständig für den Systemkontextwechsel (context switch)
  * wechsel von einem Task zu nächsten

#### Round-Robin-Verfahren

| Eigenschaft   | Wert                                                         |
| ------------- | ------------------------------------------------------------ |
| Beschreibung  | Jeder Task erhält einen gleichmäßigen Anteil der Rechenzeit. Dies **Zeitscheibe** (**time slice**) wird dabei so kurz gewählt, dass keine bemerkbaren Verzögerungen auftreten. |
| Einsatzgebiet | Mehrbenutzerbetriebssysteme/Timesharingsysteme (Linux, Windows NT, Unix...) |
| Echtzeitfähig | nein                                                         |
|               |                                                              |
|               |                                                              |

#### Earliest Deadline First Scheduling-Algorithmus (EDF)

* neigt zu überflüssigen Kontextwechsel
* unterbricht laufende Prozesse zu gunsten Prozesse mit kürzerer Laufzeit
* Berechnung der Laufzeit sporadischer Tasks ist aufwendig

| Eigenschaft   | Wert                                                         |
| ------------- | ------------------------------------------------------------ |
| Beschreibung  | Task mit nächstliegender Deadline wird ausgeführt.           |
| Besonderheit  | Produziert für jedes schedulebare Prozesssystem einen zulässigen Schedule |
| Einsatzgebiet | findet in der Praxis kaum Verwendung                         |
| Echtzeitfähig |                                                              |
|               |                                                              |

### Raten-monotone Scheduling (RMS)

| Eigenschaft   | Wert |
| ------------- | ---- |
| Beschreibung  |      |
| Einsatzgebiet |      |
| Echtzeitfähig |      |
|               |      |
|               |      |

### Multitasking

Hierbei werden mehrere Task scheinbar parallel (gleichzeitig) verarbeitet. Dabei wird die CPU unter den Tasks zeitlich aufgeteilt. Der wechsel erfolgt dabei meist so schnell das der Eindruck entsteht, das die Tasks gleichzeitig Ablaufen.

**Echtzeitbetriebssysteme** sind durchweg Multitasking-fähig, hierbei werden sie durch:

* Interrupts (Unterbrechungen)
* Timeouts (Zeitabläufen)
* Input events (Eingabeereignisse)

gesteuert.

# Embedded Systems

> Ein **verteiltes System** besteht aus Komponenten, die räumlich oder logisch verteilt sind und mittels einer Kopplung bzw. Vernetzung zum Erreichen der Funktionalität des Gesamtsystems beitragen.

> Ein **Steuergerät** (engl. Electronic Control Unit, ECU) ist die physikalische Umsetzung eines eingebetteten Systems. In mechatronischen Systemen bilden Steuergeräte und Sensorik/Aktuatorik oft eine Einheit.

> Wird Elektronik zur Steuerung und Regelung mechanischer Vorgänge räumlich eng mit den mechanischen Systembestandteilen verbunden, so sprechen wir von einem **mechatronischen System**. Der Forschungsbereich der sich mit der Entwicklung mechatronischer Systeme befasst nennt sich **Mechatronik**.

## Klassifikation und Charakteristika

### Technische Auspregung

* **kontinuierliche** Systeme
* **diskreten** Systeme
* **verteilten** Systeme
* **monolithischen** Systeme
* **hybriden** Systeme (sowohl kontinuierlichs als auch diskretes Verhalten)

> Systeme die sowohl kontinuierliche (analoge), als auch diskrete Datenteile (wertkontinuierlich) verarbeiten und/oder sowohl über kontinuierliche Zeiträume (zeitkontinuierlich), als auch zu diskreten Zeitbpunkten mit ihrer Umgebung interagieren, heißen **hybrid Systeme**.

### Sicherheitsrelevanz

* **Sicherheitskritische** Systeme (wenn Menschenleben oder die Unversehrtheit von Einrichtungen abhängt)
  z.B. Avionik, Medizintechnik und Kraftfahrzeugbereich
* **nicht Sicherheitskritische** Systeme 
  z.B. Konsumelektronik hauptsächlich nicht Sicherheitskritische Systeme
* **Zeitkritische** Systeme
* **nicht Zeitkritische** Systeme

### Produktkategorien

* Telekommunikation ( Telefon, Fax, etc.)
* Haushalt (Waschmaschine, Mikrowelle, Fernseher, etc.)
* Periphere Geräte (Tastatur, Modem, Drucker, etc.)
* Bürotechnik (Kopierer, Schreibmaschine etc.)
* Geräte für Freizeit, Hobby und Garten
* Automobiltechnik (ABS, Wegfahrsperre, Navigationssysteme, etc.)
  * Massenmarkt für eingebettete Systeme
  * häufig Zeit- und zunehmend auch sicherheitskritisch
* Öffentlicher Verkehr (Fahrkartenautomat, etc.)
* Luft- und Raumfahrttechnik
* Fertigungstechnik
* Steuerungs- und Regelungstechnik, Medizintechnik, Umwelttechnik, Militärtechnik
* Avionik (Flugzeugbau)
* uvm

### Klassifikation

#### Transformationelle Systeme

* Eingaben müssen zu beginn der Systemverarbeitung vollständig vorliegen
* Ausgaben nur verfügbar wenn die Verarbeitung vollständig terminiert
* Keine interaktion während der Verarbeitung möglich (=> kein Einfluss auf die Ergebnisse)

#### Interaktive Systeme

* Ausgabe nicht nur bei Terminierung
* Interaktion und Synchronisierung mit der Umgebung
* Interaktion wird durch das System bestimmt
* proaktive Synchronisierung durch das System

#### reaktive Systeme

> Ein reaktives System kann aus Software und/oder Hardware bestehen und setzt Eingabeereignisse deren zeitliches Auftreten meist nicht vorhergesagt werden kann - oftmals aber nicht notwendigerweise unter EInhaltung von Zeitvorgaben - in Ausgabeereignisse um.

- Synchronisierung dich Systemumgebung
- Reagieren auf ihre Umwelt
- Arbeiten häufig Nebenläufig
- müssen sehr zuverlässig sein
- müssen Zeitschranken einhalten (Echtzeitsysteme)
- sind in Hardware als auch Software realisiert
- werden in komplexen, verteilten Systemplattformen implementiert
- Die funktionale Korrektheit ist ein wichtiger Faktor der Entwicklung
- eingebettet in komplexe bsp. mechanische, chemische oder biologische Systemumgebung => eingebettete Systeme

## Bestandteile

* Kontrolleinheit
* Regelstrecke
* Benutzerschnittstelle
* technische Systemumgebung
* menschliche Systembenutzer

# Definitionen

> Als **Steuergerät** (engl. **Electronic Control Unit**, **ECU**) wird die eigentliche Steuereinheit eines mechatronischen Systems verstanden.
>
> Steuergeräte sind im Prinzip wie folgt aufgebaut: Die Kernkomponente des Steuergeräts stellt ein Mikrocontroller oder Mikroprozessor (Beispiele: Power PC, Alpha, PC) dar. Zusätzlich kann es optional ein externes RAM und/oder ROM besitzen sowie sonstige Peripherie und Bauelemente.
>
> Mikrocontroller kennzeichnen eine Klasse von Mikroprozessoren, die auf den speziellen Anwendungsbereich der Steuerung von Prozessen zugeschnitten sind. Wir betrachten im Folgenden einige Spezialfälle genauer.

> Ein **ASIP** (**applikationsspezifischer Prozessor**) ist ein Prozessor, der von seiner Struktur als auch von seinem Befehlssatz her auf seinen Einsatz für bestimmte Anwendungen hin optimiert ist. Er besitzt spezielle Instruktionssätze, funktionale Einheiten, Register und spezielle Verbindungsttrukturen. 
>
> * kostengünstiger aufgrund abgespeckter Prozessoren
> * aufgrund Programmierbarkeit flexibel
> * höhere Verarbeitungsgeschwindigkeit und geringere Leistungsaufnahme aufgrund optimierter Strukturen
> * **Nachteil** = komplizierte und aufwendige Entwicklung

> Ein **DSP** ist ein spezieller Mikroprozessor, der Befehle (und damit Verarbeitungseinheiten) zur Durchführung von Signal-Verarbeitungs-Aufgaben (bsp. Fast Fourier Transformation, **FFT**) besitzt. 
>
> * Optimiert auf die häufig vorkommenden Opperationen bei der digitalen Signalverarbeitung (bsp. schnelle Multiplikation)
> * hoher Stellenwert ist die Effizienz dieser Operationen
> * **Einsatz** bsp. MP3 decoder oder Sprachsignalverarbeitung oder Bildverarbeitung

> Das **Field Programmable Gate Array** (**FPGA**) ist ein komplexer, programmierbarer Logikbaustein, der zum Aufbau digitaler, logischer Schaltungen dient. Er besteht im Wesentlichen aus einzelnen Funktionsblöcken, die in einer regelmäßigen Struktur (**Array**) angeordnet sind, und einen Netzwerk von Verbindungen zwischen diesen Blöcken. Bei FPGAs wird die Implementierung von logischen Funktionen hauptsächlich durch die Programmierung der Verbindungsleitungen zwischen den Logikblöcken erreicht.
>
> * zwei Arten von FPGAs
>   * rekonfigurierbare (unter verwendung von Speichertechnologien wie SRAM)
>     * Nachteil: sie sind flüchtig
>   * nicht rekonfigurierbare (einmal Konfiguriert immer Konfiguriert, umsetzung durch physikalische Zerstörung der nicht benötigten Verbindungsleitungen)
> * Realisierung von Speicherzellen möglich
> * Eignung zur Realisierung von Steuererwerken (in Form endlicher Automaten)
> * Im Gegensatz zu gewöhnlichen **Gate Arrays** (**GA**) sind FPGAs programmierbare Logikbausteine, deren Funktionalität durch das Zusammenschalten verschiedener Funktionsblöcke erreicht wird 
