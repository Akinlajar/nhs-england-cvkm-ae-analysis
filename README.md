# Cardiovascular, Kidney and Metabolic Disease in North West A&E Departments

**NHS England · Healthcare Public Health, North West region · June to August 2026**

> **No code or data is published here.** This work was carried out inside NHS England's secure data environment (UDAL) under the Five Safes, and the analysis is unpublished while it supports an ICB commissioning proposal. This page describes the problem, the pipeline design, the methods and the skills involved.

**Stack:** Databricks SQL (NHS UDAL, Azure) · SNOMED CT · Python (matplotlib, python-pptx) · Tableau

---

## At a glance

| | |
|---|---|
| Data | Emergency Care Data Set (ECDS): 3,978,791 North West A&E attendances |
| Clinical definition | 607 SNOMED CT codes, built from 13 seed concepts and signed off clinically |
| Pipeline | 2 reusable foundation views and 13 steps, regenerating in about 36 seconds |
| Audiences | Regional senior leadership, cardiac, kidney and metabolic leads, and the three North West ICB cardiovascular leads |
| Outcome | Now supporting an ICB commissioning proposal |

---

## The question
The regional Healthcare Public Health lead asked how much cardiovascular, kidney and metabolic (CVKM) disease falls on North West A&E departments, and where the inequalities are. I turned that brief into a defined cohort, a scope agreed in a Project Implementation Document, and a milestone plan.

## Pipeline design (described, not published)

```
ECDS attendances (UDAL, Databricks)
        │
        ▼
Foundation view 1: attendances with all 13 diagnosis fields
        │
        ▼
Foundation view 2: CVKM flags from the 607-code definition
   (primary-diagnosis cohort and "recorded anywhere" cohort, each visit counted once)
        │
        ▼
13 analysis steps: demographics, geography (ICB and trust),
   arrival mode, admission, coding coverage
        │
        ▼
Python (matplotlib, python-pptx): 27-slide pack rebuilt from source
Tableau: interactive dashboard for live presentation
```

This replaced a 500-line scoping sheet. Changing the date range reruns the whole output.

## Methods

### Building the clinical definition
- Started from 13 seed SNOMED CT concepts and walked the hierarchy with a recursive SQL query, reaching 294 kidney and diabetes codes across 8 conditions. These were combined with 313 cardiovascular codes into a 607-code definition.
- Checked the definition against the national ECDS reference specification: 45 codes were redundant and 11 were missing.
- Resolved three clinical boundary questions with an A&E consultant and a national GP lead before sign-off.

### Data quality and fairness
- Found that **41% of attendances had no diagnosis code**.
- Built a coding coverage table by ICB and trust (Greater Manchester 65.3%, Lancashire and South Cumbria 55.4%, Cheshire and Merseyside 54.0%).
- Reported results on two denominators (all attendances and coded attendances), so that low counts in poorly recording areas read as under-recording rather than lower need.

### Quality assurance
- Reconciliation checks caught a transcription error and an inherited SNOMED identifier typo that was breaking the code expansion.
- Rebuilt a senior colleague's published cardiovascular analysis as a control, matched it, and raised the two metrics that differed rather than adjusting my own. Both were reconciled before presenting.

### Governance
- All processing stayed inside UDAL under the Five Safes; only aggregate outputs left the environment.

---

## Delivery and leadership
- **Owned the work end to end:** from a one-line brief to scope, cohort definition, pipeline, outputs and presentations.
- **Led clinical engagement:** agreed the code definition with an A&E consultant and a national GP lead.
- **Ran a weekly stakeholder meeting** across analytics, urgent and emergency care, and public health.
- **Absorbed a late scope change:** extended the analysis to a new year in the final week, delivered the next day by reusing the pipeline, with every count reconciled.
- **Communicated to two audiences:** a Python-generated slide pack for regional senior leaders (cut from 37 to 27 slides after feedback), and a live Tableau dashboard for the North West CVKM Task and Finish group, including the three ICB cardiovascular leads.
- **Left the work rerunnable:** plain-English code documentation, a methodology record and a handover note.
- Featured in the NHS England North West Weekly Bulletin for work on reducing inequalities in emergency care.

## Skills demonstrated
SQL pipeline design (views, recursive queries, reusable steps) · clinical coding (SNOMED CT, ECDS) · data quality assessment · health inequalities analysis · information governance (Five Safes) · automated reporting in Python · Tableau dashboards · stakeholder management and clinical engagement · presenting to senior and non-technical audiences

---

## Author
**Judah Akinlaja**, Health Data Scientist · MSc Health Data Science, University of Manchester
[LinkedIn](https://www.linkedin.com/in/judah-akinlaja) · [Portfolio](https://judahakinlajar.co.uk)
