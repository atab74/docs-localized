.. _Installation:

Installation
============

Voraussetzungen
---------------

Veyon ist für den Betrieb auf Standard-Computern unter Windows oder Linux ausgelegt. Es gibt keine speziellen :index:`Mindestanforderungen` an die Hardware. Es muss ein aktuelles vom Hersteller bzw. der Community unterstütztes :index:`Betriebssystem` eingesetzt werden:

* Windows 7, 8 oder 10 (32/64 Bit)
* Linux mit Qt in mindestens Version 5.5
    * Debian 9 oder höher
    * Ubuntu 16.04 oder höher
    * openSUSE 42.2 oder höher
    * Fedora 24 oder höher
    * CentOS 7.3 oder höher

Ein :index:`Mischbetrieb` zwischen Windows- und Linux-Computern ist problemlos möglich. Die Computer müssen über ein TCP-/IP-kompatibles :index:`Netzwerk` verbunden sein, wobei die Übertragungstechnologie (drahtgebunden/kabellos) nur hinsichtlich der erreichbaren Performance eine Rolle spielt. Für den Einsatz von Veyon mit mehr als 10 Computern wird ein Gigabit-Netzwerk empfohlen, da der Demo-Modus (siehe Anwenderhandbuch) andernfalls möglicherweise nicht performant genug arbeitet. Gleiches gilt für kabellose Netzwerke (:index:`WLAN`), so dass mindestens der Funkstandard IEEE 802.11n zum Einsatz kommen sollte.


Vorbereitungen
--------------

Laden Sie zunächst die Installationsdateien für Ihre Plattform von der Veyon-Downloadseite [#releases]_ herunter. Für Windows-Computer wird der Einsatz der 64-Bit-Variante (`win64`) empfohlen. Für 32-Bit-Installationen müssen Sie die 32-Bit-Variante (`win32`) verwenden.

.. [#releases] https://github.com/veyon/veyon/releases/

Installation auf einem Windows-Computer
---------------------------------------

Führen Sie die :index:`Installationsdatei` mit Administratorrechten aus und folgen Sie den Anweisungen auf dem Bildschirm. Auf Computern, auf denen keine Master-Applikation benötigt wird (z. B. Schülerrechner), können Sie im Dialog *Komponenten auswählen* die Komponente *Veyon Master* abwählen.

Nach Abschluss der Installation wird standardmäßig der *Veyon Configurator* gestartet, ein Werkzeug zur Einrichtung und Anpassung Ihrer Veyon-Installation. Im nächsten Kapitel :ref:`Einrichtung` wird die Verwendung ausführlich beschrieben.


Installation auf einem Linux-Computer
-------------------------------------

Die Installation von Veyon unter :index:`Linux` hängt stark von der verwendeten Distribution ab. Üblicherweise können Sie das Programm über die jeweilige Softwareverwaltung installieren, sofern Veyon im Paketarchiv Ihrer Distribution zur Verfügung steht. Andernfalls haben Sie immer die Möglichkeit, eine aktuelle Version von Veyon aus den Quellen zu übersetzen und zu installieren. Weiterführende Informationen finden Sie auf der Github-Projektseite [#github].

.. [#github] https://github.com/veyon/veyon/


.. index:: Automatische Installation, unattended installation, silent installation, Installationsautomatisierung, Deinstallation
.. _AutoInstall:

Automatische Installation (silent installation)
------------------------------------------------

Grundlagen
++++++++++

Die von der Community bereitgestellten Veyon-Windows-Installer können im Modus *silent* ausgeführt werden, d. h. es es erfolgt keine Nutzerinteraktion und die Installation läuft automatisch ab. Das ist insbesondere für automatisierte Deployments in größeren Umgebungen hilfreich. Veyon lässt sich somit leicht mit allen gängigen Softwareverteilungsmechanismen integrieren.

Indem der :index:`Installer` mit dem Kommandozeilenparameters ``/S`` gestartet wird, werden alle Operationen ohne Rückfragen und Ausgaben durchgeführt. Das Gleiche gilt auch für das Deinstallationsprogramm.

Beispiele
+++++++++

Veyon im *silent*-Modus installieren:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S

Veyon im *silent*-Modus deinstallieren:

.. code-block:: none

	C:\Program Files\Veyon\uninstall.exe /S

:index:`Installationsverzeichnis` bei einer automatischen Installation angeben:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /D=C:\Veyon

.. note:: Aufgrund einer Unzulänglichkeit in der verwendeten Installersoftware (NSIS) muss die Option ``/D=...`` immer als letztes Argument übergeben werden.

.. _InstallationKonfigurationsimport:

Veyon-Konfiguration nach der Installation automatisch anwenden:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /ApplyConfig=%cd%\MyConfig.json

.. important:: Sie müssen einen absoluten Pfad für die :index:`Konfigurationsdatei` angeben, da das intern aufgerufene Kommandozeilenwerkzeug (*Veyon Control*) nicht im Installationsverzeichnis als Arbeitsverzeichnis ausgeführt wird. Nutzen Sie daher entweder die vorgeschlagene ``%cd``-Variable oder ersetzen sie mit einem absoluten Pfad.

Automatische Installation ohne Veyon Master:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /NoMaster

Sämtliche Veyon-bezogenen Einstellungen während der Deinstallation löschen:

.. code-block:: none

	C:\Program Files\Veyon\uninstall.exe /ClearConfig
