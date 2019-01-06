# Exploring MIMIC-III Critical Care Database

The examples in this repository build in the information from the [MIMIC-III: Getting Started](https://github.com/EarlGlynn/MIMIC-III-Getting-Started) repository.

## Repository Directories

Let's build a data dictionary with information about fields by table and how they can be used.

The MIMIC-III database schema can be [viewed online here](https://mit-lcp.github.io/mimic-schema-spy/tables/admissions.html).

## Database tables

### patients

* Explore the six fields in the `patients` table.

* Why is there a pattern in the counts of records by subject_id?

* Let's compute age at death for patients with both dob (date of birth) and dod (date of death) defined.

* To protect patient anonymity dates were shifted.  Patients originally >89 years old show up as 300 years old! This is an unusual approach.

* Database drivers `RPostgres` and `PostgreSQL` give different age-at-death density plots (for now) for not handling date computations correctly.

### admissions

* Explore the 15 fields in the `admissions` table.

* A log scale was used to view a density plot for length-of-stay computed form admit time to discharge time.

* The relationship between the `diagnosis` field in this table and the `diagnoses_icd` table information is unclear.

### diagnoses

* Explore the `diagnoses_icd` fact table with additional information in the `d_icd_diagnosis` dimension table.

* A bar plot of `seq_num` (diagnosis priority) shows values can range from 1 to 39, but usually are less than 10.

* The dimension table has many icd 90 codes that are never referenced by a fact table record.

* The fact table has over 140 icd 9 codes that cannot be found in the dimension table.

 A `left_join` is likely more desirable than an `inner_join` when connecting the tables.

* Computed Summaries

  * Counts by ICD Diagnosis COde

  * Counts by primary vs secondary diagnosis by ICD Diagnosis Code

  * Counts by 10 year age intervals by ICD Diagnosis Code
