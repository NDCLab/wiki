---
layout: default
title: Programming Standards
parent: Etiquette
nav_order: 2
---

![random_number](https://user-images.githubusercontent.com/26397102/124515039-73b09d80-ddac-11eb-98b4-cf4d8905dfa3.png)

## Outline 

* [Introduction](#Introduction)
* [Naming](#Naming)
* [Python](#Python)
* [Containerization](#Containerization)

## Introduction
The following documentation details programming standards used by the lab for various protocols, programming languages, and tools.

Standardization of the way each lab-member writes code eases [cognitive load](https://en.wikipedia.org/wiki/Cognitive_load) which directly supports debugging, code legibility, and future development. 

For any recommendations on practices, please feel free to directly reach out to the lab tech. 

## Naming
Naming conventions for functions, variables, packages, and files are discussed thoroughly in the [naming-conventions](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/etiquette/naming-conventions.html) page. 

## Python

- Global variables should not be used

- Leave out return types and parameter types in the function header.<br/>
    For example, do this:
    ```python
    def funcName(a, b):
        ...
    ```
    ...not this:
    ```python
    def funcName(a: int, b: int) -> int:
        ...
    ```

- Compartmentalize features into modules. 

- Each function should have a **single** responsibility. Functions that do multiple complex things should be broken into multiple functions. 

- If a function is running into >100 lines of code or contains some potentially reusable code, and is not inseparable, further decompose the function into helper functions.<br/> 
    For example:
    ```python
    def funcName(a, b):
        # remove extension and other characters for file 
        file_name1 =  "test_file.eeg".lower().replace("-", "").replace("_", "").replace(" ", "")
        file_name1 =  filename[:-4] 

        # do same for other file
        file_name 2=  "test_file_EXTRA.eeg".lower().replace("-", "").replace("_", "").replace(" ", "")
        file_name2 =  filename[:-4] 
    ```

    ...can be decomposed into:
    ```python
    def file_standardize(fn):
        file_name =  fn.lower().replace("-", "").replace("_", "").replace(" ", "")
        return filename[:-4] 

    def funcName(a, b):
        file_name1 =  file_standardize("test_file.eeg")
        file_name2 =  file_standardize("test_file_EXTRA.eeg")
    ```

- Every main feature function should contain docstrings (following [PEP 257](https://www.python.org/dev/peps/pep-0257/#multi-line-docstrings)) that follow the format of [MNE functions](https://github.com/mne-tools/mne-python/blob/maint/0.22/mne/io/egi/egi.py#L89-L154) and describe **at most** the following:
    - A brief description as to what the function does.
    - Parameters: which inputs will be provided to the function?
    - Throws: which exceptions will the function throw (if any)?
    - Returns: which inputs will be returned, and what changes will be made to them?
  
    Example:
    ```python
    def add_up(a, b):
        """A function that returns the sum of two inputs 
        Parameters 
        ----------
        a : int
            any integer
        b : in
            any integer

        Returns 
        ----------
        a + b
        """
        return a + b
    ```

    This documentation should be as **non-restrictive** as possible. That is, minimize implicit preconditions (don't make assumptions on user input) and maximize implicit postconditions. This will ensure that features are resilient and break correctly and informatively when improper input is provided. 

    Note that if the documentation for any of these categories is empty, it is not required to list it.  For example, a function that returns nothing will likewise have no "returns" listed in the docstring. 

- For [documenting classes](https://www.python.org/dev/peps/pep-0257/#multi-line-docstrings): "docstring for a class should summarize its behavior and list the public methods and instance variables."<br/>
    Example:
    ```python
    class Dog(Animal):
        """Dog class that can learn and execute tricks 
        
        Instance Variables
        ----------
        name: str
            the dog's name 
        tricks: list
            a list of strings that contain tricks in string form

        Public Methods
        ----------
        learn_trick(trick)
            method to take in "trick" and store it into tricks list
        
        do_trick()
            method to randomly print out a trick to console
        """
    ```

- Avoid magic numbers.<br/>
    For example, do this:
    ```python
    PI = 3.14159
    circumference = PI * Math.pow(radius, 2)
    ```
    ...not this:
    ```python
    circumference = 3.14159 * Math.pow(radius, 2)
    ```


## Containerization
- Updates to container content should be discrete and announced events. This will prevent unexpected behavior (sudden unsupported packages, changes in kernel, etc.) in local environments. 
