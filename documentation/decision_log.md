# Decision Log

## D001 — Dataset Selection

**Decision:** Use the Diabetes 130-US Hospitals dataset.

**Status:** Confirmed


## D002 — Target Definition

**Decision:** Formulate the prediction task as binary classification.

**Positive class:** `<30` — readmitted within 30 days.

**Negative class:** `NO` and `>30`.

**Observed distribution:**
- Class 0: 90,409 (88.84%)
- Class 1: 11,357 (11.16%)

**Status:** Confirmed


## D003 — Duplicate Records

**Finding:** 0 completely duplicated rows were found.

**Decision:** No exact duplicate rows will be removed.

**Status:** Confirmed


## D004 — Encounter Identifier

**Finding:** `encounter_id` contains 101,766 unique values
for 101,766 encounters.

**Decision:** Exclude `encounter_id` from predictive modelling
because it functions as a unique encounter identifier rather than
a meaningful predictive feature.

**Status:** Confirmed


## D005 — Patient Identifier

**Finding:**
- 71,518 unique patients
- 16,773 patients have multiple encounters
- 6,339 patients have 3 or more encounters

**Decision:** `patient_nbr` will not be used as a predictive feature.

A patient-level grouping strategy will be investigated for
train/test splitting to prevent encounters from the same patient
appearing in both training and testing sets.

**Status:** Provisional — further diagnostic required.


## D006 — Class Imbalance

**Finding:** The positive class represents only 11.16% of encounters.

**Decision:** Accuracy will not be used as the sole measure of model
performance. Imbalance-handling strategies will be experimentally
evaluated.

**Status:** Confirmed.


## D007 — Prediction Unit

**Decision:** Each observation will represent a hospital encounter.

**Evidence:**
101,766 encounters and 71,518 unique patients were identified.
16,773 patients have multiple encounters, and 6,481 patients have
encounters belonging to both binary readmission classes.

**Reason:**
The target represents readmission following a specific encounter,
rather than a permanent patient characteristic.

**Status:** Confirmed


## D008 — Encounter Identifier

**Feature:** encounter_id

**Finding:**
101,766 unique values across 101,766 encounters.

**Decision:**
Exclude from predictive modelling because it is a unique encounter
identifier.

**Status:** Confirmed


## D009 — Patient Identifier

**Feature:** patient_nbr

**Finding:**
71,518 unique patients across 101,766 encounters.

16,773 patients have multiple encounters.

**Decision:**
Do not use patient_nbr as a predictive feature.

Retain it temporarily for patient-level grouping during dataset
splitting to prevent the same patient appearing in both training
and testing sets.

**Status:** Confirmed


## D010 — Class Imbalance

**Finding:**
90,409 (88.84%) encounters are negative and 11,357 (11.16%) are
positive for 30-day readmission.

**Decision:**
Accuracy will not be treated as the sole performance metric.
Class-imbalance strategies will be evaluated experimentally.

**Status:** Confirmed


## D011 — Prediction Time Point

**Decision:** TBD

**Options considered:**
1. Admission/early-encounter prediction
2. Encounter-level prediction using information collected
   throughout the encounter

**Reason for investigation:**
Several features, including discharge-related information and
length of hospital stay, may not be available at admission.

**Status:** Requires further investigation