<script>
    alert("hello");
</script>

# Ziel der Schulung

In dieser Schulung soll das Konzept der regulären Ausdrücke insbesondere für Fachanwender erläutert werden.

Zu Beginn einfache Beispielübungen sollen diese Anwender zur Nutzung diese mächtigen Werkzeuges befähigen.

Technische Vorkenntnisse werden nicht vorausgesetzt, jedoch sind Grundkenntnisse in Office hilfreich.

# Was sind reguläre Ausdrücke?

Der Begriff „regulärer Ausdruck“ kommt aus der Informatik. Diese dient im wesentlichen zur Beschreibung von Zeichenketten in einem eher theoretischen Zusammenhang („reguläre Sprachen“).

Unabhängig davon kann dieses Konzept für ein sehr mächtiges und zielgerichtetes „Suchen und Ersetzen“ verwendet werden. Unter anderem bieten Excel und notepad++ diese Funktionalität.

# Schulungsumgebung

Für die Schulung beabsichtigen wir ein sogenanntes Notebook zur Verfügung zu stellen, in dem die regulären Ausdrücke erprobt werden können und die Lösung von Übungsaufgaben selbstverantwortlich kontrolliert werden kann.

Bislang ist nicht klar, auf welcher Plattform dies durchgeführt werden soll. Hier bieten sich google cloud services, microsoft azure oder eine lokale installation an. Inwieweit cloudera hier angemessen wäre ist zu klären.

# Schulungskonzeption

## Schulungskonzeption

Beschreibung der Schulungsumgebung und Vorgehensweise (noch offen, tbd).


## Lektion 1: Zeichen, Zahlen und Sonderzeichen

Wenn wir in der Praxis von Textdarstellungen sprechen, so geht es im wesentlichen um drei immer um drei Gruppen:

- Zeichen (a,b,c, … , z,A,B,C, … ,Z)
-	Zahlen (0,1,2, … 9)
-	Sonderzeichen (jedes „Textstückchen“, das nicht bereits schon oben dargestellt ist, z.B. !“§%& usw.)

Meistens wird hier der sog. ASCII Code verwendet, siehe hierzu ASCII Tabellen im Netz (z.B. https://de.wikipedia.org/wiki/American_Standard_Code_for_Information_Interchange).
Für die Übung stellen wir uns nun einen „Automaten“ vor, der für gegebene Zeichenketten Teilstrings findet. Wie er das tut, ist in diesem Schritt egal.

##	Übung 1: Zeichen, Zahlen und Sonderzeichen

###	Übung 1a: Zeichen

Im Beispiel sind folgende Zeichenketten (hier BICs) gegeben:

COBADEFFXXX

DEUTDEFFXXX

COBADEFFXXX

<div class="alpha">

-	Definiere Teilzeichenkette, die die Commerzbank BICs herausfiltern. 
-	Welches Zeichen charakterisiert Commerzbank BICs im Beispiel minimal (Achtung: Die Lösung ist nicht eindeutig).
-	Der Dezimale Ascii Code 40 stellt die linksoffene Klammer dar und kann mit der Tastenkombination Alt – 40 (Ziffernpad) abgerufen werden. Wie lautet der Ascii Code für das Zeichen „@“ ?

</div>
    
### Übung 1b: Ziffern

In einem Kommentarfeld werden Nachrichtentypen wie 
103 from 12.03.2016
MT103 dated Nov. 2016
MT202 blabla
Your 202
Your MT202Cov

- Definiere Teilzeichenkette, die nur aus Ziffern besteht und nur Text anzeigt, der sich auf den Nachrichtentyp MT103 bezieht. 
- Ist es möglich nur mit Ziffern alle Texte zu finden, die sich auf MT202xxx Transaktionen beziehen?

###	Übung 1c: Sonderzeichen

Sonderzeichen sind ein spezielles Thema. So bezeichnet der Punkt „.“ etwa eine Joker (wildcard) für ein beliebiges Zeichen (warum so etwas überhaupt Sinn macht erklären wir später). Für ein Sonderzeichen (also z.B. den Punkt) benötigt man eine spezielle Kennzeichnung, man muss dem Automat sagen dass jetzt das Zeichen Punkt kommt und nicht der wildcard. Dazu verwendet man den backslash: „ \\.“. 
Betrachte folgende Beispiele:
123.00 EUR
123.24 USD
MT103

- Finde über ein Sonderzeichen alle Textketten, die wie ein Betrag aussehen.
- Was würde passieren, wenn wir die obige Beispielliste um 100 SGD erweitern und dann die Abfrage unter a) erneut durchführen?

##	Lektion 2: Ein Zeichen einschließen oder ausschließen

In dieser Lektion betrachten wir das einschließen oder ausschließen eines einzelnen Zeichens bei der Suche in einem Text.
Die Syntax hierfür ist nicht besonders schwer:

-	[abc] bezeichnet ein Zeichen, das a, b oder c ist
-	[^abc] bezeichnet ein Zeichen, das nicht a, b oder c ist.
Mit diesem Baustein kann man nun differenziert Texte auswählen, wie wir in der nachfolgenden Übung sehen werden. 
Manchmal ist es sinnvoll ganze Bereiche zu Kennzeichnen:
-	[a-z] bezeichnet ein Zeichen „zwischen“ a und z
-	[0-9] bezeichnet eine Zahl „zwischen“ 0 und 9.

Dies wollen wir in nachfolgender Übung vertiefen.

### Übung 2: Ein Zeichen einschließen oder ausschließen

In dieser Übung betrachten wir die folgende Sammlung von IBANs und Kontonummern:
DE27100777770209299700 
DE11520513735120710131 
AT411100000237571500
AL90208110080000001039531801
BE68844010370034
DK5750510001322617
EE342200221034126658
400 654657
8051465
78988798654

-	Finde alle IBANs, die mit D beginnen (Tipp:verwende hierfür die [ ] - Syntax).
-	Finde alle IBANs, die nicht mit D beginnen.
-	Finde alle IBANs, die mit DE beginnen (Tip: wende die [ ] – Syntax zweimal an).
-	Finde alle IBANs im Text (Tip: Bereich)
-	Finde alle Kontonummern (Tip: Den Anfang einer Zeile kennzeichnet man mit ^).

## Lektion 3: Wiederholungsfaktoren

Mittlerweile wissen wir schon, wie man durch Wiederholung (DE) Ausdrücke erkennen kann. Da man nicht alles Tippen will gibt es Wiederholungsfaktoren:

-	{n}  muss n-mal vorkommen
-	{min,} muss mindestens min mal vorkommen
-	{0,max} darf höchstens max mal vorkommen
-	{min,max} kommt mindestens min mal und höchstens max mal vor

Einige Fälle werden mit eigenen Symbolen versehen (?, * oder +):

-	{0,} oder * kommt beliebig oft vor
-	{1,} oder + kommt mindestens einmal vor
-	{0,1}  oder ? ist optional, kommt 1 mal oder gar nicht vor.

Z.B. Ergibt [a]+ Treffer die Zeichenfolgen: a oder aa oder aaa , usw.
Achtung: a*  trifft immer irgendwas, denn jede Zeichenfolge enthält 0 mal das Zeichen a.

Diese Wiederholungsfaktoren sind gierig (greedy), dass heißt, sie versuchen möglichst treffen. Dies kann man sehr schön an einem Beispiel sehen:
Beispiel: Schauen wir uns den Text ABCDEB an. Dann trifft der reguläre Ausdruck A.*B nicht nur AB sondern findet ABCDEB.
Tatsächlich kann man diese Suche auch lazy schalten. Dies wird durch ein nachgestelltes Fragezeichen erreicht.
Beispiel: Schauen wir uns den Text ABCDEB an. Dann trifft der reguläre Ausdruck A.*?B tatsächlich AB.
In den nachfolgenden Übungen versuchen wir nun das Verständnis für Wiederholungsfaktoren zu schärfen."

###	Übung 3: Wiederholungsfaktoren

Wir verwenden wieder das Beispiel aus Übung 4.5.

- Finde alle IBANS, die mit einem A beginnen, dann einen beliebigen Buchstaben haben gefolgt von einer beliebigen Folge von Ziffern.
- 	Wie oben, jedoch mit 01 am Ende."

## Lektion 4: Leerzeichen und andere Hürden

Als Ergänzung zu obigen Lektionen sei hier noch erwähnt, dass mit \\d eine Ziffer bezeichnet wird und mit \\D eine Nicht – Ziffer. Analog bezeichnet \\w ein alphanumerisches (Ziffern und Zeichen!) und \\W ein nicht alphanumerisches Zeichen.
Oftmals benötigt man das mit \\s bezeichnete Leerzeichen (whitespace charakter) und als Gegenstück  \\S das Nicht – Leerzeichen.
Anwendungsmöglichkeiten werden wir in der nachfolgenden Übung aufzeigen.
Eine fortgeschrittene Ergänzung hierzu ist das Erkennen von Tabulatoren (\	) Zeilenumbrüchen (\\r).

###	Übung 4: Leerzeichen und andere Hürden

Betrachte den folgenden Beispielsatz:

DE27 1007 7777 0209 2997 00 

DE11520513735120710131

AT411100000237571500

AL90208110080000001039531801

BE68844010370034

DK5750510001322617

EE342200221034126658

400 654657

8051465

78 9887986 54

-	Erkenne die deutschen IBANs mit einem regulären Ausdruck, der die verschiedenen obigen Schreibweisen umfasst (Tip: Verwende \\d und \\s)
-	Erkenne Kontonummern, die an beliebigen Stellen (außer am Anfang) Leerzeichen enthalten können.
