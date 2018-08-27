.. index:: Troubleshooting, Fehlersuche, Fehleranalyse, Fehlerbehebung

.. _Troubleshooting:

Troubleshooting (Fehleranalyse und -behebung)
=============================================

.. important:: Wenn es zu Problemen im Zusammenspiel von Master- und Client-Computern kommt, sollte zunächst immer sichergestellt werden, dass auf allen Computern eine identische Veyon-Konfiguration eingesetzt wird. Zur Fehlervermeidung ist es dabei generell empfehlenswert, die Konfiguration nicht manuell über den Veyon Configurator zu importieren, sondern diesen Vorgang über die :ref:`Installation <AutoInstall>` oder :ref:`Kommandozeilenschnittstelle` zu automatisieren. Die Konfiguration muss auch bei jeder Änderung im Rahmen der Fehlersuche auf alle betroffenen Computer übertragen werden.


Zugriff auf einen Computer ist nicht möglich
--------------------------------------------

Wenn der Zugriff auf einen Computer über den Veyon Master nicht möglich ist, kann dies mehrere Ursachen haben.

Netzwerkprobleme
++++++++++++++++

Zunächst sollte die grundlegende Erreichbarkeit des Computers über das Netzwerk überprüft werden. Nutzen Sie dafür das üblicherweise jedem Betriebssystem beiliegende Hilfsprogramm ``ping``, um :index:`Verbindungsprobleme` zu diagnostizieren.

Probleme mit dem Veyon-Dienst
+++++++++++++++++++++++++++++

Wenn der Computer anpingbar ist, muss kontrolliert werden, ob der Veyon-Dienst korrekt läuft. Öffnen Sie dazu den Veyon Configurator und öffnen die Konfigurationsseite :ref:`Dienstkonfiguration`. Im Abschnitt :ref:`DienstAllgemein` sollte der Status des Diensts mit dem Wert *Läuft* angezeigt werden. Andernfalls kann der Dienst über die Schaltfläche :guilabel:`Dienst starten` gestartet werden. Ist dies nicht erfolgreich, kann eine Neuinstallation von Veyon Abhilfe schaffen. Ändert auch eine Neuinstallation nichts an der Situation, können Sie in den Logdateien des Veyon-Diensts sowie den Systemmeldungen des Betriebssystem nach Fehlermeldungen und -ursachen suchen. Zusätzlich ergeben sich in der Dienstverwaltung des Betriebssystem ggf. weitere Hinweise oder Einstellmöglichkeiten.

.. index:: telnet, netstat

Dienst- und Firewalleinstellungen
+++++++++++++++++++++++++++++++++

Läuft der Dienst, muss sichergestellt sein, dass er auf dem korrekten Netzwerkport auf eingehende Verbindungen lauscht. Dies kann auf dem lokalen Computer mit Hilfe von ``telnet`` verifiziert werden:

.. code-block:: none

    telnet localhost 11100

Neben allgemeinen Programmausgaben muss die Zeichenkette ``RFB 003.008`` ausgegeben werden. Ist die Ausgabe nicht wie erwartet, sind die :ref:`Netzwerkeinstellungen <Netzwerkeinstellungen>`, speziell der Primäre Dienst-Port, zu überprüfen und ggf. auf ihre Vorgabewerte zurückzustellen.

Im nächsten Schritt muss der gleiche Zugriff auch von einem anderen Computer im Netzwerk aus möglich sein. Auch hier kann ``telnet`` zur Diagnose genutzt werden, wobei das Programmargument ``localhost`` durch den Name oder die IP-Adresse des entsprechenden Computers ersetzt werden muss. Scheitert der Zugriff, muss sichergestellt werden, dass die Option :guilabel:`Nur Verbindungen vom lokalen Computer erlauben` in den :ref:`Netzwerkeinstellungen <Netzwerkeinstellungen>` deaktiviert ist. Auch die :ref:`Computerzugriffskontrolle` sollte zunächst deaktiviert werden, da der Dienst automatisch nur auf ``localhost`` lauscht, wenn aufgrund aktuell zutreffender Regeln der Zugriff von außen ohnehin nicht erlaubt ist. Wenn beide Einstellungen in Ordnung sind, muss aus der Ausgabe von

.. code-block:: none

    netstat -a

ersichtlich sein, dass der Dienst auf Port ``11100`` nicht (nur) auf ``localhost`` bzw. ``127.0.0.1`` lauscht (Status ``LISTEN``, ``ABHÖREN`` o.ä.).

