.. _Konfigurationsreferenz:

Konfigurationsreferenz
======================

In diesem Kapitel sind alle Konfigurationsseiten im Veyon Configurator sowie alle Konfigurationsoptionen mit ihren jeweiligen Bedeutungen beschrieben. Es dient in erster Linie als Referenz, um Details zu bestimmten Einstellmöglichkeiten nachzuschauen. Eine Anleitung und Hinweise zur Einrichtung befinden sich im Kapitel :ref:`Einrichtung`.

.. _Allgemein:

Allgemein
---------

.. _Benutzeroberflaeche:

Benutzeroberfläche
++++++++++++++++++

:index:`Sprache`
    Die verwendete Sprache für sowohl die grafischen Benutzeroberflächen als auch Kommandozeilenwerkzeuge kann bei Bedarf angepasst werden. Es stehen alle Sprachen zur Auswahl, für die eine teilweise oder vollständige Übersetzung vorliegt. Es sollte beachtet werden, dass sich die Änderung der Sprache erst nach einem Programmneustart auswirkt. Beim standardmäßig eingestellten Vorgabewert passt sich Veyon an die im Betriebssystems eingestellte Sprache an, sofern die Sprache unterstützt wird. Andernfalls wird Englisch als Ausweichoption verwendet.

    **Vorgabe:** *Spracheinstellung des Systems verwenden*

:index:`High-DPI-Skalierung`
    Beim Einsatz von Veyon auf hochaufgelösten Bildschirmen mit hoher Pixeldichte (DPI>150) sollte diese Option aktiviert werden. Sofern aktiviert werden die Benutzeroberflächen größer dargestellt, so dass vor allem visuelle Elemente mit Textbeschriftungen besser lesbar sind.

    **Vorgabe:** *deaktiviert*

.. _Logaufzeichnung:

Logaufzeichnung
+++++++++++++++

Über verschiedene Optionen kann das Verhalten der :index:`Logaufzeichnung` beeinflusst werden. Diese Einstellungen sind vor allem dann interessant, wenn es zu Problemen beim Einsatz von Veyon kommt. :index:`Logdateien` können hier Aufschluss über mögliche Fehlerursachen geben.

:index:`Logdateiverzeichnis`
    Über diese Einstellung kann festgelegt werden, in welchen Ordner Logdateien abgelegt werden. Üblicherweise sollte hier eine Platzhaltervariable verwendet werden. Eine ausführliche Beschreibung möglicher Werte befindet sich im Abschnitt :ref:`Platzhaltervariablen`.

    **Vorgabe:** *$TEMP*

:index:`Loglevel`
    Der Loglevel legt fest, wie detailliert Logmeldungen aufgezeichnet werden. Bei der Fehlersuche kann es hilfreich sein, den Loglevel auf den Wert :guilabel:`Debugmeldungen und alles andere` festzulegen. Hierbei können sich allerdings schnell große Datenmengen ansammeln. Im Regelbetrieb sollten nur Warnungen und Fehler aufgezeichnet werden.

    **Vorgabe:** *Informationen, Warnungen und Fehler*

:index:`Logdateigröße begrenzen`
    Damit die Logdateien im Laufe der Zeit nicht zu groß werden und unnötigen :index:`Speicherplatz` belegen, kann deren Größe über diese Option begrenzt werden. Wenn aktiviert, kann eine obere Grenze für die Größe einzelner Logdateien eingestellt werden.

    **Vorgabe:** *deaktiviert / 1 MB*

:index:`Logdateien rotieren`
    Im Zusammenspiel mit der Begrenzung der Logdateigröße kann es darüber hinaus hilfreich sein, die Logdateien zu rotieren. In diesem Fall wird eine Logdatei beim Erreichen der eingestellten Grenze nach ``Veyon...log.0`` umbenannt. Vorher rotierte Dateien werden so umbenannt, dass sich die Zahl in der Dateiendung immer um 1 erhöht. Ist die maximale Anzahl an Rotationen erreicht, wird die älteste Datei (d. h. mit der höchsten Zahl) gelöscht.

    **Vorgabe:** *deaktiviert / 10x*

