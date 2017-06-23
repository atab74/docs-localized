.. _LDAP:

LDAP/AD-Integration
===================

Dieses Kapitel beschäftigt sich mit der Anbindung von LDAP-kompatiblen Servern an Veyon. Im Folgenden wird nur der Oberbegriff *LDAP* verwendet und meint damit alle LDAP-kompatiblen Produkte bzw. Technologien wie *OpenLDAP*, *Samba* und *Active Directory*. Über die LDAP-Integration ist es möglich, die in den meisten Umgebungen bereits bestehenden Informationen über Benutzer, Benutzergruppen, Computer sowie Räume zu nutzen, anstatt diese manuell in der Veyon-Konfiguration nachzubilden. Zum einen können LDAP-Benutzer und -Benutzergruppen als Datenbasis für die :ref:`Zugriffskontrolle` genutzt werden. Zum anderen kann der Veyon Master die anzuzeigenden Räume und Computer direkt aus dem Verzeichnisdienst laden.

Die Konfiguration der LDAP-Integration erfolgt über die Konfigurationsseite :guilabel:`LDAP` im Veyon Configurator. Diese Seite gliedert sich in verschiedene Unterseiten für :ref:`Grundeinstellungen`, :ref:`Umgebungseinstellungen`, :ref:`Erweiterte Einstellungen` sowie :ref:`Integrationstests`.


.. _Grundeinstellungen:

Grundeinstellungen
------------------

Die Grundeinstellungen betreffen alle grundlegenden Parameter für den Zugriff auf einen LDAP-Server. Sie sind in jedem Fall zwingende Voraussetzung für eine korrekt arbeitende LDAP-Integration.

Allgemein
+++++++++

LDAP-Server und Port
    Hier muss die Adresse des LDAP-Servers (Name oder IP-Adresse) eingetragen werden. Wenn ein anderer Port als der Standard-LDAP-Port 389 zum Einsatz kommt, muss der Port-Parameter entsprechend angepasst werden.

Anonymer Bind / Bind-Zugangsdaten verwenden
    Je nach Umgebung und Konfiguration des LDAP-Servers sind LDAP-Abfragen entweder als anonymer Benutzer oder nur mit Benutzername und Passwort möglich. Wenn der Serverzugriff ein Benutzername und Passwort erfordert, muss die Option :guilabel:`Bind-Zugangsdaten` aktiviert werden und die Zugangsdaten müssen in den zwei folgenden Eingabefeldern eingetragen werden. Andernfalls kann die Vorgabeoption :guilabel:`Anonymer Bind` verwendet werden.

Bind-DN
    Der Bind-DN ist der Benutzername, mit dem eine Anmeldung am Server durchgeführt wird, um anschließend LDAP-Operationen durchzuführen. Das Format hängt allerdings stark vom LDAP-Server und dessen Konfiguration ab. Mögliche Formate sind ``User``, ``DOMAIN\User`` oder ``cn=User,…,dc=example,dc=org``.

Bind-Passwort
    In Verbindung mit dem Bind-DN muss das zugehörige Passwort eingetragen werden.

Über die Schaltfläche :guilabel:`Testen` kann überprüft werden, ob der Serverzugriff mit den eingetragenen Parametern funktioniert.

.. tip:: Veyon führt ausschließlich lesende LDAP-Operationen durch. Es kann daher als zusätzliche Sicherheitsmaßnahme ein dedizierter Benutzer angelegt werden, der nur Lesezugriff auf das LDAP-Verzeichnis hat, z. B. "Veyon-LDAP-RO". Für diesen Benutzer kann ggf. weiterhin der Zugriff auf relevante Attribute eingeschränkt werden.

Base-DN
+++++++

Über den Base-DN wird die grundlegende Basis im Verzeichnis festgelegt, unter der alle zu verwendenden Objekte abgelegt sind. Diese ergibt sich üblicherweise aus der DNS- oder AD-Domäne (siehe auch `RFC 2247 <https://www.ietf.org/rfc/rfc2247.txt>`_).

Wenn ein fester Base-DN zum Einsatz kommt, muss die Vorgabeoption :guilabel:`Fester Base-DN` aktiviert werden und der Base-DN in das Eingabefeld eingetragen werden. Über die Schaltfläche :guilabel:`Testen` kann überprüft werden, ob die Einstellung korrekt ist und Einträge gefunden werden können.

