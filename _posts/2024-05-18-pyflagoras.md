---
title: Pyflagoras - Pride Flag Colour Picker
author: Annabel
date: 2024-05-18 12:07:00 +/-TTTT
categories: 
    - showcase     # TAG names should always be lowercase
    - project
tags: thrive
---

## Project Overview
Pyflagoras is a Python project and command-line interface tool to generate pride flags (in the `.svg` format) from an image. It's inspired by an online trend of (manually) colourpicking pride flags from colourful photos - in particular, the Twitter account [@prideflagbot](https://twitter.com/prideflagbot).

This tool has been tested on Windows 10 and Linux (VM running Debian 12, as seen in the preview). 

<center><video width="560" height="315" src= "/assets/img/posts/project-pyflagoras.mp4"></video></center>

## Installation
Run the following in your terminal (e.g Command Prompt).
```python
pip install pyflagoras
```

Alternatively, you can clone and build the repository from source. 

1. Obtain a copy of the source code with Git.
    ```bash
    git clone https://github.com/phthallo/pyflagoras
    ```
2. `cd` into the project folder and build it (you'll need the build tool beforehand -  `pip install build`)
    ```bash
        py -m build
    ```
3. Install the wheel using the following. Replace `x.x.x` with Pyflagoras' version number.
    ```bash
        py -m pip install dist/pyflagoras-x.x.x-py3-none-any.whl
    ```

## Usage
To generate a pride flag from an image, you'll need a path to the image and the ID of the pride flag to use. For instance:
```python
pyflagoras -f transgender_1999 
```

Run the following to bring up a help menu (also shown below). 

If you run into errors or issues, use the `--verbose` flag to bring up more information about the processes currently running. 

```python
pyflagoras -f transgender_1999 image.png
```

```
usage: pyflagoras [-h] [-f FLAG] [-n NAME] [--verbose] [--version] [-l] image

A command line interface tool to generate pride flags from images.

positional arguments:
  image                 Path to the image to generate a flag from.
                        Examples:
                            image.png
                            foo/bar/image.jpg

options:
  -h, --help            show this help message and exit
  -f FLAG, --flag FLAG  The ID (<flag_name>_<year_of_release>) of the flag to generate.
                        Examples:
                            intersexInclusive_2021
                            nonbinary_2014
                        Default:
                            progressPride_2018
  -n NAME, --name NAME  Customise the name of the final .svg. The following can be used as part of the file name:
                        Format placeholders:
                            {n}: File name (e.g celeste_classic)
                            {N}: File name (full) (e.g celeste_classic.png)
                            {f}: Flag name (e.g Progress Pride)
                            {F}: Flag ID (e.g progressPride_2018)
                        Examples:
                            pyflagoras celeste_classic.png -n "{f}_{n}" [renders Progress Pride_celeste_classic.svg]
                        Default:
                            {n}_{F} [renders celeste_classic_progressPride_2018.svg]

  --verbose             Enable verbosity (for general info and debugging)
  --version             show the program's version number and exit
  -l, --list            show all flag ids and exit

Documentation, issues and more: https://github.com/phthallo/pyflagoras
```

Visit this project's [repo](http://github.com/phthallo/pyflagoras) for the source code, and to open an issue/contribute :)

Happy Pride!