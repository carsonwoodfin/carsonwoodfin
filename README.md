# Clinical Complexity, Neighborhood Vulnerability, and Access to Anti-Amyloid Therapy



## Project Overview

This project examines whether neighborhood social vulnerability, non-neurologic
comorbidity burden, and selected medication-class burden are associated with
receipt of anti-amyloid therapy (ATT) among patients seen at the
Memory Diagnostic Center (MDC)



The analysis builds on an earlier geospatial analysis showing that MDC patients
who received ATT disproportionately lived in more advantaged neighborhoods. The
current project evaluates whether clinical complexity is also associated with
treatment receipt and whether adjustment for comorbidity and medication burden
helps explain the observed neighborhood vulnerability gradient.



## Research questions

1. Does ATT receipt differ across neighborhood Social Vulnerability Index (SVI)
categories?
2. Is non-neurologic comorbidity burden associated with ATT receipt?
3. Is selected medication-class burden associated with ATT receipt?
4. Do comorbidity and medication burden attenuate the association between
neighborhood SVI and ATT receipt?



## Study Population



The primary cohort includes patients in the St. Louis regional MDC dataset who
were seen between July 1, 2023, and January 31, 2026 and a geo-codable address.

* Descriptive cohort: 4,758 patients
* Adjusted analytic cohort: 4,628 Black or White patients with known male or
female gender
* ATT recipients in the adjusted cohort: 398
* Census tract represented in the adjusted cohort: 608

The St. Louis regional cohort was selected to improve geographic comparability
and align the analysis with the regional neighborhood-vulnerability question.



## Restricted data

The source patient-level dataset is restricted and is not included in this
repository or submission. It contains direct identifiers and may only be accessed
in an approved environment.

This project package contains:

* R analysis code
* Aggregate statistical tables
* De-identified figures
* Documentation

It does not contain names, medical record numbers, addresses, exact dates,
patient-level geographic information, or patient-level analytic records



## Primary outcome

att_indicator identifies whether a patient received anti-amyloid therapy
during the study period.

## Neighborhood exposure

SVI_quart represents census tract Social Vulnerability Index categories:
* Q1: Most advantaged
* Q2
* Q3
* Q4: Highest social vulnerability



## Non-neurologic comorbidity burden

The primary comorbidity measure is an eight-domain count containing:
* Hypertension
* Hyperlipidemia
* Diabetes
* Cerebrovascular disease
* Myocardial infarction
* Chronic kidney disease
* Liver cirrhosis
* Polyneuropathy



The general diabetes and type 2 diabetes indicators were combined because type
2 diabetes was nested within the broader diabetes indicator. Diabetes therefore
contributes no more than one point to the score.

Central nervous system conditions were excluded from the primary composite
because the indicator was nearly universal and could reflect the neurologic
condition underlying memory-clinic attendance or ATT eligibility. CNS
conditions were examined separately in a sensitivity analysis.

Comorbidity categories were defined as:

* Low: 0-1 conditions
* Moderate: 2 conditions
* High: 3 or more conditions



## Selected medication-class burden



Medication burden was calculated from nine selected medication classes:

* Anticoagulants
* Antihypertensives
* Antiplatelets
* GLP-1 receptor agonists
* Acetylcholinesterase inhibitors
* Antidepressants
* Biguanides
* Memantine
* Statins



Medication categories were defined as:

* None: 0 selected classes
* Moderate: 1-3 selected classes
* High: 4 or more selected classes



This measure represents selected medication-class burden and should not be
interpreted as total medication count or conventional polypharmacy



## Statistical analysis



The analysis includes:

* Aggregate descriptive statistics
* Exact binomial 95% confidence intervals
* Conventional logistic regression
* Bias-reduced logistic regression
* Census-tract clustered standard errors
* Sequential regression models
* CNS sensitivity analysis
* Multicollinearity diagnostics



The primary adjusted model includes:

* SVI category
* Non-neurologic comorbidity burden
* Selected medication-class burden
* Age per five years
* Gender
* Race
* Distance from Barnes-Jewish Hospital per 10 miles



Mean bias-reduced logistic regression was used as the primary adjusted model
because ATT events were sparse in the highest-SVI and Black patient groups.
Conventional logistic regression and Census-tract clustered standard errors
were used as supporting sensitivity analyses



## Key findings

ATT receipt declined across neighborhood SVI categories

* Q1: 10.1%
* Q2: 8.4%
* Q3: 5.0%
* Q4: 1.4%