Soll eine generische Veyon-Konfiguration beispielsweise an mehreren Standorten mit unterschiedlichen Base-DNs eingesetzt werden, kann Veyon so konfiguriert werden, dass der Base-DN immer dynamisch über Naming-Contexts abgefragt wird. Hierfür muss die gleichnamige Option aktiviert werden und ggf. das Naming-Context-Attribut angepasst werden. Über die Schaltfläche :guilabel:`Testen` kann überprüft werden, ob ein Base-DN ermittelt werden konnte.

Nach dem Import einer generischen Veyon-Konfiguration ohne festen Base-DN ist es zudem über die :ref:`LDAP-CLI` möglich, den Base-DN zu ermitteln und in die lokale Konfiguration zu schreiben.

.. _Umgebungseinstellungen:

Umgebungseinstellungen
----------------------

Nachdem die Grundeinstellungen konfiguriert und getestet wurden, können nun die umgebungsspezifischen Einstellungen vorgenommen werden. Über diese Einstellungen wird festgelegt, in welchen Bäumen sich Objekte befinden und wie bestimmte Objektattribute heißen. Anhand dieser Parameter kann Veyon alle benötigten Informationen aus dem LDAP-Verzeichnis abfragen.

Objektbäume
+++++++++++

Objektbäume sind Organisations- bzw. Struktureinheiten, in denen bestimmte Typen von Objekten (Benutzer, Gruppen, Computer) abgelegt sind. Die jeweiligen CNs (Common Names) oder OUs (Organizational Units) müssen *ohne Base-DN* in den entsprechenden Eingabefeldern eingetragen werden. Hinter jedem Eingabefeld steht eine Schaltfläche zum Überprüfen des jeweiligen Objektbaums zur Verfügung.


Benutzerbaum
    Hier muss der LDAP-Baum (ohne Base-DN) eingetragen werden, in dem sich die Benutzer(objekte) befinden. Typische Beispiele sind ``OU=Users`` oder ``CN=Users``.

Gruppenbaum
    Hier muss der LDAP-Baum (ohne Base-DN) eingetragen werden, in dem sich die Gruppen(objekte) befinden. Typische Beispiele sind ``OU=Groups` oder ``CN=Groups``.

Computerbaum
    Hier muss der LDAP-Baum (ohne Base-DN) eingetragen werden, in dem sich die Computer(objekte) befinden. Typische Beispiele sind ``OU=Computers`` oder ``CN=Computers``.

.. _Computergruppenbaum:

Computergruppenbaum
    Wenn sich Computergruppen in einem anderen Baum als die regulären (Benutzer-)Gruppen oder in einem Unterbaum befinden, kann der entsprechende LDAP-Baum hier eingetragen werden. Andernfalls wird der Gruppenbaum verwendet, um auch Computergruppen abzufragen und ggf. über einen spezifischen Objektfilter (s.u.) zu filtern.

Rekursive Suchoperationen in Objektbäumen durchführen
    Über diese Option kann gesteuert werden, ob Objekte rekursiv abgefragt werden sollen. Die Suche findet dann nicht nur im festgelegten Baum sondern auch in ggf. vorhandenen Unterbäumen statt.

    Vorgabe: *deaktiviert*


Objektattribute
+++++++++++++++

Damit Veyon den abgefragten Objekten die benötigten Informationen entnehmen kann, müssen die Namen einiger Objektattribute konfiguriert werden, da sich diese je nach Umgebung und LDAP-Server zum Teil erheblich unterscheiden. Hinter jedem Eingabefeld steht eine Schaltfläche zum Überprüfen des jeweiligen Attributnamens zur Verfügung.

Attribut Benutzerlogin
    Dieses Attribut muss den Anmeldenamen eines Benutzers enthalten. Das Attribut wird verwendet, um das LDAP-Benutzerobjekt zu ermitteln, das zu einem angemeldeten Benutzer gehört. Im OpenLDAP-Umfeld kommt oft der Attributname ``uid`` zum Einsatz, während bei Active Directory der Name ``sAMAccountName`` üblich ist.

Attribut Gruppenmitglieder
    Über dieses Attribut werden in Gruppenobjekten die Gruppenmitglieder aufgeführt. Das Attribut wird verwendet, um die Gruppen zu ermitteln, in denen ein Benutzer Mitglied ist. Je nach Konfiguration wird das Attribut auch für die Zuordnung von Computern zu Räumen genutzt. Im OpenLDAP-Umfeld kommt oft der Attributname ``member`` zum Einsatz, während bei Active Directory der Name ``memberUid`` üblich ist.

Attribut Computername
    Hier muss der Name eines Attributs eingetragen werden, in dem der DNS-Name des Computers gespeichert ist. Das Attribut wird verwendet, um das LDAP-Computerobjekt zu ermitteln, das zu einem bestimmten Computername (Hostname) gehört. Im OpenLDAP-Umfeld kommt oft der Attributname ``name`` zum Einsatz, während bei Active Directory der Name ``dNSHostName`` üblich ist.

Computernamen sind als vollqualifizierte Domainnamen gespeichert
    Diese Option legt fest, ob für die Zuordnung von Computernamen zu LDAP-Computerobjekten der `vollqualifizierte Domainname (FQDN) <https://de.wikipedia.org/wiki/Fully-Qualified_Host_Name>`_ verwendet werden soll. Wenn die Computernamen im LDAP-Verzeichnis ohne Domain-Anteil gespeichert sind, muss diese Option deaktiviert, andernfalls aktiviert werden.
    
    Vorgabe: *deaktiviert*

