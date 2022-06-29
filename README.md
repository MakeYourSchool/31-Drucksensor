Drucksensor
----

<img src=https://www.makeyourschool.de/wp-content/uploads/2018/10/31_drucksensor-1024x1024.jpg width=400px>

Bildquelle: *Wissenschaft im Dialog*

Der Drucksensor ermöglicht es, Kräfte, die auf den Sensor wirken, zu bestimmen. Wird die Sensorfläche belastet, ändert sich der elektrische Widerstand zwischen den Anschlusspins. Durch eine Widerstandsmessung, kann folglich auf den einwirkenden Druck (also Kraft pro Flächeneinheit) geschlossen werden.

Da ein Arduino nicht direkt eine Widerstandsänderung messen kann, wird eine Messverstärkerschaltung benötigt. Eine Möglichkeit bietet hierfür ein sogenannter Spannungsteiler, bei dem der Sensor in Reihe mit einem zweiten Widerstand zwischen Versorgungsspannung und Masse gelegt wird. Der Arduino kann schließlich die Widerstandsänderung als Spannungsänderung über einen analogen Pin erfassen.

Der Sensor kann genutzt werden, um eine Berührung eines Objekts zu erkennen. Zusätzlich lässt sich die tatsächliche Kraft, die auf das Objekt ausgeübt wird, ermitteln.

