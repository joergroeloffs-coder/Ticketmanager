# Vorgemerkt

Was besprochen, aber noch nicht gebaut ist. Kein Versprechen, sondern ein
Gedächtnis: Sitzungen enden, die Liste bleibt. Erledigtes wandert nach unten.

## Nächste Überarbeitung

### Schrift auf dem Türschirm größer

Das Urteil bekommt am Handy zwischen 250 und 450 Punkte Höhe, die Schrift
steht bei `clamp(26px, 8vw, 44px)`. Auf den Bildern ist zu sehen, dass
darunter noch Luft ist — die farbige Fläche trägt auch eine deutlich größere
Schrift, ohne dass Grün oder Rot dadurch schlechter zu erkennen wären. Der
Grund ist das, was zählt; er darf mitwachsen, muss aber deutlich kleiner
bleiben als das Urteil selbst.

Zu bedenken: „Andere Veranstaltung" und „Bereits eingelöst" sind lange
Wörter. Die Schrift muss sich am längsten Urteil messen, nicht am kürzesten,
sonst bricht „Veranstaltung" mitten im Wort um. Gemessen wird wieder auf
360 × 640, 375 × 667, 375 × 812 und 393 × 852, und zwar mit allen sechs
Urteilen, nicht nur mit „Gültig".

Aufwand: klein. Eine Sitzung mit Bildern zum Vergleichen.

### Kassenseite auf dem Verkaufsgerät: kompakter, auf eine Seite

Auf dem Laptop, auf dem verkauft wird, passt die Kassenseite nicht auf einen
Schirm. Die Kacheln sind gut zu treffen, aber zu groß; die Buchung steht
darunter und ist erst nach dem Scrollen zu sehen. Wer verkauft, will Kacheln
und Buchung gleichzeitig sehen.

Was zu ändern ist:

- **Kacheln annähernd quadratisch und kleiner.** Heute `min-height:110px` in
  zwei Spalten, ab 680 Punkten in dreien. Auf einem breiten Schirm dürfen es
  mehr Spalten und ein festes Seitenverhältnis sein.
- **Der Kopf schrumpft.** „Winterfest" muss dort nicht in sechsundzwanzig
  Punkt stehen — wer die Veranstaltung angelegt hat, weiß, welche läuft. Klein
  genug, dass es noch zu erkennen ist, mehr nicht.
- **Die Buchung nach rechts**, als Liste: Artikel, Preis, darunter die Summe.
  Daneben die Kacheln.

Es ist dieselbe Frage wie beim Einlassschirm auf dem Laptop, nur für die
andere Seite: breiter Schirm, also nebeneinander statt untereinander. Beide
sollten denselben Umbruchpunkt benutzen und in einem Zug gemacht werden.

Zu bedenken:

- Die Buchungskarte enthält mehr als die Liste — Gastname, die Wahl zwischen
  einem Code je Platz und einem für alle, die vier Drucklayouts, den
  Druckknopf. Das alles in eine schmale Spalte zu pressen wird eng. Zu
  entscheiden: wandert die ganze Karte nach rechts, oder nur Liste und Summe,
  und die Druckwahl bleibt darunter?
- „Ohne Scrollen" trägt nur bis zu einer gewissen Zahl von Kategorien. Ab
  wann rollt das Kachelfeld für sich, statt die ganze Seite länger zu machen?
- Die Kacheln dürfen nicht so klein werden, dass man auf einem Berührschirm
  danebentrifft. Etwa neunzig bis hundertzehn Punkte im Quadrat ist die
  Untergrenze.
- Die Seite ist auf 1080 Punkte Breite begrenzt (`.seitenBreite`). Für zwei
  Spalten nebeneinander könnte das zu schmal sein.

Aufwand: mittel. Reine Anordnung, aber mehr Entscheidungen als beim
Einlassschirm. Gemessen auf 1280 × 800, 1440 × 900 und 1920 × 1080, dazu mit
vier und mit zehn Kategorien.

### Einlassschirm auf dem Verkaufsgerät: Bild links, Urteil rechts

Der Türschirm gilt nur für gesperrte Geräte. Auf dem Gerät, auf dem verkauft
wird — meist ein Laptop —, steht der Einlass weiter im gewöhnlichen Layout,
und dort ist das Kamerabild mit `width:100%; max-height:320px` viel zu groß.
Es schiebt das Urteil aus dem Bild; ob grün oder rot erscheint, ist ohne
Scrollen nicht zu sehen. Genau der Fehler, den der Türschirm am Handy behoben
hat — auf dem breiten Schirm ist er nur später aufgefallen.

Ein Laptop ist breit und nicht hoch. Die Lösung ist deshalb nicht dieselbe
wie am Handy (untereinander), sondern nebeneinander: links das Kamerabild,
klein, rechts daneben das Urteil, groß.

Zu bedenken:

- Ab welcher Breite umgeschaltet wird. Unter etwa 700 Punkten bleibt es
  untereinander, sonst wird die Spalte zu schmal für „Andere Veranstaltung".
- Der Kasten *Zuletzt geprüft* steht darunter und darf nicht mitwachsen.
- Auf dem Verkaufsgerät wird zwischen Kasse und Einlass hin- und hergesprungen;
  die Kamera läuft dabei weiter. Das Umschalten darf sie nicht anhalten.
- Das Urteil darf hier ruhig ebenfalls vollflächig grün oder rot werden. Am
  Handy hat sich das bewährt, und der Grund ist derselbe: aus zwei Metern
  Entfernung über den Tresen zu erkennen.

