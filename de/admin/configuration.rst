.. _Einrichtung:

Einrichtung
===========

Um mit der Einrichtung zu beginnen, starten Sie den Veyon Configurator, sofern dies nach Abschluss der Installation nicht schon automatisch erfolgt ist. Mit diesem Programm ist es möglich, eine lokale Veyon-Installation einzurichten und anzupassen. Die grafische Oberfläche ist dabei in verschiedene themen- bzw. komponentenbezogene Konfigurationsseiten untergliedert. Je nach installierten Plugins kann es zusätzliche Konfigurationsseiten geben.

.. image:: images/configurator.png
   :scale: 75 %
   :align: center

Für einen Schnellstart zum Kennenlernen der Software müssen Sie zunächst nur die :ref:`Anmelde-Authentifizierung` aktivieren und in der Konfigurationsseite :ref:`Lokale Daten` einen Raum sowie einzelne Computer hinzufügen. Alle anderen Einstellungen können Sie auf den Vorgabewerten belassen.

Im weiteren Verlauf des Kapitels werden alle Konfigurationsseiten sowie alle Konfigurationsoptionen mit ihren jeweiligen Bedeutungen behandelt.

Allgemein
---------

Die grundlegenden Einstellungen auf der Hauptseite betreffen alle :ref:`Komponenten` von Veyon. Dazu zählen die Sprache, Logaufzeichnung sowie das Netzwerkobjektverzeichnis.

Benutzeroberfläche
++++++++++++++++++

Sprache
    Die verwendete Sprache für sowohl die grafischen Benutzeroberflächen als auch Kommandozeilenwerkzeuge kann bei Bedarf angepasst werden. Es stehen alle Sprachen zur Auswahl, für die eine teilweise oder vollständige Übersetzung vorliegt. Bitte beachten Sie, dass sich die Änderung der Sprache nach einem Programmneustart auswirkt. Beim standardmäßig eingestellten Vorgabewert passt sich Veyon an die im Betriebssystems eingestellte Sprache an, sofern die Sprache unterstützt wird. Andernfalls wird Englisch als Ausweichoption verwendet.

    **Vorgabe:** *Spracheinstellung des Systems verwenden*

High-DPI-Skalierung
    Beim Einsatz von Veyon auf hochaufgelösten Bildschirmen mit hoher Pixeldichte (DPI>150) sollte diese Option aktiviert werden. Sofern aktiviert werden die Benutzeroberflächen größer dargestellt, so dass vor allem visuelle Elemente mit Textbeschriftungen besser lesbar sind.

    **Vorgabe:** *deaktiviert*


Logaufzeichnung
+++++++++++++++

Über verschiedene Optionen kann das Verhalten der Logaufzeichnung beeinflusst werden. Diese Einstellungen sind vor allem dann interessant, wenn es zu Problemen beim Einsatz von Veyon kommt. Logdateien können hier Aufschluss über mögliche Fehlerursachen geben.

Logdateiverzeichnis
    Über diese Einstellung kann festgelegt werden, in welchen Ordner Logdateien abgelegt werden. Üblicherweise sollte hier eine Platzhaltervariable verwendet werden. Eine ausführliche Beschreibung möglicher Werte befindet sich in der :ref:`Konfigurationsreferenz` im Abschnitt :ref:`Platzhaltervariablen`.

    **Vorgabe:** *%TEMP%*

Loglevel
    Der Loglevel legt fest, wie detailliert Logmeldungen aufgezeichnet werden. Bei der Fehlersuche kann es hilfreich sein, den Loglevel auf den Wert :guilabel:`Debugmeldungen und alles andere` festzulegen. Hierbei können sich allerdings schnell große Datenmengen ansammeln. Im Regelbetrieb sollten nur Warnungen und Fehler aufgezeichnet werden.

    **Vorgabe:** *Informationen, Warnungen und Fehler*

Logdateigröße begrenzen
    Damit die Logdateien im Laufe der Zeit nicht zu groß werden und unnötigen Speicherplatz belegen, kann deren Größe über diese Option begrenzt werden. Wenn aktiviert, kann eine obere Grenze für die Größe einzelner Logdateien eingestellt werden.

    **Vorgabe:** *deaktiviert / 1 MB*

