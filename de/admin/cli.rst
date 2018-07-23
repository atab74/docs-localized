.. index:: Kommandozeilenschnittstelle, Kommandozeilenwerkzeug, Kommandozeile

.. _Kommandozeilenschnittstelle:

Kommandozeilenschnittstelle
===========================

Zur Durchführung von administrativen Aufgaben steht neben dem *Veyon Configurator* auch das Kommandozeilenwerkzeug *Veyon Control* zur Verfügung. Das Programm lässt sich über den Befehl ``veyon-ctl`` in der Kommandozeile aufrufen. Befindet sich das Installationsverzeichnis von Veyon nicht in der Umgebungsvariable ``$PATH`` (Linux) bzw. ``%PATH%`` (Windows), muss zunächst in das Installationsverzeichnis gewechselt werden oder das Verzeichnis dem Programmname vorangestellt werden.

Wird das Programm mit dem Argument ``help`` aufgerufen, wird eine Liste mit allen verfügbaren Modulen angezeigt. Diese kann abhängig von den installierten Veyon-Plugins variieren:

.. code-block:: none

    $ veyon-ctl help
    Verfügbare Module:
        authkeys - Befehle zur Verwaltung von Authentifizierungsschlüsseln
        config - Befehle zur Verwaltung der Veyon-Konfiguration
        ldap - Befehle zum Konfigurieren und Testen der LDAP-/AD-Integration
        networkobjects - Befehle zur Verwaltung des eingebauten Netzwerkobjektverzeichnisses
        remoteaccess - Fernansicht oder -Steuerung eines Computers
        service - Befehle zur Konfiguration und Steuerung des Veyon-Diensts
        shell - Befehle für Shellfunktionalitäten

Jedes :index:`Modul` unterstützt den Befehl ``help``, so dass zu jedem Modul eine Liste mit allen verfügbaren Befehlen angezeigt werden kann. Beispielausgabe für das Modul ``config``:

.. code-block:: none

    $ veyon-ctl config help
    Verfügbare Befehle:
        clear - Systemweite Veyon-Konfiguration löschen
        export - Konfiguration in angegebene Datei exportieren
        get - Konfigurationswert für gegebenen Schlüssel lesen und ausgeben
        import - Konfiguration aus angegebener Datei importieren
        list - Alle Konfigurationsschlüssel und -werte auflisten
        set - Angegebenen Wert in angegebenen Konfigurationsschlüssel schreiben
        unset - Angegebenen Konfigurationsschlüssel zurücksetzen (löschen)
        upgrade - Konfiguration von Programm und Plugins aktualisieren und speichern

Bei einigen Modulen kann dem Befehl ``help`` ein :index:`Befehlsname` als weiteres Argument übergeben werden, um spezifische Hilfe zum jeweiligen Befehl zu erhalten:

.. code-block:: none

    $ veyon-ctl remoteaccess help control

    remoteaccess control <host>


Authentifizierungsschlüsselverwaltung
-------------------------------------

Das Modul ``authkeys`` erlaubt die Verwaltung von Authentifizierungsschlüsseln, so dass gängige Operationen wie der Import eines Authentifizierungsschlüssels oder die Zuweisung einer Benutzergruppe einfach automatisiert werden können.

``create <NAME>``
    Dieser Befehl erzeugt ein neues Authentifizierungsschlüsselpaar und speichert den privaten und öffentlichen Schlüssel im konfigurierten Schlüsselverzeichnis. Als Argument muss ein Name für den Schlüssel angegeben werden, der nur auch Buchstaben bestehen darf.

``delete <SCHLÜSSEL>``
    Dieser Befehl löscht den Authentifizierungsschlüssel ``<SCHLÜSSEL>`` aus dem konfigurierten Schlüsselverzeichnis. Bitte beachten Sie, dass ein Schlüssel nicht wiederhergestellt werden kann, sobald er gelöscht wurde.

