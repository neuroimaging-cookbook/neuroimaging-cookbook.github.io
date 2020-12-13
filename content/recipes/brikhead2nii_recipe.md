---
title: Using 3dAFNItoNIFTI to convert AFNI files to NIFTI files
tags: [convert, brik, head, nifti]
modality: [fmri, smri, dmri]
language: [bash]
software: [AFNI]
---

This recipe converts BRIK/HEAD (AFNI) files to NIFTI (.nii) files using 3dAFNItoNIFTI.
https://afni.nimh.nih.gov/pub/dist/doc/program_help/3dAFNItoNIFTI.html



```bash
#!/bin/bash

3dAFNItoNIFTI -prefix prefixname dataset
```