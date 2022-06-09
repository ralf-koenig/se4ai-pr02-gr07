## Meta-Anforderungen aus der Aufgabenstellung / Requirements

Siehe [Projektbeschreibung / Zweites Projekt (updated)](https://moodle2.uni-leipzig.de/mod/resource/view.php?id=1856858&redirect=1)

Vollständigkeit der Anforderungen im Projekt wichtiger als der Funktionsumfang.

### 0. Thema und Mehrwert, Rohdaten, Trainingsdaten
Jede Gruppe kann das Thema ihres Projektes grundsätzlich frei wählen. Einzige
Bedingung ist, dass der Anwendungsfall ihrer Anwendung einem (hypothetischen) Unternehmen
oder einer sonstigen Organisation einen klaren Mehrwert bietet. Dies sollte anhand einer
entsprechenden Requirements-Analyse festgehalten und innerhalb des Repositories mit
abgegeben werden. Dabei sollen nicht nur bereits vorhandene vollständig gelabelte Daten
verwendet werden, sondern im Rahmen des Projektes auch Rohdaten erhoben und durch eine
Preprocessing-Pipeline dem Modell geeignet zur Verfügung gestellt werden.

### 1. Experiment Tracking
Parameter und Ergebnisse der Experimente, die im Entwicklungsprozess der KI-Komponente nötig sind, 
sollen mittels MLFlow getrackt werden.

### 2. Versionierung von Daten und Modellen
Während im ersten Projekt Daten sowie Modelle im
selben Git-Repository versioniert wurden, sollen Daten nun mittels DVC und Modelle über die
Model Registry von MLFlow versioniert werden. Zum Verfolgen (und Versionieren) der Features
soll außerdem ein Feature Store verwendet werden.

### 3. Pipelines
Im Projekt sollen mindestens die folgenden Pipelines vorhanden sein, hierfür eignen
sich MLFlow-Projekte:-
 - **Data Preprocessing Pipeline**, welche mit den Rohdaten startet und mit dem Hinzufügen
der Features zum Feature Store endet
 - **Training Pipeline**, welche mit dem Laden der aktuellen Features aus dem Feature Store
beginnt und mit dem Push des trainierten Models in die Model Registry endet.

### 4. Feedback
Ähnlich zum ersten Projekt soll ein Endnutzer (je nach Ihrem gewählten Thema) die
Möglichkeiten haben, falsche Vorhersagen mit Feedback zu versehen, sodass das Feedback
Eingang in die Trainingsdaten findet und für das Re-Training berücksichtigt wird.

### 5. Monitoring
Über ein Dashboard (z.B. ELK Stack) sollen nicht-funktionale Eigenschaften Ihrer
KI-Komponente visualisiert werden.

### 6. Integration der KI-Komponente/Frontend
Neben der Entwicklung der KI-Komponente und
zugehöriger Infrastruktur soll das Modell in eine – dem gewählten Thema gerechte – Anwendung
integriert sein. Dies kann z.B. eine Webseite, ein IDE-Plugin oder eine Standalone-Anwendung
sein. Es kann auf die Erstellung einer sinnvollen API (z.B. FastAPI) zurückgegriffen werden,
jedoch soll das finale Ergebnis dem entsprechen, was ein Endnutzer erwarten würde.