Nach :index:`Standardfehlerausgabe` loggen
    Wenn Programmkomponenten von Veyon in einem Kommandozeilenfenster ausgeführt werden, kann über diese Option festgelegt werden, ob Logmeldungen über den Kanal Standardfehlerausgabe (``stderr``) oder Standardausgabe (``stdout``) ausgegeben werden. Diese Einstellung ist in erster Linie für Scriptoperationen relevant.

    **Vorgabe:** *aktiviert*

In :index:`Windows-Ereignisanzeige` loggen
    Für ein zentrales Management ist es in einigen Fällen hilfreich, Logmeldungen direkt in die Windows-Ereignisanzeige zu loggen. Diese Einstellung beeinflusst nicht die normale Logdateiaufzeichnung. Unter Linux ist die Einstellung wirkungslos.

    **Vorgabe:** *deaktiviert*

Über die Schaltfläche :guilabel:`Alle Logdateien leeren` können alle Veyon-Logdateien sowohl im Logdateiverzeichnis des aktuellen Benutzers als des Systemdiensts gelöscht werden.


.. _Netzwerkobjektverzeichnis:

Netzwerkobjektverzeichnis
+++++++++++++++++++++++++

Ein :index:`Netzwerkobjektverzeichnis` stellt in Veyon Informationen über :index:`Netzwerkobjekte` bereit. Netzwerkobjekte sind Computer sowie Räume, in denen sich Computer befinden. Die Daten aus dem Netzwerkobjektverzeichnis werden vom Veyon Master verwendet, um :index:`Computerraumverwaltung` mit Einträgen zu befüllen. Auch für die Zugriffskontrolle wird auf Daten im Netzwerkobjektverzeichnis zurückgegriffen. Standardmäßig wird ein Backend verwendet, das diese Daten in der lokalen Veyon-Konfiguration speichert und von dort ausliest, siehe Abschnitt :ref:`Lokale Daten`.

:index:`Backend`
    Über diese Einstellung kann das gewünschte Netzwerkobjektverzeichnis-Backend gewählt werden. Abhängig von der Installation stehen neben dem Standard-Backend weitere Backends beispielsweise zur :ref:`LDAP` zur Verfügung.

    **Vorgabe:** *Standard (Objekte in lokaler Konfiguration speichern)*

:index:`Aktualisierungsintervall`
    Das Netzwerkobjektverzeichnis kann im Hintergrund automatisch aktualisiert werden, was beim Einsatz von dynamischen Backends wie LDAP praktisch sein kann. Das zeitliche Intervall für diese Aktualisierungen kann mit dieser Einstellung geändert werden.

    **Vorgabe:** *60 Sekunden*


.. _Dienstkonfiguration:

Dienst
------

.. _DienstAllgemein:

Allgemein
+++++++++

:index:`Icon im Infobereich` verstecken
    Standardmäßig zeigt der Veyon-Dienst ein Icon im Infobereich (auch *Systemabschnitt der Kontrollleiste*) an, um den ordnungsgemäßen Betrieb sowie Informationen zur :index:`Programmversion` und belegten Netzwerkports anzuzeigen. Die Anzeige des Icons kann unterbunden werden, indem diese Option aktiviert wird.

    **Vorgabe:** *deaktiviert*

:index:`SAS-Generierung` in Software aktivieren (Strg+Alt+Entf)
    In der Standardkonfiguration ist es unter Windows für Anwendungsprogramme nicht möglich, die Secure-Attention-Sequence (Strg+Alt+Entf) zu generieren und somit den Druck dieser Tasten zu simulieren. Über diese Einstellung wird eine Policy in die Windows-Registry geschrieben, die dieses Verhalten ändert. Es wird empfohlen, diese Option aktiviert zu lassen, damit die Tastenkombination :kbd:`Strg+Alt+Entf` an einen ferngesteuerten Computer gesendet werden kann. Der ferngesteuerte Computer kann andernfalls z. B. nicht aus der Ferne entsperrt werden. Auch eine Nutzeranmeldung ist dann nicht möglich, da hierfür üblicherweise die Tasten :kbd:`Strg+Alt+Entf` gedrückt werden müssen.

    **Vorgabe:** *aktiviert*