Scheitert der :index:`Portzugriff` von außen weiterhin, verhindert in aller Regel eine :index:`Firewall` den Zugriff und muss entsprechend umkonfiguriert werden. Unter Linux betrifft das die Einstellungen von ``iptables``, ``ufw`` o. ä. Konsultieren Sie hierzu die jeweiligen Handbücher der verwendeten Software. Unter Windows wird die im Betriebssystem integrierte Windows-Firewall von Veyon automatisch konfiguriert, sofern in den :ref:`Netzwerkeinstellungen <Netzwerkeinstellungen>` die Option :guilabel:`Firewall-Ausnahme aktivieren` auf ihren Vorgabewert (*aktiviert*) gestellt ist. Wird eine Firewall-Lösung eines Drittanbieters eingesetzt, muss diese so konfiguriert werden, dass die TCP-Ports 11100 (Primärer Dienst-Port) sowie 11400 (Demoserver) von außen erreichbar sind.

Authentifizierungseinstellungen
+++++++++++++++++++++++++++++++

Eine weitere Fehlerursache können falsche oder unzureichende :ref:`Authentifizierungseinstellungen <Authentifizierung>` sein. Für erste Tests sollte daher (auf beiden Computern!) immer die :ref:`Anmelde-Authentifizierung <AnmeldeAuthentifizierung>` aktiviert und die *Schlüsseldatei-Authentifizierung* deaktiviert sein. Sobald der Test der Anmelde-Authentifizierung am lokalen Computer erfolgreich ist, funktioniert auch der Zugriff von außen.

Wenn die :ref:`Schlüsseldatei-Authentifizierung <SchluesselAuthentifizierung>` eingesetzt wird, muss diese aktiviert werden und die Schlüsseldateien auf Master- und Client-Computer müssen zusammenpassen. Auf dem Client-Computer muss die öffentliche Schlüsseldatei exakt den selben Inhalt wie auf dem Master-Computer haben. Ist der Zugriff dennoch nicht möglich, sind unter Umständen die :index:`Zugriffsrechte` nicht in Ordnung. Der Veyon-Dienst muss :index:`Lesezugriff` auf die *öffentliche Schlüsseldatei* haben, während der Nutzer des Veyon Masters die *private Schlüsseldatei* lesen können muss. Besteht der Fehler weiterhin, müssen die :ref:`Basisverzeichnisse <Basisverzeichnisse>` für die Schlüsseldateien auf allen Computern gelöscht werden und auf dem Master-Computer ein neues Schlüsselpaar erstellt werden. Anschließend muss der öffentliche Schlüssel auf allen Client-Computern erneut importiert werden.

Einstellungen für die Computerzugriffskontrolle
+++++++++++++++++++++++++++++++++++++++++++++++

Auch eine fehlerhafte Konfiguration der Computerzugriffskontrolle kann dazu führen, dass auf einen Computer nicht zugegriffen werden kann. Im ersten Schritt empfiehlt es sich, über den Veyon Configurator die :ref:`Computerzugriffskontrolle` komplett zu deaktivieren. Nun kann festgestellt werden, welche der eingestellten Methoden für die Computerzugriffskontrolle evtl. fehlerhaft konfiguriert ist.

Werden :ref:`Autorisierte Benutzergruppen für Computerzugriff` eingesetzt, muss überprüft werden, ob die Liste der autorisierten Benutzergruppen vollständig ist und der zugreifende Benutzer Mitglied in einer der Benutzergruppen ist.

Die :ref:`Zugriffskontrollregeln` können ebenfalls Ursache dafür sein, dass ein Computerzugriff nicht möglich ist. So muss es in jedem Fall mindestens eine Regel geben, über die der Zugriff unter bestimmten Bedingungen erlaubt wird. Wenn dies sichergestellt ist, kann zur weiteren Fehlersuche eine Regel am Ende der Liste eingefügt werden, bei der die Option :guilabel:`Regel immer verarbeiten und Bedingungen ignorieren` aktiviert und die Aktion :guilabel:`Zugriff erlauben` ausgewählt ist. Diese Regel kann dann schrittweise so lange in der Regelliste nach oben verschoben werden, bis der Zugriff funktioniert bzw. der Test die gewünschten positiven Ergebnisse liefert. Die unterhalb der Testregel befindliche Zugriffsregel ist dann Ursache für die Zugriffsverweigerung und kann näher untersucht und entsprechend korrigiert werden.


Einstellungen werden nicht korrekt gespeichert/geladen
------------------------------------------------------

Nach dem Update von frühen Beta-Versionen von Veyon 4 kann es vorkommen, dass einige Konfigurationsschlüssel inkonsistent sind und neu erstellt werden müssen. Dies kann sich darin äußern, dass Einstellungen nicht korrekt gespeichert bzw. wieder geladen werden, beispielsweise lokale Raum- und Computerinformationen. In diesem Fall sollte die :ref:`Konfiguration vollständig zurückgesetzt <ConfigClear>` und auf Basis der Vorgabewerte neu erstellt werden.


Räume und Computer aus LDAP-Verzeichnis werden im Master nicht angezeigt
------------------------------------------------------------------------

Stellen Sie sicher, dass:

* in der Konfigurationsseite :guilabel:`Allgemein` das :ref:`Netzwerkobjektverzeichnis` auf den Wert *LDAP* eingestellt ist
* die LDAP-Integrationstest :guilabel:`Alle Mitglieder eines Computerraums auflisten` sowie :guilabel:`Alle Computerräume auflisten` erfolgreich sind und Objekte zurückgeben
* in der Konfigurationsseite :guilabel:`Master` die Optionen zur Feineinstellung des Verhaltens auf ihren Vorgabewerten eingestellt sind


Der automatische Wechsel zum aktuellen Raum funktioniert nicht
--------------------------------------------------------------

Wenn die :ref:`Option zum automatischen Wechsel zum aktuellem Raum <RoomAutoSwitch>` aktiviert ist, beim Start des Veyon Masters aber keine Wirkung zeigt, sollte zunächst sichergestellt werden, dass der Master-Computer auch im :ref:`Netzwerkobjektverzeichnis` für den jeweiligen Raum als Computer hinterlegt ist. Unabhängig davon kann der Master-Computer über die Option :ref:`Lokalen Computer in Computerraumverwaltung ausblenden <AutoHideLocalComputer>` in der Computerraumverwaltung ausgeblendet werden.

Sind alle Einträge im Netzwerkobjektverzeichnis korrekt, liegt in aller Regel ein Problem mit der DNS-Konfiguration im Netzwerk vor. Stellen Sie sicher, dass sowohl Computernamen in IP-Adressen als auch IP-Adressen zurück in Computernamen aufgelöst werden können. Unter den meisten Betriebssystemen steht hierfür das Diagnosewerkzeug ``nslookup`` zur Verfügung. Der Aufruf des Programms mit dem lokalen Computername als Argument muss eine gültige IP-Adresse zurückliefern. Ein zweiter Aufruf mit der ermittelten IP-Adresse muss wiederum den Computername zurückgeben.

Arbeitet die Funktion trotz korrektem DNS-Setup nicht wie gewünscht, kann im zweiten Schritt der :ref:`Loglevel <Loglevel>` auf den höchsten Wert (*Debug*) gesetzt werden und in der Logdatei ``VeyonMaster.log`` im :ref:`Logdateiverzeichnis <Logdateiverzeichnis>` nach Fehlerursachen gesucht werden. Hierbei geben die Meldungen *"initializing rooms"* sowie *"found local rooms"* Aufschluss über mögliche Probleme.


Bildschirmsperre kann über Strg+Alt+Entf (Ctrl+Alt-Del) umgangen werden
-----------------------------------------------------------------------

Damit sämtliche Tastatureingaben und Tastenkombinationen im Modus Bildschirmsperre vollständig blockiert werden, ist nach der Veyon-Installation unter Windows ein Neustart des Computers erforderlich. Ohne Neustart ist der Veyon-spezifische Treiber für Eingabegeräte noch nicht aktiv und Tastatureingaben können somit noch nicht abgefangen werden.


Im Demo-Modus wird auf Client-Computern nur ein schwarzer Bildschirm oder ein schwarzes Fenster angezeigt
---------------------------------------------------------------------------------------------------------

Stellen Sie sicher, dass

* in der Konfigurationsseite :guilabel:`Dienst` unter den :ref:`Netzwerkeinstellungen` der Demoserver-Port auf dem Vorgabewert ``11400`` eingestellt ist
* in der Konfigurationsseite :guilabel:`Dienst` die Firewall-Ausnahmen auf dem Master-Computer aktiviert sind bzw. eine Drittanbieter-Firewall so konfiguriert ist, dass eingehende Verbindungen auf TCP-Port ``11400`` möglich sind
* der Benutzer des Veyon Masters Zugriff auf den eigenen Computer (d. h. den lokalen Veyon-Dienst) hat. In einem Zugriffsregelwerk verbietet u. U. eine Regel den Zugriff auf einen Computer, wenn ein Lehrer angemeldet ist. In diesem Fall sollte eine möglichst weit am Anfang angeordnete Regel mit der aktivierten Bedingung *Zugreifender Computer ist localhost* erstellt werden, die den Zugriff erlaubt. Andernfalls kann der Demoserer nicht auf den Bildschirminhalt des Lehrer-PCs zugreifen und an die Client-Computer verteilen.

Der Server stürzt mit XIO- oder XCB-Fehlern unter Linux ab
----------------------------------------------------------

Es gibt bekannte Probleme mit bestimmten Versionen von KDE und Qt unter Linux, die den Veyon-Server zum Absturz bringen. Das betrifft ebenso verschiedene andere VNC-Server-Implementierungen. Wenn Sie von solchen Abstürzen betroffen sind, wird empfohlen, KDE/Qt zu aktualisieren. Als letzte Notlösung können Sie die X-Damage-Erweiterung in der VNC-Server-Konfiguration deaktivieren. Dies hat jedoch negative Auswirkungen auf die Gesamtperformance.
