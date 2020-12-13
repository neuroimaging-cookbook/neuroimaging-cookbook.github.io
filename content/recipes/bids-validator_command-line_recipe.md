---
title: BIDS Validation Recipe
date: 2020-12-13
tags: [bids, bids-validator, command line, bids apps]
utility: [preprocessing]
modalities: [all]
languages: [bash]
software: [bids-validator, npm]

authors: [Arshitha Basavaraj]
github_handle: [Arshitha]
---

This recipe uses the `bids-validator` command line tool to verify if a specified dataset conforms to the 
BIDS specification [1](#ref1). This recipe uses v1.5.7 of the bids-validator

This is an especially important step if you intend to uses any of the BIDS Apps [2](#ref2)like fMRIPrep, MRIQC, etc [3](#ref3) 

## Ingredients
- Node.js (at least version 10.11.0) [Installation](https://nodejs.org/en/)

## Prep
- Install bids-validator [3](#ref4)
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


<!-- ## Common Errors with Solutions
BIDS Validator errors are quite informative so cross referencing those with BIDS specification [1](#ref1) would answer most of your questions. If not, there's always Neurostars! It's been an incredibly valuable resource  -->

## Sources 
<a name="ref1"></a>[BIDS Specification](https://bids-specification.readthedocs.io/en/stable/)
<a name="ref2"></a>[BIDS Apps](https://bids-apps.neuroimaging.io/)
<a name="ref3"></a>[Available BIDS Apps](https://bids-apps.neuroimaging.io/apps/)
<a name="ref4"></a>[BIDS Validator GitHub Page](https://mail.google.com/mail/u/0/#inbox)