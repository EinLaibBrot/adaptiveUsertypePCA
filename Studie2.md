# Erläuterungen zu Piri
Im Rahmen einer Masterarbeit wurden zwei verschiedene Bots in der Plattform Botpress entwickelt, die zur Durchführung zweier Studien vewendet wurden.
Beide Bots sind als Config-File zum Download hinterlegt und können in eigene Botpress Projekte geladen und wiederverwendet werden. Es gilt zu beachten, dass sich die Plattform Botpress seit Erstellung der Bots weiterentwickelt hat und z.T. einige Aspekte nach heutigem Stand auch anders hätten implementiert werden können.


# Bot Studie 2
Stellt die Nutzenden vor Lernaufgaben und bietet ihnen 1) nach einer Bestimmung des Nutzertypen 2) auf ihren Nutzertypen angepasste Gamification-Elemente und in einem anschließenden Durchgang 3) randomisierte Elemente.

Es werden folgende Dateien zum Download bereitgestellt:

 - Studie 2.bpz (Botpress Export)

![Ablauf](https://app.diagrams.net/?title=Prototyp1%20Ablauf.drawio#R1VlRV5swFP41POqBhNL2sa2tPrgdz7oddW9puYXMQLoQbOuvX1KSAqLWuSn4ArlfLiT57ndzU%2brgSbI9F2Qdf%2bEhMAe54dbBZw5Cnhf01E0juwOCCiQSNDRYCczpAxjQNWhOQ8hqjpJzJum6Di55msJS1jAiBN/U3Vac1UddkwgawHxJWBO9pqGMC3SA%2biV%2bATSK5WF9w6InIdbZrCSLScg3FQhPHTwRnMuilWwnwDR7lpfiudkzvYeJCUjlax4Iyc3y9y2ajb%2b5yeLu61ikP3Yn9jWZ3NkVQ6gIMCYXMuYRTwmbluhY8DwNQb/WVVbpc8n5WoGeAn%2bBlDsTTZJLrqBYJsz0Nqdup8FzsYQX5jswEiAiAvnSugzpejGVEQwz58ATkGKnHAQwIul9PdrEiCY6%2bJW8qoah9i9oNtO%2bJyw3IzkoYFKz4qtWpFs/85Uzwc7IZ4yqSSN3lGcbEjPrqQYunRtRq8dkE1MJ8zXZc7lRqVnn/x6EpErjIzVSqjCp4/Z8VLQ7bF%2bk0fSioeHdpntg7E2ZOxgbLK7kDfbdd6Iefy6B2z3uqMA7pW8rlFLfY4iElvN4oq/DWZ5Gjk7KgCRaa8VVIVPBCtXnEsTe6V%2bE/R8k/FjBflPBHnpCwcF7CdgL2lCwIlDsbvTzpz0XW%2bBWASfuqYsPyNnWjFFYu6p1BYIqDkAY8O1ZgV6ZFX6nsgI1suIMEh4JsqL7/X2xEvr00THFIx%2b3rfhh24qv6t09IvW3q9p/paq9fqdk7Tc3e5IBo6kW9UxLesEjSJWhIqKul/ROaVE1xkBSuVGh6eA%2bj/1%2by6oPGrR%2bv/J0ZS2Ofwthz34XsCWhhx6Tfait6SLTt5kAxeFWEz8qaNduLbOOh736ZoNaL6/uk7yjJu9zmYdq5Yyujgm9u3xjr3W%2bm1VR843fwPenULjvts74oOVy6rrDWkE99XvoY8%2bPtoIeLbWDTlVaO%2b1KrtTS4CFXyeJek1ikECcdrKp%2br23xo1Z%2b/3/8WdKSevzDQbe%2bHKBm%2be24xIP%2bo5Nj6xu8DWmFw9EiW8Ysz7LO0eW/4wlEmeX39H1f5W8JPP0D)

## Ziele

Der Bot soll aufbauend auf Studie 1 zeigen, dass eine Bestimmung der Nutzertypen praktisch möglich ist und, dass sich ein CA basierend auf diesem Wissen durch die Wahl der Spielelemente adaptiv verhalten kann und so die Nutzungserfahrung steigert.

Ablauf

 1. Begrüßung
 2. Bestimmung des Nutzertypen
 3. Task1 Ablauf
 4. 2 randomisierte Spielelemente
 6. Task 2 Ablauf
 7. 2 adaptive Spielelemente

## Dialog-Ausprägungen 🗣

### Hexad
Variante des von Krath et al. (2023) entwickelten verkürzten Fragebogens mit 12 Items. Nutzereingabe erfolgt in einer Buttonauswahl für eine Likert-Skala.

### Workflow Task1
Hier sind die ersten Aufgaben hinterlegt. Der Aufbau erfolgt typischerweise mit einem Frageblock und je nach gegebener Antwort wird zu einem "CorrectAnswer" oder "WrongAnswer" Block geroutet. Ein Counter zählt außerdem die Anzahl der korrekten Antworten mit.
Durch den Aufbau lassen sich leicht weitere Aufgaben ergänzen oder bestehende austauschen.

### Workflow Task2
Weiterer Ablauf von fünf Aufgaben. Der Aufbau ist relativ ähnlich zu Task1, um eine hohe Vergleichbarkeit gewährleisten zu können.

### Spielelemente
Pro Hexad Nutzertyp wurden zwei verschiedene Spieldesignelemente ausgewählt, die eine möglichst hohe Resonanz mit diesem Nutzertyp aufweisen (vgl. Tondello et al. 2016).
Diese werden exemplarisch erklärt und dargestellt. Die Nutzenden sollen diese anschließend bewerten.


## Technische Besonderheiten
Hier ist eine kurze Übersicht der technischen Besonderheiten.
### Variablen
Die Ergebnisse der Fragen werden in Workflow-Variablen gespeichert. Die wichtigsten Variablen werden im folgenden kurz erläutert.
|Variablen Name|Beschreibung  |
|--|--|
| stage |Zeigt momentan Stand im Ablauf und dient zur Orchestrierung (s.u.)|
| ge1, ge2, ge3 | Verwendete GameElements |
| usertype | Ermittelter Nutzertyp |
| {achiever, disruptor, socialicer, philanthropist, free, player}1,2 | Für alle Nutzertypen existieren zwei Variablen zur Speicherung des Userfeedbacks  |


### Ermittlung des Hexad-Nutzertypen nach Beantwortung aller Fragen der Baseline⁉️

Der Nutzertyp lässt sich berechnen nach dem folgenden Prinzip:

 1. Antworten auf die numerische Skala mappen. Bei den festen Antwortmöglichkeiten durch Buttons wird dafür die Position im Likert-Array bestimmt
 2. Einzelne Nutzertypenzustimmung berechnen (immer die Werte der entsprechenden zwei Items, die einen Nutzertyp aufladen, summieren.
 3. Nutzertyp mit der höchsten Summe ist der primär vorliegende Nutzertyp (können mehrere sein)


Eine nähere Erläuterung kann der Literatur entnommen werden (vgl. Krath et al. 2023).

### Adaptive Game Engine 🤖

Zur Navigation durch die verschiedenen Blöcke wird die Variable *stage* verwendet. Sie kann die folgenden Werte annehmen und dient als Routing-Bedingung:

| Value | Erläuterung  |
|--|--|
| 0 | Randomisiertes GameElement 1 wird aufgerufen |
| 1 | Randomisiertes GameElement 2 wird aufgerufen |
| 10 | Adaptives GameElement 1 wird aufgerufen |
| 11 | Adaptives GameElement 1 wird aufgerufen |
| 2 | Aufgabenblock 2 wird aufgerufen  |
| 12 | Ende wird aufgerufen |
|  |  |

Die AGE soll zuerst nach Ablauf von Task1 zwei verschiedene, zufällige Spielmechaniken (SM) präsentieren, die NICHT dem Hexad Nutzertyp entsprechen. Die dem Nutzertyp entsprechende SM werden in den Variablen *ut1* und *ut2* hinterlegt und ausgeschlossen, genau wie als zweite SM auch die bereits als erste SM verwendete Mechanik ausgeschlossen wird.

Im adaptiven Modus werden dann genau diese Mechaniken aus *ut1* und *ut2* verwendet.

### Datenspeicherung
Die erhobenen Daten werden innerhalb der Botpress Applikation in sogenannten DataTables gespeichert. Diese können als vereinfachte Datenbanken betrachtet werden.

**Data1Table** speichert das komplette Datenset, bestehend aus demographischen Daten, bestimmtem Nutzertyp und den dargestellten Spielmechaniken sowie der Nutzereinstellung.

**Data2Table** dient zur Speicherung der demographischen Daten direkt nach dem Ausfüllen dieser und kann so zur Betrachtung der Abbruchrate genutzt werden.

### Debug
Um den komplexen Ablauf leichter debuggen zu können und z.B. nicht immer den Hexad Fragebogen beantworten zu müssen, wurde ein _Debug Cheat_ eingebaut. Wird als Name "Debug" angegebenn, springt der Ablauf des Bots in den Debug Block und wird von dort zum hinterlegten Debug-Ziel geroutet.
