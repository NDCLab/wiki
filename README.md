# wiki

Comprehensive NDC Lab documentation https://ndclab.github.io/wiki/

## Git Workflow 

![ndcworkflowmain](https://user-images.githubusercontent.com/26397102/119031107-521c6380-b970-11eb-8f8f-59c0dae17333.png)


Folder/branch organization should follow this convention:

`->main`
- Up to date and live production branch with properly reviewed changes
- *no direct commits*

`->main-feature-[featureName]`
- Ongoing development and testing of feature to be pull requested into `main` 
- *no direct commits*

`-->main-[featureName]-[yourName]`
- *only* branch available for personal development, must be branched off of `main-feature-[featureName]` branch
- Merged into `-->main-[featureName]-[featureName]` after a pull-request (code review)

## Directory/Navbar Structure 

```yml
wiki
├── _sass
├── docs
|    ├──Onboarding
|    ├──_assets
|    ├──general-information
|    ├──project-specific-docs
|    ├──technical-docs
|    ...
├── LICENSE
├── _config.yml
├── index.md
├── ndcwikiicon.png
...
```

* `_sass`
    * Contains sass styling files that control the color-scheme, font, and other NDC wiki styles ([light guide to sass](https://sass-lang.com/guide))

* `docs`
    * directory that details the navbar structure. Pages and sub-pages reside here.

    * `Onboarding`
        
        * `onboarding.md`
        * `accessing-hpc.md`
        * `certifications.md`
    
    * `docs/_assets`
        * images of the ndc wiki

* `_config.yml`
    * yaml file that details wiki meta-data (title, theme, logo, etc) 

* `index.md`
    * Home-page content
    ![image](https://user-images.githubusercontent.com/26397102/115584943-ce982580-a290-11eb-9f54-8d9b94957e21.png)

## Guide to Website Development

Jekyll theme detailed in original [developer repo](https://github.com/pmarsceill/just-the-docs)

### Building site on local
To view what the site would look like with the applied formatting and styles as seen on the live site, build a local copy using the listed steps. 

All commands listed in a quote-block are terminal commands. 

After completing the listed steps, only `bundle exec jekyll serve` is the only command needed to build the local site, unless the gem-files are updated. 

#### Windows/Linux 

1. Navigate to your system's root folder and install Ruby using the following [documentation](https://www.ruby-lang.org/en/documentation/installation/).

2. Install bundler and jekyll by running:
    > gem install jekyll bundler

3. Init the wiki using
    > bundle init 

4. This will create a gemfile called `Gemfile`. Add the following to this newly created file: 
    ```ruby
    gem "just-the-docs"
    gem "jekyll-remote-theme"
    ```

5. Install the newly listed gems using: 
    > bundle install

6. Add the following block anywhere in the `_config.yml` file
    ```yml
    plugins:
        - jekyll-remote-theme
    ```

7. Run the following command to build the website on your local machine. 
    > bundle exec jekyll serve

#### MacOS
MacOS comes with a default system installation for Ruby. However, it's advisable to use a seperate version of Ruby installed using "homebrew" to avoid permission errors.

1. Navigate to your system's root folder and install command-line-tools 
    > xcode-select --install

    > export SDKROOT=$(xcrun --show-sdk-path)

2. Install Homebrew by following the instructions on the [Homebrew homepage](https://brew.sh/) to paste a specific command into your Terminal.

3. Install Ruby using homebrew
    > brew install ruby

    > echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.bash_profile

5. Install bundler and jekyll by running:
    > gem install --user-install bundler jekyll

6. Navigate to your local `wiki` repository and initialize the repo.
    > cd wiki
    > bundle init 

7. This will create a gemfile called `Gemfile`. Add the following to this newly created file: 
    ```ruby
    gem "just-the-docs"
    gem "jekyll-remote-theme"
    ```

8. Install the newly listed gems using: 
    > bundle install

9. Add the following block anywhere in the `_config.yml` file
    ```yml
    plugins:
        - jekyll-remote-theme
    ```

10. Run the following command to build the website on your local machine. 
    > bundle exec jekyll serve

### Page Creation 

To create a page on the wiki and link it to the left-hand navigation bar, create the markdown file inside of the [docs/](https://github.com/NDCLab/wiki/tree/gh-pages/docs) directory and specify its' position on the navbar in the header.  

```yml
---
layout: default
title: <title>
nav_order: <navbar-ordinal>
---

# <title>
```

#### Working Example

The *contributing* tab on the wiki is placed on the 6th position in the navbar by specifying the following header in the [docs/contributing.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/contributing.md) file: 

```yml
---
layout: default
title: contributing
nav_order: 6
---

# Contributing 
// Rest of file continues here 
```

![image](https://user-images.githubusercontent.com/26397102/115580335-98f13d80-a28c-11eb-8fc2-e382e534d625.png)

### Parent & Child Page Creation 

To create a page/tab that contains sub-pages, create a directory inside of [docs/](https://github.com/NDCLab/wiki/tree/gh-pages/docs) named after the page/tab you plan on creating.

For example, to add a tab called `A` on the wiki navbar, create directory `docs/A/`. 

Next, create a markdown file inside of this directory and specify its position on the navbar and set the `has_children` tag to be `true`. 

```yml
---
layout: default
title: <title>
nav_order: <navbar-ordinal>
has_children: true
---

# <title>
```

To create child pages located underneath this parent page, create a markdown file also located in this directory and specify the parent title in the header: 

```yml
---
layout: default
title: <title>
parent: <parent-title> 
nav_order: <navbar-ordinal>
---

# <title>
```

#### Working Example

The *onboarding* tab on the wiki contains the child *accessing the hpc* in the navbar by specifying the following header in the [Onboarding/onboarding.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/Onboarding/onboarding.md) file:

```yml
---
layout: default
title: Onboarding
nav_order: 2
has_children: true
permalink: /docs/onboarding
---

# Onboarding
```

and the following directory structure:
```yml
wiki
...
├── docs
|    ├──Onboarding
|    |      ├── onboarding.md
```

followed by the [Onboarding/accessing-hpc.md](https://github.com/NDCLab/wiki/blob/gh-pages/docs/Onboarding/accessing-hpc.md) header: 

```yml
---
layout: default
title: Accessing the HPC
parent: Onboarding
nav_order: 2
---

## Accessing the HPC
```

located in the `docs/Onboarding/` directory

```yml
wiki
...
├── docs
|    ├──Onboarding
|    |     ├── onboarding.md
|    |     ├── accessing-hpc.md
```

![image](https://user-images.githubusercontent.com/26397102/115582028-28e3b700-a28e-11eb-9d05-1ac32db43609.png)
