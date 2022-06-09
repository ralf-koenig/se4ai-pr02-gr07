# Wohnungspreisschätzer für Leipzig

## Abgrenzung
* Konzentration auf eine Stadt (Leipzig)
* Wohnungspreisschätzer (nicht ganzes Haus, nicht Grundstücke)
* Preisvorhersage (Regression model) -> ähnlich zu ersten Projekt

## Rohdaten

### Angebotspreise von Wohnungen
  * fertiger Datensatz: https://www.kaggle.com/ -> Wohnungs- und Hauspreise von Boston und Kalifornien
    * damit könnte man flott schon mal loslegen und eine ML-Komponente bauen
    * aber halt für die Preise und Features, die dort drin sind
  * sonst eigene Rohdatengewinnung aus Immobilienplattformen
    * Scraping von ImmoScout: https://www.youtube.com/watch?v=uo6KsoB4n1U
    * Immoscout API: https://api.immobilienscout24.de/main/api-products/
    * Scraping-Projekte auf GitHub:
      * https://github.com/asmaier/ImmoSpider
      * https://github.com/balzer82/immoscraper

### Idee: Mietpreisspiegel der Stadt Leipzig
  * teilt die Stadt schon ein in Gebiete
  * hat Durchschnittswerte für Quadratmeterpreis von Mietwohnungen, von da kann man rückschließen auf Wohnungspreis
      
### Hilfsfunktionen
- GPS-Koordinaten: Input: Straße + Hausnummer => Google Maps oder OSM geben GPS-Koordinaten zurück
- Kartendarstellung ggf. mit OSM, da Google Maps ggf. teuer

## Günstige Eigenschaften für unser Projekt
* an sich Standard-Projekt → viele Quellen und ähnliche umgesetzte Projekte
* Genügend öffentliche Daten (außer den echten realen Kaufpreisen am Ende)
* Datensatz von Kaggle anfangen → später eigene Daten scrapen
* ähnlich zu erstem Projekt (Regression model)
  * erstes Projekt war ein Classifier auf recht sauberen Trainingsdaten
  * zweites Projekt könnte ein Classifier in eine Preiskategorie werden

## Herausforderungen bei der Vorhersage

Komplexe Preisbildung wegen Vielzahl von Features

### Einmalkosten der Wohnung

Der Wohnungspreis bildet sich aus vielen Fakten. Eine Wohnung hat viele Eigenschaften, z.B.

  * Größe der Wohnung in Quadratmeter, Anzahl Zimmer der verschiedenen Typen (Wohnräume, Schlafzimmer, Bad, Küche)
  * Schnitt der Zimmer
  * Lage in einem Gebäude (z.B. EG, Dachgeschoss, Souterrain)
  * Lage in einer Stadt: Stadtbezirk und Umgebung, z.B.
    * Arbeitsplätze
    * Soziale Infrastruktur wie Kindergärten und Schulen
    * Verkehrs-Infrastruktur (Straßen, ÖPNV, Parken)
    * Geschäfte
    * Kulturelle Angebote, Parks, Grün, etc.
  * Zustand der Gebäudesubstanz 
    * Alter des Gebäudes
    * Sanierungsstand bei Dach, Fassade, Fenster, Elektrik, gerade für ältere Wohnungen
  * Internetversorgung des Gebäudes und der Wohnung
  * Energetische Aspekte
    * Realisierung der Heizung (Gas, Öl, Fernwärme, Wärmepumpe)
    * Realisierung der Warmwasser-Versorgung (Gas, Öl, Fernwärme, Wärmepumpe)
    * Energiebedarf Realisierung Dämmung und Fenster, Energieausweis
    * Photovoltaik auf dem Dach
  * Ausstattung der Wohnung (Altersgerecht, Rolladen, Markisen, Balkon/Terrasse)
  * Ausstattung des Gebäudes an sich (Aufzug, Tiefgarage, Garten, ...)
  * Einfluss von Umweltrisiken wie Überschwemmungen, Starkregen, Abschattung
  * Nebenkosten für Makler
  
### Folge- und Betriebskosten

Die Folge- und Betriebskosten koppeln rück auf den Preis der Wohnung an sich. 
Käufer beziehen diese Folgekosten in die Kaufentscheidung mit ein.

  * Kosten der Arbeitswege abhängig von der Entfernung zur Arbeitsstelle, Home Office verändert das
  * Kosten für Sanierung/Renovierung/Ausbau/Umbau der Wohnung an sich
  * Kosten für Gebäudesanierung und dessen Ausstattung
  * Kosten für Heizung und Warmwasser
  * Kosten für Strom (Photovoltaik auf dem Dach kann das verändern)
  * Betriebskosten für Energie, Müllentsorgung, Gartenpflege, etc.
  * Grundsteuer

### Gesamtwirtschaftliche Rahmenbedingungen

Auch diese koppeln rück. Sie lassen einen Immobilienmarkt erhitzen oder abkühlen.

* Entwicklung der Inflation, Löhne, Zinsen
* Entwicklung am Aktienmarkt
* Immobilien als Wertanlage / "Betongold"
* Spekulation mit Immobilien