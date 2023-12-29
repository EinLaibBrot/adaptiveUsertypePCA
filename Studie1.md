# Erläuterungen zu Piri
Im Rahmen einer Masterarbeit wurden zwei verschiedene Bots in der Plattform Botpress entwickelt, die zur Durchführung zweier Studien vewendet wurden.
Beide Bots sind als Config-File zum Download hinterlegt und können in eigene Botpress Projekte geladen und wiederverwendet werden. Es gilt zu beachten, dass sich die Plattform Botpress seit Erstellung der Bots weiterentwickelt hat und z.T. einige Aspekte nach heutigem Stand auch anders hätten implementiert werden können.


# Bot Studie 1
Kann auf verschiedenen Wegen und Dialogen die Hexad-Nutzertypen der Anwendenen bestimmen.

Es werden folgende Dateien zum Download bereitgestellt:

 - Studie 1.bpz (Botpress Export)
 - counter.js (Node.JS Server für den Nutzerzugriffscounter)
 - api2.js (Node.JS Server für die Speicherung und Darstellung der Ergbnisse)

![Ablauf](https://app.diagrams.net/?title=Prototyp1%20Ablauf.drawio#R1VlRV5swFP41POqBhNL2sa2tPrgdz7oddW9puYXMQLoQbOuvX1KSAqLWuSn4ArlfLiT57ndzU%2brgSbI9F2Qdf%2bEhMAe54dbBZw5Cnhf01E0juwOCCiQSNDRYCczpAxjQNWhOQ8hqjpJzJum6Di55msJS1jAiBN/U3Vac1UddkwgawHxJWBO9pqGMC3SA%2biV%2bATSK5WF9w6InIdbZrCSLScg3FQhPHTwRnMuilWwnwDR7lpfiudkzvYeJCUjlax4Iyc3y9y2ajb%2b5yeLu61ikP3Yn9jWZ3NkVQ6gIMCYXMuYRTwmbluhY8DwNQb/WVVbpc8n5WoGeAn%2bBlDsTTZJLrqBYJsz0Nqdup8FzsYQX5jswEiAiAvnSugzpejGVEQwz58ATkGKnHAQwIul9PdrEiCY6%2bJW8qoah9i9oNtO%2bJyw3IzkoYFKz4qtWpFs/85Uzwc7IZ4yqSSN3lGcbEjPrqQYunRtRq8dkE1MJ8zXZc7lRqVnn/x6EpErjIzVSqjCp4/Z8VLQ7bF%2bk0fSioeHdpntg7E2ZOxgbLK7kDfbdd6Iefy6B2z3uqMA7pW8rlFLfY4iElvN4oq/DWZ5Gjk7KgCRaa8VVIVPBCtXnEsTe6V%2bE/R8k/FjBflPBHnpCwcF7CdgL2lCwIlDsbvTzpz0XW%2bBWASfuqYsPyNnWjFFYu6p1BYIqDkAY8O1ZgV6ZFX6nsgI1suIMEh4JsqL7/X2xEvr00THFIx%2b3rfhh24qv6t09IvW3q9p/paq9fqdk7Tc3e5IBo6kW9UxLesEjSJWhIqKul/ROaVE1xkBSuVGh6eA%2bj/1%2by6oPGrR%2bv/J0ZS2Ofwthz34XsCWhhx6Tfait6SLTt5kAxeFWEz8qaNduLbOOh736ZoNaL6/uk7yjJu9zmYdq5Yyujgm9u3xjr3W%2bm1VR843fwPenULjvts74oOVy6rrDWkE99XvoY8%2bPtoIeLbWDTlVaO%2b1KrtTS4CFXyeJek1ikECcdrKp%2br23xo1Z%2b/3/8WdKSevzDQbe%2bHKBm%2be24xIP%2bo5Nj6xu8DWmFw9EiW8Ysz7LO0eW/4wlEmeX39H1f5W8JPP0D)

## Ziele

Der Bot von Studie 1 verfolgt das Ziel, die Umsetzung der Hexad-Nutzertypen Bestimmung zuerst durch die etablierte Fragebogen Methodik mit einer Likert-Skala zu bestimmen und anschließend die Ergebnisse mit einem von drei verschiedenen anderen Bestimmungsansätzen zu vergleichen. Es wird somit die Ergebnissgenauigkeit zur Baseline verglichen, als auch die wahrgenommene Nutzungserfahrung durch den UEQ-Fragebogen.

## Dialog-Ausprägungen 🗣
Es stehen folgende Ausprägungen zur Bestimmung des Hexad-Nutzertyps zur Verfügung:
### Baseline
Variante des von Krath et al. (2023) entwickelten verkürzten Fragebogens mit 12 Items. Nutzereingabe erfolgt in einer Buttonauswahl für eine Likert-Skala.

### Ausprägung 1 - Hexad-12-AI
Diese Version verwendet ebenso den Fragebogen nach Krath et al., lediglich die Antworten werden durch das Freitext-Chatfenster erfasst und durch "AI Tasks" ausgewertet.

Beispiel eines Prompts zur Auswertung
`The user was asked: "Du hilfst deinen Kommilitonen gerne bei ihren Aufgaben. Wie sehr trifft das auf dich zu?"
Match his answer to a likert scale from 1 to 7. 1 is "i dont like to help at all" and 7 "i love to help."`

### Ausprägung 2 - UniStory
Hier werden anstelle der Items nach Krath et al. eigene Formulierungen verwendet, die mehr an den Alltag von Studierenden angepasst sind. Nutzereingabe erfolgt in einer Buttonauswahl für eine Likert-Skala.

### Ausprägung 3 - UniStory AI
Diese Version verwendet ebenso den an den Universitätsalltag angepassten Fragebongen, lediglich die Antworten werden durch das Freitext-Chatfenster erfasst und durch "AI Tasks" ausgewertet (siehe Ausprägung 1).


### UEQ Fragebogen
Jeweils nach der Baseline und nach der randomisierten Ausprägung erfolgt ein Block mit der Kurzversion des UEQ Fragebogens.

## Technische Besonderheiten
Hier ist eine kurze Übersicht der technischen Besonderheiten.
### Variablen
Die Ergebnisse der Fragen werden in Workflow-Variablen gespeichert. Die wichtigsten Variablen werden im folgenden kurz erläutert.
|Variablen Name|Beschreibung  |
|--|--|
| path |Randomisiert zw. 1-3, entscheidet welche Ausprägung abgefragt wird.|
| playertype1a | Ermittelter Nutzertyp der Baseline |
| playertype1b | Ermittelter Nutzertyp bei Ausprägung 1 |
| playertype3a | Ermittelter Nutzertyp bei Ausprägung 2 |
| playertype3a | Ermittelter Nutzertyp bei Ausprägung 3 |
| UEQ_raw_X | UEQ Items der Baseline |
| UEQ_v_X | UEQ Items der Ausprägung |

Außerdem wurden in dem Bot folgende Umgebungsvariablen hingefügt, um die Zugriffsdaten für den Statistikserver zu speichern. Die Daten wurden in der hier hochgeladenen Version anonymisiert.

### Ermittlung des Hexad-Nutzertypen nach Beantwortung aller Fragen ⁉️

Der Nutzertyp lässt sich berechnen nach dem folgenden Prinzip:

 1. Antworten auf die numerische Skala mappen
	 2. Bei den festen Antwortmöglichkeiten durch Buttons wird dafür die Position im Likert-Array bestimmt
	 3. Bei Freitextantworten wird eine AI-Task beauftragt
 2. Einzelne Nutzertypenzustimmung berechnen (immer die Werte der entsprechenden zwei Items, die einen Nutzertyp aufladen, summieren.
 3. Nutzertyp mit der höchsten Summe ist der primär vorliegende Nutzertyp (können mehrere sein)


Eine nähere Erläuterung kann der Literatur entnommen werden (vgl. Krath et al. 2023).

### Orchestrator 🤖

Zur Auswahl einer der Ausprägungen wird die Variable _path_ in einem Codeblock durch eine JavaScript-Funktion mit einem zufälligen Wert gefüllt. Anschließend sind Transitions eingebaut, die je nach Wert von _path_ den nächsten Block aufrufen.

### API as a Storage
Der Codeblock _counter++_ nach Abfrage der demographischen Daten ruft eine URL auf einem Server auf. Dadurch wird dort ein Zähler hochgezählt, sodass die Anzahl der Nutzenden an diesem Punkt ermittelt werden kann. Die Funktionsweise dafür ist in der *counter.js* Datei hinterlegt.

Die gesammelten Werte werden in einer JSON-Nachricht am Ende des Ablaufs zu einem Server gesendet und dort lokal in einer csv-Datei gespeichert. Dieser bietet als Node.JS Applikation die Endpunkte:

|Endpunkt|Funktion|
|--|--|
| /storedata | Speichern der Ergebnisse eines Durchgangs |
| /view-data |  Anschauen der bisherigen Ergebnisse in tabellarischer Form|
|  /download| Download der csv-Datei |

Die Applikation verwendet einen apiKey, der zum Aufruf einer der Endpunkte im http-Header mitgesendet werden muss.
