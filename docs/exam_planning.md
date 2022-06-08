## Prüfungsplan-Solver für Data Science/Informatik-Studiengänge

### 0. Thema und Mehrwert, Rohdaten, Trainingsdaten

Prüfungspläne (Prüfung, Student, Raum, Zeit, Lehrkraft) erstellen aus Constraints wie 
Rohdaten 
- Belegungszahlen (anonymisiert)
- Prüfungszeiträume
- Prüfungsordnungen und Plan-Einschreibezahlen
- Räume und deren Kapazitäten 
- Studenteneinschreibungen in den Lehrveranstaltungen
- konkrete Prüfungsbelegung
- synthetisch, oder auch über Quellen wie https://www.informatik.uni-leipzig.de/~stundenplan/block.html
oder https://www.informatik.uni-leipzig.de/ifijung/10/service/stundenplaene.html

Mehrwert: Gute, kollisionsfreie Prüfungspläne für die Studenten und Lehrkräfte. Entlastung des Studienbüros Math/Inf.
Planung ggf. interaktiv beeinflussen lassen, indem man Constraints dazu nimmt oder streicht.

Daraus künstliche Studenten und künstliche Lehrkräfte ableiten. (Vermeidung realer Personendaten)
Alles, was nicht personenbezogen ist (Studiengänge, Lehrveranstaltungen, Räume, Kapazitäten), kann hingegen recht real 
modelliert werden. Synthetisierte Daten eines Semesters generieren für die ganzen Entitäten. Einige Realwelt-Objekte (z.B. Studiengänge 
Master Informatik und Master Data Science samt Studentenzahlen realistisch implementieren. Ablage z.B. in Relationaler 
Datenbank.)

### 1. Experiment Tracking

Experimente sind:
- ein Semester und Prüfungen am Ende (dort mehrere Läufe)
- Wiederholungsprüfungen

### 2. Versionierung von Daten und Modellen

- Verwaltung in relationaler Datenbank bietet sich an sich an. Praktisch eine Planungsdatenbank.
- Planungsläufe werden dort gleich versioniert.

### 3. Pipelines
### 3.1 Data Preprocessing Pipeline
nimmt Rohdaten und fügt Features dem Feature Store hinzu
### 3.2 Training Pipeline
Laden der Features bis Push in die Model Registry
 - => Daten (alte Prüfungsdaten etc.) mit einbeziehen?

### 4. Feedback

von Kommiliton*innen, von Lehrkräften, auch von Studienbüro?
künstliche Sichten auf Nutzeraccounts, die allen offenstehen

### 5. Monitoring

generisch

### 6.1 Integration der KI-Komponente
- KI-Komponente: CSP Solver oder Answer Set Programming (akzeptiert), fertigen Solver nehmen, Problem passend 
  formulieren, dann Metriken auf den Lösungen messen
- Metriken anbieten, die zu optimieren sind, z.B. Abstände zwischen den Prüfungen für die Studenten.
- Güte/Performance der Vorschläge beurteilen (z.B. Anzahl an Kollisionen, erfüllter Wünsche).

### 6.2 Frontend
- API => Tool oder Almaweb zur Integration anbieten, geht nicht in der Zeit
- (kleine) Web-Anwendung für Endbenutzer dazu bauen: angebracht und ausreichend
