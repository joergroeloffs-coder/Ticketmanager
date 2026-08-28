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

Über die Adresse oben liest die Kasse QR-Codes mit der Kamera. Das
verlangt Chrome oder Edge; Firefox und Safari bringen den eingebauten
QR-Leser nicht mit, dort wird der Code eingetippt.

Aus einer heruntergeladenen Datei heraus (`file://`) bleibt die Kamera
aus — das untersagen alle Browser. Verkauf, Druck und das Eintippen
funktionieren dort trotzdem vollständig.

## Herkunft

Farben, Maße und Druckbild stammen aus dem Fering Vereinsmanager, der
Verwaltungssoftware des Vereins. Die Ticketkasse steht bewusst für sich
allein, damit sie am Eingang auch ohne Netz läuft.
