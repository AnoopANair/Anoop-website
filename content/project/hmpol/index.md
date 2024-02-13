---
title: HM-POL Project
summary: Python package for calculating the higher order moments and polarizabilities from first principles.
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
# HM-POL

### Introduction

The HMPOL project focuses on using point charge perturbations to obtain the higher order polarizabilities, specifically the dipole-dipole, dipole-quadrupole and quadrupole-quadrupole polarizability. The code also has the functionality to calculate the higher order polarizabilities till the hexadecapole. It still under development.

### Running the code [with PYSCF]
    conda create --name HMPOL
    conda activate HMPOL
    pip3 install hmpol


copy the following H2O molecule geometry in a  **molecule.xyz** file

    3
    Properties=species:S:1:pos:R:3 pbc="F F F"
    O       -0.00000000       0.00000000       0.06664447
    H        0.76804750       0.00000000      -0.52889132
    H       -0.76804750       0.00000000      -0.52889132


And run the following script to test out the HMPOL implemetation with pyscf

    from pyscf import gto
    from ase.io import read
    from hmpol import Pols
    import numpy as np
    from ase.visualize import view
    from ase.units import Bohr, Ha


    mol = gto.Mole()
    molecule = read("molecule.xyz")
    mol.atom = "molecule.xyz" 
    mol.basis = "augccpvqz"
    mol.build()


    field_strength_F = 0.00486/Ha*Bohr


    pols = Pols(molecule,mol, irrep=False, field_strength_F=field_strength_F)

    print("dd polarizability")
    print(pols.calc_dd_pol())
    print("dq polarizability")
    print(pols.calc_dq_pol())
    print("qq polarizability")
    print(pols.calc_qq_pol())


#### Output

**dd polarizability**

    [[10.7822  0.      0.    ]
    [ 0.     10.4492  0.    ]
    [-0.      0.     10.5741]]

**dq polarizability**

    [[[ 0.     -0.     -8.4645]
    [-0.     -0.     -0.    ]
    [-8.4645 -0.     -0.    ]]

    [[ 0.     -0.     -0.    ]
    [-0.     -0.     -3.1742]
    [-0.     -3.1742  0.    ]]

    [[-1.2882  0.     -0.    ]
    [ 0.      4.6134 -0.    ]
    [-0.     -0.     -3.3252]]]

**qq polarizability**

    [[[[16.6621 -0.      0.    ]
    [-0.     -8.9976  0.    ]
    [ 0.      0.     -7.6646]]

    [[-0.     13.1964 -0.    ]
    [13.1964 -0.      0.    ]
    [-0.      0.      0.    ]]

    [[ 0.     -0.     15.2958]
    [-0.      0.      0.    ]
    [15.2958  0.     -0.    ]]]


    [[[-0.     13.1964 -0.    ]
    [13.1964 -0.      0.    ]
    [-0.      0.      0.    ]]

    [[-8.9976 -0.      0.    ]
    [-0.     17.9951 -0.    ]
    [ 0.     -0.     -8.8643]]

    [[ 0.      0.      0.    ]
    [ 0.     -0.     13.0965]
    [ 0.     13.0965 -0.    ]]]


    [[[ 0.     -0.     15.2958]
    [-0.      0.      0.    ]
    [15.2958  0.     -0.    ]]

    [[ 0.      0.      0.    ]
    [ 0.     -0.     13.0965]
    [ 0.     13.0965 -0.    ]]

    [[-7.6646  0.     -0.    ]
    [ 0.     -8.8643 -0.    ]
    [-0.     -0.     16.5288]]]]