---
layout: default
title: launch-checklist
parent: launch-checklist
nav_order: 9
---

Before going live, make sure that you have completed everything on this list.


## GitHub

- [x] Readme and Contributing files are beautiful and public-facing.
- [x] Launch version of REDCap has been exported as a Data Dictionary.
- [x] PsychoPy experiment is available either on GitHub or GitHub readme includes a note that it will be released on GitLab after close of data collection.
- [x] All code and data monitoring assets specific to the pilot data are moved into an "pilot" subfolder within their respective top-level folders (so that main study data may not reside loose in each folder).


## REDCap

- [x] Survey queue has been fully tested.
- [x] All screener questions and all questions involving identifiable data are marked as "Identifiers."
- [x] No user role has access to output identifiers.
- [x] Only the appropriate lab members have access to the project.


## PsychoPy

- [x] Experiment has been fully tested.
- [x] Only desired data points are included in the output CSV.
- [x] The experiment name and output file names match data monitoring conventions.


## GitLab/Pavlovia

If participants will complete an online behavioral task:
- [x] Experiment has been fully tested online on multiple browsers.
- [x] Pavlovia experiment is "Running" and has credits assigned.
- [x] Mechanism by which participants access the task (likely via a link within REDCap) has been tested and properly outputs data with the participant ID (but no other identifiers).


## gDrive

- [x] Study notebook includes launch date and any appropriate notes up to this point.
- [x] If using a gDrive study tracker, the lab manager has moved it to the special area and removed access to all by the subset of lab members working on the project.


## HPC

- [x] All source data and derivatives specific to the pilot data are moved into an "pilot" subfolder within their respective top-level folders (so that main study data may not reside loose in each folder).


## Protocol

- [x] Protocol is finalized and PI has sat through as a mock participant under this final version of the protocol.