:index:`Autostart`
    Diese Option legt fest, ob der Veyon-Dienst im Betriebssystem als :index:`Systemdienst` registriert wird, so dass er automatisch beim Hochfahren des Computers gestartet wird.

    **Vorgabe:** *aktiviert*

Zusätzliche Argumente
    Wird der Veyon-Dienst als Systemdienst registriert, können über diese Einstellung zusätzliche Programmargumente festgelegt werden, die das Betriebssystem dem Veyon-Diest beim Start übergibt. Nähere Angaben zu möglichen Optionen befinden sich im Abschnitt :ref:`ServiceArgumente`.

    **Vorgabe:** *<leer>*

    
.. _Netzwerkeinstellungen:

Netzwerk
++++++++

:index:`Primärer Dienst-Port`
    Diese Einstellung legt den primären :index:`Netzwerkport` fest, auf dem der Veyon-Dienst arbeitet, d. h. auf eingehende Verbindungen lauscht und diese annimmt.

    **Vorgabe:** *11100*

Port des internen VNC-Servers
    Diese Einstellung legt den Netzwerkport fest, auf dem der interne :index:`VNC-Server` arbeitet. Dieser Port ist von außen nicht erreichbar und wird nur vom Veyon-Dienst verwendet, um über einen internen VNC-Server auf Bildschirmdaten zuzugreifen und diese nach außen weiterzuleiten.

    **Vorgabe:** *11200*

Funktionsverwalter-Port
    Diese Einstellung legt den Netzwerkport fest, auf dem der :index:`Funktionsverwalter` arbeitet. Diese interne Komponente des Veyon-Diensts stellt die Schnittstelle zwischen Veyon-Dienst und Funktionsprozessen bereit. Funktionsprozesse laufen im Gegensatz zum Veyon-Dienst im Kontext des angemeldeten Benutzers aus und müssen daher über diese Schnittstelle mit dem Veyon-Dienst kommunizieren. Dieser Port ist von außen nicht erreichbar.

    **Vorgabe:** *11300*

Demoserver-Port
    Diese Einstellung legt den Netzwerkport fest, auf dem der :index:`Demoserver` arbeitet. Der Demoserver stellt während einer Vorführung Bildschirmdaten des Lehrer-Computers im Netzwerk zur Verfügung.

    **Vorgabe:** *11400*

:index:`Firewall-Ausnahme` aktivieren
    Unter Windows kann ein Prozess je nach Systemkonfiguration unter Umständen nicht öffentlich auf einem Port lauschen, da Verbindungsanfragen durch die :index:`Windows-Firewall` blockiert werden. Um den Zugriff auf den Dienst-Port sowie den Demoserver-Port zu ermöglichen, müssen Ausnahmen für die Windows-Firewall konfiguriert werden. Dies geschieht standardmäßig automatisch im Rahmen der Installation. Wenn dieses Verhalten nicht gewünscht ist und eine manuelle Konfiguration erfolgen soll, kann diese Option deaktiviert werden.

    **Vorgabe:** *aktiviert*

Nur Verbindungen vom lokalen Computer erlauben
    Wenn der Veyon-Dienst für andere Computer im Netzwerk nicht erreichbar sein soll, kann diese Option aktiviert werden. Für normale Rechner, auf die mit dem Veyon Master zugegriffen werden soll, darf diese Option nicht aktiviert werden. Für Lehrer-Computer kann die Option hingegen sinnvoll sein, um unabhängig von den Zugriffskontrolleinstellungen zusätzliche Sicherheit zu schaffen. Der Zugriff auf den Demoserver wird durch diese Einstellung nicht beeinflusst.

    **Vorgabe:** *deaktiviert*


