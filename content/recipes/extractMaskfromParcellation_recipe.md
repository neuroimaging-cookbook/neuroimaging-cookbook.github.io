---
title: Using 3dcalc to create a binary mask from a parcellation scheme
date: 2020-12-14
tags: [extract, mask, binarize, parcellation, roi]
utility: [processing]
modality: [fmri, smri, dmri]
language: [bash]
software: [afni]

authors:
- name: Shawn Rhoads
  github_handle: shawnrhoads
---

This recipe uses 3dcalc in AFNI to output a binarized 3D image file (nifti) of a region-of-interest in a parcellation scheme that is indexed by number of parcels.

Ingredients:
- [AFNI>=20.3.03](https://afni.nimh.nih.gov/pub/dist/doc/htmldoc/index.html)
- [3dcalc](https://afni.nimh.nih.gov/pub/dist/doc/program_help/3dcalc.html)

## Example usage:
```bash
#!/bin/bash

ATLAS_FILENAME='Harvard_Oxford_Atlas.nii.gz'
MASK_NAME='r_amygdala'
ROI_INDEX=102 # index assigned to parcel/region of interest in atlas parcellation scheme (the index for right amygdala in Harvard Oxford atlas is 102)

3dcalc -a ${ATLAS_FILENAME} -prefix ${MASK_NAME}.nii.gz -expr "amongst(a,${ROI_INDEX})"
```

You can also extract all parcels using a .txt file containing a parcel name on each row:
```bash
#!/bin/bash

ATLAS_FILENAME='Harvard_Oxford_Atlas.nii.gz'
MASKLIST_FILENAME='Harvard_Oxford_Atlas_ROIs.txt'

ROI_INDEX=0
for MASK_NAME in $(cat "${MASKLIST_FILENAME}); do
    ROI_INDEX=$((COUNTER+1))
    3dcalc -a ${ATLAS_FILENAME} -prefix ${MASK_NAME}.nii.gz -expr "amongst(a,${ROI_INDEX})"
done
```