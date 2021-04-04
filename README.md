# Python Spatial Programming with Geopandas
## Assignment

### Background
We previously worked with python within the framework of QGIS but python is most flexible when used in stand-alone mode, which allows us to decouple the QGIS framework libraries from the base libraries of python and explicitly add libraries of our own. As with other languages, the power of Python comes from the plethora of high-quality libraries that extend the base functionality of the core python programming language. In the realm of spatial python there are many libraries but we will start with a couple: `geopandas`, `shapely`, `rasterio`, and `rasterstats`. With that said, we will be reliant on specific libraries to be installed for this assignment and to unify the workspaces across all individual student machines (Windows and Macs of various versions with different pre-existing software installed), we will be using a `docker` base image that includes the geospatial libraries we want to use as well as the IDE (Spyder) that we want to use. We'll get to what Spyder is in a bit. 

#### Anaconda
Python relies on libraries that extend the basic functionality. These libraries are installed and managed primarily by two different methods. `pip` may be more familiar to you if you have used python previously. `conda` is what we will use because it manages dependencies better and the conda library repos (aka `channels`) support the geospatial libraries better than `pip`'s `PyPi`.

We won't get into the specifics of how to install the packages themselves though you are encouraged to create your own conda install, your own conda environment(s), and install your own libraries. However, for building an application that uses a variety of geospatial packages this is quite challenging because different libraries may depend on the same core geo or math library (which is good) but may also require a different version (which is bad and causes us to fail to install the library). To complicate matters, different versions of libraries may have different dependency versions. To make it even more complex and infurirating, different channels or repos may have libraries that have their own nuanced dependencies. Not to make it even worse, but the order of installation also makes a difference. Therefore, for this class we are going to be using a docker container that already has the right versions of libraries installed that we will need for this assignment. 

#### Integrated Development Environment (IDE) - Spyder
When developing code or working with structured files in HTML, JSON, YAML, etc., it is helpful to use a special type of text editor that does syntax highlighting as well as more advanced functions such as being able to complete typing commands or variables because they are context-aware as well as have integrations with runtimes. For this class we will be using `Spyder`, an IDE for Python that includes smart editing, integrated runtime, and a variable explorer, allowing you to visually inspect your variables as you are running through your program. Like the geospatial libraries, this is a python library with its own dependencies and I have wrapped it up in the same docker container. Since it is a Graphical User Interface (GUI), it has special requirements for building windows and interacting with your mouse and keyboard that are slightly morecomplicated running through docker so we are going to be running them inside a browser. 

