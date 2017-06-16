.. _Regelwerk für Computerzugriff:

Regelwerk für Computerzugriff
=============================

Einführung
----------

Wenn eine detaillierte Kontrolle darüber benötigt wird, welcher Benutzer unter bestimmten Umständen auf bestimmte Computer zugreifen darf, kann dies mit Hilfe von Zugriffskontrollregeln realisiert werden. Im Folgenden wird der Begriff *Regel* als Synonym für *Zugriffskontrollregel* verwendet.

Wenn ein Benutzer versucht, auf einen Computer zuzugreifen, werden die definierten Zugriffskontrollregeln nacheinander abgearbeitet bis alle Bedingungen einer Regel zutreffen. Sobald alle aktivierten Bedingungen einer Regel zutreffen, werden keine weiteren Regeln abgearbeitet und die hinterlegte Aktion wird ausgeführt (Ausnahme: Regel ist deaktiviert).

Die Regeln können über den Veyon Configurator in der Konfigurationsseite :ref:`Zugriffskontrolle` im Abschnitt :guilabel:`Zugriffskontrollregeln` eingerichtet werden. Standardmäßig ist die Regelliste leer. In diesem Fall werden alle Zugriffsversuche verweigert, da es keine Regel gibt, die den Zugriff explizit erlaubt. Das bedeutet, dass mindestens eine Regel definiert werden muss, die den Zugriff unter bestimmten Bedingungen erlaubt.


Regeln hinzufügen und bearbeiten
--------------------------------

Nach Betätigung der Schaltfläche :guilabel:`+` öffnet sich ein Dialog, der die Erstellung einer neuen Regeln ermöglicht. Bestehende Regeln können mit einem Doppelklick oder der Schaltfläche mit dem Stiftsymbol geöffnet und bearbeitet werden.

Eine Regel besteht prinzipiell aus allgemeinen Einstellungen, Bedingungen und einer Aktion, die ausgeführt wird, wenn alle Bedingungen zutreffen. Der Dialog gliedert sich entsprechend in drei Bereiche. Im Folgenden werden die Bedeutungen der einzelnen Optionen in den verschiedenen Dialogbereichen erläutert.

Allgemein
+++++++++

Im Eingabefeld :guilabel:`Regelname` sollte zunächst ein Name für die Regel vergegeben werden, über den die Regel später identifiziert und der in der Regelliste angezeigt wird. Zu Dokumentationszwecken kann eine optionale Beschreibung im Eingabefeld :guilabel:`Regelbeschreibung` ergänzt werden.

Die Option :guilabel:`Regel immer verarbeiten und Bedingungen ignorieren` bewirkt, dass für die Regelverarbeitung die weiter unten eingestellten Bedingungen nicht überprüft werden und die eingestellte Aktion immer ausgeführt wird. Das ist vor allem für Fallback-Regeln am Ende der Regelliste hilfreich, um bei Bedarf einzustellen, dass der angemeldete Benutzer um Erlaubnis gefragt wird, wenn sonst keine Regel greift.

Über die Option :guilabel:`Alle Bedingungen umkehren` kann festgelegt werden, dass alle aktivierten Bedingungen invertiert ausgewertet werden, d. h. aktivierte Bedingungen dürfen nicht zutreffen. Wenn beispielsweise die Bedingung *Kein Benutzer angemeldet* aktiviert ist, greift die Regel nur, wenn ein oder mehrere Benutzer angemeldet sind. Wenn eine Bedingung konfiguriert ist, dass ein Benutzer Mitglied einer bestimmten Gruppe sein muss, greift die Regel nur, wenn der Benutzer *nicht* Mitglied der Gruppe ist.

Bedingungen
+++++++++++

Damit eine Regel verarbeitet wird, müssen eine oder mehrere Bedingungen zutreffen.

