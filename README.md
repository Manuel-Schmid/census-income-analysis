# Census-Income (KDD) Analyse

Der Datensatz [Census-Income (KDD)](https://archive.ics.uci.edu/dataset/117/census+income+kdd) enthält demografische und arbeitsbezogene US-Volkszählungsdaten aus den Jahren 1994 und 1995, die von dem U.S. Census Bureau erhoben wurden. Er wird in der Informatik und im Bereich Machine Learning oft als Benchmark-Datenbank genutzt, um vorherzusagen, ob das Einkommen einer Person über oder unter 50'000 USD liegt.

## 1. Bedeutung KDD
KDD steht für Knowledge Discovery in Databases. Es bezeichnet den gesamthaften, wissenschaftlichen Prozess des Findens von nützlichen Mustern und Erkenntnissen in grossen Datenmengen.


<!-- ## 1. Kontext & Zielstellung
Der Datensatz basiert auf den Erhebungen der jährlichen demografischen Befragung des **US Census Bureau** (Current Population Survey, Jahre 1994 und 1995). Ziel der Datenanalyse bzw. des Machine-Learning-Modells ist eine **binäre Klassifikation**: Es soll vorhergesagt werden, ob das jährliche Einkommen einer Person unter oder über $50.000 liegt (`INCOME`). -->

## 2. Umfang & Struktur
* **Stichprobengröße:** $N = 199.523$ Beobachtungen (Zeilen)
* **Anzahl Merkmale:** 42 Spalten (41 Prädiktoren + 1 Zielvariable)
* **Zielvariable (`INCOME`):** Binär (Klassen: unter bzw. über $50.000/Jahr)

## 3. Verwendete Spaltennamen
Im Notebook werden die technischen UCI-Spaltennamen in verständlichere englische Namen umbenannt. Die folgenden Namen werden deshalb in der weiteren Analyse verwendet:

| Ursprünglicher Name | Verwendeter Name | Bedeutung |
|---|---|---|
| `AAGE` | `AGE` | Alter |
| `ACLSWKR` | `CLASS_OF_WORKER` | Klasse der beschäftigten Person |
| `ADTINK` | `INDUSTRY_CODE` | Industriecode |
| `ADTOCC` | `OCCUPATION_CODE` | Berufscode |
| `AHGA` | `EDUCATION` | Bildungsabschluss |
| `AHSCOL` | `ENROLLED_IN_EDU` | Aktueller Schul- oder Ausbildungsbesuch |
| `AMARITL` | `MARITAL_STATUS` | Familienstand |
| `AMJIND` | `MAJOR_INDUSTRY` | Hauptbranche |
| `AMJOCC` | `MAJOR_OCCUPATION` | Hauptberufsgruppe |
| `ARACE` | `RACE` | Ethnie bzw. Rasse |
| `AREORGN` | `HISPANIC_ORIGIN` | Hispanische Herkunft |
| `ASEX` | `SEX` | Geschlecht |
| `AUNMEM` | `LABOR_UNION_MEMBER` | Gewerkschaftsmitgliedschaft |
| `AUNTYPE` | `UNEMPLOYMENT_REASON` | Grund der Arbeitslosigkeit |
| `AWKSTAT` | `EMPLOYMENT_STATUS` | Vollzeit-/Teilzeit- und Erwerbsstatus |
| `CAPGAIN` | `CAPITAL_GAINS` | Kapitalgewinne |
| `GAPLOSS` | `CAPITAL_LOSSES` | Kapitalverluste |
| `DIVVAL` | `DIVIDENDS` | Dividendenerträge |
| `FILESTAT` | `TAX_FILER_STATUS` | Steuerstatus |
| `GRINREG` | `PREV_REGION` | Region des vorherigen Wohnsitzes |
| `GRINST` | `PREV_STATE` | Bundesstaat des vorherigen Wohnsitzes |
| `HHDFMX` | `HOUSEHOLD_STAT_DETAILED` | Detaillierter Haushalts- und Familienstatus |
| `HHDREL` | `HOUSEHOLD_SUMMARY` | Zusammengefasste Haushaltsbeziehung |
| `MARSUPWRT` | `WEIGHT` | Stichprobengewicht |
| `MIGMTR1` | `MIGRATION_MSA` | Veränderung der MSA-Zugehörigkeit |
| `MIGMTR3` | `MIGRATION_REG` | Veränderung der Region |
| `MIGMTR4` | `MIGRATION_WITHIN_REG` | Umzug innerhalb der Region |
| `MIGSAME` | `SAME_HOUSE_1YR` | Gleicher Haushalt wie vor einem Jahr |
| `MIGSUN` | `MIGRATION_SUNBELT` | Frühere Wohnsitzregion Sunbelt |
| `NOEMP` | `NUM_EMPLOYEES` | Anzahl Beschäftigte beim Arbeitgeber |
| `PARENT` | `PARENTS_PRESENT` | Familienmitglieder unter 18 bzw. Elternpräsenz |
| `PEFNTVTY` | `BIRTH_COUNTRY_FATHER` | Geburtsland des Vaters |
| `PEMNTVTY` | `BIRTH_COUNTRY_MOTHER` | Geburtsland der Mutter |
| `PENATVTY` | `BIRTH_COUNTRY_SELF` | Eigenes Geburtsland |
| `PRCITSHP` | `CITIZENSHIP` | Staatsbürgerschaft |
| `SEOTR` | `SELF_EMPLOYED` | Selbstständigkeit |
| `VETQVA` | `VET_QUESTIONNAIRE` | Fragebogen für die Veteranenverwaltung |
| `VETYN` | `VETERANS_BENEFITS` | Veteranenleistungen |
| `WKSWORK` | `WEEKS_WORKED` | Gearbeitete Wochen im Jahr |
| `AHRSPAY` | `WAGE_PER_HOUR` | Stundenlohn |
| `year` | `YEAR` | Erhebungsjahr |
| `income` | `INCOME` | Einkommensklasse |

## 4. Inhaltliche Kategorisierung der Features
Die 41 Prädiktoren lassen sich inhaltlich in folgende Themenblöcke unterteilen:

* **Demografie & Herkunft:** Alter (`AGE`), Geschlecht (`SEX`), Ethnie/Rasse (`RACE`), hispanische Herkunft (`HISPANIC_ORIGIN`), Staatsbürgerschaft (`CITIZENSHIP`) und Geburtsländer (`BIRTH_COUNTRY_SELF`, `BIRTH_COUNTRY_FATHER`, `BIRTH_COUNTRY_MOTHER`).
* **Erwerbstätigkeit & Beruf:** Erwerbsstatus (`EMPLOYMENT_STATUS`), Arbeitsklasse (`CLASS_OF_WORKER`), Branchen- und Berufscodes (`INDUSTRY_CODE`, `OCCUPATION_CODE`, `MAJOR_INDUSTRY`, `MAJOR_OCCUPATION`), gearbeitete Wochen pro Jahr (`WEEKS_WORKED`), Stundenlohn (`WAGE_PER_HOUR`), Betriebsgröße (`NUM_EMPLOYEES`), Selbstständigkeit (`SELF_EMPLOYED`) und Gewerkschaftsmitgliedschaft (`LABOR_UNION_MEMBER`).
* **Finanzen:** Kapitalgewinne (`CAPITAL_GAINS`), Kapitalverluste (`CAPITAL_LOSSES`), Dividendenerträge (`DIVIDENDS`) und Steuerstatus (`TAX_FILER_STATUS`).
* **Haushalt, Familie & Bildung:** Familienstand (`MARITAL_STATUS`), Haushaltsrolle und -beziehung (`HOUSEHOLD_SUMMARY`, `HOUSEHOLD_STAT_DETAILED`), Elternpräsenz (`PARENTS_PRESENT`), Schulbesuch (`ENROLLED_IN_EDU`) und Bildungsabschluss (`EDUCATION`).
* **Migration:** Wohnsitz im Vorjahr (`SAME_HOUSE_1YR`), Migrationscodes (`MIGRATION_MSA`, `MIGRATION_REG`, `MIGRATION_WITHIN_REG`, `MIGRATION_SUNBELT`) sowie vorherige Region und Bundesstaat (`PREV_REGION`, `PREV_STATE`).
* **Veteranenstatus:** Fragebogen und Leistungen für Veteranen (`VET_QUESTIONNAIRE`, `VETERANS_BENEFITS`).