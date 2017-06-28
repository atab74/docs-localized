.. _FAQ:

FAQ - Häufig gestellte Fragen
=============================

.. index:: iTALC

Wie kann ich eine bestehende iTALC-Installation zu Veyon migrieren?
-------------------------------------------------------------------

Ist es möglich, den Veyon Master auf mehreren Computern zu verwenden?
---------------------------------------------------------------------

Kann ich eine selber generierte Datei mit Raum- und Computerinformationen importieren/verwenden?
------------------------------------------------------------------------------------------------

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
