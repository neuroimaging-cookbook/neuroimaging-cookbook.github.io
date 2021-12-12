---
title: Extract BOLD time-series data from parcellation atlas or ROI using AFNI 
date: 2021-12-12
tags: [extract, time-series, roi, parcellation]
utility: [processing]
languages: [bash]
modalities: [fMRI]
software: [afni]

authors:
- name: Junaid S Merchant
  github_handle: JunaidMerchant
---

## Extracting BOLD time-series data from parcellation atlas or ROI using AFNI. 

This recipe allows you to extract parcel- or ROI-averaged time-series data from 4D functional MRI file and optionally print it to a text file. If using a parcellation atlas, this will output each parcel's time-series data as rows in a tab-separated text file. This is particularly useful if you are wanting to create functional connectivity matrices or conduct an inter-subject correlation analysis. 
- Can handle fMRI files in any format (.nii, .nii.gz, BRIK/HEAD)
- Important: requires ROI and BOLD files are of the same resolution. 

## Requirements 
- `afni` [installation](https://afni.nimh.nih.gov/pub/dist/doc/htmldoc/background_install/main_toc.html), in particular, `3dROIstats` function from afni. [full usage](https://afni.nimh.nih.gov/pub/dist/doc/program_help/3dROIstats.html)
- `bash`

## Usage (basic)
This is the basic usage that would print the averaged-time series data to screen. If you give a parcellation atlas as the mask file, this will output averaged time series data for each parcel in columns:
```
3dROIstats -mask ${ROI_FILE} ${4D_BOLD_FILE}
```

## Usage (to print to file)
This is approach will write the extracted time-series data to tab-separated text file that can be opened with excel for example. It will include columns/headers (input) File, Sub-brick (which individual 3D file), and columns for each ROI/parcel. To exclude the columns for input filename/sub-brick and column headers, use -quiet option:
```bash
3dROIstats -mask ${ROI_FILE} ${4D_BOLD_FILE} > ${OUTPUT_TEXT_FILE}
```

## Example - looping through numerous participants, and writing their time-series data to files
This example utilizes the approach aboven to extract data from a sample of participants. 
```bash
# Define subject level files and subject directory (where subject data is)
SUBJECTS=("subj_01" "subj_02" "subj_03")
SUBJ_DIR="/path/to/subject_directory"

# Define ROI or parcellation atlas
ROI_FILE="/path/to/roi_file.nii.gz"

# Define output directory
OUT_DIR="/path/to/output_directory"

# Now loop through
for subject in ${SUBJECTS}; do

	# Run 3dROIstats as before, but add in filename suffix and extensions for BOLD and output files
	3dROIstats -mask ${ROI_FILE} ${SUBJ_DIR}/${subject}_4D_BOLD.nii.gz > ${OUT_DIR}/${subject}_timeseriesdata.txt

done
```