.. index:: VNC-Server, interner VNC-Server, externer VNC-Server

VNC-Server
++++++++++

Plugin
    Standardmäßig verwendet Veyon eine interne plattformspezifische VNC-Server-Implementierung, um die Bildschirmdaten eines Rechners bereitstellen zu können. In einigen Sonderfällen kann es gewünscht sein, ein Plugin mit einer anderen Implementierung zu verwenden. Wenn beispielsweise bereits ein separater VNC-Server auf dem Computer installiert ist, kann dieser anstatt des internen VNC-Servers verwendet werden, indem das Plugin :guilabel:`Externer VNC-Server` gewählt wird. In diesem Fall müssen das Passwort und der Netzwerkport des installierten VNC-Servers eingegeben werden.

    **Vorgabe:** *Eingebauter VNC-Server*


.. _Masterkonfiguration:

Master
------

Verzeichnisse
+++++++++++++

Für die Verzeichniseinstellungen sollten Platzhaltervariablen anstatt absoluter Pfade verwendet werden, damit die Konfiguration generisch ist und benutzerunabhängig funktioniert. Eine ausführliche Beschreibung möglicher Werte befindet sich im Abschnitt :ref:`Platzhaltervariablen`.

:index:`Benutzerkonfiguration`
     In dem hier eingestellten Verzeichnis wird die benutzerspezifische Konfiguration des Master-Programms abgelegt. Diese Konfiguration beinhaltet Einstellungen der Benutzeroberfläche sowie die Computerauswahl der letzten Sitzung.

     **Vorgabe:** *$APPDATA/Config*

:index:`Bildschirmfotos`
    In dem hier eingestellten Verzeichnis werden alle Bilddateien abgespeichert, die über die Bildschirmfoto-Funktion aufgenommen wurden. Wenn es beispielsweise gewünscht ist, die Dateien in einem zentralen Sammelordner abzulegen, kann hier ein anderer Verzeichnispfad eingetragen werden.

    **Vorgabe:** *$APPDATA/Screenshots*


.. index:: Computerraumverwaltung, Benutzeroberfläche

Benutzeroberfläche & Verhalten
++++++++++++++++++++++++++++++

Zugriffskontrolle beim Programmstart durchführen
    Diese Einstellung legt fest, ob die ggf. konfigurierte :ref:`Computerzugriffskontrolle` auch beim Start des Veyon Masters durchgeführt werden soll. Auch wenn die Zugriffskontrolle in jedem Fall clientseitig durchgesetzt wird, kann diese zusätzliche Option dafür sorgen, dass Benutzer ohne Zugriffsrechte den Veyon Master gar nicht erst starten können und die Sicherheit damit noch sichtbarer wird.

    **Vorgabe:** *deaktiviert*

Beim Start automatisch zu aktuellem Raum wechseln
    Standardmäßig werden nach Start des Veyon Masters beim vorherigen Mal ausgewählten Computer angezeigt. Wenn stattdessen alle Computer des Raums angezeigt werden sollen, in dem sich der Master-Computer befindet, kann diese Option aktiviert werden. Der Veyon Master versucht dann über das eingestellte :ref:`Netzwerkobjektverzeichnis` zu ermitteln, zu welchem Raum der lokale Computer gehört. Alle Computer dieses Raums werden dann angezeigt.

    **Vorgabe:** *deaktiviert*

Nur aktuellen Raum in Computerraumverwaltung anzeigen
    Die Computerraumverwaltung listet standardmäßig alle Räume auf, die sich im eingestellten :ref:`Netzwerkobjektverzeichnis` befinden. Die Aktivierung dieser Option bewirkt hingegen, dass nur der Raum aufgeführt wird, in dem sich der Master-Computer befindet. Dies kann insbesondere in größeren Umgebungen die Übersichtlichkeit deutlich erhöhen.

    **Vorgabe:** *deaktiviert*

