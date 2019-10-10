# Lab: Python Spatial Programming with Shapely and Fiona
## Worth: 40
## Due: 7 days
## Assignment

## Background
We previously worked with python within the framework of QGIS but python is most flexible when used in stand-alone mode, which allows us to decouple the QGIS framework libraries from the base libraries of python and explicitly add libraries of our own. As with other languages, the power of Python comes from the plethora of high-quality libraries that extend the base functionality of the core python programming language. In the realm of spatial python there are many libraries but we will start with two: `shapely` and `fiona`.

_This lab adapted from https://macwright.org/2012/10/31/gis-with-python-shapely-fiona.html
and https://automating-gis-processes.github.io/CSC18/lessons/L1/Geometric-Objects.html_
Shapely and Fiona are essential Python tools for geospatial programming written by Sean Gillies. Use them instead of ESRI’s Python toolchain. They are free, stable, and mean you can post your code on GitHub and nonrich people will be able to run it.

Reference:
- [Shapely docs](https://shapely.readthedocs.io/en/stable/manual.html)
- [Fiona docs](https://fiona.readthedocs.io/en/latest/)

## Setup Conda Environment
Follow instructions in [conda_setup.md](conda_setup.md) to setup your environment.

## Follow shapely+fiona tutorial
Follow the tutorial in [shapely-fiona-tutorial-1.md](shapely-fiona-tutorial-1.md) using the Anaconda Shell. To enter python in the shell, enter: 
```
python
```
Then you will see a prompt
```
>>>
```
At the prompt you can enter your python commands such as `print('hello')` or `8*6` or `import shapely`

### Deliverable: Screenshot of final step
Take a screenshot of the final step in the tutorial as run from Anaconda shell. Name it `screenshot-1.png`. Add it to a new `solution` branch of this repository. 

## Follow Geometric Objects Tutorial in Spyder
Follow the tutorial, [tutorial-2.md](tutorial-2.md) using the Spyder Integrated Development Environment (IDE).

### Deliverable: Screenshot of the iPython window
At completion of the tutorial, take a screen capture of the iPython window 