Benutzer ist Mitglied von Gruppe
    Über diese Bedingung kann festlelegt werden, dass entweder der zugreifende oder lokal angemeldete Benutzer Mitglied einer bestimmten Gruppe sein muss. Die gewünschte Gruppe kann ausgewählt werden. Wenn keine oder die falschen Gruppen zur Auswahl stehen, muss ggf. das *Datenbackend* unter den allgemeinen Einstellungen zur :ref:`Computerzugriffskontrolle` angepasst werden.

Computer befindet sich im Raum
    Über diese Bedingung kann festlelegt werden, dass sich entweder der zugreifende oder lokal Computer in einem bestimmten Raum befinden müssen. Der gewünschte Raum kann ausgewählt werden. Wenn keine oder die falschen Räume zur Auswahl stehen, muss ggf. das *Datenbackend* unter den allgemeinen Einstellungen zur :ref:`Computerzugriffskontrolle` angepasst werden.

Zugreifender Computer befindet sich im selben Raum wie der lokale Computer
    Über diese Bedingung kann festlelegt werden, dass sich der zugreifende und der lokal Computer im selben Raum befinden müssen. Damit kann beispielsweise unterbunden werden, dass ein Lehrer auf Computer eines anderen Kurses in einem anderen Raum zugreifen kann. 

Zugreifender Computer ist localhost
    Wenn diese Bedingung aktiviert ist, greift die Regel nur, wenn der Zugriff vom lokalen Computer aus erfolgt. Damit kann beispielsweise sichergestellt werden, dass Lehrer auf den lokalen Veyon-Dienst zugreifen können. Dieser Zugriff ist notwendig, damit der Veyon Master bestimmte Funktionen über den Veyon-Dienst ausführen kann (u. a. den Server für den Demo-Modus).
    
Zugreifender Benutzer hat eine oder mehrere Gruppen gemeinsam mit lokalem (angemeldeten) Benutzer
    Über diese Bedingung kann festlelegt werden, dass der zugreifende und lokal angemeldete Benutzer Mitglieder in mindestens gemeinsamen Gruppe sein müssen, beispielsweise einer Benutzergruppe für einen Kurs oder ein Seminar.

Zugreifender Benutzer ist angemeldeter Benutzer
    Als Alternative zur Bedingung :guilabel:`Zugreifender Computer ist localhost` kann auch der Zugriff eines Benutzers auf eigene Sitzungen erlaubt werden. Hierfür muss diese Bedingung aktiviert werden.
    
Zugreifender Benutzer ist bereits verbunden
    Im Zusammenspiel mit der Bedingung :guilabel:`Zugreifender Computer befindet sich im selben Raum wie der lokale Computer` kann ein erweitertes Regelwerk geschaffen werden, dass den Zugriff auf andere Räume unter bestimmten Bedingungen doch erlaubt. Hierzu zählt die Möglichkeit, auf einen Computer zuzugreifen, wenn der zugreifende Benutzer bereits verbunden ist. Wenn sich der Lehrer zusätzlich zu Raum A auch im Raum B auf einem Lehrer-Computer anmeldet und sich dort im Veyon-Master die Computer von Raum B anzeigen lässt, hat der Veyon-Dienst auf den Computern in Raum B eine Verbindung vom Lehrer. Dann kann der Lehrer auch von Raum A aus auf Raum B zugreifen, wenn diese Bedingung mit einer Erlauben-Aktion aktiviert ist.

Kein Benutzer angemeldet
    Über diese Bedingung kann festgelegt werden, wie auf einen Computer zugregriffen werden kann, wenn kein Benutzer angemeldet ist. Zur Unterstützung bei der Computeradministration kann es beispielsweise hilfreich sein, immer auf einen Computer zugreifen zu können, wenn kein Benutzer angemeldet ist.

.. important:: Wenn mehr als eine Bedingung aktiviert wird, muss **jede** Bedingung zutreffen, damit die Regel angewendet wird (logisches UND). Wenn nur eine von mehreren Regeln zutreffen soll (logisches ODER), müssen mehrere Zugriffskontrollregeln erstellt werden.

