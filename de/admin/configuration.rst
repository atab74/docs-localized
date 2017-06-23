.. _Einrichtung:

Einrichtung
===========

Um mit der Einrichtung zu beginnen, starten Sie den Veyon Configurator, sofern dies nach Abschluss der Installation nicht schon automatisch erfolgt ist. Mit diesem Programm ist es möglich, eine lokale Veyon-Installation einzurichten und anzupassen. Die grafische Oberfläche ist dabei in verschiedene themen- bzw. komponentenbezogene Konfigurationsseiten untergliedert. Je nach installierten Plugins kann es zusätzliche Konfigurationsseiten geben.

.. image:: images/configurator.png
   :scale: 75 %
   :align: center

In der :ref:`Konfigurationsreferenz` sind alle alle Konfigurationsseiten sowie alle Konfigurationsoptionen mit ihren jeweiligen Bedeutungen beschrieben.


Überblick
---------

Die grundlegenden Einstellungen in der Konfigurationsseite :ref:`Allgemein` betreffen alle :ref:`Komponenten` von Veyon. Dazu zählen Einstellungen zur :ref:`Benutzeroberflaeche`, :ref:`Logaufzeichnung` sowie das :ref:`Netzwerkobjektverzeichnis`, in welchem sich die im Master angezeigten Räume und Computer befinden.

Die Einstellungen in der Konfigurationsseite :ref:`Dienstkonfiguration` beeinflussen die Funktionsweise des Veyon-Diensts (Veyon Service) und dienen dem Finetuning in einigen Sonderfällen. Für einen reibungslosen Betrieb sollten die Einstellungen im Regelfall nicht geändert werden.

Alle Einstellungen in der Konfigurationsseite :ref:`Masterkonfiguration` betreffen ausschließlich das Verhalten und die Funktionen des Veyon Masters und gelten systemweit für alle Benutzer.

.. tip:: Für einen Schnellstart zum Kennenlernen der Software müssen zunächst nur in der Konfigurationsseite :ref:`Authentifizierungskonfiguration` die :ref:`Anmelde-Authentifizierung <AnmeldeAuthentifizierung>` aktiviert und in der Konfigurationsseite :ref:`Lokale Daten` ein Raum sowie einzelne Computer hinzufügt werden. Nachdem die Konfiguration :ref:`auf alle Computer übertragen wurde <ImportExportKonfiguration>`, kann der Veyon Master bereits gestartet und genutzt werden.

.. _Authentifizierung:

Authentifizierung
-----------------

Damit auf einen Computer zugegriffen werden kann, auf dem der Veyon-Dienst läuft, muss sich der zugreifende Benutzer zunächst authentifizieren, d. h. seine Identität bzw. Nutzungsberechtigung nachweisen. Andernfalls wäre ein uneingeschränkter Zugriff von jedem Nutzer auf jeden Computer möglich, auf dem der Veyon-Dienst läuft. Ein Zugriff ohne Authentifizierung ist nicht möglich. Die Einrichtung erfolgt über die Konfigurationsseite :ref:`Authentifizierungskonfiguration` im Veyon Configurator.

.. _Authentifizierungsmethoden:

Authentifizierungsmethoden
++++++++++++++++++++++++++

Grundlegend stehen in Veyon mit der Schlüsseldatei-Authentifizierung sowie der Anmelde-Authentifizierung zwei verschiedene Authentifizierungsmethoden Verfügung, die einzeln oder parallel eingesetzt werden können.

Die **Schlüsseldatei-Authentifizierung** basiert auf einem `Public-Key-Verschlüsselungsverfahren <https://de.wikipedia.org/wiki/Public-Key-Verschl%C3%BCsselungsverfahren>`_, d. h. es kommen ein öffentlich bekannter Schlüssel sowie ein zugehöriger privater Schlüssel zum Einsatz, auf den nur bestimmte Benutzer Zugriff haben dürfen. Bei einer Verbindungsanfrage sendet der Veyon-Dienst eine zufällige Zeichenfolge an den Veyon Master, die dieser mit Hilfe des privaten Schlüssels kryptografisch signieren muss. Die Signatur wird an den Veyon-Dienst zurückgesendet und anhand des öffentlichen Schlüssels überprüft. Diese Überprüfung ist nur dann erfolgreich, wenn die Signatur mit dem passenden privaten Schlüssel erzeugt wird. Die Authentizität des Gegenübers ist dann sichergestellt. Schlägt die Signaturüberprüfung fehl, wird die Verbindung geschlossen.