Manuelles Hinzufügen von Räumen zur Computerraumverwaltung erlauben
    Im Zusammenspiel mit der Option *Nur aktuellen Raum in Computerraumverwaltung anzeigen* kann optional erlaubt werden, weitere Räume manuell zur Computerraumverwaltung hinzuzufügen. Wenn die Option aktiviert ist, wird eine zusätzliche Schaltfläche :guilabel:`Raum hinzufügen` angezeigt, die einen Dialog mit allen verfügbaren Räumen öffnet.

    **Vorgabe:** *deaktiviert*

Lokalen Computer in Computerraumverwaltung ausblenden
    Im Regelbetrieb ist es oft nicht gewünscht, den eigenen Computer anzuzeigen und raumweit aktivierte Funktionen auch auf dem eigenen Computer zu aktivieren (z. B. Bildschirmsperre). Wenn ein solches Verhalten gewünscht ist, kann diese Option aktiviert werden.

    **Vorgabe:** *deaktiviert*

Leere Räume in Computerraumverwaltung ausblenden
    Unter bestimmten Umständen befinden sich im :ref:`Netzwerkobjektverzeichnis` Räume ohne Computer, beispielsweise aufgrund von bestimmten LDAP-Filtern. Solche leeren Räume können über diese Option aus der Computerraumverwaltung ausgeblendet werden.

    **Vorgabe:** *deaktiviert*

Filterfeld für Computer in Computerraumverwaltung ausblenden
    Das Filterfeld zum Suchen von Computern kann über diese Option bei Bedarf ausgeblendet werden, um in überschaubaren Umgebungen die Benutzeroberfläche möglichst einfach zu halten.

    **Vorgabe:** *deaktiviert*

Funktion bei :index:`Doppelklick`
    Wenn ein Computer im Veyon Master doppelt angeklickt wird, kann eine vorgegebene Funktion gestartet werden. Üblich ist hier die Verwendung der Funktionen *Fernsteuerung* oder *Fernansicht*.

    **Vorgabe:** *<Keine Funktion>*

Funktionen
++++++++++

Über die zwei Listen im Abschnitt :guilabel:`Funktionen` kann voreingestellt werden, welche Funktionen im Veyon Master verfügbar sind. Einzelne Funktionen können somit bei Bedarf deaktiviert werden, so dass entsprechende Schaltflächen und Kontextmenüeinträge im Veyon Master nicht angezeigt werden. Dies kann die Übersichtlichkeit der Benutzeroberfläche erhöhen, wenn bestimmte Funktionen ohnehin nicht verwendet werden sollen.

Eine Funktion kann in die jeweils andere Liste verschoben werden, indem sie markiert und die jeweilige Schaltfläche mit den Pfeilsymbolen betätigt wird. Zusätzlich hat auch ein Doppelklick auf eine Funktion die gleiche Wirkung.

.. _Authentifizierungskonfiguration:

Authentifizierung
-----------------

Authentifizierungsmethoden
++++++++++++++++++++++++++

Für die im Kapitel :ref:`Einrichtung` beschriebenen :ref:`Authentifizierungsmethoden` stehen die gleichnamigen Optionen zur Verfügung. Sobald eine Option aktiviert wurde, ist die Einrichtung der jeweiligen Authentifizierungsmethode möglich.

:index:`Schlüsseldatei-Authentifizierung`
    Über diese Option wird die :ref:`Schlüsseldatei-Authentifizierung <SchluesselAuthentifizierung>` aktiviert. Die Einrichtung erfolgt über den Schlüsseldatei-Assistent.

    **Vorgabe:** *deaktiviert*

:index:`Anmelde-Authentifizierung`
    Über diese Option wird die :ref:`Anmelde-Authentifizierung <AnmeldeAuthentifizierung>` aktiviert. Sie bedarf keiner weiteren Einrichtung und kann nach Aktivierung über die Schaltfläche :guilabel:`Testen` getestet werden.

    **Vorgabe:** *deaktiviert*

Schlüsselverwaltung
+++++++++++++++++++

.. _Basisverzeichnisse:

