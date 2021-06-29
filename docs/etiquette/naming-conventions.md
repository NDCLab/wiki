---
layout: default
title: Naming Conventions
parent: Etiquette
nav_order: 1
---

### Contents
1. [Overarching Philosophy](#overarching-philosophy)
2. [General Naming Guidance](#general-naming-guidance)
3. [Code](#code)
4. [GitHub](#github)
5. [REDCap](#redcap)
6. [Helpful Resources](#helpful-resources)

## Overarching Philosophy

All naming conventions for the NDCLab are designed to be:
* human-friendly (that is, they are descriptive and help us navigate all our projects)
* machine-friendly (that is, they make it easy for us to use automated search methods to find what we want in the shortest time possible)

### Human-friendly
We spend a lot of time looking at a computer screen. So we should use conventions that make things easier on our eyes. Here are some top guidelines to assist:<br/>
* Get used to using lowercase letters for naming things (with a teensy exception for the occasional camelCase)--this means you never have to wonder what to capitalize because you never capitalize anything!
* Build names out of "chunks," which are separated by an underscore (see below for examples).
* Within a chunk, separate words with a hyphen for easy reading (again, teensy exception for camelCase when space is at a premium).
* Use deliberate repetition to enable efficient searching across projects and over time.

### Machine-friendly
Don't confuse the machines. Recognize how computers order things by default (numerically and alphabetically) and avoid feeding them filename cryptonite. Never use:<br/>
:x: spaces<br/>
:x: accented characters (ñöé, etc.)<br/>
:x: special characters (?!:*+, etc.)<br/>

## General Naming Guidance

### Project Names

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

In the latter two examples, informativeness has been sacrificed for length. RWE is an acronym for real-world-errors, which was considered too long for default usage.

Project names are used as top-level folder names on GitHub and Google Drive.

### Folder Names

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

### File Names

No two files should share an identical name. Ever.

File names should be built in "chunks."  Examples of potential chunks:

* date
* project name
* a reflection on the document's unique content (e.g. a particular analysis or write-up)

For example, here are some good file names:
> 2021-06-01_social-context-alpha_prelim-analysis_anxiety<br/>
> 2021_06-30_social-context-alpha_prelim-analysis_exec-function

Alternately, if all files are stored within a space specific to the social-context-alpha project and you don't need to track chronology, you could use:
> 01_anxiety_methods<br/>
> 02_anxiety_analysis<br/>
> 03_anxiety_results

### Dates (YYYY-MM-DD)

Whenever dates are used, the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) convention is used to avoid any ambiguity.  Examples:

>1905-09-27 ([This paper](https://www.astro.puc.cl/~rparra/tools/PAPERS/e_mc2.pdf) was published on this date.)<br/>
>2020-03-11 (The WHO made an [important statement](https://www.who.int/director-general/speeches/detail/who-director-general-s-opening-remarks-at-the-media-briefing-on-covid-19---11-march-2020) on this date.)

## Code

In general, all lab code should align with the conventions used in [PEP 8](https://www.python.org/dev/peps/pep-0008/#naming-conventions) and [BIDS](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html#file-name-structure). Always use descriptive names that will help others understand your code.

### Function and Method Names

Wherever possible, functions and methods should be re-used across programs when referring to the same thing. For naming them, `lowercase_with_underscores` is used. Example:
> def round_sum (num_1, num_2):<br/>
> &nbsp;&nbsp;&nbsp;&nbsp;return math.round(num_1+num_2)

In special circumstances where names are too long, `camelCase` can be used.

### Class Names

`UpperCamelCase` is used for class names. Example:
>class ImageSprite

### Constants

`CAPITALIZED_WITH_UNDERSCORES` is used for constants. Example:
>MAX_PARTICIPANTS = 10

### Variable Names

For naming variables, `lowercase_with_underscores` is also used. Example:
> subject_name = "bob"

## GitHub

### Repository Names
Repositories should be named identically to the associated project. For example:

> social-context-alpha

### Branch Names
By default, repositories have a `main` branch and a `dev` branch. New branches are created from the `dev` branch and are named:

> `dev-[feature]-[yourname]`

For example, if Bob creates a new branch to create stimuli for an experiment, he would call it:

> `dev-stimuli-bob`

(Note that the wiki is an exception. It does not have a `dev` branch and new branches are created directly off `main` according to the convention `[feature]-[yourname]`.)

### Commit Messages
Git commit messages (specifically, the commit subject line) should be concise, informative, and in the imperative tense. There is no final period.<br/>

:white_check_mark: Correct typo<br/>
:white_check_mark: Add counterbalancing content<br/>
:white_check_mark: Optimize function X<br/>
:x: Fix<br/>
:x: Re-wrote the entire script so now it works right<br/>
:x: Added a feature.

The seven great rules of commit messages make for easy reading [here](https://chris.beams.io/posts/git-commit/).

## REDCap

### Instrument Names
Each element within REDCap is an "instrument." These should be named:
>instrument_sX_rX_eX

Where:
* `instrument` is the name of the instrument/survey/questionnaire, limited to 10 characters
* `sX` is the **session** number to distinguish across different time points of a longitudinal study
* `rX` is the **run** number to distinguish logical groupings of data collection within a particular session
* `eX` is the **event** number to distinguish repeated use of the instrument before and after an experimental manipulation within a given run

In the above, "X" is replaced by a numerical value (1, 2, 3) to indicate the ordering of data collection.  For instance, in a longitudinal study, a pre-task questionnaire to establish the "initial state" of a participant is employed. Each instrument employed is numbered distinctly:

| instrument | collection point |
| --- | :-- |
| initState_s1_r1_e1 | gathered during the initial 2021 session with the participant and as part of the first part of the study |
| initState_s1_r2_e1 | gathered during the initial 2021 session with the participant and as part of the second part of the study, but **before** the experimental manipulation |
| initState_s1_r2_e2 | gathered during the initial 2021 session with the participant and as part of the second part of the study, and **after** the experimental manipulation |
| initState_s2_r1_e1 | gathered during a follow-up session in 2023 with the participant and as part of the first part of that follow-up study |

### Variable Names

#### Scored Instruments

Variable names are used in REDCap to identify the responses to specific questions asked of study participants. They are identical to their associated instrument name, except that `iX` is added to specify the item number. For example, the first three questions of the `initState` instrument would be named:<br/>
> initState_i1_s1_r1_e1<br/>
> initState_i2_s1_r1_e1<br/>
> initState_i3_s1_r1_e1

By default, if a question within an instrument will require the output of subvariables, REDCap automatically appends `___X` to the end of the base variable name. For instance:<br/>
> initState_i1_s1_r1_e1___1<br/>
> initState_i1_s1_r1_e1___2<br/>
> initState_i1_s1_r1_e1___3

In other cases, however, an instrument may contain sub-items that REDCap cannot automate. For these questions, the sub-item must be built into the variable name manually:
> initState_i1-sub1_s1_r1_e1<br/>
> initState_i1-sub2_s1_r1_e1<br/>
> initState_i1-sub3_s1_r1_e1

#### Unscored Instruments

In relatively rare but important cases, such as instruments that gather demographic data, the use of `i1`, `i2`, `i3` for item numbers will be an impediment to data analysis. For surveys that do not get scored or factored for analysis, a more informative convention should be used:<br/>
> demo_sleep_s1_r1_e1<br/>
> demo_exercise_s1_r1_e1<br/>
> demo_caffeine_s1_r1_e1

## Helpful Resources
* Awesome [slidedeck](https://speakerdeck.com/jennybc/how-to-name-files) from [Jenny Bryan](https://jennybryan.org/).<br/>
* Another awesome [slidedeck](https://slides.djnavarro.net/project-structure/#1) from [Danielle Navarro](https://djnavarro.net/).