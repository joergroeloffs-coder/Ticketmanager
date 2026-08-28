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

## Herkunft

Farben, Maße und Druckbild stammen aus dem Fering Vereinsmanager, der
Verwaltungssoftware des Vereins. Die Ticketkasse steht bewusst für sich
allein, damit sie am Eingang auch ohne Netz läuft.