Aufwand: klein bis mittel. Reine Anordnung, kein neuer Zustand. Gemessen wird
auf 1280 × 800, 1440 × 900 und einem schmalen Fenster, damit der Umbruch
stimmt.

### Bar je Kasse auf dem Abschluss

Der Abschluss nennt unter *Zusammen* den Betrag, der an Bargeld da sein muss —
ohne Stornos, ohne nachgetragene Karten. Er gilt aber für die Veranstaltung,
nicht für die einzelne Geldkassette. Verkaufen zwei Leute nebeneinander, sagt
er 533,00 €, aber nicht, wie viel davon in welcher Kassette liegen muss. Beim
Abrechnen am Küchentisch ist das die gesuchte Zahl.

Die Zuordnung ist längst da: das Kassenzeichen steht vorne in jeder Nummer
(`SF26-B0007X1`). Es käme eine Tabelle *Bar je Kasse* dazu, wie es sie für
den Einlass schon gibt.

Dazuzusagen: Karten ohne gesetztes Kassenzeichen landen unter *ohne Zeichen*,
und die Zahlen stimmen erst nach dem Abgleich.

Aufwand: eine halbe Sitzung.

## Ohne Datum

### Eine Generalprobe an echter Technik

Der wichtigste offene Punkt und der einzige, den ich nicht selbst erledigen
kann. Geprüft ist alles gegen einen Browser ohne Kamera, ohne Drucker und
ohne Menschen. Was fehlt: zwei Geräte, dreißig echte Karten, ein echter
Drucker, das echte Apps Script, einmal absichtlich das Netz abgeschaltet.
Was dabei herauskommt, ist mehr wert als die nächsten fünf Fassungen.

### Nur senden, was sich geändert hat

Bei jedem Abgleich reist der ganze Stand über das Netz — 153 Byte je Karte.
Ein Abend allein ist harmlos; über die Jahre wächst es, und das Abschließen
hilft nur, wenn es auch benutzt wird. Ein Abgleich, der nur die Änderungen
seit dem letzten Stand schickt, wäre der saubere Weg.

Aufwand: mittel. Der Zähler `stand` ist da, die Änderungen müssten mitgezählt
werden.

### Kategorien je Veranstaltung

`db.kats` ist eine einzige flache Liste für alle Abende. Beim Grünkohlessen
stehen dieselben Kacheln wie beim Sommerfest. Die Abrechnung bleibt richtig —
der Preis wird beim Verkauf in die Karte geschrieben —, aber die Kassenseite
wird mit jeder Veranstaltung voller.

### Die Sicherungsdatei entschärfen

Sie enthält Schlüssel, Adresse der Ablage und Zugangswort im Klartext. Ein
Backup sollte kein Generalschlüssel sein.

### Eine Papierliste der Nummern zum Anlegen

Die Türliste gibt es. Was fehlt, ist der umgekehrte Weg: abgehakte Karten
hinterher schnell eintragen, ohne jede einzeln zu suchen.

## Besprochen und verworfen

### PayPal im QR-Code

Machbar nur mit einem Server: die Schlüssel von PayPal dürfen nicht in einer
öffentlichen Seite stehen. Für einen Abend mit Bargeld unverhältnismäßig.

### Ein Kassensystem für den Verkaufsstand

Erwogen: Bondruck, Mehrwertsteuersätze, Warengruppen, Bestände, Abrechnung
nach Steuersatz. Technisch wäre das wenig Arbeit — der Rollendruck steht, die
Kategorien sind fast schon Warengruppen.

Verworfen aus zwei Gründen, und beide sind grundsätzlich.

**Recht.** Wer eine elektronische Kasse benutzt, braucht nach § 146a AO eine
zertifizierte technische Sicherheitseinrichtung, dazu Belegausgabe,
DSFinV-K-Export und die Meldung ans Finanzamt. Eine TSE ist Hardware oder ein
kostenpflichtiger Cloud-Dienst mit geheimem Schlüssel; an beides kommt eine
öffentliche Seite ohne Server nicht heran. Gemeinnützigkeit befreit davon
nicht. (Keine Steuerberatung — die Frage gehört dem Steuerberater des Vereins
vorgelegt, und zwar auch für die Ticketkasse selbst.)

**Bauweise.** Diese Anwendung ist offline zuerst, jedes Gerät für sich,
Zusammenführen beim Abgleich, Löschen über Grabsteine. Eine Kasse braucht das
Gegenteil: ein lückenloses, unveränderbares Journal je Kasse. Die Grabsteine
sind hier richtig und wären dort ein Verstoß gegen die GoBD — ihr ganzer Zweck
ist, dass Dinge verschwinden. Das wäre kein Umbau, sondern eine andere
Maschine im selben Gehäuse.

Was stattdessen bleibt: die Warenzählung, wie sie ohnehin stattfindet, und die
Zahl auf dem Abschluss, wie viel Geld in der Kasse sein muss. Braucht der
Verein wirklich eine Kasse, wird sie gekauft, nicht gebaut.

## Erledigt

- 2.8 Türschirm fürs Einlasshandy; Karten anderer Abende richtig erkannt
- 2.7 Geräte an der Tür auf reinen Einlass beschränkbar
- 2.6 Bedienungsanleitung als PDF
- 2.5 Grabsteine, Archiv, Türliste
