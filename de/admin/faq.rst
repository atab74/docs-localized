.. _FAQ:

FAQ - Häufig gestellte Fragen
=============================

Funktioniert Veyon unter Chrome OS (ChromeBooks) oder macOS?
------------------------------------------------------------

Derzeit ist Veyon ausschließlich für Linux- oder Windows-basierte Umgebungen verfügbar. Die Weiterentwicklung ist aber u. a. darauf ausgerichtet, Veyon auf weitere Plattformen zu portieren und entsprechende Installationsdateien bereitzustellen. Hierbei ist das Veyon-Projekt auf Mithilfe von erfahrenen Software-Entwicklern angewiesen, insbesondere für die Portierung auf macOS und Android.

Wie kann ich Computer hinzufügen, so dass ich darauf zugreifen kann?
--------------------------------------------------------------------

Wenn das voreingestellte :ref:`Netzwerkobjektverzeichnis` verwendet wird, müssen lediglich auf der Konfigurationsseite :ref:`Lokale Daten` die entsprechenden Räume angelegt und Computer hinzugefügt werden. Anschließend stehen diese im Veyon Master zur Verfügung.

Ist die :ref:`LDAP-/AD-Integration <LDAP>` eingerichtet, muss das Netzwerkobjektverzeichnis ebenfalls noch auf LDAP umgestellt werden, damit die Computer aus dem Verzeichnis im Veyon Master angezeigt werden.

.. index:: iTALC

Wie kann ich eine bestehende iTALC-Installation zu Veyon migrieren?
-------------------------------------------------------------------

Auch wenn sich iTALC und Veyon konzeptuell wenig unterscheiden, ist für den Einsatz von Veyon eine komplette Neuinstallation und Einrichtung notwendig, da sich Konfigurations- und Dateiformate sowie deren Speicherorte geändert haben und nicht kompatibel sind. Für eine Migration muss iTALC daher zunächst vollständig deinstalliert werden. Es wird empfohlen, danach einen Neustart des Computers durchzuführen. Anschließend kann Veyon installiert und analog zu iTALC eingerichtet werden.

Während die Einrichtung der Authentifizierungsmethoden sehr ähnlich ist, erfolgt die Konfiguration von Räumen und Computern über den Veyon Configurator und nicht mehr im Master. In diesem Zusammenhang sollte überprüft werden, ob die neue :ref:`LDAP-/AD-Integration <LDAP>` genutzt werden kann, um Räume und Computer automatisch in Veyon verfügbar zu machen.

Ist es möglich, den Veyon Master auf mehreren Computern zu verwenden?
---------------------------------------------------------------------

Der Einsatz von Veyon Master auf mehreren Computern ist problemlos möglich. Hierzu muss wie auch bei den Client-Computern sichergestellt werden, dass die identische Konfiguration auf allen Master-Computern zum Einsatz kommt. Wird die Anmelde-Authentifizierung genutzt, sind keine weiteren Schritte notwendig. Für die Schlüssel-Authentifizierung muss der private Schlüssel auf alle Master-Computer verteilt werden.

Wie kann ein bestehender VNC-Server gemeinsam mit Veyon verwendet werden?
-------------------------------------------------------------------------

In einigen Umgebungen ist bereits ein VNC-Server installiert (z. B. UltraVNC) oder wird systemseitig bereitgestellt (z. B. VNC-basierter Zugriff auf virtuelle Desktops in VDI-Umgebungen). Hier kann es unter Umständen zu Performanceeinbußen oder Konflikten mit dem Veyon-internen VNC-Server kommen. In solchen Fällen wird empfohlen, Veyon so einzurichten, dass der bestehende (externe) VNC-Server mitbenutzt wird, anstatt den internen VNC-Server zu starten. Die Konfiguration erfolgt im Veyon Configurator in der Konfigurationsseite :ref:`Dienstkonfiguration` im Abschnitt :ref:`VNCServer`.

Kann ich eine selber generierte Datei mit Raum- und Computerinformationen importieren/verwenden?
------------------------------------------------------------------------------------------------

Mit Veyon 4.0 ist dies leider noch nicht möglich, allerdings wird es in Veyon 4.1 eine Importmöglichkeit sowie eine Kommandozeilenschnittstelle zur Raum- und Computerverwaltung geben.

Wie kann ich die Auswahl der angezeigten Computer exportieren/importieren?
--------------------------------------------------------------------------

Die Auswahl der angezeigten Computer wird in der persönlichen :ref:`Benutzerkonfiguration <Benutzerkonfiguration>` gespeichert. Soll diese für mehrere Benutzer verwendet werden, gibt es prinzipiell zwei Vorgehensweisen. Zum einen kann die Benutzerkonfigurationsdatei z. B. durch Anmeldescripte in das jeweilige Profil des Benutzers kopiert werden. Alternativ kann die Benutzerkonfiguration auch in einem gemeinsam verwendeten Verzeichnis (z. B. Netzlaufwerk) abgelegt werden und die :ref:`Einstellung <Benutzerkonfiguration>` dahingehend geändert werden, dass die Benutzerkonfiguration aus diesem Verzeichnis geladen wird. Hierbei ist zu beachten, dass die Zugriffsrechte ggf. angepasst werden müssen, damit Änderungen durch die Benutzer nicht in die globale Benutzerkonfiguration zurückgeschrieben werden.

In diesem Zusammenhang sei auch auf die Funktion zum :ref:`Automatischen Wechsel in den aktuellen Klassenraum <RoomAutoSwitch>` verwiesen, über die sich das eigentlich gewünschte Verhalten u. U. direkt realisieren lässt.


Wie kann ich den Master-Computer in der Computerraumverwaltung ausblenden?
---------------------------------------------------------------------------

Hierfür muss lediglich die Option :ref:`Lokalen Computer in Computerraumverwaltung ausblenden <AutoHideLocalComputer>` aktiviert werden.


Was passiert, wenn keine Zugriffskontrollregel zutrifft?
--------------------------------------------------------

Wenn es bei der Abarbeitung der eingestellten Zugriffskontrollregeln keine Regel gibt, bei der alle aktivierten Bedingungen zutreffen, wird der Zugriff verweigert und die Verbindung geschlossen. Damit wird verhindert, dass einem Angreifer der Zugriff aufgrund eines unvollständigen Regelwerks aus Versehen erlaubt wird.
