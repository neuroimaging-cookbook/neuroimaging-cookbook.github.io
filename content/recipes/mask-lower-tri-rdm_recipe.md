---
title: Mask lower triangle of a Representational Dissimilarity Matrix (RDM)
tags: [vectorize, flatten, representational similarity, connectivity, functional connectivity, structural connectivity, rdm, lower triangle, mask, array, matrix]
utility: [preprocessing]
modality: [any]
language: [python]
software: [numpy]
---

This recipe takes a Representational Dissimilarity Matrix (RDM) as a square numpy array, masks the diagonal and lower triangle, and outputs a flattened numpy array of the upper triangle. 

Easily adaptable for Representational Similarity Analysis (RSA), Functional/Structural Connectivity analyses, or other analyses with related pipelines with symmetric, square matrices.

```py
def flatten_matrix(square_matrix):
    assert square_matrix.shape[0] == square_matrix.shape[1], "Must be a square numpy array"
    
    # mask the diagonal and lower triangle and output flattened array
    vector_of_edges = square_matrix[np.triu_indices(len(square_matrix), k=1)] 

    return vector_of_edges
```

## Example usage:
```py
import pandas as pd, numpy as np

square_matrix = np.array([[1,0,0,0],
                          [0,1,0,0],
                          [0,0,1,0],
                          [0,0,0,1]])

flatten_matrix(square_matrix)
```
Recipe by [Shawn Rhoads](https://github.com/shawnrhoads)