Logdateien rotieren
    Im Zusammenspiel mit der Begrenzung der Logdateigröße kann es darüber hinaus hilfreich sein, die Logdateien zu rotieren. In diesem Fall wird eine Logdatei beim Erreichen der eingestellten Grenze nach ``Veyon...log.0`` umbenannt. Vorher rotierte Dateien werden so umbenannt, dass sich die Zahl in der Dateiendung immer um 1 erhöht. Ist die maximale Anzahl an Rotationen erreicht, wird die älteste Datei (d. h. mit der höchsten Zahl) gelöscht.

    **Vorgabe:** *deaktiviert / 10x*

Nach Standardfehlerausgabe loggen
    Wenn Programmkomponenten von Veyon in einem Kommandozeilenfenster ausgeführt werden, kann über diese Option festgelegt werden, ob Logmeldungen über den Kanal Standardfehlerausgabe (``stderr``) oder Standardausgabe (``stdout``) ausgegeben werden. Diese Einstellung ist in erster Linie für Scriptoperationen relevant.

    **Vorgabe:** *aktiviert*

In Windows-Ereignisanzeige loggen
    Für ein zentrales Management ist es in einigen Fällen hilfreich, Logmeldungen direkt in die Windows-Ereignisanzeige zu loggen. Diese Einstellung beeinflusst nicht die normale Logdateiaufzeichnung. Unter Linux ist die Einstellung wirkungslos.

    **Vorgabe:** *deaktiviert*

Über die Schaltfläche :guilabel:`Alle Logdateien leeren` können alle Veyon-Logdateien sowohl im Logdateiverzeichnis des aktuellen Benutzers als des Systemdiensts gelöscht werden.


Netzwerkobjektverzeichnis
+++++++++++++++++++++++++

Ein Netzwerkobjektverzeichnis stellt in Veyon Informationen über Netzwerkobjekte bereit. Netzwerkobjekte sind Computer sowie Räume, in denen sich  Computer befinden. Die Daten aus dem Netzwerkobjektverzeichnis werden vom Veyon Master verwendet, um Computerraumverwaltung mit Einträgen zu befüllen. Auch für die Zugriffskontrolle wird auf Daten im Netzwerkobjektverzeichnis zurückgegriffen. Standardmäßig wird ein Backend verwendet, das diese Daten in der lokalen Veyon-Konfiguration speichert und von dort ausliest, siehe Abschnitt :ref:`Lokale Daten`.

Backend
    Über diese Einstellung kann das gewünschte Netzwerkobjektverzeichnis-Backend gewählt werden. Abhängig von der Installation stehen neben dem Standard-Backend weitere Backends beispielsweise zur :ref:`LDAP` zur Verfügung.

    **Vorgabe:** *Standard (Objekte in lokaler Konfiguration speichern)*

Aktualisierungsintervall
    Das Netzwerkobjektverzeichnis kann im Hintergrund automatisch aktualisiert werden, was beim Einsatz von dynamischen Backends wie LDAP hilfreich sein kann. Das zeitliche Intervall für diese Aktualisierungen kann mit dieser Einstellung geändert werden.

    **Vorgabe:** *60 Sekunden*


Dienst
------

Die Einstellungen auf der Konfigurationsseite "Dienst" beeinflussen die Funktionsweise des Veyon-Diensts (Veyon Service) und dienen dem Finetuning in einigen Sonderfällen. Für einen reibungslosen Betrieb sollten die Einstellungen im Regelfall nicht geändert werden.

Allgemein
+++++++++

Icon im Infobereich verstecken
    Standardmäßig zeigt der Veyon-Dienst ein Icon im Infobereich (auch *Systemabschnitt der Kontrollleiste*) an, um den ordnungsgemäßen Betrieb sowie Informationen zur Programmversion und belegten Netzwerkports anzuzeigen. Die Anzeige des Icons kann unterbunden werden, indem diese Option aktiviert wird.

    **Vorgabe:** *deaktiviert*