_Die folgende Anleitung ist im wesentlichen eine deutsche Übersetzung des (Anfangs des) englischsprachigen Tutorials auf [learn.adafruit.com](https://learn.adafruit.com/force-sensitive-resistor-fsr/using-an-fsr)_

## Analoge Spannungsauslesemethode mit Spannungsteiler

Der einfachste Weg, einen Widerstandssensor auszulesen, ist, ein Ende mit
der Spannung und das andere mit einem "pull-down"-Widerstand mit der Masse/Erdung (engl.: Ground/GND)
zu verbinden. Dann wird zwischen dem unveränderlichen "pull-down"-Widerstand und dem veränderlichen Drucksensor-Widerstand eine Verbindung zu einem analogen Input-Pin eines Microcontrollers, wie z.B. einem Arduino, hergestellt (siehe Bild, Drucksensor=FSR).

![image](https://user-images.githubusercontent.com/28141677/176488746-a7b566b1-c78f-4108-8ae5-71008fbb8bc6.png)

![image](https://user-images.githubusercontent.com/28141677/176488792-02661146-f1c0-4e0b-8a46-eff0ba684481.png)

Das Beispiel zeigt eine Stromversorgung mit 5V, aber es funktioniert genauso gut mit 3.3V. Mit dieser Schaltung variiert die gemessene analoge Spannung zwischen 0V (Erdung/Masse) und ca. 5V (ungefähr so viel wie die Stromversorgung).

Das Ganze basiert darauf, dass sobald sich der Widerstand vom Drucksensor verringert, sich der Gesamtwiderstand vom "pull-down"-Widerstand und dem Drucksensor zusammen von ca. 100KOhm auf 10KOhm reduziert. 
Das bedeutet, dass _mehr_ Strom durch beide Widerstände fließt, was dafür sorgt, dass die Spannung über den festen 10KOhm-Widerstand steigt. 
Ein ziemlicher Hack!

<table><tbody>
<tr>
<th>Druck (N)</th>
<th>Drucksensor(FSR) Widerstand</th>
<th>Widerstand FSR und R<br>
</th>
<th>Strom durch FSR+R</th>
<th>Spannung durch R</th>
</tr>
<tr>
<th>None</th>
<td>Unendlich</td>
<td>Unendlich!</td>
<td>0 mA</td>
<td>0V</td>
</tr>
<tr>
<th>0.2 N</th>
<td>30 Kohm</td>
<td>40 Kohm</td>
<td>0.13 mA</td>
<td>1.3 V</td>
</tr>
<tr>
<th>1 N</th>
<td>6 Kohm</td>
<td>16 Kohm</td>
<td>0.31 mA</td>
<td>3.1 V</td>
</tr>
<tr>
<th>10 N</th>
<td>1 Kohm</td>
<td>11 Kohm</td>
<td>0.45 mA</td>
<td>4.5 V</td>
</tr>
<tr>
<th>100 N</th>
<td>250 ohm<br>
</td>
<td>10.25 Kohm</td>
<td>0.49 mA</td>
<td>4.9 V</td>
</tr>
</tbody></table>

_Diese Tabelle zeigt die ungefähre analoge Spannung basierend auf dem Druck auf den Sensor/dessen Widerstand mit einer 5V Stromzufuhr und einem 10K "pull-down" Widerstand._

Beachtet, dass sich der Widerstand des Drucksensors(FSR) ungefähr linear mit dem gemessenen Druck ändert, die Spannung aber nicht!  Das liegt daran, dass die Gleichung für die Spannung so aussieht:

`Vo = Vcc (R / (R + FSR) )`

Die Spannung ist also proportional zum _inversen_ des FSR-Widerstands.

## Einfaches Anwendungsbeispiel

Verdrahtet den Drucksensor genau wie oben, aber fügt diesmal noch eine LED auf Pin 11 hinzu.

![image](https://user-images.githubusercontent.com/28141677/176494152-ab716c7c-af6b-481e-99d3-ec2bca02ef38.png)

![image](https://user-images.githubusercontent.com/28141677/176494181-80df97cc-3805-4ba0-8f4f-be01b6faef7a.png)

Der unten angefügte Arduino-Code nimmt die gemessene Spannung und lässt die LED entsprechend hell leuchten. Je stärker ihr auf den Drucksensor drückt, desto heller wird die LED! Denk daran, dass die LED an einen analogen (PWM)-Pin angeschlossen sein muss, damit das funktioniert, hier wird z.B. Pin 11 verwendet.

```c++
/* FSR (Drucksensor) Testcode

Verbinde ein Ende des Druckwiderstands mit dem Strom(5V), das andere Ende mit Analog 0.
Dann verbinde ein Ende eines 10KOhm-Widerstands von Analog 0 zur Erde.
Verbinde die LED von Pin 11 durch einen Widerstand mit der Erde.
 
Mehr Infos gibt's auch auf www.ladyada.net/learn/sensors/fsr.html */
 
int fsrAnalogPin = 0; // Druckwiderstand/FSR is mit  analog 0 verbunden
int LEDpin = 11;      // Rote LED auf pin 11 (PWM pin)
int fsrReading;       // analoger Messwert vom FSR Widerstandsteiler 
int LEDbrightness;    // Helligkeit der LED
 
void setup(void) {
  Serial.begin(9600);   // Damit wir Debug-Output an die Serial-Konsole schicken können
  pinMode(LEDpin, OUTPUT);
}
 
void loop(void) {
  fsrReading = analogRead(fsrAnalogPin); // lese Spannung aus
  Serial.print("Analog reading = ");
  Serial.println(fsrReading);
 
  // Der Analoge Messwert ist zwischen 0 und 1023, aber an einen analogen Output-Pin können wir nur Werte zwischen 0 und 255 schicken.
  // -> deswegen bilden wir den ersten Wertebereich auf den zweiten ab (engl.: map)
  LEDbrightness = map(fsrReading, 0, 1023, 0, 255);
  // LED wird heller, je stärker man drückt
  analogWrite(LEDpin, LEDbrightness);
 
  // warte 100ms, damit das ganze Stabil läuft
  // (-> maximal 10 Schleifendurchläufe pro Sekunde)
  delay(100);
}
```


Was ist "Make Your School"?
----

Im Rahmen von [*Make Your School*](https://www.makeyourschool.de/) finden an Schulen Hackdays statt. Dabei überlegen sich Schülerinnen und Schüler, wie sie ihre Schule mitgestalten und mit technischen und digitalen Tools noch besser machen können. Unterstützt werden sie dabei von Mentorinnen und Mentoren, die die Veranstaltung begleiten und fachliche Impulse geben. *Make Your School* ist ein Projekt von *Wissenschaft im Dialog*. Die Klaus Tschira Stiftung ist bundesweiter Förderer.

Mit diesen **Bibliotheken und Beispiel-Codes** kann der euch vorliegende Sensor/Aktor getestet werden. Den **Mentorinnen und Mentoren von *Make Your School*** steht es frei, die hier zusammengestellten Codes **nach Bedarf und den individuell gemachten Erfahrungen anzupassen**. Beispiele können einfach im Ordner „examples“ hinzugefügt oder bearbeitet werden. Wir werden eure Beiträge regelmäßig prüfen und das Repository mithilfe eurer Änderungsvorschläge aktualisieren.

Das Repository basiert grundlegend auf den veröffentlichten Informationen und Codes von Seeed Studio. Die deutsche Übersetzung stammt von *Make Your School*, Fehlinterpretationen und Änderungen vorbehalten. Die Informationen dürfen frei genutzt, angepasst und verbreitet werden, solange die Lizenzrechte (siehe License.txt) beachtet werden.


**Weitere Informationen:**

[Materialkoffer von *Make Your School*](https://www.makeyourschool.de/material/drucksensor/)