Für beide Basisverzeichnisse sollten Platzhaltervariablen verwendet werden. Eine ausführliche Beschreibung möglicher Werte befindet sich in der :ref:`Konfigurationsreferenz` im Abschnitt :ref:`Platzhaltervariablen`. Unter Windows können anstatt absoluter Laufwerkspfade auch `UNC-Pfade <https://de.wikipedia.org/wiki/Uniform_Naming_Convention>`_ verwendet werden.

:index:`Basisverzeichnis` der öffentlichen Schlüsseldatei
    In diesem Verzeichnis werden die rollenspezifischen öffentlichen Schlüsseldateien vom Schlüsseldatei-Assistent bei der Schlüsselgenerierung oder dem Import abgelegt. Gleichzeitig lädt der Veyon-Dienst die jeweilige öffentliche Schlüsseldatei zur Durchführung der Authentifizierung aus diesem Verzeichnis.

    **Vorgabe:** *$GLOBALAPPDATA/keys/public*

Basisverzeichnis der privaten Schlüsseldatei
    In diesem Verzeichnis werden die rollenspezifischen privaten Schlüsseldateien vom Schlüsseldatei-Assistent bei der Schlüsselgenerierung. Gleichzeitig lädt der Veyon Master die jeweilige private Schlüsseldatei aus diesem Verzeichnis, um sich an Clients zu authentifizieren.

    **Vorgabe:** *$GLOBALAPPDATA/keys/private*


.. _RefZugriffskontrolle:

Zugriffskontrolle
-----------------

.. _Computerzugriffskontrolle:

Computerzugriffskontrolle
+++++++++++++++++++++++++


:index:`Datenbackend`
    Für die Zugriffskontrolle wird ein Datenbackend als Grundlage benötigt, das Benutzer und Gruppen sowie Computer und Räume zur Verfügung stellt. Hierbei können Sie zwischen dem Standard-Backend und weiteren Plugin-spezifischen Backends wie LDAP wählen. Beim Standard-Backend werden lokale Benutzer und Gruppen sowie Räume und Computer aus der lokalen Konfiguration verwendet, siehe Abschnitt :ref:`Lokale Daten`. Wenn Sie die LDAP-Anbindung verwenden, sollten Sie hier das Backend *LDAP* auswählen.

Jedem authentifizierten Benutzer Zugriff erlauben (Standard)
    Falls die eingestellte Authentifizierung genügt (z. B. bei Verwendung der Schlüsseldatei-Authentifizierung mit eingeschränktem Zugriff auf die Schlüsseldateien) kann diese Option gewählt werden. In diesem Modus wird keine weitere Zugriffskontrolle durchgeführt.

Zugriff auf Mitglieder bestimmter Benutzergruppen einschränken
    In diesem Modus wird der Zugriff auf einen Computer auf Mitglieder von bestimmten Benutzergruppen eingeschränkt. Die autorisierten Benutzergruppen werden im Abschnitt  :ref:`Autorisierte Benutzergruppen für Computerzugriff` eingestellt.

Zugriffskontrollregeln abarbeiten
    Dieser Modus erlaubt eine detaillierte Zugriffskontrolle anhand benutzerdefinierter Zugriffskontrollregeln und bietet die meiste Flexibilität. Allerdings ist dessen initiale Einrichtung etwas komplizierter und aufwändiger, so dass für erste Tests zunächst eine der beiden anderen Zugriffskontrollmodi gewählt werden sollte.

.. index:: Autorisierte Benutzergruppen

.. _Autorisierte Benutzergruppen für Computerzugriff:

Autorisierte Benutzergruppen für Computerzugriff
++++++++++++++++++++++++++++++++++++++++++++++++