Bei der **Anmelde-Authentifizierung** sendet der Gegenüber verschlüsselt seinen Benutzername und sein Kennwort an den Veyon-Dienst. Mit diesen Zugangsdaten versucht der Veyon-Dienst anschließend eine Benutzeranmeldung am lokalen System. Schlägt diese fehl, wird die Verbindung geschlossen. Andernfalls sind Benutzername und Kennwort korrekt, so dass die Authentizität des Gegenübers sichergestellt ist.

Beide Methoden haben Vor- und Nachteile, so dass die Wahl der richtigen Methode von der Umgebung, den Sicherheitsanforderungen und den Komfortwünschen abhängt.

.. _SchluesselAuthentifizierung:

**Schlüsseldatei-Authentifizierung**

+-------------------------------------------------+-------------------------------------------------+
| Vorteile                                        | Nachteile                                       |
+=================================================+=================================================+
| * keine Anmeldung mit Benutzername und Passwort | * höherer Aufwand bei der Einrichtung           |
|   beim Start des Veyon Masters notwendig        | * tatsächlicher Benutzer kann auch nach         |
| * Zugriff auf Computer kann über Zugriffsrechte |   erfolgreicher Signaturprüfung nicht           |
|   auf private Schlüsseldatei einfach und        |   zweifelsfrei sichergestellt werden            |
|   zentral gesteuert werden                      | * Systemweiter Austausch von kompromittierten   |
|                                                 |   Schlüsselpaaren notwendig                     |
+-------------------------------------------------+-------------------------------------------------+

.. _AnmeldeAuthentifizierung:

**Anmelde-Authentifizierung**

+-------------------------------------------------+-------------------------------------------------+
| Vorteile                                        | Nachteile                                       |
+=================================================+=================================================+
| * einfache und aufwandsarme Einrichtung         | * Anmeldung mit Benutzername und Passwort bei   |
| * zweifelsfreie Sicherstellung der Identität    |   jeder Verwendung des Veyon Masters notwendig  |
|   des Gegenübers, so dass effektive und sichere |                                                 |
|   Zugriffskontrolle_ möglich ist                |                                                 |
+-------------------------------------------------+-------------------------------------------------+

Die jeweilige Authentifizierungsmethode kann wie in der Konfigurationsreferenz im Abschnitt :ref:`Authentifizierungskonfiguration` beschrieben aktiviert und eingerichtet werden.


Schlüsselverwaltung
+++++++++++++++++++

Um die Schlüsseldatei-Authentifizierung zu nutzen, muss zunächst ein Schlüsselpaar bestehend aus einem privaten und öffentlichen Schlüssel erzeugt werden. Hierfür steht ein entsprechender Assistent zur Verfügung. Starten Sie diesen und folgen den vorgeschlagenen Schritten.

Sobald die Schlüsseldatei-Authentifizierung eingerichtet ist und mit einem Client-Computer funktioniert, können die Schlüssel auch auf einem gemeinsamen Netzlaufwerk abgelegt und die :ref:`Basisverzeichnisse <Basisverzeichnisse>` angepasst werden. Auf den Client-Computern muss dann nur noch die Veyon-Konfiguration importiert werden, während die Schlüsseldateien nicht manuell importiert werden müssen.

.. attention:: Die private Schlüsseldatei darf nur Nutzern zugänglich sein, denen der Zugriff auf andere Computer gestattet sein soll. Wenn die Datei auf einem Netzlaufwerk liegt, muss daher unbedingt darauf geachtet werden, dass der Zugriff per Datei-ACL o. ä. eingeschränkt wird!


.. _Zugriffskontrolle:

Zugriffskontrolle
-----------------

Mit Hilfe des Moduls Zugriffskontrolle kann detailliert festgelegt werden, welche Benutzer auf einen Computer zugreifen dürfen. Die Zugriffskontrolle wird während der Verbindungsinitialisierung nach der Authentifizierung durchgeführt. Während die Authentifizierung die Authentizität eines zugreifenden Benutzers sicherstellt, schränkt die Zugriffskontrollfunktionalität den Computerzugriff auf autorisierte (berechtigte) Benutzer wie beispielsweise Lehrer ein.

