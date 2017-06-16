.. _Troubleshooting:

Troubleshooting (Fehleranalyse und -behebung)
=============================================


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