Attribut Computer-MAC-Adresse
    Zusätzlich zum Computername sind in einigen Umgebungen auch die MAC-Adressen von Computern im LDAP-Verzeichnis hinterlegt, wenn beispielsweise der DHCP-Server ebenfalls auf das LDAP-Verzeichnis zugreift. Soll die Veyon-Funktion zum Einschalten von Rechnern via `Wake-on-LAN <https://de.wikipedia.org/wiki/Wake_On_LAN>`_ verwendet werden, muss hier der entsprechende Attributname eingetragen werden, da die MAC-Adresse für diese Funktion benötigt wird. Typische Beispiele sind ``hwAddress`` oder ``dhcpAddress``.

.. _Erweiterte Einstellungen:

Erweiterte Einstellungen
------------------------

Mit den erweiterten Einstellungen kann die LDAP-Integration und die Verwendung der Informationen aus dem LDAP-Verzeichnis an individuelle Bedürfnisse angepasst werden.

Optionale Objektfilter
++++++++++++++++++++++

Mit Hilfe von LDAP-Filtern können die von Veyon verwendeten LDAP-Objekte eingeschränkt werden, wenn beispielsweise Computerobjekte wie Drucker im Veyon Master nicht angezeigt werden sollen. Hinter jedem Eingabefeld steht eine Schaltfläche zum Überprüfen des jeweiligen Attributnamens zur Verfügung.

.. important:: Die optionalen Filter folgen dem üblichen Schema für LDAP-Filter (siehe z. B. `RFC 2254 <https://www.ietf.org/rfc/rfc2254.txt>`_ oder `Active Directory: LDAP Syntax Filters <https://social.technet.microsoft.com/wiki/contents/articles/5392.active-directory-ldap-syntax-filters.aspx>`_), allerdings mit der Besonderheit, dass äußere Klammern nicht mit angegeben werden dürfen. Beispielsweise muss ein einfacher objectClass-Filter als ``objectClass=XYZ`` und nicht ``(objectClass=XYZ)`` definiert werden.
 
Filter für Benutzer
    Hier kann ein LDAP-Filter für Benutzer eingetragen werden, z. B. ``objectClass=person`` oder ``&(objectClass=person)(objectClass=veyonUser)``.

Filter für Benutzergruppen
    Hier kann ein LDAP-Filter für Benutzergruppen eingetragen werden, z. B. ``objectClass=group`` oder ``|(cn=teachers)(cn=students)(cn=admins)``.

Filter für Computer
    Hier kann ein LDAP-Filter für Computer eingetragen werden, z. B. ``objectClass=computer`` oder ``&(!(cn=printer*))(!(cn=scanner*))``.

.. _Computergruppenfilter:

Filter für Computergruppen
    Hier kann ein LDAP-Filter für Computergruppen eingetragen werden, z. B. ``objectClass=room`` oder ``cn=Raum*``.


Identifizierung von Gruppenmitgliedern
++++++++++++++++++++++++++++++++++++++

Der Inhalt der Gruppenmitgliedsattribute unterscheidet sich in verschiedenen LDAP-Implementierungen. Während im Active Directory der Distinguished Name (DN) eines Objekts im member-Attribut hinterlegt ist, wird bei OpenLDAP meist der Anmeldename eines Benutzers (``uid`` o. ä.) oder der Computername gespeichert. Damit Veyon für die Abfrage von Gruppen eines Benutzers oder Computers den richtigen Wert verwendet, muss hier die passende Einstellung gewählt werden.

Distinguished name (Samba/AD)
    Diese Option muss gewählt werden, wenn im member-Attribut einer Gruppe der Distinguished Name (DN) eines Objekts gespeichert wird. Üblicherweise arbeiten Samba- oder AD-Server nach diesem Schema.