Aktion
++++++

Wenn alle aktivierten Bedingungen einer Regel zutreffen, wird im Hinblick auf den Computerzugriff eine festgelegte Aktion ausgeführt. Diese Aktion kann im Bereich :guilabel:`Aktion` eingestellt werden:

Zugriff erlauben
    Der Zugriff auf einen Computer wird erlaubt und weitere Regeln werden nicht verarbeitet. Wenn es in der Regelliste eine weiter unten angeordnete Regel gibt, die den Zugriff verweigern würde, wird der Zugriff trotzdem erlaubt. Es muss mindestens eine Regel mit dieser Aktion geben.

Zugriff verweigern
    Der Zugriff auf einen Computer wird verweigert und weitere Regeln werden nicht verarbeitet. Wenn es in der Regelliste eine weiter unten angeordnete Regel gibt, die den Zugriff erlauben würde, wird der Zugriff trotzdem verweigert.

Angemeldeten Benutzer um Erlaubnis fragen
    Bei dieser Aktion wird auf dem Computer ein Dialog angezeigt, über den der angemeldete Benutzer wählen kann, ob er den Zugriff erlauben oder verweigern möchte. Unabhängig von der Benutzerentscheidung werden keine weiteren Regeln verarbeitet.

Keine (Regel deaktiviert)
    Mit dieser Aktion wird die Regel ignoriert und mit der Verarbeitung der nächsten Regel fortgesetzt. Diese Option kann genutzt werden, um einen inaktiven Dummy-Eintrag zur visuellen Untergliederung der Regelliste zu erzeugen.

Mit einem Klick auf die Schaltfläche :guilabel:`OK` wird die Regel bzw. die vorgenommenden Änderungen übernommen und der Dialog geschlossen.


Regeln sortieren
----------------

.. important:: Die definierten Zugriffskontrollregeln werden nacheinander in der Reihenfolge der Liste abgearbeitet. Gleichzeitig wird die Aktion der ersten zutreffenden Regel durchgeführt, selbst wenn nachfolgende Regeln auch zutreffen würden und zu einer anderen Aktion führen würden.

Alle angelegten Regeln können über die Schaltflächen mit den Pfeilsymbolen umsortiert werden. Regeln, die Zugriffe anhand bestimmter Kriterien grundlegend unterbinden oder erlauben sollen, sollten möglichst weit oben stehen. Regeln zur Abdeckung von Spezialfällen können weiter unten stehen. Regeln zur Umsetzung eines Ausweichverhaltens sollten am Schluss stehen.


Logische Verknüpfung von Regeln
-------------------------------

Wenn mehr als eine Bedingung aktiviert wird, muss *jede* Bedingung zutreffen, damit die Regel angewendet wird (logisches UND). Wenn nur eine von mehreren Regeln zutreffen soll (logisches ODER), müssen mehrere Zugriffskontrollregeln erstellt werden.

Mit Grundkenntnissen in Boolescher Algebra kann die Option *Alle Bedingungen umkehren* als Negations-Operator in Verbindung mit invertierten Aktionen genutzt werden, um erweiterte Anwendungsszenarien zu modellieren. Wenn ein Benutzer beispielsweise in zwei bestimmten Gruppen Mitglied sein muss, um den Zugriff auf einen Computer zu erlauben, können zwei einzelne Regeln erzeugt werden, die den Zugriff verbieten, wenn der Benutzer *nicht* Mitglied in einer der beiden Gruppe ist.


Regelwerk testen
----------------

Im Abschnitt :guilabel:`Computerzugriffskontrolle` kann das eingerichtete Regelwerk über die Schaltfläche :guilabel:`Testen` mit verschiedenen Szenarien überprüft werden. Im Testdialog können die Parameter zur Nachstellung eines Szenarios eingegeben werden. Mit der Schaltfläche :guilabel:`OK` werden die Regeln mit den anhand der Parameter abgearbeitet und eine Meldung mit dem Testergebnis wird angezeigt.
