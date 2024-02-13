---
title: SCME Project
summary: A polarizable potential for accurate and efficient solvent simulations
tags:
  - Deep Learning
date: '2016-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: 
  focal_point: Smart

links:
  - icon: twitter
    icon_pack: fab
    name: Follow
    url: https://twitter.com/georgecushen
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---


## Code compilation

### Install the dependences

Using conda: 

    conda create --name SCMEENV
    conda activate SCMEENV
    conda install -c conda-forge gpaw
    conda install -c conda-forge ase
    conda install cmake
    conda install -c conda-forge pybind11
    conda install -c conda-forge gcc
    conda install make

Using pip:

    pip3 install pybind11[global]

### Run the compilation script

    ./ex.sh


## Single Center Expansion
We write the electrostatic potential as


$V(r) = \frac{\mu_\alpha r_\alpha}{r^3} + \frac{\theta_{\alpha\beta}r_\alpha r_\beta}{r^5} + \frac{\Omega_{\alpha\beta\gamma}r_\alpha r_\beta r_\gamma}{r^7} + \frac{\Phi_{\alpha\beta\gamma\delta}r_\alpha r_\beta r_\gamma r_\delta}{r^9}$
