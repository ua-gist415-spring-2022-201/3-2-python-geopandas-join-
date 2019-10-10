
# Conda environment setup

In your lab machine, open "Anaconda Shell". This will open an interactive shell.

Next, set up a new conda environment with:
```
conda create --name python37 python=3.7
```
This creates a new python environment that uses python 3.7. We will need to activate it:
```
conda activate python37
```
Now that we have created the environment we can install our libraries. In this lab we will need `shapely` and `fiona`. To install libraries with conda:
```
conda install shapely
```
It will ask you to `Proceed ([y]/n(?)` - Press `y` or `Enter`
Similarly, for fiona:
```
conda install fiona
```

If you close your shell and re-open it, if your conda environment is not active, you can activate it with `conda activate python37`
For more details on conda environments: [Mananging conda environments](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
