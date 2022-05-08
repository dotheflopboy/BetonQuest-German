# Events List

## Cancel quest: `cancel`

Dieses Event funktioniert genauso wie ein [Quest-Abbrecher im Rucksack](Reference.md#canceling-quests).
Das Ausführen ist gleichbedeutend damit, dass der Spieler auf den Knochen klickt. Das einzige Argument ist der Name eines Questabbrechers, wie im Abschnitt _cancel_ definiert

!!! example
    ```YAML
    cancel wood
    ```

## Chat player message `chat`

Dieses Event sendet die angegebene Nachricht als Spieler. Daher sieht es so aus, als hätte der Spieler die Nachricht gesendet.
Du kannst in diesem Event nur `%player%` als Variable verwenden.
Zusätzliche Nachrichten können definiert werden, indem sie mit  `|`  getrennt werden. Wenn du `|` in der Nachricht werden willst nutze `\|`.

Wenn ein Plugin nicht mit dem sudo / command-Event funktioniert, musst du dieses Event verwenden.

!!! example
    ``` YAML
    sendMSG: "chat Hallo!"
    sendMultipleMSGs: "chat Hey %player%|ban %player%|pardon %player%"
    sendPluginCommand: "chat /someCommand x y z"
    ```

## Chest Clear: `chestclear`
 
**persistent**, **static**

Dieses Event entfernt alle Gegenstände aus einer Truhe an einem bestimmten Ort. Das einzige Argument ist ein Standort.

!!! example
    ```YAML
    chestclear 100;200;300;world
    ```

## Chest Give: `chestgive`

**persistent**, **static**

Dies funktioniert genauso wie das `give` Event, aber es legt die Gegenstände in einer Truhe an einer bestimmten Stelle ab.
Das erste Argument ist ein Ort, das zweite Argument ist eine Liste von Elementen, wie im `give` Event.
Wenn die Truhe voll ist, werden die Gegenstände auf den Boden fallen gelassen.
Die Truhe kann jeder andere Block mit Inventar sein, z. B. ein Trichter oder ein Spender.
BetonQuest protokolliert einen Fehler in der Konsole, wenn dieses Ereignis ausgelöst wird, sich aber an der angegebenen Position keine Truhe befindet.

!!! example
    ```YAML
    chestgive 100;200;300;world emerald:5,sword
    ```

## Chest Take: `chesttake`
 
**persistent**, **static**

Dieses Event funktioniert genauso wie das `Take` Event, aber es nimmt Gegenstände aus einer Truhe an einem bestimmten Ort. 
Es wird genau so definiert wie das `chestgive` Event.

!!! example
    ```YAML
    chesttake 100;200;300;world emerald:5,sword
    ```

## Clear entities: `clear`

Dieses Event entfernt alle angegebenen Mobs aus dem angegebenen Bereich.
Das erste erforderliche Argument ist eine Liste von Mobs (ausgesucht von [here](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html)) durch Kommata abgetrennt.
Als nächstes kommt der Standort.
Danach folgt der Radius um den Standort (eine positive Zahl oder eine Variable). 
Optional kannst du das Argument `name:` angeben, gefolgt vom Namen, den entfernte Mobs haben müssen.
Du kannst das `marked:` Argument nutzen, um nur Mobs zu entfernen, die im `Spawn` Event markiert sind.

!!! example
    ```YAML
    clear ZOMBIE,CREEPER 100;200;300;world 10 name:Monster
    ```

## Compass: `compass`

Mit diesen Event kannst du ein Kompass-Ziel für den Spieler setzen oder löschen. You may also directly set the player's compass destination as well.
Wenn ein Ziel hinzugefügt wird, kann der Spieler einen bestimmten Ort als Ziel seines Kompasses auswählen.
Um das Ziel auszuwählen, muss der Spieler seinen Rucksack öffnen und auf das Kompasssymbol klicken.
Das erste Argument ist `add`,`del` oder `set`, und der zweite ist der Name des Ziels, wie im Abschnitt _compass_ definiert. 
Beachte: Wenn du ein Ziel setzt, wird es nicht automatisch als Ziel-Wahl des Spielers gesetzt.

Das Ziel muss im Abschnitt `compass` definiert sein. Du kannst für jede Sprache einen eigenen Ziel-Namen setzten oder einen allgemeinen Namen setzen, und optional ein eigenes item hinzufügen (aus dem _items_ Abschnitt) welches im Rucksack angezeigt wird.
Beispiel für ein Kompassziel:

```YAML
compass:
  beton:
    name:
      de: Ziel
      en: Target
      pl: Cel
    location: 100;200;300;world
    item: scroll
```

!!! example
    ```YAML
    compass add beton
    ```

## Command: `command`

**persistent**, **static**

Führt den angegebenen Befehl von der Konsole aus. Gebe den Befehl OHNE Schrägstrich an.
Du kannst hier Variablen verwenden, aber andere Variablen als `%player%` werden nicht funktionieren, wenn das Event von einen verzögerten `folder` Event ausgelöst wird
und der Spieler offline ist. Du kannst zusätzliche Befehle definieren, indem du sie mit dem Zeichen `|` trennst.
Wenn du das Zeichen `|` in einen Befehl verwenden willst nutze `\|`.

Suchst du nach [führe ein Befehl aus Spieler aus](#sudo-sudo)?

!!! example
    ```YAML
    command kill %player%|ban %player%
    ```

## Conversation: `conversation`

Startet ein Gespräch am Standort des Spielers. Das einzige Argument ist die ID der Konversation. Dies umgeht die Konversations-Permission!

!!! example
    ```YAML
    conversation village_smith
    ```

## Damage player: `damage`

Verletzt den Spieler um die angegebene Schadensmenge. Das einzige Argument ist eine Zahl (kann Gleitkommazahlen haben).

!!! example
    ```YAML
    damage 20
    ```

## Delete Point: `deletepoint`

**persistent**, **static**

Löschst die Spielerpunkte in einer bestimmten Kategorie.

!!! example
    ```YAML
    deletepoint npc_attitude
    ```

## Door: `door`

**persistent**, **static**

Dieses Event kann Türen, Falltüren und Zauntore öffnen und schließen. Die Syntax ist genau dieselbe wie im obigen `lever` Event.

!!! example
    ```YAML
    door 100;200;300;world off
    ```

## Remove Potion Effect: `deleffect`

Entfernt die angegebenen Trankeffekte vom Spieler. Nutze `any` anstelle einer Liste von Typen, um alle Trankeffekte vom Spieler zu entfernen.

!!! example
    ```YAML
    deleffect ABSORPTION,BLINDNESS
    ```

## Potion Effect: `effect`

Fügt dem Spieler einen bestimmten Trankeffekt hinzu.
Das erste Argument ist der Tranktyp. Sie finden alle verfügbaren Typen [hier](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/potion/PotionEffectType.html). 
Das zweite Argument ist eine Ganzzahl, die definiert, wie lange der Effekt in Sekunden anhält.
Das dritte Argument, ebenfalls ganzzahlig, definiert die Stärke des Effekts (1 bedeutet erstes Level).
Füge einen Parameter `ambient` hinzu, um Trankpartikel unsichtbarer erscheinen zu lassen (genauso wie Beacon-Effekte).
Um Partikel zu verbergen, fügen Sie einen Parameter `hidden` hinzu. Um das Symbol für den Effekt auszublenden, fügen Sie `noicon` hinzu.

!!! example
    ```YAML
    effect BLINDNESS 30 1 ambient icon
    ```

## Explosion: `explosion`

**static**

Erzeugt eine Explosion. Es kann Feuer machen und Blöcke zerstören. Du kannst auch die Leistung definieren, also achte darauf, deinen Server nicht wegzublasen.
Die Standard-TNT-Leistung ist 4, während Wither bei der Schöpfung 7 ist. Das erste Argument kann 0 oder 1 sein und gibt an, ob die Explosion Feuer erzeugen wird (wie Geister Feuerball).
Das zweite Argument ist auch 0 oder 1, aber dies definiert, ob der Block zerstört wird oder nicht.
Das dritte Argument ist die Leistung (Float-Zahl).
Das letzte Argument ist der Ort.

!!! example
    ```YAML
    explosion 0 1 4 100;64;-100;survival
    ```

## Folder: `folder`

**persistent**, **static**

Es ist so etwas wie ein Container für mehrere Events. Du kannst es verwenden, um deinen Code zu verschönern.
Es verfügt auch über eine optionale Verzögerung und einen in Sekunden gemessenen Zeitraum (Du kannst Ticks oder Minuten verwenden, indem du `ticks` oder `minutes` Argument hinzufügst).
Es ist Konstant für Events markiert als _persistent_, was bedeutet, dass die Events auch nach dem Abmelden des Spielers ausgelöst werden.
Beachten jedoch, dass alle Bedingungen falsch sind, wenn der Spieler offline ist (auch invertierte),
diese Events sollten also nicht durch irgendwelche Bedingungen blockiert werden!
Das einzige erforderliche Argument ist eine durch Kommas getrennte Liste von Events.

Es gibt auch drei optionale Argumente: `delay:`, `period:` und `random:`.
Delay und Period ist eine Anzahl von Sekunden.
Delay ist die Zeit vor der Ausführung und period ist die Zeit zwischen den einzelnen Events.
Es ist optional und es leer zu lassen ist dasselbe wie `delay:0` oder `period:0`.
Random ist die Anzahl der Events, die zufällig zum Auslösen ausgewählt werden. Es ist optional und wenn du es leer lässt oder weglässt, werden alle Events ausgelöst.

!!! example
    ```YAML
    folder event1,event2,event3 delay:5 period:5 random:1
    ```

## Give Items: `give`

Gibt dem Spieler vordefinierte Gegenstände. Sie werden genau so angegeben wie im  `item` Abschnitt definiert. Es können mehrere Gegenstände auf einmal gegeben werden, indem man sie mit einen Komma trennt, außerdem kann jeder Gegenstand eine Anzahl haben angegeben durch `:` gefolgt von der Anzahl nach den Gegenstand.
Die Standard-Anzahl ist 1.
Wenn der Spieler nicht den erforderlichen Platz im Inventar hat, werden die Gegenstände auf den Boden fallen gelassen, es sei denn, es handelt sich um Questgegenstände. Dann werden sie in den Rucksack gesteckt.
Du kannst dan Parameter `notify` angeben, um dem Spieler eine einfache Nachricht über den Erhalt von Gegenständen anzuzeigen.

!!! example
    ```YAML
    give emerald:5,emerald_block:9
    ```

## Give journal: `givejournal`

Dieses Event gibt dem Spieler einfach sein Tagebuch. Es verhält sich genauso wie der Befehl **/j**.

!!! example
    ```YAML
    givejournal
    ```

## Global point: `globalpoint`

**persistent**, **static**

Dies funktioniert auf die gleiche Weise wie das normale Punkte-Event, aber anstatt die Punkte für eine Kategorie eines bestimmten Spielers zu manipulieren, manipuliert es Punkte in einer globalen Kategorie.
Diese globalen Kategorien sind Spieler unabhängig, so kannst du zum Beispiel jedes Mal, wenn ein Spieler eine Quest macht, einen Punkt zu einer solchen globalen Kategorie hinzufügen und dem 100. Spieler, der die Quest macht, einige besondere Belohnungen geben.

!!! example
    ```YAML
    globalpoint global_knownusers 1
    ```

## Global tag: `globaltag`

**persistent**, **static**

Funktioniert genauso wie ein normales Tag-Event, aber anstatt ein Tag für einen Spieler zu setzen, wird es global für alle Spieler gesetzt.

!!! example
    ```YAML
    globaltag add global_areNPCsAgressive
    ```

## If else: `if`

Dieses Event prüft eine Bedingung und führt je nach Ergebnis das erste oder zweite Event aus.
Wird folgendermaßen definiert: `if condition event1 else event2`, wobei `condition` eine Bedingung-ID ist und `event1` und `event2` Event-IDs sind.
Das `else` Parameter ist ohne praktischen Grund zwischen den Events obligatorisch.

!!! example
    ```YAML
    if sonnig lass_es_regnen else lass_es_sonnig_sein
    ```

## Journal: `journal`

**static**

Fügt einen Eintrag zum/aus dem Tagebuch eines Spielers hinzu oder löscht ihn. Tagebucheinträge müssen im Abschnitt `journal` definiert werden.
Das erste Argument ist die auszuführende Aktion, der zweite ist der Name des Eintrags, falls erforderlich.
Tagebucheinträge ändern wird auch das Journal neu laden.

Mögliche Aktionen sind:
- `add`: Fügt dem Tagebuch eine Seite hinzu.
- `delete`: Löscht eine Seite aus dem Tagebuch
- `update`: Läd das Tagebuch neu. Dies ist besonders nützlich, wenn du die Hauptseite aktualisieren musst.

!!! example
    ```YAML
    journal add quest_started
    journal delete quest_available
    journal update
    ```

## Kill: `kill`

Tötet den Spieler. Nichts anderes.

## Kill Mobs: `killmob`
 
**persistent**, **static**

Tötet alle Mobs des angegebenen Typs am Ort.
Erstes Argument ist
die [Art des Mobs](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html).
Das nächste Argument ist der Ort.
Drittes Argument ist der Radius um den Ort, in dem sich die Mobs aufhalten müssen, um getötet zu werden.
Du kannst auch das Argument `name:` angeben, gefolgt vom Namen des Mobs, der getötet werden soll.
Alle `_`-Zeichen werden durch Leerzeichen ersetzt. Wenn du nur Mobs töten möchtest, die mit dem Spawn-Mob-Event markiert wurden, verwende `marked:` Argument gefolgt vom Schlüsselwort.
Mit diesem Event können nur Mobs getötet werden, die sich in geladenen Chunks befinden.

!!! example
    ```YAML
    killmob ZOMBIE 100;200;300;world 40 name:Bolec
    ```

## Language Event: `language`

Dieses Event ändert die Sprache des Spielers in die angegebene Sprache. Es gibt nur ein Argument, den Sprachnamen.

!!! example
    ```YAML
    language en
    ```

## Lever: `lever`

**persistent**, **static**

Dieses Event kann einen Hebel umschalten. Das erste Argument ist ein Ort und das zweite ein Zustand: `on`, `off` oder `toggle`.

!!! example
    ```YAML
    lever 100;200;300;world toggle
    ```

## Lightning: `lightning`

**static**

Schlägt an einem bestimmten Ort einen Blitz ein. Einziges Argument ist der Standort.

!!! example
    ```YAML
    lightning 100;64;-100;survival
    ```

## Notification: `notify`

Zeigt eine Benachrichtigung mit dem NotifyIO-System an.

!!! warning
    Alle Doppelpunkte (`:`) im Nachrichtenteil der Benachrichtigung müssen maskiert werden, einschließlich der Variablen.
    Ein Backslash (`\`) ist erforderlich, wenn überhaupt keine Anführungszeichen (`...`) verwendet werden oder einfache Anführungszeichen (`...`).
    Zwei Backslash sind erforderlich (`\\`) bei Verwendung von doppelten Anführungszeichen (`"..."`).

    Examples:<br>
    `eventName: notify Peter:Heya %player%!` :arrow_right: `eventName: notify Peter{++\++}:Heya %player%!`<br>
    `eventName: {=='==}notify Peter:Heya %player%!{=='==}` :arrow_right: `eventName: {=='==}notify Peter{++\++}:Heya %player%!{=='==}`<br>
    `eventName: {=="==}notify Peter:Heya %player%!{=="==}` :arrow_right: `eventName: {=="==}notify Peter{++\\++}:Heya %player%!{=="==}`<br>
    `otherEvent: notify You own %math.calc:5% fish!` :arrow_right: `otherEvent: You own %math.calc{++\++}:5% fish!`

| Option                                                             | Beschreibung                                                                                                                                                           |
|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| message  	                                                         | Die Nachricht, die angezeigt wird. Unterstützt Variablen und Übersetzungen. *Erforderlich, muss zuerst sein*            	                                             |
| category 	                                                         | Lädt alle Einstellungen aus dieser Benachrichtigungskategorie. Kann eine durch Kommas getrennte Liste sein. Die erste vorhandene Kategorie wird verwendet. *Optional* |   
| io       	                                                         | irgendeine [NotifyIO](Notification-IO's-&-Categories.md). Überschreibt die „Kategorie“-Einstellungen. *Optional*                                                              |
| [NotifyIO](Notification-IO's-&-Categories.md#notify-ios) 	         | Jede Einstellung aus dem definierten NotifyIO. Kann mehrfach verwendet werden. Überschreibt die „Kategorie“-Einstellungen. *Optional*                                                    |

Die Standard NotifyIO ist `chat`, wenn kein anderes Argument als `message` angegeben ist. 
`message` ist das einzige Argument dieses Event, das nicht `Schlüssel:Wert` basierent ist. Du kannst dort beliebigen Text mit Leerzeichen hinzufügen.

Es ermöglicht dir auch, mehrere Übersetzungen mit einer speziellen Syntax bereitzustellen:
```YAML
example: "notify {en} ABC {de} DEF"
```
Der Wert in `{}` ist der Sprach-Kürzel definiert in der messages.yml. Jeder Text zwischen den Sprach-Kürzeln gehört zur Sprache des vorherigen Sprach-kürzel. 
Zwischen dem Sprach-kürzel und der Nachricht muss ein Leerzeichen stehen.
In diesem Beispiel würden englische Benutzer `ABC` und deutsche `DEF` sehen.

<h3>Beispiele:</h3>

Sehe dir die Dokumentation zu [Notify Categories](Notification-IO's-&-Categories.md#categories) und 
[Notify IO options](Notification-IO's-&-Categories.md#notify-ios) an.
Du musst beides verstehen, wenn du das Notify-System in vollem Umfang nutzen möchtest.
```YAML
#Das einfachste aller Notify-Event nur eine Chat-Nachricht:
customEvent: "notify Hallo %player%!"  

#Es ist dasselbe wie oben, da `chat` die Standard-IO ist.
theSame: "notify Hallo %player%! io:chat"

#Dieser zeigt einen Titel und einen Untertitel an:
myTitle: "notify Dies ist ein Titel.\nDies ist ein Untertitel. io:title"

#Spielt eine sound:
mySound: "notify io:sound sound:x.y.z"

#Dieses Event nutzt die Bossbar NachrichtIO mit der Option der Balkenfarbe und einen sound:
myBar: "notify Dies ist eine benutzerdefinierte Nachricht. io:bossbar barColor:red sound:block.anvil.use"

#Einige Events mit Kategorien.
myEvent1: "notify Dies ist eine benutzerdefinierte Nachricht! category:info"
myEvent2: "notify Dies ist eine benutzerdefinierte Nachricht! category:firstChoice,secondChoice"

#Du kannst auch Kategorieeinstellungen überschreiben:
myEvent3: "notify Eine andere Nachricht! category:info io:advancement frame:challenge"

#Nutze mehrere Sprachen:
mehrereSprachen: "notify {en} Hello english person! {de} Hallo deutsche Person! {es} Hola españoles!"
```



## Broadcast: `notifyall`

Dieses Event funktioniert genauso wie [notify](#notification-notify) Event, zeigt aber die Benachrichtigung für alle Online-Spieler an.

## Objective: `objective`

**persistent**, **static**

Manages the objectives. Syntax is `objective <action> name`, where `<action>` can be _start_/_add_ (one of the two),
_delete_/_remove_ or _complete_/_finish_. Name is the name of the objective, as defined in the _objectives_ section.

Using this in static contexts only works when removing objectives!

!!! example
    ```YAML
    objective start wood
    ```

## OPsudo: `opsudo`

Dieses Event ist ähnlich wie das `sudo` Event, der einzige Unterschied ist, dass es ein Befehl als Spieler mit temporäre OP-Berechtigungen ausführt.
Zusätzliche Befehle können definiert werden, indem sie mit `|` getrennt werden. Wenn du ein `|`-Zeichen in der Nachricht verwenden möchtest, verwende `\|`.

Suchst du nach [führe ein Befehl als normaler Spieler aus](#sudo-sudo)?
Suchst du nach [führe Befehle von der Konsole aus](#command-command)?

!!! example
    ```YAML
    opsudo spawn
    ```

## Party event: `party`

Führt die angegebene Liste von Events (drittes Argument) für jeden Spieler in einer Party aus. Weitere Informationen zu Partys finden Sie im Kapitel `party` im **Reference** Abschnitt.

!!! example
    ```YAML
    party 10 has_tag1,!has_tag2 give_reward
    ```

## Pick random: `pickrandom`

**persistent**, **static**

Ein weiterer Container für Events. Es wählt ein (oder mehrere) der gegebenen Events und führt sie aus.
Du musst angeben wie wahrscheinlich es ist das jeweilige Event zu bekommen, indem du einen Prozentwert vor der Event-ID setzt.
Dieses Event funktionert auch mit einem Gesamtprozentwert über 100%. 

Es wählt Standardmäßig ein Event aus der Liste, aber du kannst das Argument `amount:` angeben, wenn du willst, dass mehrere ausgewählt werden.
Beachte das nur so viele Events wie vorhanden ausgewählt werden können und `amount:0` macht nichts.

Es müssen zwei `%%` vor dem Event-Name stehen, wenn Variablen verwendet werden, eins ist von der Variable und das andere ist von der Event-Syntax.

!!! example
    ```YAML
    pickrandom 20.5%event1,0.5%event2,79%event3 amount:2
    pickrandom %point.factionXP.amount%%event1,0.5%event2,79%event3,1%event4 amount:3
    ```
    
## Point: `point`

**persistent**

Gibt dem Spieler eine bestimmte Anzahl von Punkten in einer bestimmten Kategorie. Der Betrag kann negativ sein, wenn Sie Punkte abziehen möchten.
Sie können auch ein Sternchen zum Multiplizieren verwenden (oder Division, wenn Sie einen Bruch verwenden).
Das erste Argument nach dem Event-Namen muss eine Kategorie sein, und das zweite - die Anzahl der Punkte, die vergeben/genommen/multipliziert werden sollen.
Dieses Event unterstützt auch ein optionales `notify` Argument, das Informationen über die Änderung mithilfe des Benachrichtigungssystems anzeigt.

!!! example
    ```YAML
    point npc_attitude 10
    ```
    
!!! example    
    ```YAML
    point village_reputation *0.75
    ```

## Run events: `run`

**persistent**, **static**

Mit diesem Event kannst du mehrere Anweisungen in einer angeben. Jede Anweisungen muss mit einem `^`  Zeichen starten (es trennt alle Anweisungen).
Es ist nicht dasselbe wie das `folder` Event, weil du die eigentliche Anweisung angeben musst, nicht nur den Event-Namen.
Es wird auch beim selben Tick gefeuert, nicht beim nächsten wie bei `folder`.
Verwenden Sie hier keine Bedingungen, es verhält sich seltsam. Wir werden dies in 2.0 beheben.

!!! example
    ```YAML
    run ^tag add beton ^give emerald:5 ^entry add beton ^kill
    ```

## Scoreboard: `score`

Dieses Event funktioniert genauso wie das `point`-Event, der einzige Unterschied besteht darin, dass es Scoreboards anstelle von Punkten verwendet. Sie können Punktzahlen in Zielen auf der Anzeigetafel addieren, subtrahieren, multiplizieren und dividieren.
Das erste Argument ist der Name des Ziels, das zweite eine Zahl. Es kann positiv für die Addition, negativ für die Subtraktion oder mit einem vorangestellten Sternchen für die Multiplikation sein. Das Multiplizieren mit Brüchen ist dasselbe wie das Dividieren.


!!! example
    ```YAML
    score kills 1
    ```

## Set Block: `setblock`

**persistent**, **static**

Ändert den Block an der angegebenen Position.
Das erste Argument ist ein [Block](../Reference/#block-selectors), das zweite ein Ort.
Sehr mächtig, wenn es zum Auslösen von Redstone-Apparaten verwendet wird.

!!! example
    ```YAML
    setblock REDSTONE_BLOCK 100;200;300;world
    ```

## Spawn Mob: `spawn`

**persistent**, **static**

Spawnt eine bestimmte Anzahl von Mobs eines bestimmten Typs am Ort. Das erste Argument ist ein Standort.
Das nächste ist [die Art des Mobs](https://hub.spigotmc.org/javadocs/spigot/org/bukkit/entity/EntityType.html). Das letzte, dritte Argument ist eine Ganzzahl für die Menge der zu spawnenden Mobs.
Sie können auch das Argument `name:` angeben, gefolgt vom Namen des Mobs. Alle `_` Zeichen werden mit Leerzeichen ersetzt. Sie können den gespawnten Mob auch mit einem Schlüsselwort markieren, indem Sie das Argument `marked:` verwenden.
Es wird nirgendwo angezeigt, und Sie können im Ziel `mobkill` nun nach markierten Mobs suchen.

Sie können die Rüstung angeben, die der Mob tragen wird, und die Gegenstände, mit denen er ausgestattet ist `h:` (Helm), `c:` (Brustpanzer), `l:` (Hose), `b:` (Schuhe), `m:` (Haupt Hand) and `o:` (Neben Hand) optionale Argumente. 
Dies nimmt ein Gegenstand ohne die Anzahl, so wie in dem _items_ Abschnitt definiert. Du kannst auch eine Liste von fallen gelassenen Gegenständen mit dem Argument `drops:` definieren, gefolgt von einer Liste mit Gegenständen mit Anzahl nach Doppelpunkt, geteilt durch Komma.

!!! example
    ```YAML
    spawn 100;200;300;world SKELETON 5 marked:targets
    ```

!!! example
    ```YAML
    spawn 100;200;300;world ZOMBIE name:Bolec 1 h:blue_hat c:red_vest drops:emerald:10,bread:2
    ```

## Sudo: `sudo`

Dieses Event ist ähnlich wie das `command` Event, der einzige Unterschied ist, dass es einen Befehl als Spieler auslöst (oft als Spielerbefehle bezeichnet).
Zusätzliche Befehle können definiert werden, indem sie mit  `|` getrennt werden. Wenn du das Zeichen `|` in einen Befehl nutzen willst nutze `\|`.

Suchst du nach [führe einen Befehl als OP aus](#opsudo-opsudo)?
Suchst du nach [Konsolen Befehl](#command-command)?

!!! example
    ```YAML
    sudo spawn
    ```

## Tag: `tag`

**persistent**, **static**

Dieses Event fügt dem Spieler ein Tag hinzu (oder entfernt es). Das erste Argument nach dem Namen des Events muss `add` oder `del` sein.
Als nächstes kommt der Tag-Name. Es darf keine Leerzeichen enthalten ( `_` jedoch ist okay). Zusätzliche Tags können durch Kommas getrennt (ohne Leerzeichen) hinzugefügt werden.

!!! example
    ```YAML
    tag add quest_started,new_entry
    ```

## Take Items: `take`

Entfernt Gegenstände aus dem Inventar, den Rüstungsfächern oder dem Rucksack des Spielers.
Die Gegenstände selbst müssen im Abschnitt `items` definiert werden, optional mit Anzahl nach einem Doppelpunkt.
Welche Inventar typen geprüft werden, wird durch `invOrder:` definiert.
Du kannst `Backpack`, `Inventory`, `Offhand` und `Armor` hier verwenden. Sind mehrere Typen definiert, wird nacheinander geprüft.

!!! danger
    Hinweis: Wenn es sich bei den Items nicht um Quest-Items handelt, verwenden Sie in Gesprächen kein `take`-Event mit Spieleroptionen!
    Der Spieler kann Gegenstände fallen lassen, bevor er die Option auswählt, und sie nach dem Auslösen des Events aufheben.
    Bestätigen Sie es anhand der Reaktion des NPCs!

Du kannst auch das Schlüsselwort `notify` angeben, um dem Spieler eine einfache Nachricht über den Verlust von Gegenständen anzuzeigen.

!!! example
    ```YAML
    take emerald:120,sword
    take nugget:6 notify
    take wand notify invOrder:Backpack
    take money:50 invOrder:Backpack,Inventory
    take armor invOrder:Armor,Offhand,Inventory,Backpack
    ```

## Time: `time`

Stellt die Zeit ein oder fügt sie hinzu. Das einzige Argument ist die festzulegende Zeit (Ganzzahl) oder die hinzuzufügende Zeit (Ganzzahl mit vorangestelltem +),
in 24 Stunden Format. Das Subtrahieren von Zeit erfolgt durch Hinzufügen von mehr Zeit (wenn Sie daran denken, macht es tatsächlich Sinn).
Minuten können mit Fließkomma erreicht werden.

!!! example
    ```YAML
    time +6
    ```

## Teleport: `teleport`

Teleportiert den Spieler an einen bestimmten Ort, mit oder ohne Kopfdrehung. Es wird auch das Gespräch beenden,
wenn der Spieler eins aktiv hat. Das erste und einzige Argument muss der Ort sein. Es ist eine gute Idee hier yaw und pitch zu verwenden.

!!! example
    ```YAML
    teleport 123;32;-789;world_the_nether;180;45
    ```

## Variable: `variable`

Dieses Event hat nur einen Zweck: Werte ändern, die in `variable` Ziele gespeichert sind. Das erste Argument ist
die ID des `variable` Ziels. Das zweite Argument ist der Name der zu setzenden Variablen.
Das dritte Argument ist die Wert zum einzustellen. Sowohl der Name als auch der Wert können `%...%`-Variablen verwenden. Um eine Variable zu löschen, können Sie `""` verwenden.
Sieh dir die [`variable` objective](Objectives-List.md#variable-variable) Dokumentation für weitere Informationen zum Speichern von Variablen an.
Dieses Event hat keine Auswirkung, wenn dem Spieler nicht bereits ein `variable` Ziel zugewiesen wurde.

!!! example
    ```YAML
    variable CustomVariable MyFirstVariable Goodbye!
    variable variable_objectiveID name %player%
    variable other_var_obj desc ""
    ```

## Weather: `weather`

Stellt das Wetter ein. Das Argument ist `sun`, `rain` oder `storm`.

!!! example
    ```YAML
    weather rain
    ```
    
## Give experience: `experience`

Gibt dem Spieler die angegebene Menge an Erfahrungspunkten. Du kannst auch ganze Level geben, idem du das Argument `level` hinzufügst.

!!! example
    ```YAML
    experience 4 level
    ```
