---
title: Logistics
layout: default
---
Logistics ist als Spiel geplant, welches unter Android laufen soll. Derzeit ist es noch in der Planungs- bzw. Probierphase. Es ist durch das Spiel [Der Planer](http://de.wikipedia.org/wiki/Der_Planer) inspiriert. Ich habe sogar mit Holger Beisheim (geb. Dickmann) gemailt und somit den rechtlichen Rahmen abgeklärt.

Es gibt zwei Seiten auf Google+ bzgl. dem Spiel. Die eine Seite ist die [Community](https://plus.google.com/communities/112783520362507786585), wo sich Spieler austauschen können und das andere ist das [Profil](https://plus.google.com/107995254283921704484/posts), wo ich wichtige Bekanntmachungen veröffentlichen werde. Vielleicht mache ich das auch nur alles in der Community.

## Grundlagen

Mein erster Versuch war, das Spiel per [GLSurfaceView](http://developer.android.com/reference/android/opengl/GLSurfaceView.html) zu erstellen, aber hat sich für mich als sehr umständlich herausgestellt. Der zweite Versuch war dann die beliebte [AndEngine](http://www.andengine.org/) zu benutzen, doch irgendwie kam ich damit auch nicht so wirklich weiter. 

Weitere Nachforschungen brachten mich dann zu [libgdx](http://libgdx.badlogicgames.com/) und dann habe ich noch durch Zufall [artemis](http://gamadu.com/artemis/) gefunden, die im Zusammenspiel gut sein sollen. Libgdx hat den Vorteil, dass man plattformübergreifend mit Java entwickeln kann und somit direkt auf dem Desktop entwickeln und debuggen kann. Später wird dann einfach ein anderer Starter für Android genommen und der Code klappt damit genauso unter Android. Außerderm könnte man ohne viel Aufwand fürs Web (mit Hilfe des [Google Web Toolkits](https://developers.google.com/web-toolkit/)) oder für iOS (via [MonoTouch](http://xamarin.com/monotouch|Monotouch)) ebenfalls Versionen erstellen.

So bin ich also gerade an dem Punkt angelangt, wo ich mir libgdx und artemis genauer anschaue...

## libgdx

Die Wahl von libgdx war bis jetzt am erfolgreichsten. Dank der Tutorials von [dermetfan](http://dermetfan.bplaced.net/) verstehe ich auch die Scene2d Implementation und kann es direkt in meinem Projekt anwenden. Leider ist an mir kein Designer verloren gegangen und somit wird mein Prototyp sicher alles andere als grafisch eine Sensation, aber durch einen glücklichen Umstand habe ich im libgdx Forum ein Holo UI Skin gefunden und dieses werde ich für den Anfang nehmen. Der Ersteller (Carsten) ist ebenfalls ein deutschsprachiger und somit werden Anpassungen recht schnell umgesetzt.

Außerdem wird es eine Version in deutsch und englisch geben, zumindest am Anfang. Die Sprachen können auch direkt im Spiel geändert werden, weil ich z.B. meine Testgeräte auf englisch gestellt habe, aber auch die deutschen Texte testen muss. Dabei möchte ich nicht immer erst die Systemsprache anpassen.

## Entity Systeme

Ein Entity System ist für einzelne Programmbereiche, aus meiner Sicht, sinnvoll, weil es eine logische Trennung zwischen Logik und grafischer Darstellung darstellt. Ich habe mehrere Entity Systeme getestet, die ich hier kurz anreißen möchte.

### artemis

Artemis ist ein Entity System Framework und somit kann ich es gut für einzelne Bereiche im Spiel einsetzen. Welche das sein werden, weiß ich noch nicht, aber es wird garantiert in der [Daydream](daydream) Funktionalität genutzt werden.

### ashley

Neben Artemis gibt es noch ein zweites Entity System Framework, welches derzeit sogar noch teilweise weiterentwickelt wird. Der einzige Unterschied, den ich zu Artemis feststellen konnte, ist der Fakt, dass es viel allgemeiner gehalten ist. 

Nachdem ich ein wenig mehr mit Ashley ausprobiert habe, bin ich zu dem Entschluss gekommen, dass ich mich von Artemis komplett trenne und voll und ganz auf Ashley setze. Der Artemis Programmpart wurde vollständig auf Ashley portiert und läuft auch.

## Funktionen

Hier eine grobe Übersicht der wichtigsten Funktionen die später im Spiel eingebaut sein sollen.

* [Daydream](daydream) - Bildschirmschoner (Android 4.2+)
* [Google Play Game Service](googleplaygameservice) - Unterstützung für Erfolge und/oder Highscore

Außerdem sind noch ein paar Fragen offen, die ich unter [Offene Punkte](open) zusammenfasse. Es ist also eine Art Ideensammlung.