``export <SCHLÜSSEL> [<DATEI>]``
    Dieser Befehl exportiert den Authentifizierungsschlüssel ``<SCHLÜSSEL>`` nach ``<DATEI>``. Wenn ``<DATEI>`` nicht angegeben wird, wird der Dateiname aus Name und Typ von ``<SCHLÜSSEL>`` abgeleitet.

``extract <SCHLÜSSEL>``
    Dieser Befehl extrahiert den öffentlichen Schlüsselteil aus dem privaten Schlüssel ``<SCHLÜSSEL>`` und speichert ihn als den zugehörigen öffentlichen Schlüssel. Bei der Einrichtung eines weiteren Mastercomputers genügt somit die Übertragung des privaten Schlüssels. Anschließend kann der öffentliche Schlüssel extrahiert werden.

``import <SCHLÜSSEL> [<DATEI>]``
    Dieser Befehl importiert den Authentifizierungsschlüssel ``<SCHLÜSSEL>`` aus ``<DATEI>``. Wenn ``<DATEI>`` nicht angeben wird, wird der Dateiname aus Name und Typ von ``<SCHLÜSSEL>`` abgeleitet.

``list [details]``
    Dieser Befehl listet alle verfügbaren Authentifizierungsschlüssel im konfigurierten Schlüsselverzeichnis auf. Wenn die Option ``details`` angegeben wird, wird stattdessen eine Tabelle mit Schlüsseldetails ausgegeben. Einige Details können fehlen, wenn auf einen Schlüssel nicht zugegriffen werden kann, z.B. aufgrund fehlender Leserechte.

``setaccessgroup <SCHLÜSSEL> <ZUGRIFFSGRUPPE>``
    Dieser Befehl passt die Dateizugriffsberechtigungen auf den Schlüssel ``<SCHLÜSSEL>`` so an, dass nur die Benutzergruppe ``<ZUGRIFFSGRUPPE>`` Lesezugriff darauf hat.


.. _Konfigurationsverwaltung:

Konfigurationsverwaltung
------------------------

Mit Hilfe des Moduls ``config`` lässt sich die lokale Veyon-Konfiguration verwalten. Dabei können sowohl die komplette Konfiguration als auch einzelne :index:`Konfigurationsschlüssel` gelesen oder geschrieben werden.

``clear``
    Mit diesem Befehl wird die lokale Konfiguration komplett zurückgesetzt, indem alle Konfigurationsschlüssel gelöscht werden. Dieser Befehl kann genutzt werden, um vor dem Import einer Konfiguration einen definierten Zustand ohne alte Einstellungen herzustellen:

    ``veyon-ctl config clear``

``export``
    Mit diesem Befehl lässt sich die lokale Konfiguration in eine Datei exportieren. Der Name der Zieldatei muss als zusätzlicher Argument angegeben werden:

    ``veyon-ctl config export myconfig.json``

``import``
    Dieser Befehl importiert eine zuvor exportierte Konfigurationsdatei in die lokale Konfiguration. Der Name der zu importierenden Konfigurationsdatei muss als zusätzliches Argument angegeben werden:

    ``veyon-ctl config import myconfig.json``

``list``
    Eine Liste aller Konfigurationsschlüssel und den gesetzten Werten kann über diesen Befehl angezeigt werden.

    ``veyon-ctl config list``

    Auf diese Weise lassen sich die Namen der Konfigurationsschlüssel ermitteln, um diese per ``get`` oder ``set`` einzeln zu lesen oder schreiben.

``get``
    Mit diesem Befehl kann ein einzelner Konfigurationsschlüssel ausgelesen werden. Der Name des Schlüssels muss als zusätzliches Argument übergeben werden.

    ``veyon-ctl config get Network/PrimaryServicePort``

``set``
    Mit diesem Befehl kann ein einzelner Konfigurationsschlüssel geschrieben werden. Der Name des Schlüssels sowie der gewünschte Wert müssen als zusätzliche Argumente übergeben werden:

    ``veyon-ctl config set Network/PrimaryServicePort 12345``

    ``veyon-ctl config set Service/Autostart true``

    ``veyon-ctl config set UI/Language de_DE``

