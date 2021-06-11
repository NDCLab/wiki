---
layout: default
title: Programming Standards
parent: Etiquette
nav_order: 2
---

### Contents

## Python

- Global variables should not be used

- Leave out return types and parameter types in the function header.
    Example: Do this,
    ```python
    def funcName(a, b):
        ...
    ```
    Not this,
    ```python
    def funcName(a: int, b: int) -> int:
        ...
    ```

- Compartmentalize features into modules. 
    Example: 
    ```python
    import final-reject as fj
    fj.final_reject(raw)
    ```

- Each function should have responsibility for a **single** part of its' module's functionality. Functions that do multiple things should be broken into multiple functions. This ensures reusability & relaxes cognitive load. 
     - If a function is running into >100 lines of code or contains some potentially reusable code, and is not inseparable, further decompose the function into helper functions. 
    Example:
    ```python
    def funcName(a, b):
        # remove extension and other characters for file 
        file_name1 =  "test_file.eeg".lower().replace("-", "").replace("_", "").replace(" ", "")
        file_name1 =  filename[:-4] 

        # do same for other file
        file_name 2=  "test_file_EXTRA.eeg".lower().replace("-", "").replace("_", "").replace(" ", "")
        file_name2 =  filename[:-4] 
    ```

    can be decomposed into

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
    - ~~Preconditions: what input preconditions should the user of the function abide by to ensure correct behavior.~~
    - ~~Postconditions: what will the function guarantee in its output.~~
    - Throws: which exceptions will the function throw (if any).
    - ~~Modifies: which inputs will be modified (if any).~~
    - Returns: which inputs will be returned, and what changes will be made to them.
    - ~~A small example of how the function should work, if needed.~~
  
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

        Postconditions
        ----------
        add_up(a, b) == a + b

        Returns 
        ----------
        a + b
        """
        return a + b
    ```

    This documentation should be as **non-restrictive** as possible. That is, minimize implicit preconditions (don't make assumptions on user input) and maximize implicit postconditions. This will ensure that features are resilient and break correctly and informatively when improper input is provided. 

    Note that if the documentation for any of these categories is empty, it is not required to list it.  For example, a function that returns nothing will likewise have no "returns" listed in the docstring. 

- Follow function, variable, package, and file-naming standards listed in issue #25.
---------------------FROM JESS, #25 IS NOW THE NAMING CONVENTIONS WIKI PAGE FOR YOUR CROSS-REFERENCING


- Every repository should have a succinct `readme.md` that guides development and points to relevant data.
---------------------FROM JESS, THE ABOVE WILL BE INCORPORATED INTO GITHUB ETIQUETTE OR GITHUB TEMPLATES, YOU CAN DELETE HERE

- for [documenting classes](https://www.python.org/dev/peps/pep-0257/#multi-line-docstrings): "docstring for a class should summarize its behavior and list the public methods and instance variables. 
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

## Containerization
- Updates to container content should be discrete and announced events. This will prevent unexpected behavior (sudden unsupported packages, changes in kernel) in local environments. 





---------------------FROM YANBIN, TO ADD
1. Jess incorporated this one into naming-conventions.md already.

2. Something might be added into commenting besides your perfect example:
Leave author info at the beginning of python files, including original author and authors who modified code (not only for credit, but also for the person that we can turn to), example:

```
# Authors: xxx <xxx@xxx.com> - original Author
#          xxx <xxx@xxx.com> - fix the bug for xxx
```

for authors who modify code should also comment in the place where the modification happens. 
```
# fix the bug for xxx by who
math.floor(a + b)
```

3. Avoid magic numbers.
---------------------FROM YANBIN, TO ADD