SAS-Generierung in Software aktivieren (Strg+Alt+Entf)
    In der Standardkonfiguration ist es unter Windows für Anwendungsprogramme nicht möglich, die Secure-Attention-Sequence (Strg+Alt+Entf) zu generieren und somit den Druck dieser Tasten zu simulieren. Über diese Einstellung wird eine Policy in die Windows-Registry geschrieben, die dieses Verhalten ändert. Es wird empfohlen, diese Option aktiviert zu lassen, damit die Tastenkombination :kbd:`Strg+Alt+Entf` an einen ferngesteuerten Computer gesendet werden kann. Der ferngesteuerte Computer kann andernfalls z. B. nicht aus der Ferne entsperrt werden. Auch eine Nutzeranmeldung ist dann nicht möglich, da hierfür üblicherweise die Tasten :kbd:`Strg+Alt+Entf` gedrückt werden müssen.

    **Vorgabe:** *aktiviert*

Netzwerk
++++++++

Primärer Dienst-Port
    Diese Einstellung legt den primären Netzwerkport fest, auf dem der Veyon-Dienst lauscht und Verbindungen annimmt.

    **Vorgabe:** *11100**

Port des internen VNC-Servers
    Diese Einstellung legt den Netzwerkport fest, auf dem der interne VNC-Server arbeitet. Dieser Port ist nach außen nicht erreichbar und wird nur vom Veyon-Dienst verwendet, um über einen internen VNC-Server auf Bildschirmdaten zuzugreifen und diese nach außen weiterzuleiten.

    **Vorgabe:** *11200*

Funktionsverwalter-Port
    Diese Einstellung legt den Netzwerkport fest, auf dem der Funktionsverwalter arbeitet. Diese interne Komponente des Veyon-Diensts stellt die Schnittstelle zwischen Veyon-Dienst und Funktionsprozessen bereit. Funktionsprozesse laufen im Gegensatz zum Veyon-Dienst im Kontext des angemeldeten Benutzers aus und müssen daher über diese Schnittstelle mit dem Veyon-Dienst kommunizieren.

    **Vorgabe:** *11300*

Demoserver-Port
    Diese Einstellung legt den Netzwerkport fest, auf dem der Demo-Server arbeitet. Der Demo-Server stellt während einer Vorführung Bildschirmdaten des Lehrer-Rechners im Netzwerk zur Verfügung.

    **Vorgabe:** *11400*


VNC-Server
++++++++++


Plugin
    Standardmäßig verwendet Veyon eine interne plattformspezifische VNC-Server-Implementierung, um die Bildschirmdaten eines Rechners bereitstellen zu können. In einigen Sonderfällen kann es gewünscht sein, ein Plugin mit einer anderen Implementierung zu verwenden. Wenn beispielsweise bereits ein separater VNC-Server auf dem Computer installiert ist, kann dieser alternativ verwendet werden, indem das Plugin "Externer VNC-Server" gewählt wird. In diesem Fall müssen das Passwort und der Netzwerkport des VNC-Servers eingegeben werden.

    **Vorgabe:** *Eingebauter VNC-Server*


Master
------

Verzeichnisse
+++++++++++++

Benutzeroberfläche & Verhalten
++++++++++++++++++++++++++++++

Funktionen
++++++++++

Authentifizierung
-----------------

Authentifizierungsmethoden
++++++++++++++++++++++++++

Schlüsselverwaltung
+++++++++++++++++++

.. _Anmelde-Authentifizierung:

Anmelde-Authentifizierung
+++++++++++++++++++++++++

Zugriffskontrolle
-----------------

Computerzugriffskontrolle
+++++++++++++++++++++++++


Autorisierte Benutzergruppen für Computerzugriff
++++++++++++++++++++++++++++++++++++++++++++++++

Zugriffskontrollregeln
++++++++++++++++++++++

Fehlersuche
-----------

LDAP
----

Alle Informationen rund um die Anbindung von Veyon an einen LDAP-/ActiveDirectory-Server finden Sie gesondert im Kapitel :ref:`LDAP`.

.. _Lokale Daten:

Lokale Daten
------------
