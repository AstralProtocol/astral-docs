---
description: What exactly *is* spatial data?
---

# Spatial Data Primer

A **spatial data asset** is any data asset that contains spatial or location information. This term is intentionally broad, and GeoDIDs are deliberately flexible enough to identify current and legacy spatial data types, as well as ones that haven't been developed yet.

Generally, spatial data assets to fall into two categories: **raster** and **vector**.

{% tabs %}
{% tab title="Raster" %}
Raster data are composed of grid cells identified by row and column. The whole geographic area is divided into groups of individual cells, which represent an image. Satellite images, photographs, scanned images, etc., are examples of raster data \([Janipella et al 2019](https://www.sciencedirect.com/topics/engineering/spatial-data)\).

A \(very\) simplified representation of a 3x3 pixel raster image in Python:

```text
img = [[ 1, 0, 1 ],
       [ 0, 1, 0 ],
       [ 1, 0, 1 ]]
```

![](../../.gitbook/assets/raster.png)

To start, GeoDID modules will natively support GeoTIFF raster datasets.
{% endtab %}

{% tab title="Vector" %}


In a vector dataset, **features** are individual units in the dataset, and each feature typically represents a _point_, _line_ or _polygon._ These features are represented mathematically, usually by numbers that signify either the coordinates of the point, or the vertices \(corners\) of the geometry - read more [here](https://towardsdatascience.com/spatial-data-science-for-the-uninitiated-9a78804d4efa).

```text
point =   [ 45.841616, 6.212074 ]

line =    [[ -0.131838, 51.52241 ],
           [ -3.142085, 51.50190 ],
           [ -3.175046, 55.96150 ]]

polygon = [[[ -43.06640, 17.47643 ],
            [ -46.40625, 10.83330 ],
            [ -37.26562, 11.52308 ],
            [ -43.06640, 17.47643 ]]]
            # ^^ The first and last coordinate are the same
```

![Example of vector features from Saylor Academy, https://saylordotorg.github.io/text\_essentials-of-geographic-information-systems/s11-geospatial-analysis-i-vector-o.html.](../../.gitbook/assets/vector.jpg)

The vector data formats most commonly used on the web are SVGs and GeoJSON files. SVGs - scalable vector graphics - do not have a geographic referencing system - but GeoJSON datasets do.

For the alpha implementation of the GeoDID specification, we chose GeoJSON files as our natively-supported vector filetype. For reference, here's a simple GeoJSON Polygon Feature - notice the array of vertices in the `geometry` attribute, similar to the `polygon` variable shown above:

```text
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [
              -0.0986060,
              51.5326047
            ],
            [
              -78.639101,
              35.7803929
            ],
            [
              -8.6094188,
              41.1398493
            ],
            [
              -0.0986060,
              51.5326047
            ]
          ]
        ]
      }
    }
```
{% endtab %}
{% endtabs %}

Spatial data assets are data assets - binary files, or directories of files - that contain spatially-referenced information. For v0.0, GeoDIDs natively support GeoTIFF and GeoJSON files, which are commonly-used raster and vector data formats respectively. In the future, spatial data of any format can be identified using a GeoDID, and these format extensions can be built for the `@astral-geodid` software modules.

{% hint style="info" %}
More on [GeoJSON](https://macwright.com/2015/03/23/geojson-second-bite.html) and [geojson.io](http://geojson.io/), a tool for creating and exploring GeoJSON files.

More information about [GeoTIFFs](https://www.gislounge.com/what-is-a-geotiff/), plus a [sample](https://cbers.stac.cloud/item/wMAdB8x2xmsNbdUHrc28srEdZpy/A6ExZs3csirxV7jSsrFicBf2TKBJB9xubxeAy/h88cG3tZLsmVu6iM7Mjx5Pg5agdpJnF346adC9/5XYvhxvrpCphAXhLWgKjphETpsBRhKdZV1d8LAooTo3K/93J54CWKozr1bRfaJ86XbTqHyztjFiPbckxGhpGCb9tDFFyG9NFRRyXGchpjoZzHNL2HJ2PYVENgW9?si=0&t=preview#6/-34.060280/-64.037544).

Learn more background theory on spatial data [here](https://observablehq.com/@johnx25bd/1-introducing-spatial).
{% endhint %}

