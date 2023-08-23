---
layout: default
title: Launch Checklist
parent: Study Setup
nav_order: 10
---

Before going live, make sure that you have completed everything on this list.


## GitHub

* Readme and Contributing files are beautiful and public-facing.
* Launch version of REDCap has been exported as a Data Dictionary.
* PsychoPy experiment is available either on GitHub or the readme file inside GitHub includes a note that it will be released on GitLab after close of data collection.
* All code and data monitoring assets specific to the pilot data are moved into an "pilot" subfolder within their respective top-level folders (so that main study data may not reside loose in each folder).
* Data dictionaries for all questionnaire and tasks are organized in the repo.
* Central tracker data dictionary has been created.
* Data monitoring scripts have been set up.


## REDCap

* Survey queue has been fully tested.
* All screener questions and all questions involving identifiable data are marked as "Identifiers."
* No user role has access to output identifiers.
* Only the appropriate lab members have access to the project.
* Consent matches IRB-approved language.


## PsychoPy

* Experiment has been fully tested.
* Only desired data points are included in the output CSV.
* The experiment name and output file names match data monitoring conventions.


## GitLab/Pavlovia

If participants will complete an online behavioral task:
* Experiment has been fully tested online on multiple browsers.
* Pavlovia experiment is "Running" and has credits assigned.
* Mechanism by which participants access the task (likely via a link within REDCap) has been tested and properly outputs data with the participant ID (but no other identifiers).


## gDrive

* Study notebook includes launch date and any appropriate notes up to this point.
* If using a gDrive study tracker, the lab manager has moved it to the special area and removed access to all by the subset of lab members working on the project.


## HPC

* All source data and derivatives specific to the pilot data are moved into an "pilot" subfolder within their respective top-level folders (so that main study data may not reside loose in each folder).
* Filing structure and nomenclature for all data files has been planned and confirmed to work with data monitoring processes.


## Protocol

* Protocol is finalized, approved by the IRB, and the PI has sat through as a mock participant under this final version of the protocol.

## SONA

If participants are being recruited and compensated via SONA:
* Study is set up, approved, and active on SONA.
