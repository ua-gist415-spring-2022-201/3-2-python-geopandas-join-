# Python Spatial Programming with Geopandas
## Assignment

### Background
We previously worked with python within the framework of QGIS but python is most flexible when used in stand-alone mode, which allows us to decouple the QGIS framework libraries from the base libraries of python and explicitly add libraries of our own. As with other languages, the power of Python comes from the plethora of high-quality libraries that extend the base functionality of the core python programming language. In the realm of spatial python there are many libraries but we will start with a couple: `geopandas`, `shapely`, `rasterio`, and `rasterstats`. 

#### GeoPandas
Read this [tutorial](https://geopandas.org/getting_started/introduction.html)
Browse/read the GeoPandas [user guide](https://geopandas.org/docs/user_guide.html). This will be a reference for you in this and later assignments. 

- Tutorial: https://geopandas.org/getting_started/introduction.html
- User Guide: https://geopandas.org/docs/user_guide.html

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

### Deliverables
- `spatial_join.py`
- `spatial_join.png`

### Directions
## Update conda env
Install the `descartes` library in your `geo37` environment. If you already have Spyder running you will need to restart the kernel for the new library to be usable in that session.

## Performing spatial joins
Review [Performing spatial joins](http://www.qgistutorials.com/en/docs/3/performing_spatial_joins.html) to see our objective. 

### Download and extract the data:

- [NY Boros](http://www.qgistutorials.com/downloads/nybb_19a.zip)
- [Pavement Ratings](http://www.qgistutorials.com/downloads/V_SSS_SEGMENTRATING_1.zip)

Open `Spyder` and create a new document in this repo named `spatial_join.py`.

### Load the data in python
We are going to use `geopandas` and `descartes` in this lab, so import them:
```
import geopandas
import descartes
```
`geopandas` can read shapefiles. Using the path to the extracted shapefile above:
```
nybb = geopandas.read_file('/Users/username/classes/gist415/fall-2019-online/data/nybb_19a/nybb.shp')
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
vss = geopandas.read_file('/Users/username/classes/gist415/fall-2019-online/data/V_SSS_SEGMENTRATING_1/dot_V_SSS_SEGMENTRATING_1_20190129.shp')
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
of the final step in the assignment and save it as `spatial_join.png`.