#### Geospatial libraries and notes on documentation 
Geospatial Library Reference:
- [Shapely docs](https://shapely.readthedocs.io/en/stable/manual.html)
- [Geopanda docs](http://geopandas.org/)

Docs can be good or bad. The docs for above range from "ok" to "good" (geopandas).
GeoPandas actually uses the `shapely` model for geometries and while it needs to be installed, there is little direct
interaction with this library on our part except for accessing the `shapely` geometries.

### Objective
The objective of this lab is to reproduce one of the QGIS Tutorials you did previously:
- [Performing spatial joins](http://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html)

### Prerequisites
- Python 3 must be installed [Download](https://www.python.org/downloads/)
- Docker must be installed

### Deliverables
- `spatial_join.py`
- `spatial_join.png`

### Directions

#### Getting started with Spyder
_On doing this without docker: Without docker I would have you install Anaconda, create an environment, install all the libraries, including spyder, and then have you launch `spyder` from the command line. However, the diversity of platform issues we encountered doing it this way previously required standardizing._

Within this repository there is a file [spyder_desktop.py](spyder_desktop.py). We are going to run this file which will do a little extra work to make our docker container run nicely with our windowing environment.

Navigate to the directory where this repo is checked out to and run:
```
python spyder_desktop.py -p
```
This will run the docker container which will connect to using our browser. You should shortly see something like this:
```
Using default tag: latest
latest: Pulling from aaryno/spyder-geo
Digest: sha256:0203cd9f45aef9575b75524c102c6f419007e5e905cb808c640370eec5cabd91
Status: Image is up to date for aaryno/spyder-geo:latest
docker.io/aaryno/spyder-geo:latest
Starting up docker image...
87ddf34197eb49c089716991d7e40fb75a7b66a7805fa7dbbce4420be3955434
Open your web browser with URL:
    http://localhost:6080/vnc.html?resize=downscale&autoconnect=1&password=IfM3Io6C

For a better experience, use VNC Viewer (http://realvnc.com/download/viewer)
to connect to localhost:5950 with password IfM3Io6C

You can also log into the container using the command
    ssh -X -p 2222 ubuntu@localhost -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no
with an authorized key in /Users/aaryno/.ssh/authorized_keys.
Press Ctrl-C to stop the server.
```
Additionally, your default browser may open and you will see a blue screen with a black terminal in it. If your browser does not launch, then follow the instructions in the command output to `Open your web browser with URL:`

When you open the browser you should see something like this:
![Desktop Image with Task Bar](desktop_task_bar_visible.png)

However, you may see something like this (notice that the grey task bar is missing)
![Desktop Image without Task Bar](desktop_task_bar_hidden.png)

In this case, the task bar is hidden and you will have to make it visible in order to proceed. It may help if you are on a large monitor.

##### If the grey taskbar is not visible:
On the left side of the screen you should see a little grey arrow. Click in this to expand a menu for the display. Click on the Gear Icon, then change the `Scaling Mode` to `Local Scaling`:

![Local Scaling Option](local_scaling.png)

##### Launch Spyder
Click on the bottom-left corner of the task-bar to bring up a menu and select `Programming` -> `Spyder` to launch spyder.

##### A Note on directories
This docker container has `mount`ed a host directory as `shared` and you can save files from this virtual desktop to `shared` and have them accessible from your host computer. For example, this is how the `shared` directory looks when I open it from spyder. It has mounted the directory where I checked this assignment out to (the repo directory). This is convenient since you can save your `.py` files to `shared` and then GitHub Desktop will recognize them as new.
![Shared Directory](shared_directory.png)

##### Really Getting started with Spyder (for realz this time)
This is what your Spyder IDE looks like:
 
 ![Spyder IDE](spyder-splash.png)
 
Notice the three panels. In the large panel on the left (labeled `Editor`) you can write python code and take notes. In the 
top right `Variable explorer`) you can see what variables are in scope and inspect their types and contents. In the bottom 
right ('iPython console') is an interactive python console. You can type python directly into the console or use the icons 
at the top of the `Editor` panel to send commands to the python console. Of note, the Gear icon in the console title bar
will allow you to restart the "`kernel`", which restarts python and gives you a fresh environment (with no declared 
variables or libraries imported).

In practice, it is good to use the `Editor` window to build a working program line by line, saving your progress as a new
python file, and then, after significant edits, restarting the kernel and running through the program line by line to make 
sure it works from start to finish.

The editor has a navigation bar that allows you to run a selection, a line, or the entire program:

![Spyder IDE](spyder-editor-navbar.png)

## Performing spatial joins
Review [Performing spatial joins](http://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html) to see our objective. 

### Download and extract the data:

- [NY Boros](http://www.qgistutorials.com/downloads/nybb_19a.zip)
- [Pavement Ratings](http://www.qgistutorials.com/downloads/V_SSS_SEGMENTRATING_1.zip)

You will want to save them to your repo so that they will be accessible in your `shared` directory but for the sake of unnecessary github commits, don't commit them :-)

Open `Spyder` and create a new document in this repo named `spatial_join.py`.

### Load the data in python
We are going to use `geopandas` and `descartes` in this lab, so import them:
```
import geopandas
import descartes
```
`geopandas` can read shapefiles. Using the path to the extracted shapefile above:
```
nybb = geopandas.read_file('/Users/aaryno/classes/gist604b/fall-2019-online/data/nybb_19a/nybb.shp')
```
Next, do some basic exploration of the data and the python structures made from it:
```
print(nybb)
type(nybb)
nybb.head()
```
Note that the `.head()` method is acting _on_ the geopandas dataframe and will print the values of the first 5 lines. Next, plot it (the `.plot()` method is also acting on the geopandas dataframe and plots it using the `matplotlib` library:
```
nybb.plot()
```
Do the same for the street pavement rating:
```
vss = geopandas.read_file('/Users/aaryno/classes/gist604b/fall-2019-online/data/V_SSS_SEGMENTRATING_1/dot_V_SSS_SEGMENTRATING_1_20190129.shp')
```
And explore:
```
print(vss)
type(vss)
vss.head()
vss.plot()
```

### Subset the Streets data
Geopandas gives us the ability to use array-indexing to subset the data. Let's construct a filter to get rid of the data where `RatingWord` is not `NR`:

View the data:
```
vss['RatingWord']
```
Construct a list of boolean values equal to the length of `vss` in which the value is `True` if `RatingWord` is not equal to `NR` and False otherwise:
```
vss['RatingWord'] != 'NR']
```
Now we can subset `vss` based on which values of ^ are `True`:
```
vss_sub = vss[vss['RatingWord'] != 'NR']
```
Now we have a new `GeoDataFrame` named `vss_sub` with fewer rows. Take a look at its shape and compare to `vss` to confirm:
```
vss_sub.shape
vss.shape
```
### Perform spatial join between boros and streets:
Geopandas has an `sjoin` [[doc](http://geopandas.org/reference/geopandas.sjoin.html)] operator to perform spatial joins:
```
nybb_with_vss = geopandas.sjoin(nybb, vss_sub)
```
Take a look:
```
type(nybb_with_vss)
nybb_with_vss.head()
```

### Summarize stats
We have successfully given the streets the names of the boros they reside in. Not let's summarize. This functionality is
inherited from the `pandas` library:

```
mean_rating_by_boro = nybb_with_vss.groupby(['BoroCode'])['Rating_B'].mean()
```

This creates a data frame containing the mean of `Rating_B` bu `BoroCode` across the `nybb_with_vss` dataframe.
```
type(mean_rating_by_boro)
head(mean_rating_by_boro)
```

### Join pavement summary stats to boros
The above is just a table. To give those attributes to the original boros data we need to do a table join, which in 
geopandas parlance is `.merge()`:
```
nybb_with_mean_ratings = nybb.merge(mean_rating_by_boro, on='BoroCode' )
nybb_with_mean_ratings.head()
```

### Deliverable
Save your final python file as `spatial_join.py` in this repository. Additionally, take a screenshot showing the results
of the final step in Part 1 and save it as `spatial_join.png`.
