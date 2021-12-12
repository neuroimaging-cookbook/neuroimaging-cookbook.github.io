---
title: Contributing to the Neuroimaging Cookbook
date: 2020-12-14
tags: [template, getting started]
languages: [python, markdown]
modalities: [fMRI]
software: [github]

authors:
- name: Shawn Rhoads
  github_handle: shawnrhoads
---

The title entered above will automatically appear here, so just start by explaining the recipe purpose of your recipe.

**Here are some guidelines for writing your recipe**:
- Explain briefly how the recipe works.
- Provide a link to documentation of any third-party software when possible.
- Provide the version of the software/package.
- Use bullet points for your recipe's explanation.
- Try to explain everything briefly but clearly.
- If you provide a custom function, then please provide a usage example below.

**Here are some guidelines for submitting your recipe**:
- Please use [Markdown](https://www.markdownguide.org/basic-syntax/)
- Your recipe should be concise. **Please do not exceed 100 lines.**
- Your code snippet should be roughly 1-10 lines
- Write your recipe to `content/recipes/*.md'
- Follow this heuristic for saving your recipe: `content/recipes/<user-defined-name>_recipe.md`
- If necessary, any images associated with a recipe should follow a heuristic: `content/recipes/<user-defined-name>_image_<index>.jpg`
- Please include software versions and links to software documentation when possible

Ingredients:
- Please list any software packages (and dependencies) required for this recipe

Your code snippet should be written in the code cell below. Please remember to specify the programming language used (the one below uses Python).
```py
def function_name(args):
  # code
  return 0
```

## Example usage:
If your code snippet includes a custom function, then please provide an example (or two) to demonstrate how it works in the code cell below. Please remember to specify the programming language used (the one below uses Python).
```py
function_name(val) # result
```

You can submit your recipe by copying the text from this template [HERE](https://raw.githubusercontent.com/neuroimaging-cookbook/neuroimaging-cookbook.github.io/main/content/template_recipe.md) and submiting your recipe by submitting a pull request.

Alternatively, you can suggest a recipe below.

{{< button "https://github.com/neuroimaging-cookbook/neuroimaging-cookbook.github.io/issues/new?assignees=shawnrhoads&labels=recipe&template=recipe-template.yml&title=%5BRecipe%5D%3A+" "Suggest new recipe" >}}