Die Einrichtung erfolgt über die Konfigurationsseite :guilabel:`Zugriffskontrolle` und ist in der Konfigurationsreferenz im Abschnitt :ref:`RefZugriffskontrolle` ausführlich beschrieben.

.. important:: Die Konfiguration der Zugriffskontrolle ist wie alle Einstellungen Teil der lokalen Veyon-Konfiguration. Die Konfiguration muss daher :ref:`auf alle anderen Computer übertragen werden <ImportExportKonfiguration>`, um ordnungsgemäß zu funktionieren.


.. _Lokale Daten:

Lokale Daten
------------

In der Konfigurationsseite :guilabel:`Lokale Daten` können die Räume und Computer angelegt werden, die im Veyon Master angezeigt werden. Diese Informationen werden im Gegensatz zu Backends wie LDAP in der lokalen Konfiguration gespeichert und müssen daher auf alle Computer übertragen werden.

Die Konfigurationsseite besteht aus zwei Listen. In der linken Liste sind alle konfigurierten Räume aufgeführt. Über die zwei Schaltflächen unterhalb der Liste können Räume angelegt oder gelöscht werden. Bestehende Räume können per Doppelklick bearbeitet und umbenannt werden.

In der rechten Liste sind alle Computer aufgeführt, die für den aktuell ausgewählten Raum hinterlegt sind. Über die zwei Schaltflächen unterhalb der Liste können Computer angelegt oder gelöscht werden. Die einzelnen Zellen in der Tabelle können per Doppelklick bearbeitet werden. Für jeden Computer muss ein Name sowie eine Computer-/IP-Adresse angegeben werden. Soll die Veyon-Funktion zum Einschalten von Rechnern via `Wake-on-LAN <https://de.wikipedia.org/wiki/Wake_On_LAN>`_ verwendet werden, muss auch die zugehörige MAC-Adresse eingetragen werden. Andernfalls kann diese Spalte leer gelassen werden.


LDAP
----

Alle Informationen rund um die Anbindung von Veyon an einen LDAP-kompatiblen Server wie *OpenLDAP* oder *Active Directory* befinden sich im Kapitel :ref:`LDAP`.


Fehlerbericht
-------------

In der Konfigurationsseite *Fehlerbericht* befindet sich eine Schritt-für-Schritt-Anleitung zur Erstellung eines Fehlerberichts. Diese Informationen können bei Bedarf genutzt werden, um Fehler oder Fehlverhalten an die Entwickler zu übermitteln. Bevor ein Fehlerbericht erstellt wird, sollte allerdings zunächst das Kapitel :ref:`Troubleshooting` konsultiert werden, da es sich beim Problem möglicherweise um einen Konfigurationsfehler handeln kann.


.. _ImportExportKonfiguration:

Import/Export der Konfiguration
-------------------------------

Eine wichtige Voraussetzung für den Einsatz von Veyon ist eine identische Konfiguration auf allen Computern. Eine Übertragung der Veyon-Konfiguration auf einen anderen Computer kann dabei zunächst manuell erfolgen, sollte später aber automatisiert werden. Für beide Wege stehen verschiedene Methoden zur Verfügung.

Im Veyon Configurator befindet sich im Menü :guilabel:`Datei` der Eintrag :guilabel:`Einstellungen in Datei speichern`, über den der Export der aktuellen Konfiguration in eine JSON-Datei möglich ist. Diese Datei kann auf einem anderen Computer im selben Menü über den Eintrag :guilabel:`Einstellungen aus Datei laden` importiert werden. Hierbei ist zu beachten, dass beim Import die Einstellungen in die Benutzeroberfläche geladen werden, aber erst nach Betätigung der Schaltfläche :guilabel:`Anwenden` übernommen und im System gespeichert werden.

Über das Modul :ref:`Konfigurationsverwaltung` der :ref:`Kommandozeilenschnittstelle` können sowohl Konfigurationsimport als auch -export automatisiert/scriptgesteuert durchgeführt werden.

Auch im Rahmen einer :ref:`automatisierten Installation <AutoInstall>` kann die Konfiguration ohne weitere Interaktion übernommen werden. Unter den Beispielen befindet sich auch ein :ref:`Beispiel <InstallationKonfigurationsimport>` für den Installer-Parameter ``/ApplyConfig``.
