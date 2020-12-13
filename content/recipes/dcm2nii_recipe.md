---
title: Convert DICOM files to NIFTI files
date: 2020-12-13
tags: [convert, dicom, nifti]
utilities: [cleaning, preprocessing]
modalities: [fmri, smri, dmri]
language: [python]
software: [AFNI]

authors:
- name: Bari Fuchs
  github_handle: bfuchs18
---

This recipe provides code for converting DICOM (.dcm) files to NIFTI (.nii) files

## dcm2niix
- This recipe converts dicom to nifti files using the program dcm2niix
- https://github.com/rordenlab/dcm2niix
- The only required argument for dcm2niix is the location of the folder with the DICOM files to convert, which is always the final argument provided.


```
# install dcm2niix (for mac)
curl -fLO https://github.com/rordenlab/dcm2niix/releases/latest/download/dcm2niix_mac.zip

# convert dicom files found in dicomdir, output to outdir
dcm2niix -o ~/outdir ~/dicomdir
```


## dcm2niibatch (batch conversions)
- https://github.com/rordenlab/dcm2niix/blob/master/BATCH.md
- Use dcm2niibatch to perform batch conversion of multiple dicoms using the configurations specified in a yaml file
- See github link above for yaml file format
```
dcm2niibatch batch_config.yml
```

## dcm2niix_afni (AFNI)
- This recipe will use afni's dcm2niix_afni to convert dicom files found in ~/dicomdir to nifti files, and output converted files into ~/outputdir
- For additional examples and options, see: https://afni.nimh.nih.gov/pub/dist/doc/program_help/dcm2niix_afni.html
```bash
#!/bin/bash 
dcm2niix_afni -o ~/outputdir ~/dicomdir
```


## dicom2nifti (python)
- This recipe will use the python library dicom2nifti to convert dicom files to nifti files
- https://github.com/icometrix/dicom2nifti

``` python
# install using pip
pip install dicom2nifti

# Run
import dicom2nifti

# run from commandline:
dicom2nifti /dicom_directory /output_directory

# run from python: 
dicom2nifti.convert_directory(dicom_directory, output_directory, compression=True, reorient=True)
```
