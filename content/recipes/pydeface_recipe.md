---
title: PyDeface Recipe
date: 2020-12-13
tags: [pydeface, defacing, multiple modalities defacing]
utilities: [defacing]
modalities: [all]
languages: [python]
software: [pydeface, FSL]

authors: [Arshitha Basavaraj]
github_handle: [Arshitha]
---

## Defacing Brain MRI using PyDeface 

For this recipe, we are using pydeface-2.0.0. 

## Ingredients: 
- A python environment with the following dependencies: 
  - FSL 6.0.2
  - Python 3.7.3
  - NumPy 1.17.1
  - NiBabel 2.5.1
  - Nipype 1.3.0-rc1

## Installation: 
- `pip install pydeface`

## Usage 
```bash
$ pydeface --help
# bash output
--------------
pydeface 2.0.0
--------------
usage: pydeface [-h] [--outfile path] [--force] [--applyto  [...]] [--cost mutualinfo] [--template path] [--facemask path] [--nocleanup] [--verbose]
                [--debug]
                path

positional arguments:
  path               Path to input nifti.

optional arguments:
  -h, --help         show this help message and exit
  --outfile path     If not provided adds '_defaced' suffix.
  --force            Force to rewrite the output even if it exists.
  --applyto  [ ...]  Apply the created face mask to other images. Can take multiple arguments.
  --cost mutualinfo  FSL-FLIRT cost function. Default is 'mutualinfo'.
  --template path    Optional template image that will be used as the registration target instead of the default.
  --facemask path    Optional face mask image that will be used instead of the default.
  --nocleanup        Do not cleanup temporary files. Off by default.
  --verbose          Show additional status prints. Off by default.
  --debug            Do not catch exceptions and show exception traceback (Drop into pdb debugger).
```

## Example Usage
- **Case 1**: Using default facemask and template  
	For a dataset with only T1w images, the defaults do a good job of defacing
```bash
$ mkdir pydeface-out
$ pydeface infile_T1w.nii.gz --outfile ./pydeface-out/infile_T1w_defaced.nii.gz
```
- **Case 2**: Using subject-specific templates with the `--template` flag 
Example directory tree of a sample dataset with multiple modalities
```bash
sample-dataset
├── sub-01
│   ├── sub-01_ses-01_T1w.nii.gz
│   └── sub-01_ses-01_FLAIR.nii.gz
└── sub-02
    ├── sub-02_ses-01_T1w.nii.gz
    ├── sub-02_ses-01_T2w.nii.gz
    └── sub-02_ses-01_T2star.nii.gz
```

Commands to deface `sub-02` are shown below. 

```bash
$ cd ./sub-02
$ pydeface sub-02_ses-01_T1w.nii.gz
``` 
This will output a defaced image with `sub-02_ses-01_T1w_defaced.nii.gz`

```bash
$ pydeface sub-02_ses-01_T2w.nii.gz --template sub-02_ses-01_T1w.nii.gz 
$ pydeface sub-02_ses-01_T2star.nii.gz --template sub-02_ses-01_T1w.nii.gz  
```

Final directory tree:
```bash
sample-dataset
├── sub-01
│   ├── sub-01_ses-01_T1w.nii.gz
│   └── sub-01_ses-01_T2w.nii.gz
└── sub-02
    ├── sub-02_ses-01_T1w.nii.gz
    ├── sub-02_ses-01_T1w_defaced.nii.gz
    ├── sub-02_ses-01_T2star.nii.gz
    ├── sub-02_ses-01_T2star_defaced.nii.gz
    ├── sub-02_ses-01_T2w.nii.gz
    └── sub-02_ses-01_T2w_defaced.nii.gz
```

## Sources: 
- [pydeface github page](https://github.com/poldracklab/pydeface)
- [t2w scan defacing](https://github.com/poldracklab/pydeface/issues/20#issue-300281118)

