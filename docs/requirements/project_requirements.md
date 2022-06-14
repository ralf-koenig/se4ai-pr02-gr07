# Projektspezifische Anforderungen für den Wohnungspreisschätzer in Leipzig

- Anknüpfen an Motivation und fachliche Anforderungen ableiten
- Folie 15 aus Requirements Engineering der Vorlesung einbeziehen (Struktur siehe unten)
- Software-Architektur motivieren
- die ML Ops Sachen dabei weitgehend außen vor lassen

## Kontext
<!-- Define the context in which the AI-component is deployed and operates -->

Der Wohnungspreisschätzer in Leipzig soll zwei wesentliche User Stories abdecken:

1) Als potenzieller **Kaufinteressent einer Wohnung** in Leipzig möchte ich zu einem existierenden 
Wohnungsangebot aus einer Vergleichsplattform für Wohnungen (z.B. ImmobilienScout24) eine
Preisspanne wissen, zu welchem Angebotspreisen vergleichbare Wohnungen angeboten werden. Die KI-Komponente
findet mit der zunächst abstrakt scheinenden Metrik der "Vergleichbarkeit" (letztlich sind Wohnungen ja
Unikate) eine Menge von Angeboten und berechnet dann eine Preisspanne. 
Der Mehrwert für den Kaufinteressenten ist die schnelle Einschätzbarkeit, wie das konkrete Angebot im Markt
in etwa positioniert ist.

   - Eingabe: Angebots-ID
   - Ausgabe: Liste von Angebots-IDs von vergleichbaren Angeboten, Spanne an Angebotspreisen

2) Als potenzieller **Anbieter einer Wohnung** in Leipzig möchte ich vor dem Anbieten einer Wohnung eine 
Angebotspreisspanne ermitteln, die sich aus realen Vergleichsangeboten ergibt.

    - Eingabe: Features einer Wohnung in Leipzig
    - Ausgabe: Liste von Angebots-IDs von vergleichbaren Angeboten, Spanne an Angebotspreisen

Im Prinzip ist User Story 2 ähnlich zu User Story 1, aber die Wohnung muss dafür nicht auf dem Portal 
eingestellt werden. Das spart den Anbieter Kosten (für das Einstellen und Verwalten) und ermöglicht einen
Marktvergleich ohne Offenlegung der eigenen Daten.

Das Problem wird herausfordernd, weil Wohnungen eine große Zahl von Eigenschaften haben, die auch ungleich
in der Vergleichsplattform für Wohnungen ausgefüllt sind und unterschiedlich wichtig bewertet werden. 
Das System muss also mit einem erheblichen Maß an Unsicherheit zurechtkommen.

## Daten
<!-- Define requirements on the used data to ensure correct/desired functional and non-functional behavior of the 
system -->

* Rohdaten von Wohnungsangeboten von Immoscout24
* Filtern auf Wohnungen (in Abgrenzung zu Häusern oder Gewerberaum)
* Immoscout24 macht damit bereits eine gewisse Datenintegration und Datenbereinigung, es hat auch 
Pflichtparameter
* aktuelle Daten (z.B. <4 Wochen alt)
* Feature-Modell wird im Kern übernommen, aber teils reduziert

## Modell 
<!-- Define model type, parameters, metrics, dimensions, adaptability, portability. -->

* die Anwendung verlangt eine Art Ähnlichkeitssuche und damit eine Art Clustering
* Parameter: 
  * Mindestähnlichkeit: abstrakter Parameter, damit ein anderes Wohnungsangebot in die Vergleichsliste einbezogen wird
  * maximale Anzahl der Vergleichsangebote (Top-N, eine Art Clustergröße)

## Metriken für das Echtzeit-Monitoring der in Produktion befindlichen Modelle
<!-- Enable a continuous improvement and early data/model shift detection -->

* ein Echtzeit-Monitoring der in Produktion befindlichen Modelle ist im Projekt nicht geplant

## Menschliche Einflussfaktoren
<!-- Define how humans react on, for example, automated decisions -->

* Menschen könnten einige oder alle der ausgewählten Vergleichsangebote von Wohnungen als unpassend empfinden, 
dafür soll eine Feedback-Funktion integriert werden. Jedoch ist die Auswahl der Vergleichswohnungen auch 
recht beschränkt durch die geringe Zahl von Wohnungsangeboten in Leipzig.

## Ethische Anforderungen
<!-- Define what ethical decisions are made by the system and how ethical aspects will be addressed. -->

* das System kann verwendet werden, um preisgünstige Wohnangebote schneller zu entdecken und den Markt dort
automatisiert leer zu kaufen mit einem Geschwindigkeitsvorteil gegenüber anderen. Das nehmen wir in Kauf.
* sonst keine Anforderungen

## Nicht-funktionale / Qualitätsanforderungen
<!-- Define requirements on quality attributes (explainability, legal req.) -->

* um die Qualität zu erhöhen, verarbeiten wir nur Angebote in Leipzig (begrenztes Domänenwissen über die 
eigene Stadt)

* die Vorhersagewerte können gespeichert werden und dann gegen neue Angebote, die eingestellt werden, 
getestet werden.

## Hardware-Anforderungen
<!-- Specify the HW systems the AI component trains and inferences on. -->

* die Liste der Wohnungsangebote in Leipzig bei Immoscout24 ist aktuell bei ca. 1200 Angeboten
* Hardware damit unkritisch, Menge klein genug, sogar für vollständige Vergleiche im Kreuzprodukt 1200x1200