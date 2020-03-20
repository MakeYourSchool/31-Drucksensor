Drucksensor
----

<img src=https://www.makeyourschool.de/wp-content/uploads/2018/10/31_drucksensor-1024x1024.jpg width=400px>

Der Drucksensor ermöglicht es, Kräfte, die auf den Sensor wirken, zu bestimmen. Wird die Sensorfläche belastet, ändert sich der elektrische Widerstand zwischen den Anschlusspins. Durch eine Widerstandsmessung, kann folglich auf den einwirkenden Druck (also Kraft pro Flächeneinheit) geschlossen werden.

Da ein Arduino nicht direkt eine Widerstandsänderung messen kann, wird eine Messverstärkerschaltung benötigt. Eine Möglichkeit bietet hierfür ein sogenannter Spannungsteiler, bei dem der Sensor in Reihe mit einem zweiten Widerstand zwischen Versorgungsspannung und Masse gelegt wird. Der Arduino kann schließlich die Widerstandsänderung als Spannungsänderung über einen analogen Pin erfassen.

Der Sensor kann genutzt werden, um eine Berührung eines Objekts zu erkennen. Zusätzlich lässt sich die tatsächliche Kraft, die auf das Objekt ausgeübt wird, ermitteln.

----

In diesem Repository findet ihr **Bibliotheken und Beispiel-Codes**, mit denen der hier vorliegende Sensor getestet werden kann. Wir richten uns hiermit an **jeden Mentor und jede Mentorin aus dem Rahmen von Make Your School** und ermutigen euch, die hier zusammengestellten Codes **nach Bedarf** und individuell gemachten Erfahrungen **anzupassen**. Beispiele können einfach im Ordner /examples hinzugefügt oder angepasst werden. Wir versuchen das Repository regelmäßig mit Hilfe von euren Änderungsvorschlägen zu aktualisieren.

**Weitere Informationen:**

[Materialkoffer von Make Your School](https://www.makeyourschool.de/material/)
