# Ticketkasse

Abendkasse für Veranstaltungen: Karten verkaufen, drucken und am Eingang
prüfen. Eine einzige HTML-Datei, ohne Server, ohne Netz, ohne
Abhängigkeiten.

**Im Browser öffnen:** https://joergroeloffs-coder.github.io/Ticketmanager/

## Für den Anfang: die Bedienungsanleitung

Wer die Kasse zum ersten Mal öffnet, nimmt am besten
**[`Bedienungsanleitung.pdf`](Bedienungsanleitung.pdf)** — sieben Seiten,
farbig, mit Bildschirmfotos: einrichten, verkaufen, drucken, Einlass, zwei
Geräte, abrechnen, und eine Tabelle für den Fall, dass etwas klemmt. Zum
Ausdrucken und Danebenlegen gedacht.

Dieses README ist die vollständige Beschreibung mit allen Einzelheiten; die
Anleitung ist der Weg hinein. Sie entsteht aus `Bedienungsanleitung.html` —
eine einzelne Datei mit eingebetteten Bildern, die sich im Browser über
*Drucken → Als PDF sichern* neu ausgeben lässt.

## Wie es arbeitet

Jede Karte trägt einen QR-Code aus drei Teilen: dem Kürzel der
Veranstaltung, einer laufenden Nummer und einer Signatur (HMAC-SHA-256,
gerechnet mit dem Schlüssel aus den Einstellungen). Ohne den Schlüssel
lässt sich keine gültige Karte malen; ohne die gespeicherte Liste lässt
sich keine zweimal einlösen.

Gerechnet wird in ganzen Cent. Die Daten liegen im Speicher des Browsers,
pro Gerät getrennt. Wer das Gerät wechselt oder den Abend sichern will,
nimmt *Einstellungen → Sicherung → Exportieren*.

Sollen mehrere Geräte denselben Abend führen, gibt es zwei Wege: die
Sicherung von Hand herüberreichen und *zusammenführen*, oder die **Ablage**
im eigenen Drive, aus der sich die Geräte selbst versorgen. Beides ist
Zugabe — ohne das arbeitet die Kasse für sich allein weiter.

## Als Programm einrichten

Die Kasse lässt sich wie ein gewöhnliches Programm ablegen — mit eigenem
Symbol und eigenem Fenster ohne Adresszeile. Am Eingang ist das mehr als
Zierde: es gibt dann nichts, worüber jemand versehentlich wegnavigiert.

- **Windows, Chrome oder Edge:** Adresse öffnen, im Menü ⋮ auf *Ticketkasse
  installieren*. Fehlt der Eintrag: *Weitere Tools → Verknüpfung erstellen*,
  dort *In neuem Fenster öffnen* ankreuzen.
- **Android, Chrome:** Menü ⋮ → *App installieren*.
- **iPhone und iPad, Safari:** Teilen-Knopf → *Zum Home-Bildschirm*.
- **macOS:** in Chrome wie unter Windows; in Safari *Ablage → Zum Dock
  hinzufügen*.

Wer nur eine Verknüpfung will, zieht das Symbol links in der Adresszeile auf
den Schreibtisch.

### Das Symbol

Auf dem Schreibtisch und dem Home-Bildschirm steht das gezeichnete Symbol des
Vereins: die goldene Karte mit dem QR-Code in der grünen Wanne. Es liegt als
`symbol-quelle.png` (1024 Punkte) bei; daraus entstehen `icon-512.png`,
`icon-192.png`, `icon-32.png`, `apple-touch-icon.png` und
`icon-maskable-512.png`. Das letzte hat rundum Luft, weil Android sich aus dem
Symbol einen Kreis oder ein Kleeblatt schneidet, wie es dem Gerät gefällt.

Im Reiter des Browsers ist es anders. Dort bleiben sechzehn Punkte, und ein
gerendertes Bild wird auf sechzehn Punkten zu einem Fleck — die Karte, die
Wanne, der Wagen, alles fällt zusammen. Dafür liegt `favicon.svg` bei, eine
flache Zeichnung derselben Sache in denselben Farben: sie trägt bis ganz
hinunter. Der Reiter nimmt sie, der Schreibtisch das Bild. Daneben liegt
`favicon-b.svg`, ein zweiter flacher Entwurf mit dem Suchmuster eines
QR-Codes statt der Karte.

