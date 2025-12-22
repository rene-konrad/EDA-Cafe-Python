# cafe_sales_optimization

Ein datengetriebenes Analyse-Projekt zur **Bereinigung „schmutziger“ Verkaufsdaten** und zur **Optimierung des Produktportfolios** eines Cafés.
Ziel war es, Inkonsistenzen in einem Datensatz von 10.000 Transaktionen zu beheben, um anschließend Umsatztreiber, saisonale Trends und das Kundenverhalten in Abhängigkeit von Standort und Zahlungsmethode zu identifizieren.

---

## 📊 Executive Summary

Das Projekt nutzt **Python (Pandas)** für umfangreiches Data Cleaning und **Seaborn/Matplotlib** für die explorative Datenanalyse (EDA). Der ursprüngliche Datensatz enthielt zahlreiche Fehler (z.B. Text in Zahlenfeldern, fehlende Werte, logische Lücken), die vor der Analyse rekonstruiert werden mussten.

**Die wichtigsten Ergebnisse:**
* **Volumen vs. Umsatz:** Während *Kaffee* das meistverkaufte Produkt ist, generieren *Salate und Sandwiches* aufgrund höherer Einzelpreise den meisten Umsatz.
* **Kundenverhalten:** In-Store-Kunden und Barzahler weisen tendenziell höhere Warenkörbe auf als Takeaway- oder Kreditkarten-Kunden.
* **Saisonalität:** Die Umsätze sind relativ stabil (~7.000 €/Monat), mit einem leichten Tief im Februar und Spitzen im Sommer.

---

## 🧠 Tools & Tech Stack

| Tool | Verwendung |
|------|-------------|
| **Python (Pandas & Numpy)** | Data Engineering, Typ-Konvertierung, Imputation fehlender Werte (Logische Rekonstruktion) |
| **Seaborn & Matplotlib** | Visualisierung von Verteilungen (Boxplots), Trends und Korrelationen |
| **Jupyter Notebook** | Entwicklungsumgebung und Dokumentation der Analyse |

---

## 🗂️ Methodik: Die "Triangulations"-Datenbereinigung

**Die Herausforderung:**
Der Datensatz (`dirty_cafe_sales 2.csv`) war stark verunreinigt:
* Spalten wie `Quantity` und `Total Spent` enthielten Strings wie "ERROR".
* Wichtige Metriken fehlten (NaN).
* Kategorische Daten enthielten "UNKNOWN".

**Die Lösung:**
Ich habe eine Bereinigungs-Pipeline entwickelt, die fehlende Werte logisch herleitet:
1.  **Normalisierung:** Umwandlung fehlerhafter Strings in `NaN` und Konvertierung in numerische Datentypen (`coerce`).
2.  **Logische Imputation:** Da der Zusammenhang `Total Spent = Price * Quantity` gilt, wurden fehlende Werte in einer der drei Spalten basierend auf den anderen beiden berechnet (`fillna`).
3.  **Outlier Handling:** Identifikation von Ausreißern mittels Boxplots zur Sicherstellung der Datenqualität.

---

## 📈 Analyse & Visualisierung

Die Analyse deckt Diskrepanzen zwischen Absatzmenge und Umsatzstärke auf.

### Produkt-Performance: Menge vs. Umsatz
Während Kaffee mengenmäßig führt, zeigt die Umsatzanalyse, dass „High-Ticket“-Items (Salad, Sandwich) wirtschaftlich wichtiger sind.

![Umsatz pro Produkt](path/to/revenue_chart.png)

### Saisonalität und Einnahmen
Die Analyse des Zeitverlaufs zeigt stabile Einnahmen mit saisonalen Schwankungen. Der Februar wurde als umsatzschwächster Monat identifiziert (ca. 6.600 €), während der Juni am stärksten war.

### Detail-Analyse: Kaufverhalten nach Standort
Ein Scatterplot (`Quantity` vs. `Total Spent`) zeigt, dass **In-Store** Kunden tendenziell bereit sind, höhere Beträge auszugeben als Takeaway-Kunden.
**Erkenntnis:** Das Ambiente spielt eine signifikante Rolle bei der Ausgabebereitschaft.

---

## Fazit & Business Impact
Durch die Bereinigung der Daten konnten valide strategische Empfehlungen abgeleitet werden, die im „schmutzigen“ Datensatz verborgen waren.

**Handlungsempfehlungen:**
* **Portfolio-Steuerung:** Fokus auf margenstarke Produkte (Salat/Smoothie) im Marketing legen.
* **Cross-Selling:** Nutzung von Kaffee (hohe Frequenz) als Lockmittel für Bundles mit Cookies/Sandwiches, um den durchschnittlichen Warenkorbwert zu steigern.
* **Saison-Management:** Einführung spezieller Promotions im Februar, um das saisonale Tief abzufedern.
* **Store-Experience:** Investition in Sitzmöglichkeiten, da In-Store-Kunden profitabler sind.
