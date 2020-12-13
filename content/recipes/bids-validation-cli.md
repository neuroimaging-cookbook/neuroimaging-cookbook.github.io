---
title: BIDS Validation Recipe
date: 2020-12-13
tags: [bids, bids-validator, command line, bids apps]
utility: [preprocessing]
modalities: [all]
languages: [bash]
software: [bids-validator, npm]

authors:
- name: Arshitha Basavaraj
  github_handle: Arshitha
---

## Validating BIDS formatted Datasets using `bids-validator` Command Line Tool 

This recipe uses the `bids-validator` v1.5.7 command line tool to verify if a specified dataset conforms to the 
BIDS specification [\[1\]](#ref1). There are other ways to use the bids-validator, this is just one of the methods.

This is an especially important step if you intend to uses any of the BIDS Apps [\[2\]](#ref2)like fMRIPrep, MRIQC, etc [\[3\]](#ref3) 

## Ingredients
- Node.js (at least version 10.11.0) [Installation](https://nodejs.org/en/)

## Prep
- Install bids-validator [\[3\]](#ref4)
  ```bash
  $ npm install -g bids-validator
  ```
  If you run into `Permission denied` related errors, try:
  ```bash
  $ sudo npm install -g bids-validator
  ```

## Usage
If the installation was successful, running `bids-validator --help` on your terminal should give you the following output:

```bash
Usage: bids-validator <dataset_directory> [options]
Options:
  --help, -h                  Show help                                [boolean]
  --version, -v               Show version number                      [boolean]
  --ignoreWarnings            Disregard non-critical issues            [boolean]
  --ignoreNiftiHeaders        Disregard NIfTI header content during validation
                                                                       [boolean]
  --ignoreSubjectConsistency  Skip checking that any given file for one subject
                              is present for all other subjects.       [boolean]
  --verbose                   Log more extensive information about issues
                                                                       [boolean]
  --json                      Output results as JSON                   [boolean]
  --ignoreSymlinks            Skip any symlinked directories when validating a
                              dataset                                  [boolean]
  --remoteFiles               Validate remote files.  [boolean] [default: false]
  --gitTreeMode               Improve performance using git metadata. Does not
                              capture changes not known to git.        [boolean]
  --gitRef                    Targets files at a given branch, tag, or commit
                              hash. Use with --gitTreeMode.  [default: "HEAD"]
                                                                        [string]
  --config, -c                Optional configuration file. See
                              https://github.com/bids-standard/bids-validator
                              for more info
                                        [default: ".bids-validator-config.json"]
This tool checks if a dataset in a given directory is compatible with the Brain
Imaging Data Structure specification. To learn more about Brain Imaging Data
Structure visit http://bids.neuroimaging.io
```
## Examples
Initial `sample-dataset` directory structure: 
```bash
sample-dataset
├── derivatives
│   └── pydeface-2.0.0
│       ├── sub-01
│       │   ├── sub-01_ses-01_T1w_defaced.nii.gz
│       │   └── sub-01_ses-01_T2w_defaced.nii.gz
│       └── sub-02
│           ├── sub-02_ses-01_T1w_defaced.nii.gz
│           ├── sub-02_ses-01_T2star_defaced.nii.gz
│           └── sub-02_ses-01_T2w_defaced.nii.gz
├── participants.json
├── participants.tsv
├── sub-01
│   └── ses-01
│       └── anat
│           ├── sub-01_ses-01_T1w.json
│           ├── sub-01_ses-01_T1w.nii.gz
│           ├── sub-01_ses-01_T2w.json
│           └── sub-01_ses-01_T2w.nii.gz
└── sub-02
    └── ses-01
        └── anat
            ├── sub-02_ses-01_T1w.json
            ├── sub-02_ses-01_T1w.nii.gz
            ├── sub-02_ses-01_T2star.json
            ├── sub-02_ses-01_T2star.nii.gz
            ├── sub-02_ses-01_T2w.json
            └── sub-02_ses-01_T2w.nii.gz
10 directories, 17 files
```
Now I'll run the `bids-validator` without any optional flags:
```bash
$ bids-validator sample-dataset
```
My terminal output:
```bash
bids-validator@1.5.7
  1: [ERR] The compulsory file /dataset_description.json is missing. See Section 03 (Modality agnostic files) of the BIDS specification. (code: 57 - DATASET_DESCRIPTION_JSON_MISSING)
  Please visit https://neurostars.org/search?q=DATASET_DESCRIPTION_JSON_MISSING for existing conversations about this issue.
  1: [WARN] Not all subjects contain the same files. Each subject should contain the same number of files with the same naming unless some files are known to be missing. (code: 38 - INCONSISTENT_SUBJECTS)
    ./sub-01/ses-01/anat/sub-01_ses-01_T2star.json
      Evidence: Subject: sub-01; Missing file: sub-01_ses-01_T2star.json
    ./sub-01/ses-01/anat/sub-01_ses-01_T2star.nii.gz
      Evidence: Subject: sub-01; Missing file: sub-01_ses-01_T2star.nii.gz
  Please visit https://neurostars.org/search?q=INCONSISTENT_SUBJECTS for existing conversations about this issue.
  2: [WARN] The recommended file /README is missing. See Section 03 (Modality agnostic files) of the BIDS specification. (code: 101 - README_FILE_MISSING)
  Please visit https://neurostars.org/search?q=README_FILE_MISSING for existing conversations about this issue.
        Summary:                 Available Tasks:        Available Modalities:
        12 Files, 38.63MB                                T1w
        2 - Subjects                                     T2w
        1 - Session                                      T2star
  If you have any questions, please post on https://neurostars.org/tags/bids.
```
So, we have one tiny error and two warnings but as you can see, the error messages are quite detailed.
- Errors
Adding a `dataset_description.json` file should fix the errors. See [here](https://bids-specification.readthedocs.io/en/stable/03-modality-agnostic-files.html#dataset-description) on how to create one 
- Warnings 
  1. Most datasets don't have acquisitions with the same modalities so this warning could be ignored. Including the `--ignoreSubjectConsistency ` should take of this. 
  2. A README file is recommended not `required` so we could ignore this too. Including the `--ignoreWarnings` flag should fix this. 
Let's see if these changes fixes it: 
```bash
$ bids-validator sample-dataset --ignoreSubjectConsistency --ignoreWarnings
```
woohoo!
```bash
This dataset appears to be BIDS compatible.
        Summary:                 Available Tasks:        Available Modalities:
        13 Files, 38.63MB                                T1w
        2 - Subjects                                     T2w
        1 - Session                                      T2star
  If you have any questions, please post on https://neurostars.org/tags/bids.
```
We now have valid BIDS dataset! 
<!-- ## Common Errors with Solutions
BIDS Validator errors are quite informative so cross referencing those with BIDS specification [1](#ref1) would answer most of your questions. If not, there's always Neurostars! It's been an incredibly valuable resource  -->
## Sources 
<a name="ref1"></a>[BIDS Specification](https://bids-specification.readthedocs.io/en/stable/)
<a name="ref2"></a>[BIDS Apps](https://bids-apps.neuroimaging.io/)
<a name="ref3"></a>[Available BIDS Apps](https://bids-apps.neuroimaging.io/apps/)
<a name="ref4"></a>[BIDS Validator GitHub Page](https://github.com/bids-standard/bids-validator)
<a name="ref5"></a>[Modality Agnostic Files](https://bids-specification.readthedocs.io/en/stable/03-modality-agnostic-files.html)