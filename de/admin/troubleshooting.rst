.. _Troubleshooting:

Troubleshooting (Fehleranalyse und -behebung)
=============================================

Zugriff auf einen Computer ist nicht möglich
--------------------------------------------

Wenn der Zugriff auf einen Computer über den Veyon Master nicht möglich ist, kann dies mehrere Ursachen haben.

Netzwerkprobleme
++++++++++++++++

Zunächst sollte die grundlegende Erreichbarkeit des Computers über das Netzwerk überprüft werden. Nutzen Sie dafür das üblicherweise jedem Betriebssystem beiliegende Hilfsprogramm ``ping``, um Verbindungsprobleme zu diagnostizieren.

Dienst
++++++

Wenn der Rechner anpingbar ist, muss kontrolliert werden, ob der Veyon-Dienst korrekt läuft. Öffnen Sie dazu den Veyon Configurator und öffnen die Konfigurationsseite :ref:`Dienstkonfiguration`. Im Abschnitt :ref:`DienstAllgemein` wird der Status des Diensts mit dem Wert *Läuft* anzeigen. Andernfalls kann der Dienst über die Schaltfläche :guilabel:`Dienst starten` gestartet werden. Ist dies nicht erfolgreich, kann eine Neuinstallation von Veyon Abhilfe schaffen. Hilft auch eine Neuinstallation nicht, können Sie in den Logdateien des Veyon-Diensts sowie den Systemmeldungen des Betriebssystem nach Fehlermeldungen und -ursachen suchen. Zusätzlich ergeben sich in der Dienstverwaltung des Betriebssystem ggf. weitere Hinweise oder Einstellmöglichkeiten.

Dienst- und Firewalleinstellungen
+++++++++++++++++++++++++++++++++

Läuft der Dienst, sollte sichergestellt werden, dass er auf dem korrekten Netzwerkport auf eingehende Verbindungen lauscht. Dies kann auf dem lokalen Rechner mit Hilfe von ``telnet`` verifiziert werden:

.. code-block:: none

    telnet localhost 11100

Neben allgemeinen Programmausgaben sollte die Zeichenkette ``RFB 003.008`` ausgegeben werden. Ist die Ausgabe nicht wie erwartet, sind die :ref:`Netzwerkeinstellungen`, speziell der Primäre Dienst-Port, zu überprüfen und ggf. auf ihre Vorgabewerte zurückzustellen.

Im nächsten Schritt muss der gleiche Zugriff auch von einem anderen Rechner im Netzwerk aus möglich sein. Auch hier kann ``telnet`` zur Diagnose genutzt werden, wobei das Programmargument ``localhost`` durch den Name oder die IP-Adresse des entsprechenden Computers ersetzt werden muss. Scheitert der Zugriff, sollte sichergestellt werden, dass die Option :guilabel:`Nur Verbindungen vom lokalen Computer erlauben` in den :ref:`Netzwerkeinstellungen` deaktiviert ist. Auch die :ref:`Computerzugriffskontrolle` sollte zunächst deaktiviert werden, da der Dienst automatisch nur auf ``localhost`` lauscht, wenn aufgrund aktuell zutreffender Regeln der Zugriff von außen ohnehin nicht erlaubt ist. Wenn beide Einstellungen in Ordnung sind, muss aus der Ausgabe von

.. code-block:: none

    netstat -a

ersichtlich sein, dass der Dienst auf Port 11100 nicht (nur) auf ``localhost`` bzw. ``127.0.0.1`` lauscht (Status ``LISTEN``, ``ABHÖREN`` o.ä.).

Scheitert der Portzugriff von außen weiterhin, verhindert in aller Regel eine Firewall den Zugriff und muss entsprechend umkonfiguriert werden. Unter Linux betrifft das die Einstellungen von ``iptables``, ``ufw`` o. ä. Konsultieren Sie hierzu die jeweiligen Handbücher der verwendeten Software. Unter Windows wird die im Betriebssystem integrierte Windows Firewall von Veyon automatisch konfiguriert, sofern in den :ref:`Netzwerkeinstellungen` die Option :guilabel:`Firewall-Ausnahme aktivieren` auf ihren Vorgabewert (*aktiviert*) gestellt ist. Wird eine Firewall-Lösung eines Drittanbieters eingesetzt, muss diese so konfiguriert werden, dass die Ports 11100 (Primärer Dienst-Port) sowie 11400 (Demo-Server) von außen erreichbar sind.

Authentifizierungseinstellungen
+++++++++++++++++++++++++++++++

Einstellungen für die Computerzugriffskontrolle
+++++++++++++++++++++++++++++++++++++++++++++++


Räume und Computer aus LDAP-Verzeichnis werden im Master nicht angezeigt
------------------------------------------------------------------------

Stellen Sie sicher, dass:

* in der Konfigurationsseite :guilabel:`Allgemein` das :ref:`Netzwerkobjektverzeichnis` auf den Wert *LDAP* eingestellt ist
* die LDAP-Integrationstest :guilabel:`Alle Mitglieder eines Computerraums auflisten` sowie :guilabel:`Alle Computerräume auflisten` erfolgreich sind und Objekte zurückgeben
* in der Konfigurationsseite :guilabel:`Master` die Optionen zur Feineinstellung des Verhaltens auf ihren Vorgabewerten eingestellt sind


Im Demo-Modus wird auf Client-Computern nur ein schwarzer Bildschirm oder ein schwarzes Fenster angezeigt
---------------------------------------------------------------------------------------------------------

Stellen Sie sicher, dass

* in der Konfigurationsseite :guilabel:`Dienst` die Firewall-Ausnahmen auf dem Master-Computer aktiviert sind
* der Benutzer des Veyon-Masters Zugriff auf den eigenen Computer (d. h. den lokalen Veyon-Dienst) hat. In einem Zugriffsregelwerk verbietet u. U. eine Regel den Zugriff auf einen Computer, wenn ein Lehrer angemeldet ist. In diesem Fall sollte eine möglichst weit am Anfang angeordnete Regel mit der aktivierten Bedingung *Zugreifender Computer ist localhost* erstellt werden, die den Zugriff erlaubt. Andernfalls kann der Veyon-Master nicht auf den Bildschirminhalt des Lehrer-PCs zugreifen und an die Client-Computer verteilen.
