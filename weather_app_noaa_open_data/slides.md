---
author: Filipe Fernandes
title: Building your own Weather App using NOAA Open Data and Jupyter Notebooks
date: Jul 13, 2018
---


# `whoami`

Filipe Fernandes

>- Physical Oceanographer
>- Data Plumber
>- Code Janitor
>- CI babysitter
>- Amazon-Dash-Button for conda-forge


# Previous talks: standards

<iframe width="700" height="500" src="https://www.youtube.com/embed/BV30Sk1CrM0?start=1771" frameborder="0" allow="encrypted-media" allowfullscreen></iframe>

[https://www.youtube.com/watch?v=BV30Sk1CrM0](https://www.youtube.com/watch?v=BV30Sk1CrM0)


# Previous talks: ocean models

<iframe width="700" height="500" src="https://www.youtube.com/embed/WHjU_rg81BI?start=1771" frameborder="0" allow="encrypted-media" allowfullscreen></iframe>

[https://www.youtube.com/watch?v=WHjU_rg81BI](https://www.youtube.com/watch?v=WHjU_rg81BI)



# IOOS

![](images/IOOS-RAs.jpg)


# IOOS numbers  

![](images/ioos_by_the_numbers_graphic2_feb2017-2.png)


# Code gallery

<img src="images/code-gallery.png" height=450>

[http://ioos.github.io/notebooks_demos/code_gallery](http://ioos.github.io/notebooks_demos/code_gallery)


# Standards

<p>
<img src="images/OGC_Logo_2D_Blue_x_0_0.png" height=100 style="background-color:white">
<img src="images/iso-logo-print.gif" height=100>
<img src="images/unidata-logo.png" height=100 style="background-color:white">
</p>

>- avoid customer-specific solutions
>- the standardizations happen at the data providers 

. . .

<img src="images/standards.svg" height=250 style="background-color:white">


# IOOS Web Services

| Data Type                              | Web Service                       | Response     |
|----------------------------------------|-----------------------------------|--------------|
| In-situ data<br>(buoys, stations, etc) | OGC SOS                           | XML/CSV      |
| Gridded data (models, satellite)        | OPeNDAP                           | Binary       |
| Raster Images                          | OGC WMS                           | GeoTIFF/PNG |


. . .

There is also `ERDDAP` emerging as a community standard.

# Sensor Observation Service

(OGC SOS)

>- `GetCapabilities`: metadata
>- `DescribeSensor`: detail info on the instruments
>- `GetObservation`: the data


# SOS example

```python
url = (
    'https://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/SOS?'
    'service=SOS'
    '&request=GetObservation'
    '&version=1.0.0'
    '&observedProperty=water_surface_height_above_reference'
    '&offering=urn:ioos:station:NOAA.NOS.CO-OPS:8454000'
    '&responseFormat=text/csv'
    '&eventTime=2018-07-04T00:00:00Z/2018-07-05T00:00:00Z'
    '&result=VerticalDatum==urn:ogc:def:datum:epsg::5103'
    '&dataType=PreliminarySixMinute'
)
```

# If we add Python to it

```python
url = (
    f'https://opendap.co-ops.nos.noaa.gov/ioos-dif-sos/SOS?'
    f'service=SOS&request={request}'
    f'&version={version}'
    f'&observedProperty={variable}'
    f'&offering=urn:ioos:station:NOAA.NOS.CO-OPS:8454000'
    f'&responseFormat={response}'
    f'&eventTime={yesterday:%Y-%m-%dT%H:%M:%SZ}/'
    f'{today:%Y-%m-%dT%H:%M:%SZ}'
    f'&result=VerticalDatum=={vdatum}'
    f'&dataType={data_type}'
)
```

. . .

<a href="http://localhost:8888/notebooks/00-SOS.ipynb">
  <img src="images/jupyterhub.svg" height=75 style="background-color:white">
</a>


# OPeNDAP/Climate and Forecast 

(CF)


<iframe src="http://cfconventions.org/" width="750px" height="450px"></iframe>

# CF - Metadata

```xml
float temp(ocean_time, s_rho, eta_rho, xi_rho);
    temp:standard_name = "sea_water_potential_temperature"
    temp:units = "Celsius";
    temp:coordinates = "lon_rho lat_rho s_rho ocean_time";
double s_rho(s_rho);
    s_rho:long_name = "S-coordinate at RHO-points";
    s_rho:positive = "up";
    s_rho:standard_name = "ocean_s_coordinate_g1";
    s_rho:formula_terms = "s:s_rho C:Cs_r eta:zeta depth:h
                           depth_c:hc"
```

. . .

<a href="http://localhost:8888/notebooks/01-ClimateForecast.ipynb">
  <img src="images/jupyterhub.svg" height=75 style="background-color:white">
</a>


# Web Mapping Service

(OGC WMS)

>- Simple HTTP interface for requesting geo-registered map images
>- A WMS request defines the geographic layer(s) and area of interest to be processed
>- The response to the request is one or more geo-registered map images (returned as JPEG, PNG, etc) 

. . .

<a href="http://localhost:8888/notebooks/02-WMS.ipynb">
  <img src="images/jupyterhub.svg" height=75 style="background-color:white">
</a>

# ERDDAP

The data server that the community is demanding

>- Flexible outputs: `.html` table, ESRI `.asc` and `.csv`, Google Earth `.kml`, OPeNDAP binary, `.mat`, `.nc`, ODV `.txt`, `.csv`, `.tsv`, `.json`, and `.xhtml`
>- Free RESTful API to access the data
>- Standardize dates and time in the results
>- Server-side searching and slicing

. . . 

<a href="http://localhost:8888/notebooks/03-ERDDAP.ipynb">
  <img src="images/jupyterhub.svg" height=75 style="background-color:white">
</a>


# There are many moving parts

![](images/grind_gears.gif)



# Catalog Service for the Web

(CSW)

>- A single source to find endpoints
>- Nice python interface:<br>`owslib.csw.CatalogueServiceWeb`
>- Advanced filtering:<br>`owslib.fes`

. . . 

<img src="images/one_ring.jpg" height=75 style="background-color:white">


# Harvesting

<img src="images/IOOS.svg" height=550 style="background-color:white">



# Finding the web services


```python
>>> from geolinks import sniff_link
>>> sniff_link('http://host/wms?service=SOS')
'OGC:SOS'
>>> sniff_link('http://host/wms?service=OPeNDAP:OPeNDAP')
'OPeNDAP:OPeNDAP'
>>> sniff_link('http://host/wms?service=WMS')
'OGC:WMS'
>>> sniff_link('http://host/data/roads.kmz')
'OGC:KML'
>>> sniff_link('http://host/data/roads.kml')
'OGC:KML'
```

. . .

<a href="http://localhost:8888/notebooks/04-CSW.ipynb">
  <img src="images/jupyterhub.svg" height=75 style="background-color:white">
</a>


# Putting it all together: NHC

Meteorological stations in a National Hurricane Center path prediction.

<a href="http://localhost:8888/notebooks/2017-09-09-hurricane_irma.ipynb">
  <img src="images/hurricane-irma.png" height=150 style="background-color:white">
</a>


# Putting it all together: Model skill

Modeled Significant Wave Height skill

<a href="http://localhost:8888/notebooks/2018-03-30-wave_height_assessment.ipynb">
  <img src="images/wave-height.png" height=110 style="background-color:white">
</a>

# Putting it all together: ERDDAP App

Finally the title notebook!

<a href="http://localhost:8888/notebooks/ERDDAP_timeseries_explorer-IOOS.ipynb">
  <img src="images/erddap_app.png" height=400 style="background-color:white">
</a>



# SECOORA Portal

<iframe width="700" height="500" src="https://portal.secoora.org"></iframe>


# Summary

>- Standards, web services and catalogs allow us to serve data in a unified way
>- Python powered Jupyter gives us a powerful scientific, analysis and visualization environment to fetch
>- Widgets allow for fancy data exploration


# Questions?

#### ([ocefpaf]((https://github.com/ocefpaf)))

![](images/twitter-github.png)

... g-mail, google+, etc.


[https://ocefpaf.github.io/2018-SciPy-talk](https://ocefpaf.github.io/2018-SciPy-talk)

[![Binder](http://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/ocefpaf/2018-SciPy-talk/gh-pages)