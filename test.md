Releasepolitik und Versionsnummern
=================================================
*[Zur Themenübersicht](../../themen.md)*

Inhalt
------
1. [Einleitung](#einleitung)
2. [Releasevorbereitung](#releasevorbereitung)
3. [Releasezeitpunkt](#releasezeitpunkt)
4. [Versionierung](#versionierung)

Einleitung
----------

Wenn man an einem Softwareprojekt arbeitet, ist es oft das Ziel, zu einem gewissen Zeitpunkt den Projektcode in einen konsistenten und in sich geschlossenen, möglichst fehlerfreien Zustand zu bringen, um ihn dann an potentielle Nutzer ausliefern zu können. Damit verbunden sind die Begriffe Release und Version, die oft austauschbar verwendet werden können. Der Begriff Release legt dabei den Fokus eher auf den Prozess der Auslieferung an die Nutzer, während eine Version eher mit dem internen Zustand des Codes in Verbindung gebracht wird.
Es gibt auch viele Projekte (besonders in der FLOSS-Welt), die keine expliziten Releases vornehmen, sondern versuchen, die Codebasis zu jedem Zeitpunkt möglichst konsistent und sinnvoll zu halten, sodass User jederzeit den aktuellen Zustand abgreifen und ihn auch sinnvoll benutzen können (*rolling / no release*). In dieser Ausarbeitung soll es allerdings um Projekte gehen, die einen richtigen Releasezyklus besitzen, wo also das Release eine besondere Version der Software ist, auf die explizit hingearbeitet wird.
In dieser Ausarbeitung sollen drei Aspekte betrachtet werden, die für Releases wichtig sind. Zunächst einmal sollte für das Projekt entschieden werden, wann das nächste Release anstehen soll und eventuell auch ein Plan für darauffolgende Releases. Dann muss strukturiert werden, wie das Team zusammen vorgeht, um einen releasebereiten Code zu erarbeiten. Schließlich sollte dem Release auch ein Name zugeteilt werden, der es sinnvoll in der Versionshistorie identifiziert.

Releasezeitplan
---------------

Es existieren zwei grundlegende Ansätze bei der Erstellung eines Zeitplans für Releases: der featurebasierte und der zeitbasierte Ansatz. Beim traditionelleren featurebasierten Ansatz wird festgelegt, welche Features mit dem nächsten Release ausgeliefert werden sollen, und der Releasezeitpunkt wird dementsprechend angepasst. Beim moderneren zeitbasiertem Ansatz wird hingegen ein zeitlich festgelegter Releasezyklus gewählt (z.B Release alle 6 Wochen), und alle Features, die zum Releasezeitpunkt fertig sind, werden in das Release mit aufgenommen, an dem Rest wird für spätere Releases weitergearbeitet.
Im Folgenden werden einige Vor- und Nachteile betrachtet, die die jeweiligen Ansätze mit sich bringen und es wird insbesondere auf die speziellen Anforderungen bei FLOSS-Projekten eingegangen.

#### Featurebasierter Ansatz
Featurebasierte Releases haben den Vorteil, dass sie - wenn sie funktionieren - marketingtechnisch wirkungsvoll sind und aufeinander abgestimmte Features bieten. Allerdings ist es schwierig, abzuschätzen, wann bestimmte Features fertig werden werden und dementsprechend zu planen. Desweiteren kann argumentiert werden, dass Features nie wirklich fertig sind und es immer Raum für Verbesserung gibt.
Ein mögliches Szenario als Negativbeispiel bei schlechter Planung: Die neuen Features für das nächste Projekt wurden festgelegt. Die Entwickler fangen mit der Arbeit an den Features an. Ohne unmittelbaren Zeitdruck verlaufen sie sich und Teams, die für verschiedene Features zuständig sind, arbeiten aneinander vorbei. Irgendwann steigt der Druck auf das Projekt, das nächste Release zu machen und ein Releasedatum wird gewählt,  
#### Zeitbasierter Ansatz
Zeitbasierte Releases haben den Vorteil, dass durch einen von Release zu Release gleichen Zeitplan eine Routine entsteht. Durch diese Routine kann der Bedarf nach Intervention und Koordination von Außen verringert werden und Projektteilnehmer können durch die Routine ihre Aufgaben eingespielter lösen und adäquate Erwartungen entwickeln. Außerdem kann die Routine motivierend für die Teammitglieder wirken.
Durch den festen Releasezyklus können außerdem Vorteile für die Repräsentation des Projektes gegenüber Nutzern entstehen. Die stetigen Releases können Nutzern signalisieren, dass sich das Projekt in einem gesunden Zustand befindet, gut organisiert ist und voraussichtlich in der Zukunft noch weiter Support erhalten wird.
Darüber hinaus können Nutzer sich den zeitlichen Releaserhytmus merken und erwarten daher ein Release und schauen sich möglicherweise sogar von selbst aus das neue Release an, ohne eine Benachrichtigung irgendeiner Art über das Release erhalten haben zu müssen. Dieser Aspekt kann insbesondere bei verteilter Software relevant werden, wo sich Nutzer aktiv das neue Release installieren müssen, um davon zu profitieren. Selbst bei *Software as a Service* kann es aber von Vorteil sein, wenn sich die Nutzer auf den Releasezeitpunkt einstellen können, zum Beispiel um sich über das neue Release zu informieren und eventuell Auswirkungen auf das eigene Projekt einzuschätzen.
Jedoch sind zeitbasierte Releases natürlich nur sinnvoll bei größeren Projekten, wo genügend daran gearbeitet wird, um stetig neue Releases zu erlauben.
#### Zur Länge des Releasezyklus

#### FLOSS

Vorbereitung des Codes für das Release
--------------------------------------
#### gitflow
<object data="https://nvie.com/files/Git-branching-model.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="https://nvie.com/files/Git-branching-model.pdf">
        <p>This browser does not support PDFs. Please download the PDF to view it: <a href="https://nvie.com/files/Git-branching-model.pdf">Download PDF</a>.</p>
    </embed>
</object>
Versionsname
------------
#### Semantic Versioning
Alle Projekte, die eine öffentliche API besitzen, können mit Hilfe von Semantic Versioning ihre Versionen so benennen, dass Nutzer an Hand des Versionsnamen sinnvolle Rückschlüsse auf die  Konsequenzen, die ein Upgrade auf eine neue Version mit sich bringen könnte, ziehen können. Die Benennung erfolgt wie folgt:

- Jeder Versionsname besteht mindestens aus dem Dreitupel **Major.Minor.Patch**, wobei Major-, Minor- und Patchnummer jeweils ganze Zahlen sind
- Die Versionshistorie startet bei **0.0.0**
- Bei Änderungen von einer zur nächsten Version, die **keine Auswirkungen auf die öffentliche API** mit sich bringen, wie z.B kleinen Fehlerbehebungen, wird **Patch** inkrementiert
- Bei Änderungen, die (auch) **rückwärtskompatible Änderungen der API** enthalten, wie z.B. das Hinzufügen von neuen Featuren, wird **Minor** inkrementiert und Patch zurückgesetzt
- Bei Änderungen, die (auch) Änderungen enthalten, die die in der API der Vorgängerversion getroffenen Absprachen bzw. Verträge verletzen (**breaking changes**), wird **Major** inkrementiert und Minor und Patch zurückgesetzt
- Ausnahme: solange die Majornummer 0 ist, wird Minor wie Major behandelt und Patch wie Minor.
- Optional hinter Major.Minor.Patch können noch der Name des Pre-release und Metadaten über den Build angegeben werden, für Details siehe [SemVer-Spezifikation](https://semver.org/)

Durch Vergleichen der alten mit der neuen  Versionsnummer können Nutzer also auf den ersten Blick besser einschätzen, ob durch ein Upgrade einer Dependency Änderungen am eigenen Projekt notwendig werden würden, um wieder die gewünschte Funktionalität herzustellen. Es können z.B. auch Paketmanager verwendet werden, um an Hand von der Versionsnummer automatische Upgrades auf neue Versionen zu machen, die keine *breaking changes* enthalten. Dies wird immer wichtiger, gerade in der FLOSS-Welt, da auf möglichst modulare Software gesetzt wird und es tendenziell immer mehr Dependencies gibt. 