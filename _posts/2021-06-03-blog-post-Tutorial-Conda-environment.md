---
title: 'Conda environment management'
date: 2021-06-03
permalink: /posts/2021/05/Conda environment/
tags:
  - Virtual Environment
  - Conda
categories:
  - Coding
  - Tutorial
---


Conda environment management
======

[documentation link](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) 

## 1. Important commands

1. Check existing environments
```
conda env list
```

2. Create an environment
```
conda create -n myenv
```
or 
```
conda create --name myenv
```
- if we want to create enviroment with specific python version:
```
conda create -n myenv python=3.6
```
- if we want to create environment with specific packages with specific version:
```
conda create -n myenv scipy=0.15.0 numpy 
```
- we can also install packages after creating environment
```
conda install -n myenv scipy

```
- To clone(duplicate) an environment
```
conda create --name newenv --clone myenv
```

3. Remove an environment
```
conda remove -n myenv --all
```
- verify the delete by 
```
conda info --envs 
```
or 
```
conda env list 
```

4. Activate an environment 
```
conda activate myenv
```

5. Deactivate an environment
```
conda deactivate
```

6. Check packages in a specific environment
```
conda list -n myenv
```
- Or, if the env is already activated 
```
conda list 
```
- If we only want to check if a specific package is installed
```
conda list -n myenv scipy
```


## 2. Conda vs pip
- pip is a *package manager* only for Python
- venv is a *environment manager* only for Python
- conda is both a *package and environment manager* and is language agnostic(works with any languages)
