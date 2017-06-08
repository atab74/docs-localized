Einführung
==========

Über dieses Handbuch
--------------------

Dieses Handbuch beschreibt die Installation und Einrichtung von Veyon in einem Computernetzwerk und richtet sich an Administratoren und technisch versierte Benutzer. Für Endanwender gibt es ein separates Benutzerhandbuch, in dem die Bedienung sowie die einzelnen Funktionen des Anwenderprogramms (Veyon Master) beschrieben sind.

In weiteren Abschnitten dieses Kapitels finden Sie grundlegende Informationen über Veyon und seine Bestandteile, die für die Inbetriebnahme von elementarer Bedeutung sind.

Im Kapitel :ref:`Installation` wird die Installation und Integration von Veyon auf einem Windows- oder Linux-Computer behandelt. Hier finden Sie auch Hinweise, wie Sie die Installation automatisiert durchführen können.

Die Einrichtung mit Hilfe des grafischen Einrichtungswerkzeugs sowie die verschiedenen Einstelloptionen sind im Kapitel :ref:`Einrichtung` detailliert beschrieben. Die Anbindung an einen LDAP-/ActiveDirectory-Server wird im Kapitel :ref:`LDAP` gesondert behandelt.

Veyon verfügt weiterhin über eine Kommandozeilenschnittstelle (CLI), über die sich Konfigurationsanpassungen vornehmen lassen und bestimmte Programmfunktionen verwendet oder gesteuert werden können. Alle Funktionen des Kommandozeilenwerkzeugs sind im Kapitel :ref:`Kommandozeilenschnittstelle` aufgeführt und erläutert.

Bei Problemen mit Veyon können Sie das Kapitel :ref:`Troubleshooting` konsultieren. Hier finden Sie Maßnahmen zur Fehleranalyse und -behebung. Häufige Fragen werden im Kapitel :ref:`FAQ` beantwortet.


Über Veyon
-----------

Veyon ist eine quelloffene Software für Computer-Monitoring- und Klassenraumverwaltung. Sie erlaubt die Beobachtung und Steuerung von Computerräumen sowie die Interaktion mit B
enutzern. Die wichtigsten Funktionen von Veyon sind:

* Überblick über einen (Klassen-)Raum mit allen Bildschirminhalten in einer Kachelansicht
* Fernsteuerung von Computern
* Übertragung des Lehrerbildschirms an alle anderen Computer in Echtzeit (Vollbild/Fenster)
* Sperren von Arbeitsplätzen zur Aufmerksamkeitslenkung
* Textnachrichten an Schüler senden
* Computer aus der Ferne ein- oder ausschalten sowie neustarten
* Benutzer abmelden
* Programme ausführen oder Websiten öffnen


Komponenten
-----------

Veyon besteht aus verschiedenen Programmkomponenten:

Veyon Service
    Dienstprogramm, das den Zugriff auf einen Computer, Steuerungsfunktionen und Anwendungsfunktionen bereitstellt. Das Programm wird automatisch vom Betriebssystem als Dienst mit erhöhten Privilegien ausgeführt und kann vom Benutzer nicht beendet werden.

Veyon Master
    Anwendungsprogramm, mit dem andere Computer beobachtet und gesteuert und Veyon-Funktionen genutzt werden können. Das Programm wird im regulären Anwendungsfall vom Endanwender gestartet.

Veyon Configurator
    Konfigurationswerkzeug, welches die Einrichtung und Anpassung einer lokalen Veyon-Installation über eine grafische Benutzeroberfläche ermöglicht. Das Programm wird bei Bedarf vom Administrator mit erhöhten Privilegien gestartet.

Veyon Control
    Kommandozeilenwerkzeug, das als Ergänzung zum Veyon Configurator ohne grafische Interaktion verschiedene Konfigurationsanpassungen und die Verwendung einiger Veyon-Funktionen erlaubt. Das Programm wird entweder interaktiv auf der Kommandozeile oder scriptgesteuert mit administrativen Privilegien ausgeführt. Einzelne Funktionen benötigen keine zusätzlichen Berechtigungen.