Aus einer heruntergeladenen Datei heraus greifen Symbol und Einrichtung
nicht — dafür braucht es die Adresse.

## Am Eingang

Über die Adresse oben liest die Kasse QR-Codes mit der Kamera — auf
jedem Gerät, auch auf iPhone und iPad. Sie bringt den QR-Leser selbst
mit (jsQR, Apache-2.0, im Quelltext); wo der Browser einen eingebauten
hat, wird der genommen, weil er schneller ist.

Aus einer heruntergeladenen Datei heraus (`file://`) bleibt die Kamera
aus — das untersagen alle Browser, und daran lässt sich nichts drehen.
Verkauf, Druck und das Eintippen des Codes funktionieren dort trotzdem
vollständig. Für den Einlass ist die Adresse oben der richtige Weg.

## Eine Karte für mehrere Plätze

An der Kasse steht unter *Codes* die Wahl: **je Platz ein Code** oder **ein
Code für alle**. Beim zweiten bekommt eine Familie eine Karte statt vier;
darauf steht, woraus sie besteht („2 Erwachsene, 2 Kinder") und für wie
viele sie gilt.

Die Platzzahl steht **in der Nummer** und ist damit mitsigniert:
`SF26-A0007X4` ist eine Karte für vier. Das ist kein Schönheitsfehler,
sondern der Kern: am Eingang wird eine unbekannte Karte nachgetragen —
stünde die Vier nur beim verkaufenden Gerät, zählte die Tür sie als eine
Person. So liest jedes Gerät sie direkt aus dem Code, und aus `X4` ein `X9`
zu machen zerstört die Signatur.

Am Einlass steht dann groß **„Gültig · 4 Personen"**. Gezählt werden in der
Übersicht Plätze, nicht Karten — eine Familienkarte ist ein Stück Papier,
aber vier Leute im Saal. Eine Nummer ohne `X` heißt eine Person; alle
vorher gedruckten Karten bleiben gültig.

## Druck auf Etiketten

Neben „mehrere pro Seite" und „eine pro Seite" steht an der Kasse
**Etikettenbogen**: dreißig Karten in einem Rutsch auf Aufkleber, als
Eintrittskarten oder Gutscheine.

Voreingestellt ist das verbreitetste Herma-Raster — 70 × 37 mm, 24 je
Bogen, drei mal acht, randlos. Steht auf deiner Packung etwas anderes,
trägst du es unter *Einstellungen → Etikettenbogen* ein; alle Maße sind in
Millimetern einstellbar.

### Etiketten- und Thermodrucker

Geräte, die einzelne Schildchen oder eine endlose Bahn ziehen — Brother,
Dymo, Zebra, Bondrucker — kennen kein A4. Für sie steht an der Kasse die
vierte Anordnung: **Etikettendrucker**, ein Ticket je Etikett.

Das Maß trägst du unter *Einstellungen → Etikettenbogen* ein, im unteren
Teil: Breite, Höhe und Rand in Millimetern. Voreingestellt sind 62 × 29 mm.
**Die Höhe leer zu lassen heißt fortlaufend** — dann bestimmt der Inhalt, wie
weit das Papier vorgeschoben wird; das ist der Weg für Bondrucker.

Das Seitenmaß setzt die Kasse vor jedem Druck neu. Nach einem Etikettendruck
steht A4 wieder auf A4, ohne dass jemand etwas umstellen müsste.

*Probeetikett drucken* wirft ein einzelnes Schildchen mit gestricheltem
Rahmen und den eingetragenen Maßen aus. Sitzt der Rahmen auf der Kante des
Etiketts, stimmt das Maß.

**Vor dem ersten guten Bogen:** *Ausrichtung drucken* liefert ein Blatt mit
nur den leeren Feldern. Auf weißes Papier drucken und gegen einen
Etikettenbogen halten. Stimmt es nicht, liegt es fast immer am Druckdialog
— dort muss **Tatsächliche Größe** oder **100 %** stehen, nicht „An Seite
anpassen". Das schrumpft den Bogen um ein paar Prozent, und ab der zweiten
Reihe steht alles daneben.

Der QR-Code misst auf dem Etikett 29 mm bei 25 Modulen, also einen
Millimeter je Punkt — reichlich für jede Handykamera.

## Ton am Einlass

Wer die Karte hinhält, schaut nicht auf den Bildschirm. Deshalb gibt die
Kasse Laut: ein heller, steigender Zweiklang für gültig, ein tiefes Brummen
für abgewiesen. Im Dunkeln vor der Tür unterscheidet man das ohne
hinzusehen. Abschalten unter *Einstellungen → Einlass → Ton beim Prüfen*.

Die Töne werden im Browser erzeugt, nicht aus Dateien geladen — die Kasse
bleibt eine einzige Datei. Der erste Ton kommt allerdings erst, nachdem
einmal auf *Prüfen* oder *Kamera* getippt wurde: vorher lässt kein Browser
Klang zu.

## Was sich ändern lässt, und was nicht

Veranstaltungen und Kategorien lassen sich nachträglich ändern — bei einer
Veranstaltung Name, Datum und Ort, bei einer Kategorie Bezeichnung, Preis
und Farbe. Bereits verkaufte Karten behalten dabei, was zum Zeitpunkt des
Verkaufs galt; sonst schriebe eine Preisänderung am Abend die Einnahmen des
Nachmittags um.

Eine Ausnahme: **das Kürzel einer Veranstaltung ist gesperrt, sobald Karten
dazu gedruckt sind.** Es steckt in jedem Code und ist mitsigniert — eine
Änderung machte jede gedruckte Karte ungültig, am Einlass stünde „Fremde
Veranstaltung". Solange noch keine Karte da ist, lässt es sich frei ändern.

## Zwei Geräte, ein Abend

Drinnen wird verkauft, draußen wird gescannt — dafür müssen die Geräte nicht
miteinander reden. Die Signatur im Code beweist, dass eine Karte aus dieser
Kasse stammt, auch wenn das Gerät an der Tür sie nie gesehen hat. Es lässt
sie ein und trägt sie nach.

Was dafür zu tun ist:

1. Beide Geräte auf denselben Stand bringen. Am einfachsten über die
   **Ablage** — siehe *Ein zweites Gerät einrichten* weiter unten; ein leeres
   Gerät braucht dafür nur Adresse und Zugangswort. Ohne Ablage: auf dem
   ersten Gerät exportieren, auf dem zweiten *ersetzen*, und danach das
   Kassenzeichen ändern.
2. Verkauft mehr als ein Gerät, jedem ein eigenes **Kassenzeichen** geben —
   einen Buchstaben. Er steht in der Nummer (`SF26-B0007`) und verhindert,
   dass zwei Geräte dieselbe Nummer vergeben.

Was dabei bleibt: jedes Gerät kennt zunächst nur seine eigenen Einlässe.
Wird dieselbe Karte im selben Augenblick an zwei verschiedenen Türen
vorgezeigt, fällt das nicht auf — beide lassen ein. Mit der Ablage weiß es
das zweite Gerät beim nächsten Abgleich, also nach Sekunden bis Minuten;
ohne sie erst am Ende des Abends. Wirklich ausschließen ließe es sich nur
mit einem Speicher, an dem der Einlass hängt — und der stünde still, sobald
das Netz wackelt. Bei einer Tür stellt sich die Frage nicht.

Dasselbe gilt für eine anderswo **stornierte** Karte: bis zum nächsten
Abgleich weiß die Tür nichts davon. Wer das sicher ausschließen muss,
stellt *Einstellungen → Einlass* auf **Abweisen** und bringt vorher den
Stand des verkaufenden Geräts herüber. Dann kommt nur hinein, was dort
steht.

Die nachgetragenen Karten stehen in der Übersicht für sich. Sie zählen nicht
zu den Einnahmen dieses Geräts, denn ihr Preis steht nicht im Code — er
liegt beim Gerät, das sie verkauft hat.

## Höchstzahlen

Zweihundert Sitzplätze, dreiundsechzig Essen: unter *Einstellungen →
Kategorien* trägt jede Kategorie eine **Höchstzahl**. Die Kasse zeigt den
Rest auf der Kachel — *noch 137 von 200* — und lässt nicht darüber hinaus;
die Kachel wird blass und meldet sich, wenn jemand es trotzdem versucht.

Gezählt wird je Veranstaltung. Was im Korb liegt, zählt mit: sonst ließe sich
die Grenze innerhalb einer Buchung überschreiten und es fiele erst beim
Drucken auf. Eine stornierte Karte gibt ihren Platz wieder frei. Leer heißt:
keine Grenze.

Die Höchstzahl lässt sich jederzeit ändern — wird das Fest voller als
gedacht, kostet das zwei Handgriffe.

## Übersicht und Abschluss

Unter *Tickets* steht die **Übersicht**: je Kategorie verkauft, eingelöst,
offen, verfügbar und die Einnahmen — auch für Kategorien, von denen noch
nichts verkauft ist. Darunter, wer eingelassen hat, je Gerät.

**Kasse schließen** beendet den Verkauf für diese Veranstaltung. Der Einlass
läuft weiter; es kommt vor, dass abgerechnet wird, während die letzten Gäste
noch eintrudeln. Wieder öffnen geht jederzeit an derselben Stelle.

**Drucken** legt den Abschluss auf ein A4-Blatt im Druckbild des
Vereinsmanagers — mit Veranstalter im Kopf, Datum und Kürzel. Die
Kassenprüfung will einen Beleg sehen, kein Bildschirmfoto.

Gezählt werden Plätze, nicht Karten: eine Familienkarte ist ein Stück Papier,
aber vier Leute im Saal.

## Die Türliste

Unter *Tickets* steht neben *Offene neu drucken* der Knopf **Türliste
drucken**. Darauf steht jede ausgegebene Karte dieses Abends mit Code,
Kategorie, Preis, Namen und Zustand, und vor jeder Zeile ein Kästchen zum
Abhaken.

Das ist der Weg für den Fall, dass am Eingang nichts mehr geht: Akku leer,
Kamera streikt, Netz weg, Handy heruntergefallen. Dann wird von Hand
abgehakt und der Einlass hinterher in der Kasse nachgetragen — sonst fehlt
er in der Abrechnung.

Stornierte Karten stehen mit auf dem Blatt, durchgestrichen. Eine Liste, die
nur die guten Karten zeigt, ließe die stornierte durch, und genau davor soll
sie schützen.

Die Liste einmal vor dem Abend ausdrucken und an die Kasse legen. Sie zeigt
den Stand des Augenblicks; wer nach dem Druck noch verkauft, schreibt die
Nummern unten dazu.

## Aufräumen: löschen und abschließen

Bei mehreren Geräten ist Löschen kein Wegwerfen, sondern eine Nachricht.
Wirft ein Gerät eine Veranstaltung weg und sagt es den anderen nicht, bringt
der nächste Abgleich sie zurück — die anderen haben sie ja noch. Die Kasse
schreibt darum bei jedem Löschen einen Vermerk, der mitreist und auf jedem
Gerät ausgeführt wird. Was auf einem Gerät weggeräumt wurde, verschwindet
beim nächsten Abgleich überall, und der Abgleichsbericht sagt, was fortkam.

Wer eine gelöschte Kategorie oder ein gelöschtes Kürzel später wieder
anlegt, holt es damit absichtlich zurück; auch das reist mit.

**Abschließen** ist der zweite Teil. Neben jeder Veranstaltung unter
*Einstellungen* steht der Knopf. Er dampft den Abend auf seine Zahlen ein:
die Kategorienübersicht und die Summen wandern ins **Archiv**, die einzelnen
Karten fallen fort. Von da an lässt sich für diesen Abend nicht mehr
verkaufen, und seine Karten gelten am Einlass nicht mehr — er ist vorbei.

Das ist die einzige Stelle, an der der Stand wieder kleiner wird, und er
muss kleiner werden können: bei jedem Abgleich geht der ganze Stand über das
Netz. Ein Abend mit zweihundert Karten wiegt rund dreißig Kilobyte, sein
Archiveintrag knapp ein Kilobyte. Ohne Abschließen wächst der Stand über die
Jahre monoton, und irgendwann zieht jedes Gerät im Minutentakt die
Vorjahresabende mit über das Föhrer Mobilfunknetz.

Die Archiveinträge lassen sich einzeln drucken — derselbe Kassenabschluss
wie am Abend selbst, nur aus dem Gedächtnis. **Vor dem Abschließen** ist der
richtige Zeitpunkt für eine Sicherung unter *Einstellungen → Sicherung*,
falls doch noch jemand eine einzelne Karte nachschlagen will.

## Nur Einlass: ein Gerät für die Tür

Bis Fassung 2.6 war jedes Gerät eine vollständige Kasse — auch das, das
draußen an der Tür stand und nur scannen sollte. Ein Fehlgriff in der
Ticketliste stornierte dort eine Karte, ein Fehlgriff in den Kategorien
änderte mitten im Abend einen Preis, und beides fiel erst bei der
Abrechnung auf.

Unter *Einstellungen → Einlass → Nur Einlass* wird eine vier- bis
achtstellige Zahl eingetragen und das Gerät gesperrt. Danach bleiben:

- der Einlass mit Kamera, Eingabefeld, Urteil und Ton,
- die Liste der zuletzt geprüften Karten,
- der Abgleich samt Statuszeile und einem Knopf *Jetzt abgleichen*,
- die Wahl der Veranstaltung oben rechts.

Fort sind Verkauf, Druck, Ticketliste, Kassenabschluss und alle
Einstellungen. Auch die Übernahme eines fremden Zugangs per QR-Code wird
abgewiesen — das ist eine Einstellung und hat an der Tür nichts zu suchen.
Aufgehoben wird die Beschränkung mit derselben Zahl, unten auf dem
Einlassschirm.

Zwei Dinge dazu, ehrlich gesagt:

**Es ist ein Schutzgeländer, kein Schloss.** Alles läuft im Browser dieses
Geräts. Wer sich auskennt, kommt daran vorbei — über die Entwicklerwerkzeuge
oder indem er den Browserspeicher löscht. Gegen den Fehlgriff am Eingang
hilft es vollständig, gegen den entschlossenen Insider gar nicht. Der
Fehlgriff ist der Fall, den es an der Tür wirklich gibt.

**Die Sperre gehört dem Gerät, nicht dem Abend.** Sie wandert deshalb nicht
mit dem Abgleich; sonst legte ein gesperrtes Türgerät die Kasse drinnen
gleich mit still. Jedes Gerät wird für sich gesperrt.

Wer die Zahl vergisst, kommt nur noch über *Browserdaten löschen* an das
Gerät — und damit wäre auch sein Stand fort. Ist eine Ablage eingerichtet,
holt sich das Gerät danach alles von selbst zurück; ohne Ablage ist der
Stand dieses Geräts verloren. Also aufschreiben.

## Mehrere Türen

Es können beliebig viele Geräte mitlaufen. Jedes bekommt unter
*Einstellungen → Einlass* ein eigenes **Kassenzeichen** — einen Buchstaben.
Er tut zweierlei: er hält die Kartennummern der verkaufenden Geräte
auseinander, und er steht an jeder eingelösten Karte, sodass der Abschluss
sagen kann, welche Tür wie viele durchgelassen hat.

Auch Geräte, die nur scannen, sollten deshalb einen Buchstaben bekommen.
Ohne erscheinen ihre Einlässe im Abschluss als *ohne Zeichen*.

Was dabei zu bedenken ist: jedes Gerät fragt die Ablage in seinem Takt. Bei
vielen Geräten und einminütigem Abgleich summiert sich das; Google begrenzt,
wie lange ein Skript am Tag laufen darf. Für einen Vereinsabend mit einer
Handvoll Geräten ist das kein Thema — geschrieben wird ohnehin nur, wenn es
etwas zu schreiben gibt.

## Am Ende des Abends: zusammenführen

Nach dem Einlass weiß das eine Gerät, wer bezahlt hat, und das andere, wer
gekommen ist. Erst beides zusammen ergibt den Abend.

*Einstellungen → Sicherung → **Zusammenführen*** nimmt die Sicherung des
anderen Geräts und legt sie über den eigenen Stand. Nicht "die neuere Datei
gewinnt" — das löschte, was das andere Gerät in der Zwischenzeit getan hat.
Sondern Karte für Karte:

- Karte hier unbekannt → übernehmen, mitsamt Kategorie und Preis
- hier nachgetragen, dort verkauft → Kategorie und Preis nachziehen. Der
  Nachtrag ist damit geklärt und die Karte zählt wieder zu den Einnahmen
- hier offen, dort eingelöst → eingelöst, mit dem früheren Zeitpunkt
- Widersprüche werden **gemeldet, nicht aufgelöst**

Danach steht auf dem Gerät, in das eingelesen wurde, der ganze Abend. Die
Richtung ist beliebig, und derselbe Abgleich zweimal ausgeführt ändert beim
zweiten Mal nichts mehr.

Gemeldet werden zwei Fälle. **Hier storniert, dort eingelöst** — jemand ist
mit einer stornierten Karte hineingekommen; die Karte gilt danach als
eingelöst, weil der Einlass geschehen ist, aber der Fall steht im Bericht.
Und **zwei Verkäufe unter derselben Nummer** — das passiert, wenn zwei Geräte
ohne eigenes Kassenzeichen verkauft haben. Beide Karten tragen dann denselben
Code, auf Papier nicht mehr zu unterscheiden. Der fremde Verkauf muss von Hand
nachgetragen werden. Das Kassenzeichen verhindert genau das; es ist der Grund,
warum es existiert.

Der Schlüssel muss auf beiden Geräten derselbe sein, sonst wird der Abgleich
abgelehnt: Karten aus einer anderen Kasse ließen sich hier nicht prüfen.

*Stattdessen ersetzen* gibt es weiterhin — es wirft alles Gespeicherte weg und
übernimmt die Datei. Das ist der Weg, ein frisches Gerät einzurichten, und
nicht der Weg, zwei Stände zusammenzubringen.

## Ablage: der Abgleich von selbst

Statt die Sicherung von Hand herüberzuschicken, können die Geräte sie sich
selbst holen. Dafür liegt `ablage.gs` bei — ein kleines Google-Apps-Script,
das als Web-App veröffentlicht wird und in *deinem* Drive eine einzige Datei
führt. Die Geräte rufen nur diese Adresse auf: keine Anmeldung am Eingang,
kein Google-Konto auf fremden Handys, und die Daten bleiben in eurem Drive.

Die Einrichtung steht oben in `ablage.gs`. Danach kommen Adresse und
Zugangswort in der Ticketkasse unter *Einstellungen → Ablage* hinein, dazu
wie oft abgeglichen werden soll.

### Ein zweites Gerät einrichten

Auf dem neuen Gerät nur die Adresse und das Zugangswort eintragen und
einmal *Jetzt abgleichen* drücken.

Beides abzutippen ist auf einem Handy eine Zumutung — die Adresse allein hat
rund hundertfünfzig Zeichen. Deshalb geht es auch so: auf dem eingerichteten
Gerät *Einstellungen → Ablage → **Zugang als QR-Code zeigen***, auf dem neuen
*Einlass → Kamera* und den Code vom Bildschirm des anderen abfotografieren.
Die Kasse fragt nach, trägt Adresse und Zugangswort ein und gleicht sofort ab.

### Wenn der Abgleich klemmt

*Einstellungen → Ablage → **Verbindung prüfen*** fragt die Ablage einmal und
zeigt, was zurückkommt — Status, Typ und der Anfang der Antwort. Die
häufigsten Fälle nennt die Kasse beim Namen:

| was zurückkommt | was zu tun ist |
| --- | --- |
| eine **Anmeldeseite** | Bei *Bereitstellen → Bereitstellungen verwalten* muss „Wer hat Zugriff" auf **Jeder** stehen — nicht auf „Jeder mit einem Google-Konto" |
| eine **Internetseite** statt Daten | Die Adresse gehört zu keiner bereitgestellten Web-App, oder sie endet nicht auf `/exec` |
| **nicht erreichbar** | Kein Netz, oder die Adresse stimmt nicht |
| **Zugangswort stimmt nicht** | Im Skript steht ein anderes — oder die Änderung wurde nie als neue Version bereitgestellt |

Der letzte Fall ist der häufigste nach einer Änderung am Skript: *Speichern*
allein reicht nicht. Es braucht *Bereitstellen → Bereitstellungen verwalten →
Stift → Version: Neue Version → Bereitstellen*. Sonst läuft weiter die alte.

In diesem Bild steckt das Zugangswort im Klartext. Es gehört auf den
Bildschirm des eigenen Geräts und nicht in eine Mail, einen Ausdruck oder ein
Foto. Alles Übrige kommt von selbst:
Veranstaltungen, Kategorien samt Farben, verkaufte Karten — und der
Schlüssel.

Dass der Schlüssel mitkommt, gilt nur für ein **leeres** Gerät, auf dem
noch keine Veranstaltung, keine Kategorie und keine Karte steht. Dort ist
nichts zu verlieren, und wer Adresse und Zugangswort hat, gehört ohnehin
dazu. Hat das Gerät schon einen eigenen Stand, wird der Abgleich abgelehnt:
zwei verschiedene Schlüssel im selben Haus bedeuten, dass die Karten des
einen beim anderen als gefälscht gelten. Dann entweder von Hand denselben
Schlüssel eintragen oder das Gerät unter *Zurücksetzen* leeren.

Das **Kassenzeichen** kommt ausdrücklich nicht mit — es ist die Kennung
dieses einen Geräts. Es wird gar nicht erst in die Ablage geschrieben.

Der Ablauf ist immer derselbe:

    holen  →  zusammenführen  →  zurücklegen

Beim Zurücklegen nennt das Gerät den Zählerstand, auf dem es aufsetzt. Hat
inzwischen ein anderes geschrieben, lehnt die Ablage ab und schickt den
neuen Stand mit; dann wird noch einmal gerechnet. Ohne diesen Schritt ginge
verloren, was das andere Gerät in der Zwischenzeit getan hat — der Fehler,
den eine schlichte Sicherung im Minutentakt macht.

Geschrieben wird nur, wenn es etwas zu schreiben gibt. Ein Gerät, das
danebensteht und nichts verkauft, holt bloß und legt nichts ab — Google
begrenzt, wie lange ein Skript am Tag laufen darf, und das soll nicht für
immer denselben Stand draufgehen.

Alles bleibt dabei zuerst auf dem Gerät. Fällt das Netz aus, arbeiten Kasse
und Einlass weiter und gleichen später ab. Es geht nichts verloren; es
dauert nur länger, bis beide dasselbe wissen. Das Intervall ist deshalb
unkritisch — eine Karte, die das Türgerät noch nicht kennt, wird ohnehin
nachgetragen.

Wer die Adresse **und** das Zugangswort hat, kann den ganzen Abend lesen und
überschreiben. Beides gehört auf die Geräte des Vereins und nicht in eine
Rundmail. Was hochgeladen wird, ist der Stand ohne diese Zugangsdaten und
ohne das Kassenzeichen — das ist die Kennung des jeweiligen Geräts und darf
nicht wandern.

## Fassungen

Die Nummer steht oben in der Kopfzeile der Kasse. Wer zwei Geräte
nebeneinanderlegt, sieht daran, ob beide denselben Stand haben.

| | |
| --- | --- |
| **2.7** | Geräte an der Tür lassen sich auf reinen Einlass beschränken |
| 2.6 | Bedienungsanleitung als PDF; Restzahl auf der Kachel wieder lesbar |
| 2.5 | Löschen hält über Geräte hinweg, Abende abschließen, Türliste zum Abhaken |
| 2.4 | gezeichnetes Symbol des Vereins auf Schreibtisch und Home-Bildschirm |
| 2.3 | Druck auf Etiketten- und Thermodrucker |
| 2.2 | eigenes Symbol, als Programm einrichtbar |
| 2.1 | Höchstzahlen je Kategorie, eine Übersicht statt dreier |
| 2.0 | Kassenabschluss zum Drucken, Einlass je Gerät ausgewiesen |
| 1.9 | Verbindung prüfen: sagt, warum ein Abgleich klemmt |
| 1.8 | Zugang zur Ablage per QR-Code auf das zweite Gerät |
| 1.7 | ein leeres Gerät richtet sich aus der Ablage selbst ein |
| 1.6 | Hausfarben auf den Kacheln, Veranstaltungen änderbar, Ton am Einlass |
| 1.5 | farbige Kacheln, Kategorien änderbar, Sammelkarten, Etikettendruck |
| 1.4 | Ablage im Drive: die Geräte gleichen sich selbst ab |
| 1.3 | Zusammenführen zweier Stände von Hand, über eine Sicherung |
| 1.2 | Nachtragen unbekannter Karten am Einlass, Kassenzeichen |
| 1.1 | eigener QR-Leser — Kamera auch auf iPhone, iPad und Windows |
| 1.0 | Hausstil des Vereinsmanagers, Anordnung an der Kasse wählbar |

## Herkunft

Farben, Maße und Druckbild stammen aus dem Fering Vereinsmanager, der
Verwaltungssoftware des Vereins. Die Ticketkasse steht bewusst für sich
allein, damit sie am Eingang auch ohne Netz läuft.
