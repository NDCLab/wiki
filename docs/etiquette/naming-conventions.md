---
layout: default
title: Naming Conventions
parent: Etiquette
nav_order: 1
---

### Contents
1. [Overarching Philosophy](#overarching-philosophy)
2. [General Guidance](#general-guidance)
3. [Code](#code)
4. [Resources](#resources)

# Overarching Philosophy

All naming conventions for the NDCLab are designed to be:
* human-friendly (that is, they are descriptive and help us navigate all our projects)
* machine-friendly (that is, they make it easy for us to use automated search methods to find what we want in the shortest time possible)

### Human-friendly
We spend a lot of time looking at a computer screen. So we should use conventions that make things easier on our eyes. Here are some top guidelines to assist:<br/>
:white_check_mark: Only use lowercase letters in names (with a teensy exception for camelCase)--this means you never have to wonder what to capitalize because you never capitalize anything!<br/>
:white_check_mark: Build names out of "chunks," which are separated by an underscore (see below for examples).<br/>
:white_check_mark: Within a chunk, separate words with a hyphen for easy reading (teensy exception for camelCase when space is at a premium).<br/>
:white_check_mark: Use deliberate repetition to enable efficient searching across projects and over time.

### Machine-friendly
Don't confuse the machines. Recognize how computers order things by default (numerically and alphabetically) and avoid their cryptonite:<br/>
:x: spaces<br/>
:x: accented characters<br/>
:x: special characters<br/>

# General Guidance

## Project Names

Project names should be informative but concise. Words are separated by hyphens. All project names begin with a lowercase letter. Examples:

>mind-reading<br/>
>social-context-alpha

In some situations, space may be limited. In such cases, hyphens may be replaced with camelCase. Examples:

>brainBox<br/>
>baseEEG

When future spin-offs of a project are envisaged, the original project is named the "-alpha" project and spin-offs should use an informative modifier. Examples:

>social-context-alpha<br/>
>rwe-alpha<br/>
>rwe-valence<br/>

In the latter examples, informativeness has been sacrificed for length. RWE is an acronym for real-world-errors, which was considered too long for default usage.

Project names are used as top-level folder names on GitHub and Google Drive.

## Folder Names

The re-use of top-level folder names across projects and platforms is encouraged to simplify navigation. For instance, on the HPC, all active projects have a "collecting" folder used for the storage of incoming data from study participants.

Three main paradigms are employed in establishing folder naming conventions for a particular context; the choice depends upon the particular context and use case:

**simple name**
>collecting/<br/>
>analyses/

**chronological ordering**
>2021-08-13_nsf_buzzell_theta-development/<br/>
>2021-10-05_nimh_buzzell_theta-dev-anxiety/

**logical ordering**
>01_design/<br/>
>02_protocols/<br/>
>03_recruitment/<br/>

If using logical ordering, left pad your numbers with zeros, as in the examples above. Since many computer programs order items starting with the first character, this left-padding ensures that "10" actually comes after "09."

## File Names

No two files should share an identical name. Ever.

File names should be built in "chunks."  Examples of potential chunks:

* date
* project name
* a reflection on the document's unique content (e.g. a particular analysis or write-up)

____________________EXAMPLE


## Dates (YYYY-MM-DD)

Whenever dates are used, the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) convention is used to avoid any ambiguity.  Examples:

>1905-09-27 ([This paper](https://www.astro.puc.cl/~rparra/tools/PAPERS/e_mc2.pdf) was published on this date.)<br/>
>2020-03-11 (The WHO made an [important statement](https://www.who.int/director-general/speeches/detail/who-director-general-s-opening-remarks-at-the-media-briefing-on-covid-19---11-march-2020) on this date.)


# Code

In general, all lab code should align with the conventions used in [PEP8](https://www.python.org/dev/peps/pep-0008/#naming-conventions) and [BIDS](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html#file-name-structure).

## Function Names

Function names are built with camelCase and underscores.
re-use across programs (but not within) to refer to the same thing

## Variable Names

### Scripts

xxx

### REDCap

### Instrument Names
Each element within REDCap is an "instrument." These should be named:
>instrument_sX_rX_eX

Where:
* "instrument" is the name of the instrument/survey/questionnaire, limited to 10 characters
* "sX" is the **session** number to distinguish across different time points of a longitudinal study
* "rX" is the **run** number to distinguish logical groupings of data collection within a particular session
* "eX" is the **event** number to distinguish repeated use of the instrument before and after an experimental manipulation within a given run

In the above, "X" is replaced by a numerical value (1, 2, 3) to indicate the ordering of data collection.  For instance, in a longitudinal study, a pre-task questionnaire to establish the "initial state" of a participant is employed. Each point of data gathered is numbered distinctly:

| variable | collection point |
| --- | :-- |
| initState_s1_r1_e1 | gathered during the initial 2021 session with the participant and as part of the first part of the study |
| initState_s1_r2_e1 | gathered during the initial 2021 session with the participant and as part of the second part of the study, but **before** the experimental manipulation |
| initState_s1_r2_e2 | gathered during the initial 2021 session with the participant and as part of the second part of the study, and **after** the experimental manipulation |
| initState_s2_r1_e1 | gathered during a follow-up session in 2023 with the participant and as part of the first part of that follow-up study |


# Resources
Awesome [slidedeck](https://speakerdeck.com/jennybc/how-to-name-files) from [Jenny Bryan](https://jennybryan.org/).<br/>
Another awesome [slidedeck](https://slides.djnavarro.net/project-structure/#1) from [Danielle Navarro](https://djnavarro.net/).