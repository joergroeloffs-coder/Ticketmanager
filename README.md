# Ticketkasse

Abendkasse für Veranstaltungen: Karten verkaufen, drucken und am Eingang
prüfen. Eine einzige HTML-Datei, ohne Server, ohne Netz, ohne
Abhängigkeiten.

**Im Browser öffnen:** https://joergroeloffs-coder.github.io/Ticketmanager/

## Wie es arbeitet

Jede Karte trägt einen QR-Code aus drei Teilen: dem Kürzel der
Veranstaltung, einer laufenden Nummer und einer Signatur (HMAC-SHA-256,
gerechnet mit dem Schlüssel aus den Einstellungen). Ohne den Schlüssel
lässt sich keine gültige Karte malen; ohne die gespeicherte Liste lässt
sich keine zweimal einlösen.

Gerechnet wird in ganzen Cent. Die Daten liegen im Speicher des Browsers
— pro Gerät getrennt, nirgends sonst. Wer das Gerät wechselt oder den
Abend sichern will, nimmt *Einstellungen → Sicherung → Exportieren*.

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

**Vor dem ersten guten Bogen:** *Ausrichtung drucken* liefert ein Blatt mit
nur den leeren Feldern. Auf weißes Papier drucken und gegen einen
Etikettenbogen halten. Stimmt es nicht, liegt es fast immer am Druckdialog
— dort muss **Tatsächliche Größe** oder **100 %** stehen, nicht „An Seite
anpassen". Das schrumpft den Bogen um ein paar Prozent, und ab der zweiten
Reihe steht alles daneben.

Der QR-Code misst auf dem Etikett 29 mm bei 25 Modulen, also einen
Millimeter je Punkt — reichlich für jede Handykamera.

## Zwei Geräte, ein Abend

Drinnen wird verkauft, draußen wird gescannt — dafür müssen die Geräte nicht
miteinander reden. Die Signatur im Code beweist, dass eine Karte aus dieser
Kasse stammt, auch wenn das Gerät an der Tür sie nie gesehen hat. Es lässt
sie ein und trägt sie nach.

Was dafür zu tun ist:

1. Auf beiden Geräten denselben **Schlüssel** eintragen (*Einstellungen →
   Schlüssel*) und dieselbe Veranstaltung mit demselben **Kürzel** anlegen.
   Bequemer: auf dem ersten Gerät exportieren, auf dem zweiten importieren.
2. Verkauft mehr als ein Gerät, jedem ein eigenes **Kassenzeichen** geben —
   einen Buchstaben. Er steht in der Nummer (`SF26-B0007`) und verhindert,
   dass zwei Geräte dieselbe Nummer vergeben.

Was dabei bleibt: jedes Gerät kennt nur seine eigenen Einlässe. Wird dieselbe
Karte an zwei verschiedenen Türen vorgezeigt, fällt das nicht auf — dafür
bräuchte es einen gemeinsamen Speicher. Bei einer Tür genügt das hier.

Ebenso kann ein Gerät nicht wissen, ob eine Karte anderswo **storniert**
wurde. Wer das ausschließen muss, stellt *Einstellungen → Einlass* auf
**Abweisen** und spielt vor dem Einlass die Liste des verkaufenden Geräts
ein. Dann kommt nur hinein, was dort steht.

Die nachgetragenen Karten stehen in der Übersicht für sich. Sie zählen nicht
zu den Einnahmen dieses Geräts, denn ihr Preis steht nicht im Code — er
liegt beim Gerät, das sie verkauft hat.

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
| **1.5** | farbige Kacheln, Kategorien änderbar, Sammelkarten, Etikettendruck |
| 1.4 | Ablage im Drive: die Geräte gleichen sich selbst ab |
| 1.3 | Zusammenführen zweier Stände von Hand, über eine Sicherung |
| 1.2 | Nachtragen unbekannter Karten am Einlass, Kassenzeichen |
| 1.1 | eigener QR-Leser — Kamera auch auf iPhone, iPad und Windows |
| 1.0 | Hausstil des Vereinsmanagers, Anordnung an der Kasse wählbar |

## Herkunft

Farben, Maße und Druckbild stammen aus dem Fering Vereinsmanager, der
Verwaltungssoftware des Vereins. Die Ticketkasse steht bewusst für sich
allein, damit sie am Eingang auch ohne Netz läuft.
