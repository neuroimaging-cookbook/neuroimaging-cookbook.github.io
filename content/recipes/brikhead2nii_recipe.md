---
title: Using 3dAFNItoNIFTI to convert AFNI files to NIFTI files
date: 2020-12-13
tags: [convert, brik, head, nifti]
utilities: [cleaning, preprocessing]
modality: [fmri, smri, dmri]
language: [bash]
software: [AFNI]

authors:
- name: [Bari Fuchs]
  github_handle: [bfuchs18]
---

This recipe converts BRIK/HEAD (AFNI) files to NIFTI (.nii) files using 3dAFNItoNIFTI.
https://afni.nimh.nih.gov/pub/dist/doc/program_help/3dAFNItoNIFTI.html



```bash
#!/bin/bash

3dAFNItoNIFTI -prefix prefixname dataset
```