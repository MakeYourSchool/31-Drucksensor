Drucksensor
----

<img src=https://www.makeyourschool.de/wp-content/uploads/2018/10/31_drucksensor-1024x1024.jpg width=400px>

Bildquelle: *Wissenschaft im Dialog*

Der Drucksensor ermöglicht es, Kräfte, die auf den Sensor wirken, zu bestimmen. Wird die Sensorfläche belastet, ändert sich der elektrische Widerstand zwischen den Anschlusspins. Durch eine Widerstandsmessung, kann folglich auf den einwirkenden Druck (also Kraft pro Flächeneinheit) geschlossen werden.

Da ein Arduino nicht direkt eine Widerstandsänderung messen kann, wird eine Messverstärkerschaltung benötigt. Eine Möglichkeit bietet hierfür ein sogenannter Spannungsteiler, bei dem der Sensor in Reihe mit einem zweiten Widerstand zwischen Versorgungsspannung und Masse gelegt wird. Der Arduino kann schließlich die Widerstandsänderung als Spannungsänderung über einen analogen Pin erfassen.

Der Sensor kann genutzt werden, um eine Berührung eines Objekts zu erkennen. Zusätzlich lässt sich die tatsächliche Kraft, die auf das Objekt ausgeübt wird, ermitteln.

----

Im Rahmen von [*Make Your School*](https://www.makeyourschool.de/) finden an Schulen Hackdays statt. Dabei überlegen sich Schülerinnen und Schüler, wie sie ihre Schule mitgestalten und mit technischen und digitalen Tools noch besser machen können. Unterstützt werden sie dabei von Mentorinnen und Mentoren, die die Veranstaltung begleiten und fachliche Impulse geben. *Make Your School* ist ein Projekt von *Wissenschaft im Dialog*. Die Klaus Tschira Stiftung ist bundesweiter Förderer.

Mit diesen **Bibliotheken und Beispiel-Codes** kann der euch vorliegende Sensor/Aktor getestet werden. Den **Mentorinnen und Mentoren von *Make Your School*** steht es frei, die hier zusammengestellten Codes **nach Bedarf und den individuell gemachten Erfahrungen anzupassen**. Beispiele können einfach im Ordner „examples“ hinzugefügt oder bearbeitet werden. Wir werden eure Beiträge regelmäßig prüfen und das Repository mithilfe eurer Änderungsvorschläge aktualisieren.

Das Repository basiert grundlegend auf den veröffentlichten Informationen und Codes von Seeed Studio. Die deutsche Übersetzung stammt von *Make Your School*, Fehlinterpretationen und Änderungen vorbehalten. Die Informationen dürfen frei genutzt, angepasst und verbreitet werden, solange die Lizenzrechte (siehe License.txt) beachtet werden.


**Weitere Informationen:**

[Materialkoffer von *Make Your School*](https://www.makeyourschool.de/material/drucksensor/)
