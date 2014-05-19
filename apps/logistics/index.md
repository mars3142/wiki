====== Logistics ======

Logistics ist als Spiel geplant, welches unter Android laufen soll. Derzeit ist es noch in der Planungs- bzw. Probierphase. Es ist durch das Spiel [[http://de.wikipedia.org/wiki/Der_Planer|Der Planer]] inspiriert. Ich habe sogar mit Holger Beisheim (geb. Dickmann) gemailt und somit den rechtlichen Rahmen abgeklärt.

Es gibt zwei Seiten auf Google+ bzgl. dem Spiel. Die eine Seite ist die [[https://plus.google.com/communities/112783520362507786585|Community]], wo sich Spieler austauschen können und das andere ist das [[https://plus.google.com/107995254283921704484/posts|Profil]], wo ich wichtige Bekanntmachungen veröffentlichen werde. Vielleicht mache ich das auch nur alles in der Community.

===== Grundlagen =====

Mein erster Versuch war, das Spiel per [[http://developer.android.com/reference/android/opengl/GLSurfaceView.html|GLSurfaceView]] zu erstellen, aber hat sich für mich als sehr umständlich herausgestellt. Der zweite Versuch war dann die beliebte [[http://www.andengine.org/|AndEngine]] zu benutzen, doch irgendwie kam ich damit auch nicht so wirklich weiter. 

Weitere Nachforschungen brachten mich dann zu [[http://libgdx.badlogicgames.com/|libgdx]] und dann habe ich noch durch Zufall [[http://gamadu.com/artemis/|Artemis]] gefunden, die im Zusammenspiel gut sein sollen. Libgdx hat den Vorteil, dass man plattformübergreifend mit Java entwickeln kann und somit direkt auf dem Desktop entwickeln und debuggen kann. Später wird dann einfach ein anderer Starter für Android genommen und der Code klappt damit genauso unter Android. Außerderm könnte man ohne viel Aufwand fürs Web (mit Hilfe des [[https://developers.google.com/web-toolkit/|Google Web Toolkits]]) oder für iOS (via [[http://xamarin.com/monotouch|Monotouch]]) ebenfalls Versionen erstellen.

So bin ich also gerade an dem Punkt angelangt, wo ich mir libgdx und artemis genauer anschaue...

===== libgdx =====

Die Wahl von libgdx war bis jetzt am erfolgreichsten. Dank der Tutorials von [[http://dermetfan.bplaced.net/|dermetfan]] verstehe ich auch die Scene2d Implementation und kann es direkt in meinem Projekt anwenden. Leider ist an mir kein Designer verloren gegangen und somit wird mein Prototyp sicher alles andere als grafisch eine Sensation, aber durch einen glücklichen Umstand habe ich im libgdx Forum ein Holo UI Skin gefunden und dieses werde ich für den Anfang nehmen. Der Ersteller (Carsten) ist ebenfalls ein deutschsprachiger und somit werden Anpassungen recht schnell umgesetzt.

Außerdem wird es eine Version in deutsch und englisch geben, zumindest am Anfang. Die Sprachen können auch direkt im Spiel geändert werden, weil ich z.B. meine Testgeräte auf englisch gestellt habe, aber auch die deutschen Texte testen muss. Dabei möchte ich nicht immer erst die Systemsprache anpassen.

===== artemis =====

Artemis ist ein Entity System Framework und somit kann ich es gut für einzelne Bereiche im Spiel einsetzen. Welche das sein werden, weiß ich noch nicht, aber es wird garantiert in der [[apps:logistics:daydream|Daydream]] Funktionalität genutzt werden.

===== ashley =====

Neben Artemis gibt es noch ein zweites Entity System Framework, welches derzeit sogar noch teilweise weiterentwickelt wird. Der einzige Unterschied, den ich zu Artemis feststellen konnte, ist der Fakt, dass es viel allgemeiner gehalten ist.

===== Funktionen =====

Hier eine grobe Übersicht der wichtigsten Funktionen die später im Spiel eingebaut sein sollen.

^  Funktion  ^  Beschreibung  ^
|  [[apps:logistics:daydream|Daydream]]  |Bildschirmschoner (Android 4.2+)|
|  [[apps:logistics:googleplaygameservice|Google Play Game Service]]  |Unterstützung für Erfolge und/oder Highscore|

Außerdem sind noch ein paar Fragen offen, die ich unter [[apps:logistics:open|Offene Punkte]] zusammenfasse. Es ist also eine Art Ideensammlung.