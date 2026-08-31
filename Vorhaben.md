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

## Erledigt

- 2.8 Türschirm fürs Einlasshandy; Karten anderer Abende richtig erkannt
- 2.7 Geräte an der Tür auf reinen Einlass beschränkbar
- 2.6 Bedienungsanleitung als PDF
- 2.5 Grabsteine, Archiv, Türliste
