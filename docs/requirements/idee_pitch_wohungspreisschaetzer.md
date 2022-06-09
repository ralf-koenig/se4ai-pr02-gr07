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