Higher-SVI groups also had greater-than-average non-neurologic comorbidity
and selected medication class-burden.



In the primary adjusted model:

* Q3 was associated with lower odds of ATT receipt than Q1
* The Q4 estimate indicated lower receipt but was imprecise because only 4 Q4
patients received ATT.
* High non-neurologic comorbidity burden was associated with lower ATT receipt.
* High selected medication-class burden was associated with lower ATT receipt.
* White patients had higher adjusted odds of ATT receipt than Black patients.
* Distance was not independently associated with ATT receipt



Sequential models suggested that adjustment for demographic composition and
distance produced the greatest attenuation of the unadjusted SVI association.
Comorbidity and medication burden produced modest additional attenuation
but did not fully account for the neighborhood gradient.

The overall findings remained substantively consistent after adjustment for CNS
conditions and when conventional model standard errors were clustered by census
tract.



## Project files


```text
project/
├── README.md
├── 01_mdc_stl_att_svi_analysis_FINAL.R
├── clinical_complexity_paper_FINAL.docx
├── Clinical_Complexity_SVI_ATT_FINAL.pptx
├── Aggregate_Results/
│   ├── Figures/
│   │   ├── att_receipt_by_svi.png
│   │   ├── att_receipt_by_svi_and_comorbidity.png
│   │   ├── att_receipt_by_svi_and_medication.png
│   │   └── primary_adjusted_forest_plot.png
│   └── Tables/
│       ├── att_receipt_by_svi.csv
│       ├── att_receipt_by_svi_and_comorbidity.csv
│       ├── att_receipt_by_svi_and_medication.csv
│       ├── cns_sensitivity_model.csv
│       ├── conventional_logistic_model.csv
│       ├── multicollinearity_diagnostics.csv
│       ├── primary_model_presentation_table.csv
│       ├── sequential_svi_models.csv
│       └── tract_clustered_sensitivity_model.csv
└── Documentation
 └── README.md
```
## Software requirements

The analysis was conducted in R using:

* tidyverse
* janitor
* broom
* brglm2
* sandwich
* lmtest
* car



Install the required packages once:

```install.packages(
c(
"tidyverse",
"janitor",
"broom",
"brglm2",
"sandwich",
"lmtest",
"car"
)
)
```


## Running the analysis

1. Obtain authorized access to the MDC\_STL.csv
2. Store the restricted dataset in the approved analysis environment.
3. Set the R working directory to the project directory.
4. Confirm that the data\_file value in the script points to the authorized
source file.
5. Restart R to create an empty session.
6. Run the complete script:
source("01\_mdc\_stl\_att\_svi\_analysis\_FINAL.R")
7. Confirm that aggregate tables and figures are written to aggregate\_results.

The script does not export patient-level records.



## Reproducibility and FAIR practices



This project supports FAIR principles by:

* Using descriptive and consistent filenames
* Providing machine-readable aggregate CSV outputs
* Providing a complete R analysis script
* Documenting variable construction and analytical decisions
* Recording the R session and package version information
* Separating restricted source data from shareable outputs
* Providing metadata needed to interpret and reuse the aggregate deliverables



Patient-level data cannot be openly accessible because of privacy, institutional,
and regulatory requirements.



##Important limitations

* The analysis is observational and cannot establish causality.
* Neighborhood SVI is a census-tract measure and should not be interpreted as an
individual patient characteristic.
* Reasons for receiving or not receiving ATT were not directly measured.
* ATT eligibility, biomarker status, patient preference, caregiver support,
insurance, and referral pathways may contribute to the observed associations.
* Only four Q4 patients in the adjusted cohort received ATT, producing imprecise
estimates.
* Only seven Black patients in the descriptive MDC\_STL cohort received ATT.
* The selected medication-class measure is not a complete measure of
polypharmacy.
* CNS conditions require additional definition and were therefore handled
separately.



##AI use disclosure

Generative AI was used as a support tool for code organization, debugging,
visualization refinement, documentation, and interpretation checks. The research
questions, cohort definitions, variable construction decisions, and clinical
interpretations were developed by the project author.

I executed the analysis in R, reviewed the code and aggregate outputs,
confirmed the analytic sample and event counts, and checked the report results
against the exported results. AI assistance was used to help implement and
refine portions of the statistical workflow, including more advanced R syntax
and model-output organization.

AI tools did not access the restricted patient-level dataset or protected health
information. Work involving AI was limited to code guidance, approved variable
names, methodological discussion, and aggregate or de-identified outputs.