Die Konfiguration dieses Zugriffskontrollmodus ist unkompliziert. Die linke Liste beinhaltet alle durch das Datenbackend bereitgestellten Benutzergruppen. Standardmäßig sind dies alle lokalen Benutzergruppen. Wenn die :ref:`LDAP-/AD-Integration <LDAP>` eingerichtet ist, werden alle LDAP-Benutzergruppen angezeigt. Sie können nun eine oder mehrere Gruppen wählen und diese anhand der entsprechenden Schaltfläche zwischen den zwei Listen in die rechte Liste übertragen. Alle Mitglieder jeder Gruppe in der rechten Liste können nun auf den Computer zugreifen. Vergessen Sie nicht, die Konfiguration auf alle Computer zu übertragen.

Über die Schaltfläche :guilabel:`Testen` im Abschnitt :guilabel:`Computerzugriffskontrolle` kann überprüft werden, ob ein bestimmter Benutzer über die eingestellten Gruppen auf einen Computer zugreifen dürfte.

.. _Zugriffskontrollregeln:

Zugriffskontrollregeln
++++++++++++++++++++++

Die Einrichtung eines Regelwerks für die Zugriffskontrolle inkl. Anwendungsszenarien ist im Kapitel :ref:`Regelwerk für Computerzugriff` ausführlich beschrieben.


LDAP
----

Alle Optionen zur Anbindung von Veyon an einen LDAP-kompatiblen Server sind im Kapitel :ref:`LDAP` ausführlich beschrieben.

.. _Platzhaltervariablen:

Platzhaltervariablen für Dateipfade
-----------------------------------

:index:`Platzhaltervariablen` können unter jedem Betriebssystem in beiden unter Windows oder Linux geläufigen Formen ``$VARIABLE`` und ``%VARIABLE%`` verwendet werden.

============= =================
Variable      Expandierter Pfad
============= =================
APPDATA       Benutzerspezifisches Verzeichnis für :index:`Programmdaten` von Veyon, z. B. ``...\Benutzer\Anwendungsdaten\Veyon`` unter Windows oder ``~/.veyon`` unter Linux
HOME, PROFILE :index:`Homeverzeichnis` des angemeldeten Benutzers, z. B. ``C:\Benutzer\Admin`` unter Windows oder ``/home/admin`` unter Linux
GLOBALAPPDATA Systemweites Verzeichnis für Programmdaten von Veyon, z. B. ``C:\ProgramData\Veyon`` unter Windows oder ``/etc/veyon`` unter Linux
TMP, TEMP     Benutzerspezifisches Verzeichnis für :index:`temporäre Dateien`, für den Veyon-Dienst unter Windows wird ``C:\Windows\Temp`` verwendet, unter Linux immer ``/tmp``
============= =================


.. _ServiceArgumente:

Programmargumente für Veyon-Service
-----------------------------------

Abhängig vom Betriebssystem, unter dem Veyon eingesetzt wird, können dem Veyon-Dienst verschiedene :index:`Programmargumente` übergeben werden. Die gewünschten Argumente sind bei den :ref:`allgemeinen Diensteinstellungen <DienstAllgemein>` einzutragen.

====================== ================= =========
Parameter              Betriebssystem    Bedeutung
====================== ================= =========
``-session <ID>``      *<alle>*          Eine Ganzzahl zwischen ``0`` und ``99`` kann als optionale :index:`Session-ID` genutzt werden, um mehrere Instanzen des Veyon-Dienstes in verschiedenen Benutzersitzungen auf dem gleichen Computer zu betreiben. Die Session-ID wird auf die in den :ref:`Netzwerkeinstellungen` konfigurierten Ports addiert, so dass jede Veyon-Dienst-Instanz auf unterschiedlichen Ports arbeitet. Im :ref:`Netzwerkobjektverzeichnis` muss der absolute Port (Primärer Dienst-Port + Session-ID) zusammen mit der Computer-/IP-Adresse angegeben werden, z. B. ``192.168.2.3:11104``.
``<x11vnc-Parameter>`` Linux             Dem Veyon-Dienst können alle vom ``x11vnc``-Programm unterstützten Parameter übergeben werden. Nähere Informationen dazu befinden sich im `x11vnc-Handbuch <http://....>`_.
====================== ================= =========