``unset``
    Mit diesem Befehl kann ein einzelner Konfigurationsschlüssel gelöscht werden, d.h. Veyon verwendet dann den internen :index:`Vorgabewert`. Der Name des Schlüssels muss als zusätzliches Argument übergeben werden:

    ``veyon-ctl config unset Directories/Screenshots``

``upgrade``
    Mit diesem Befehl kann die Konfiguration von Veyon und allen Plugins aktualisiert und gespeichert werden. Dies kann notwendig sein, wenn sich Einstellungen oder Konfigurationsformate aufgrund von Programm- oder Pluginaktualisierungen geändert haben.


LDAP
----

Die Befehle des Moduls ``ldap`` sind im Kapitel :ref:`LDAP` im Abschnitt :ref:`LDAP-CLI` dokumentiert.


Netzwerkobjektverzeichnis
-------------------------

Wie im Abschnitt :ref:`Raeume und Computer` beschrieben, bietet Veyon ein eingebautes Netzwerkobjektverzeichnis, das genutzt werden kann, wenn kein LDAP-Server zur Verfügung steht. Dieses Netzwerkobjektverzeichnisses kann sowohl grafisch im Veyon Configurator als auch auf der Kommandozeile verwaltet werden. Bestimmte Operationen wie der CSV-Import stehen derzeit sogar ausschließlich auf der Kommandozeile zur Verfügung. Für die meisten Befehle steht eine ausführliche Beschreibung mit Beispielen unter der befehlsspezifischen Hilfe zur Verfügung. Folgende Befehle können im Modul ``networkobjects`` verwendet werden:

``add <TYPE> <NAME> [<HOST ADDRESS> <MAC ADDRESS> <PARENT>]``
    Dieser Befehl fügt ein Objekt hinzu, wobei ``<TYPE>`` ``room`` oder ``computer`` sein kann. ``<PARENT>`` kann als Name oder UUID angegeben werden.

``clear``
    Mit diesem Befehl wird das komplette Netzwerkobjektverzeichnis zurückgesetzt, d.h. alle Räume und Computer werden gelöscht. Diese Operation ist vor allem vor jedem automatisierten Import sinnvoll.

``dump``
    Mit diesem Befehl wird das komplette Netzwerkobjektverzeichnis als flache Tabelle ausgegeben. Jede Eigenschaft wie Objekt-UID, Typ oder Name wird als separate Spalte ausgegeben.

``export <DATEI> [room <RAUM>] [format <FORMAT-STRING-MIT-VARIABLEN>]``
    Mit diesem Befehl kann entweder das komplette Netzwerkobjektverzeichnis oder nur der angegebene Raum in eine Textdatei exportiert werden. Über einen Formatstring und den darin enthaltenen Variablen lässt sich die Formatierung steuern, so dass z.B. eine CSV-Datei erzeugt werden kann. Gültige Variablen sind ``%type%``, ``%name%``, ``%host%``, ``%mac%`` und ``%room%``.

``import <DATEI> [room <RAUM>] [format <FORMATSTRING-MIT-VARIABLEN>] [regex <REGULÄRER-AUSRUCK-MIT-VARIABLEN>]``
    Mit diesem Befehl kann eine Textdatei in das Netzwerkobjektverzeichnis importiert werden. Über einen Formatstring oder einen regulären Ausdruck und den darin enthaltenen Variablen lässt sich die Verarbeitung der Eingabedaten steuern. Auf diese Weise können sowohl CSV-Dateien als auch anderweitig strukturierte Daten eingelesen werden. Gültige Variablen sind ``%name%``, ``%host%``, ``%mac%`` und ``%room%``. In der Befehlshilfe sind verschiedene Beispiele gegeben.