Konfiguriertes Attribut für Benutzer-Login oder Computername (OpenLDAP)
    Diese Option muss gewählt werden, wenn im member-Attribut einer Gruppe der Benutzer-Anmeldename oder Computername hinterlegt ist. Üblicherweise arbeiten OpenLDAP-Server nach diesem Schema.


Computerräume
+++++++++++++

Computerräume können auf zwei verschiedenen Wegen über ein LDAP-Verzeichnis abgebildet werden. Im einfacheren Fall gibt es für jeden Computerraum eine Computergruppe, in denen alle Computer des Raums Mitglied sind. Bei dieser Vorgehensweise ist keine Anpassung des LDAP-Schemas notwendig. Alternativ kann auch der Raumname als spezielles Attribut in jedem Computerobjekt hinterlegt sein.

Dedizierte Computergruppen
    Mit dieser Option wird festgelegt, dass Computerräume über Computergruppen abgebildet werden. Sämtliche Computergruppen werden dann im Veyon Master als Räume angezeigt. In jedem Raum werden alle Computer angezeigt, die Mitglied der jeweiligen Gruppe sind. Wenn alle nicht LDAP-Gruppen als Räume angezeigt werden sollen, muss entweder ein dedizierter Computergruppenbaum_ konfiguriert werden oder die Computergruppen über einen Computergruppenfilter_ eingeschränkt werden.

    Vorgabe: *aktiviert*

Gemeinsames Attribut
    Wenn das LDAP-Schema für Computerobjekte ein spezielles Attribut für die Zuordnung zu einem Raum vorsieht, kann diese Option aktiviert und der Attributname eingetragen werden. Über die Schaltfläche :guilabel:`Testen` kann überprüft werden, ob die Mitglieder eines Computerraums anhand des konfigurierten Attributs korrekt abgefragt werden können.
    
    Vorgabe: *deaktiviert*


.. _Integrationstests:

Integrationstests
-----------------

Mit Hilfe der Integrationstests kann die LDAP-Integration als Ganzes überprüft werden. Über die Schaltflächen können verschiedene Tests durchgeführt werden. Alle Tests sollten erfolgreich sein und gültige Ergebnisse liefern.


Verwendung von LDAP-Backends
----------------------------

Mit der erfolgreichen Konfiguration der LDAP-Integration können nun die LDAP-Backends aktiviert werden. Hierfür müssen das :ref:`Netzwerkobjektverzeichnis` sowie das Datenbankend für die :ref:`Computerzugriffskontrolle` angepasst werden. Erst mit der Umstellung des Netzwerkobjektverzeichnisses auf *LDAP* werden im Veyon Master die Raum- und Computerinformationen aus dem LDAP-Verzeichnis verwendet.

.. attention:: Nach Umstellung des Datenbankends für die Computerzugriffskontrolle sollten die konfigurierten Zugriffsregeln unbedingt überprüft werden, da sich die Gruppen- und Rauminformationen ändern und somit die Zugriffsregeln in den meisten Fällen nicht mehr gültig sind oder nicht mehr korrekt verarbeitet werden.

.. _LDAP-CLI:

Kommandozeilenschnittstelle
---------------------------

Über die :ref:`Kommandozeilenschnittstelle` von Veyon sind einige LDAP-spezifischen Operationen möglich. Alle Operationen stehen im Modul ``ldap`` zur Verfügung. Eine Liste aller unterstützen Befehle wird über ``veyon-ctl ldap help`` ausgegeben, während befehlsspezifische Hilfetexte über ``veyon-ctl ldap help <Befehl>`` angezeigt werden können.

``autoconfigurebasedn``
    Mit diesem Befehl kann der verwendete Base-DN automatisch ermittelt und in die Konfiguration fest eingetragen werden. Als Argumente müssen eine LDAP-Server-URL sowie optional ein Naming-Context-Attribut angegeben werden:

    ``veyon-ctl ldap autoconfigurebasedn ldap://192.168.1.2/ namingContexts``

    ``veyon-ctl ldap autoconfigurebasedn ldap://Administrator:MYPASSWORD@192.168.1.2:389/``

``query``
    Dieser Befehl erlaubt die Abfrage von LDAP-Objekten (``rooms``, ``computers``, ``groups``, ``users``) und dient in erster Linie der Fehlersuche. Die Funktion kann aber auch für die Entwicklung von Scripten für die Systemintegration hilfreich sein.

    ``veyon-ctl ldap query users``

    ``veyon-ctl ldap query computers``
