# FHIR to cBioPortal Data Transformation Pipeline


This repository contains a Jupyter Notebook workflow for transforming clinical and genomic data from **FHIR format** into the **cBioPortal-compatible TXT file structure**. It is designed to support translational cancer research by bridging EHR systems (FHIR) and cancer genomics platforms (cBioPortal).

## 📘 Project Overview

The notebook:
- Ingests and standardizes patient metadata, clinical events, molecular data, and treatment recommendations
- Converts and structures data into cBioPortal-compatible `.txt` files
- Computes derived variables such as:
  - `AGE`
  - `OS_MONTHS`
  - `DFS_MONTHS`
  - `MTB_days_after_diagnosis`
- Maps clinical codes, statuses, and dates into longitudinal timelines
- Outputs valid files including:
  - `data_clinical_patient.txt`
  - `data_clinical_sample.txt`
  - `data_clinical_events.txt`
  - `data_mutations.txt`
  - Associated `meta_*.txt` files

## 📁 Outputs

The script produces the following core files:
- `data_clinical_patient.txt`
- `data_clinical_sample.txt`
- `data_clinical_timeline.txt` 
- `data_mutations.txt`
- `meta_study.txt`
- `meta_clinical.txt`
- `meta_mutations.txt`, etc.

These files can be validated through cBioPortal validator script `validateData.py` or `validateStudies.py`. 
And later uploaded through cBioPortal importer script `cbioportalImporter.py`.

## ✅ Features

- Handles various date formats with robust parsing
- Auto-generates `SAMPLE_ID` using hashed `PATIENT_ID`
- Converts therapy, status, recommindations info into timeline events
- Integrates therapy recommendations with evidence metadata
- Compatible with cBioPortal validation and import scripts

## ⚠️ Known Limitations

- Some fields are populated with placeholders (e.g., `.` or default statuses)
- Data consistency checks (e.g., cross-file ID matching) must be carefully validated
- Relies on CSV files extracted from patient$everything Bundles
- `validateData.py` must be run to confirm compliance with cBioPortal schema

## 🛠 Usage

1. Open `FHIR_to_Cbioportal.ipynb` in Jupyter Notebook
2. Execute all cells to generate and inspect `.txt` files
3. Run cBioPortal validator:
   ```bash
   python validateData.py -s <your_study_directory>

## 🧪 Requirements
Python 3.7+
pandas, numpy, dateutil, and other standard scientific Python packages