``list``
    Mit diesem Befehl wird das komplette Netzwerkobjektverzeichnis als formatierte Liste ausgegeben. Im Gegensatz zum Befehl ``dump`` wird die Hierarchie von Räumen und Computern durch entsprechende Formatierung wiedergegeben.

``remove <OBJECT>``
	Dieser Befehl entfernt das angegebene Objekt aus dem Verzeichnis. ``<OBJECT>`` kann als Name oder UUID angegeben werden. Wenn ein Raum entfernt wird, werden alle darin befindlichen Computer ebenfalls entfernt.


Fernzugriff
-----------

Das Modul ``remoteaccess`` stellt Funktionen zum grafischen Fernzugriff auf Computer zur Verfügung. Es handelt sich hierbei um die gleichen Funktionen, die auch aus dem Veyon Master heraus erreichbar sind. Die über das Kommandozeilenwerkzeug bereitgestellte Funktion kann beispielsweise genutzt werden, um eine :index:`Programmverknüpfung` für den direkten Zugriff auf einen bestimmten Computer anzulegen.

``control``
    Mit diesem Befehl wird ein Fenster mit der Funktion :index:`Fernsteuerung` geöffnet, mit der ein entfernter Computer gesteuert werden kann. Als Argument muss die Computer- oder IP-Adresse des Computers (sowie optional der TCP-Port) übergeben werden:

    ``veyon-ctl remoteaccess control 192.168.1.2``

``view``
    Mit diesem Befehl wird ein Fenster mit der Funktion :index:`Fernansicht` geöffnet, mit der ein entfernter Computer überwacht werden kann. In diesem Modus wird der Bildschirminhalt in Echtzeit angezeigt, aber es ist keine Interaktion mit dem Computer möglich, solange die entsprechende Schaltfläche in der Werkzeugleiste nicht betätigt wird. Als Argument muss die Computer- oder IP-Adresse des Computers (sowie optional der TCP-Port) übergeben werden:

    ``veyon-ctl remoteaccess view pc5:5900``


Dienststeuerung
---------------

Mit Hilfe des Moduls ``service`` lässt sich der lokale Veyon-Dienst steuern.

``register``
    Mit diesem Befehl wird der Veyon-Dienst im Betriebssystem als Dienst registriert, so dass er beim Hochfahren des Computers automatisch gestartet wird.

    ``veyon-ctl service register``

``unregister``
    Mit diesem Befehl wird die :index:`Dienst-Registrierung` im Betriebssystem entfernt, so dass der Veyon-Dienst beim Hochfahren nicht mehr automatisch gestartet wird.

    ``veyon-ctl service unregister``

``start``
    Mit diesem Befehl wird der Veyon-Dienst gestartet.

    ``veyon-ctl service start``

``stop``
    Mit diesem Befehl wird der Veyon-Dienst beendet.

    ``veyon-ctl service stop``

``restart``
    Mit diesem Befehl wird der Veyon-Dienst neugestartet.

    ``veyon-ctl service restart``

``status``
    Mit diesem Befehl wird der Status des Veyon-Dienst abgefragt und angezeigt.

    ``veyon-ctl service status``


Shell
-----

Einfache Shellfunktionalitäten werden vom Modul ``shell`` bereitgestellt. Wird dieses Modul ohne Angabe weiterer Argumente aufgerufen, wird ein interaktiver Modus gestartet. In diesem Modus können alle CLI-Befehle direkt eingegeben werden können, ohne das Programm ``veyon-ctl`` für jeden Befehl angeben und aufrufen zu müssen. Der Modus kann durch Eingabe des Schlüsselworts ``exit`` verlassen werden.

Weiterhin kann das Modul zur automatisierten Abarbeitung von Befehlen in einer Textdatei genutzt werden, um eine einfache Stapelverarbeitung zu realisieren:

``run <DATEI>``
    Dieser Befehl führt die in der Textdatei angegebenen Befehle zeilenweise aus. Operationen werden unabhängig vom Ergebnis vorangegangener Operationen ausgeführt, d.h. ein Fehler führt nicht zum Abbruch.
