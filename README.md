# `empirical-manual` README

Welcome to Cornell Policy Group Applied Policy Lab's Empirical Project Manual! 

> If you are a CPG APL *analyst* looking to access the manual site, please visit https://cornellpolicygroup.github.io/empirical-manual/

> If you are a CPG APL *administrator*, please review this README for details on how to manage this live empirical project guidebook. Please update this README and other relevant documentation as necessary for posterity.

## Overview

This repo contains all the source files used to build our empirical project manual site. This README will cover the structure of this repo as well as the mechanisms by which changes are deployed to the live site.

## General Notes

- This manual is built as a Jupyter Book and deployed using GitHub Pages
- When updating the manual, all you need to do is to write changes locally and push them to the repo. Actions (specifically, the `deploy-jupyter-notebook.yml` workflow) will take care of building and deploying the notebook to GitHub Pages.
- For support, visit https://jupyterbook.org/en/stable/intro.html or ask ChatGPT (seriously, it's great).

> **Hey! Did you contribute pages to this manual?** You deserve credit! Add your name and graduation year to the "Author" line in `_config.yml`. The structure should look like:

```
author:
  - Elliott Serna '27
  - Jane Doe '26
  - John Smith '28 
```

## Repo Structure

In general, this repo follows the structure:

```
empirical-manual/
├── _build/
│   └── [built output files]                # Generated files after build (e.g., HTML, PDFs)
├── _config.yml                             # Configuration file for the project (e.g., site settings, theme)
├── _toc.yml                                # Defines the table of contents and structure of the manual
├── content/
│   ├── XX-Name.md                          # Section (e.g., 01-Ab-Initio.md for major topics)
│   ├── XX-YY-Name.md                       # Subsection (e.g., 03-01-Abstract.md for subsections of a section)
│   ├── XX-YY-ZZ-Name.md                    # Sub-subsection (e.g., 08-01-03-Variability.md for more detailed breakdowns)
│   ├── citations.md                        # Bibliography or citation-related content
│   └── images/                             # Images used throughout the manual
│       └── [image files]                   # Image files such as .png, .jpg, etc.
├── index.md                                # Main entry page or introduction to the manual
├── logo.png                                # Logo for the manual/project
├── references.bib                          # BibTeX file for citations and references
└── requirements.txt                        # Python dependencies required for building the manual
```

Some highlights include:

- `index.md` is the content file for the front (main) page of the manual.
- `_toc.yml` is the table of contents file that manages the website structure and encodes the navigation bar on the website.
- `content/` is where all content pages within different sections are housed. All files here will be markdown (.md) files.
- `_build/` is where all source files are outputted as files readable by GitHub Pages (e.g., from markdown to HTML). These are auto-generated everytime you push changes to the repo.

Though you will seldom have to edit the other files, it's helpful to know:

- `references.bib` is a BibTeX (used in LaTeX) file where you can add references and citations you may include on content pages.
- `_config.yml` is a backend file that sets the paramaters by which the manual will be built and displayed. Learn more at https://jupyterbook.org/customize/config.html
- `logo.png` is the CPG logo displayed on the site. If the logo ever changes, you can change this file, just be sure to rename it as `logo.png`.
- `requirements.txt` are any Python packages (dependencies) you may need to build the manual.

## GitHub Actions

Much of the build and deployment process is automized by the `deploy-jupyter-notebook.yml` workflow run within GitHub itself. This workflow buids and deploys changes to the GitHub Pages site every time you push any changes to this repo.

What is helpful to know for debugging is that all *source* files (e.g., content .md files, images, etc.) are housed on the `main` branch. When you push changes, then, push them to `main`. Actions will take automize everything from within `main` and deploy to the site.

There exists a `gh-pages` branch as well. This is a carry-over from having to manually build and deploy the manual without an automized workflow. This branch is now defunct.


## Contact

For general help, visit https://jupyterbook.org/en/stable/intro.html, ask ChatGPT, or contact CPG leadership. 

> If needed, this manual was initially built by Elliott Serna '27. Feel free to contact him at es2242@cornell.edu for more structural or contextual questions pertinent to this particular project.
