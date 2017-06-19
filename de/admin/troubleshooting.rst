.. _Troubleshooting:

Troubleshooting (Fehleranalyse und -behebung)
=============================================

Zugriff auf einen Computer ist nicht möglich
--------------------------------------------

Wenn der Zugriff auf einen Computer über den Veyon Master nicht möglich ist, kann dies mehrere Ursachen haben.

Zunächst sollte die grundlegende Erreichbarkeit des Computers über das Netzwerk überprüft werden. Nutzen Sie dafür das üblicherweise jedem Betriebssystem beiliegende Hilfsprogramm ``ping``.

Wenn der Rechner anpingbar ist, muss kontrolliert werden, ob der Veyon-Dienst korrekt läuft. Öffnen Sie dazu den Veyon Configurator und öffnen die Konfigurationsseite :guilabel:`Dienst`. Im Abschnitt :guilabel:`Allgemein` wird der Status des Diensts mit dem Wert *Läuft* anzeigen. Andernfalls kann der Dienst über die Schaltfläche :guilabel:`Dienst starten` gestartet werden. Ist dies nicht erfolgreich, kann eine Neuinstallation von Veyon Abhilfe schaffen. Hilft auch eine Neuinstallation nicht, können Sie in den Logdateien des Veyon-Diensts sowie den Systemmeldungen des Betriebssystem nach Fehlermeldungen und -ursachen suchen.

Läuft der Dienst, sollte sichergestellt werden, dass er auf dem korrekten Netzwerkport auf eingehende Verbindungen lauscht. Hierzu sind die :ref:`Netzwerkeinstellungen`, speziell der Primären Dienst-Port, zu überprüfen und ggf. auf ihre Vorgabewerte zurückzustellen.


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
