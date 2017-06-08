.. _Installation:

Installation
============

Voraussetzungen
---------------

Veyon ist für den Betrieb auf Standard-Computern unter Windows oder Linux in einem TCP-/IP-kompatiblen Netzwerk ausgelegt. Es gibt keine speziellen Mindestanforderungen an die Hardware. Es muss ein aktuelles vom Hersteller bzw. Community unterstütztes Betriebssystem eingesetzt werden:

* Windows 7, 8 oder 10 (32/64 Bit)
* Linux mit Qt >= 5.6
    * Debian 9
    * Ubuntu 16.04
    * openSUSE 42.2
    * Fedora 24
  
Ein Mischbetrieb zwischen Windows- und Linux-Computern ist problemlos möglich. 


Vorbereitungen
--------------

Laden Sie zunächst die Installationsdateien für Ihre Plattform von der Projekt-Website [#website]_ herunter. Für Windows-Computer wird der Einsatz der 64-Bit-Variante (`win64`) empfohlen. Für 32-Bit-Installationen müssen Sie die 32-Bit-Variante (`win32`) verwenden.

.. [#website] https://github.com/veyon/veyon/releases/

Installation auf einem Windows-Computer
---------------------------------------

Führen Sie die Installationsdatei mit Administratorrechten aus und folgen Sie den Anweisungen auf dem Bildschirm.

Installation auf einem Linux-Computer
-------------------------------------


Automatische Installation (silent installation)
------------------------------------------------


Grundlagen
++++++++++

Der vom Veyon-Projekt bereitgestellte NSIS-Installer kann im Modus *silent* ausgeführt werden, d. h. es es erfolgt keine Nutzerinteraktion und die Installation läuft automatisch ab. Das ist insbesondere für automatisierte Deployments in größeren Umgebungen hilfreich. Veyon lässt sich somit leicht mit allen gängigen Softwareverteilungsmechanismen integrieren.

Indem der Installer mit dem Kommandozeilenparameters "/S" gestartet wird, werden alle Operationen ohne Rückfragen und Ausgaben durchgeführt. Das Gleiche gilt auch für das Deinstallationsprogramm.

Beispiele
+++++++++

Veyon im *silent*-Modus installieren:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S

Veyon im *silent*-Modus deinstallieren:

.. code-block:: none

	C:\Program Files\Veyon\uninstall.exe /S

Installationsverzeichnis bei einer automatischen Installation angeben:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /D=C:\Veyon

.. note:: Aufgrund eines Fehlers in der zugrundeliegenden Installationssoftware (NSIS) muss die Option ``/D=...`` immer als letztes Argument übergeben werden.

Veyon-Konfiguration nach der Installation automatisch anwenden:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /ApplyConfig=%cd%\MyConfig.json
  
.. important:: Sie müssen einen absoluten Pfad für die Konfigurationsdatei angeben, da der intern aufgerufene Veyon Configurator nicht im Installationsverzeichnis als Arbeitsverzeichnis ausgeführt wird. Nutzen Sie daher entweder die vorgeschlagene ``%cd``-Variable oder ersetzen sie mit einem absoluten Pfad.

Automatische Installation ohne Master-Anwendung:

.. code-block:: none

	veyon-x.y.z-win64-setup.exe /S /NoMaster

Sämtliche Veyon-bezogenen Einstellungen während der Deinstallation löschen:

.. code-block:: none

	C:\Program Files\Veyon\uninstall.exe /ClearConfig
