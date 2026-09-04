# 📘 Kreditstatus‑Vorhersage mit R

## 📌 Projektübersicht

Dieses Projekt wurde als Studienprojekt an der AKAD University durchgeführt.  
Ziel ist die vollständige Bearbeitung eines Data‑Science‑Workflows zur **Vorhersage des Kreditstatus** (*Fully Paid* vs. *Charged Off*) auf Basis des LendingClub‑Datensatzes.

Der Workflow umfasst:

- Datenbereinigung  
- Explorative Datenanalyse (EDA)  
- Feature Engineering  
- Modellbildung  
- Evaluation (Confusion Matrix, ROC, AUC)

Der Datensatz enthält **39.717 Kreditfälle** mit **111 Variablen**, darunter Kreditmerkmale, Kundeninformationen, Bonitätsindikatoren und Prozessdaten.

---
## 📄 HTML‑Bericht ansehen

Der vollständige Analysebericht ist hier als HTML‑Seite verfügbar:

🔗 **https://marijke-analytics.github.io/Kreditrisiko_logistische_Regression/web78_aufgabe_1.html**


## 📂 Projektstruktur

```
├── web78_aufgabe_1.R        # Hauptskript mit vollständigem Workflow
├── loan_dictionary.csv      # Variablenbeschreibungen
└── README.md                # Projektdokumentation
```

---

## 🔧 Verwendete Technologien

- **R 4.5.2**
- **RStudio**
- **ggplot2** – Visualisierungen  
- **ggcorrplot** – Korrelationsheatmaps  
- **dplyr** – Datenmanipulation  
- **caret** – Modelltraining & Evaluation  
- **pROC** – ROC‑Kurven & AUC  

---

## 🧹 1. Datenbereinigung

Der Rohdatensatz enthält:

- uneinheitliche Datentypen (z. B. Prozentwerte als Strings),
- unstrukturierte Textfelder,
- Variablen mit extrem vielen NAs,
- Redundanzen,
- Leakage‑Variablen (Informationen nach Kreditvergabe),
- hochkardinale Kategorien (z. B. ZIP‑Codes).

Bereinigungsschritte:

- Entfernen irrelevanter Variablen (`id`, `member_id`, Textfelder, URLs)
- Entfernen von Leakage‑Variablen (z. B. `total_pymnt`, `last_pymnt_d`)
- Entfernen von Variablen mit >50 % NA
- Umwandlung typischer NA‑Codierungen (`""`, `"NA"`, `"NULL"`)
- Typkonvertierungen (z. B. `int_rate` → numerisch)
- Entfernen von Zeilen mit kritischen NA‑Werten

Ergebnis: ein konsistenter, modellierbarer Datensatz.

---

## 📊 2. Explorative Datenanalyse (EDA)

Die EDA umfasst:

### **Korrelationsanalyse**
- Heatmap zentraler numerischer Variablen  
- starke Zusammenhänge zwischen `loan_amnt`, `funded_amnt`, `installment`  
- hohe Korrelation zwischen `grade_num` und `int_rate`

### **Univariate Analysen**
- Boxplots für Kreditbeträge, Einkommen, Bonitätsmerkmale  
- Histogramme für Zinssätze und Kreditbeträge  
- Häufigkeitsverteilung des Kreditstatus

### **Bivariate Analysen**
- Vergleich von `loan_amnt`, `installment`, `int_rate` nach Kreditstatus  
- Wahrscheinlichkeiten für *Charged Off* nach Kreditzweck  
- Wahrscheinlichkeiten für *Fully Paid* nach Kredit‑Grade

Die Visualisierungen zeigen klare Muster, die für die Modellbildung relevant sind.

---

## 🤖 3. Modellbildung

Zielvariable:  
`loan_status` → binär kodiert (*Fully Paid* vs. *Charged Off*)

Schritte:

1. Train/Test‑Split (caret)
2. Auswahl relevanter Merkmale
3. Training eines Klassifikationsmodells (z. B. Logistic Regression, Random Forest)
4. Bewertung mittels:
   - Confusion Matrix  
   - ROC‑Kurve  
   - AUC  
   - Schwellenwertoptimierung

Das Modell zeigt eine solide Trennschärfe zwischen guten und schlechten Kreditfällen.

---

## 📈 4. Ergebnisse & Erkenntnisse

- Höhere Zinssätze und schlechtere Grades korrelieren stark mit Ausfallwahrscheinlichkeit.
- Kleine Unternehmen (*small_business*) haben die höchste *Charged Off*‑Rate.
- Höhere Kreditbeträge und höhere monatliche Raten erhöhen das Risiko.
- Einkommen hat nur moderaten Einfluss.
- Das finale Modell erreicht eine gute AUC und klare Entscheidungsgrenzen.

---

## 📁 Dateien & Reproduzierbarkeit

Das gesamte Projekt ist vollständig reproduzierbar:

- Alle Schritte sind im Skript dokumentiert.
- Plots werden direkt im Skript erzeugt.
- Der Datensatz muss im angegebenen Pfad liegen oder entsprechend angepasst werden.

---

## 👩‍💻 Autorin

**Marijke Haupt**  
AKAD University – Master Data Science  
Modul WEB78 – Programmtechniken in Data Science  
Betreuer: **Dr. Martin Prause**

---

## 📜 Lizenz

Dieses Projekt dient ausschließlich akademischen Zwecken im Rahmen des Moduls WEB78.
