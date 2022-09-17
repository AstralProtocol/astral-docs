# On-chain Spatial Data Registry

The fully decentralized spatial data registry stores all data on-chain. Due to technology limitations, we built a lightweight solution to organize and query the geospatial data using the [geohash](https://en.wikipedia.org/wiki/Geohash) geocode system to build a data structure called a `GeoTree`.

## Geohash

Geohashing is a method that encodes coordinates as a string of characters. In the geohash system, the Earth's surface is divided into 32 rectangles, each one corresponding to a specific  character. The characters include all numbers and letters except `a`, `i`, `l` and `o`. Each top level rectangle is subsequently divided into 32 rectangles, representing a second level of detail. This pattern can be continued for an infinite number of nested rectangles, so that every level corresponds with its identifier character. The more characters we specify, the smaller the rectangle will be. For example, the geohash `de2f7` with five characters is five nested rectangles deep.

<figure><img src="../.gitbook/assets/Mercator_projection_Square.svg" alt=""><figcaption><p>geohash level 1 with "d" divided to show level 2. Base map by <a href="https://commons.wikimedia.org/wiki/User:Strebe">Strebe</a> - Own work, <a href="https://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>, <a href="https://commons.wikimedia.org/w/index.php?curid=17700069">Link</a></p></figcaption></figure>

The short alphanumeric format of a geohash lends itself well to a Solidity implementation that doesn't support floating point numbers. Additionally, it's convenient to remove characters from the end of a hash to query locations that are less and less precise.

### Point Locations

Our current implementation of the spatial data registry only indexes a single latitude/longitude point. For polygons, we calculate the centroid off-chain and use that value to register a location.

The registry stores data at level 8, which corresponds to a square of 20x20 meters. Any point inside that square will be resolved to the same geohash.
