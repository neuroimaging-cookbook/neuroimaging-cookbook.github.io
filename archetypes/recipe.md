---
title: {{ replace .Name "-" " " | title }}
date: {{ .Date }}
tags: [extract, mask, roi, etc]
utilities: [cleaning, preprocessing, analysis, etc]
modalities: [fmri, smri, dmri, egg, meg, fnirs, etc]
languages: [python, r, bash, etc]
software: [afni, fsl, spm, nilearn, etc]

authors: [First Lastname]
github_handle: []
---

## Explain briefly what the recipe does.

- Explain briefly how the recipe works.
- Provide a citation and link to documentation of any third party software.
- Provide the version of the software/package
- Use bullet points for your recipe's explanation.
- Try to explain everything briefly but clearly.

To format code, add it between a pair of 3 ticks (`)

```py
def function_name(args):
  # code
  return 0
```


```py
function_name(val) # result
```
