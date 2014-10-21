Usage: gdal2xyz_geocentricSpace.py [-skip factor] [-printLatLon] [-addheader] [-srcwin xoff yoff width height]
     [-radius value_m or -radiusBand n] [-latBand n] [-lonBand n] [-band b] srcfile [dstfile]
Note: if no radius or radiusBand is sent, the radius will default to the Moon = 1737400.0

* brackets [ ] indicate optional parameter. If no output file, will write to stdout
* defaults to band 1 if nothing is sent (only applicable when using -printLatLon)
* -srcwin offsets, width, and height values should be sent in meters
* -addheader will add a one row with field names

Use one or none for
 * -printLatLon will use GDAL/map projection to calculate Lat/Lon for every pixel

To override lat/lon calculations with values from a band
 * -latBand n
 * -lonBand m
 * -radiusBand r

Here are some use cases:

% gdal2xyz_geocentricSpace.py -addheader input.cub
* creates geocentric "Y, X, Radius (Moon)" to stdout with header line

% gdal2xyz_geocentricSpace.py -addheader input.cub out.csv
* creates geocentric "Y, X, Radius (Moon)" to out.csvi with header line

% gdal2xyz_geocentricSpace.py -addheader -latBand 2 -lonBand 3 input.cub out.csv
* creates geocentric "Y, X, Radius (Moon)" using lat,lon from bands 2,3 

% gdal2xyz_geocentricSpace.py -addheader -radiusBand 1 -latBand 2 -lonBand 3 input.cub out.csv
* creates geocentric "Y, X, Radius" using lat,lon,radius from bands 2,3,1 

% gdal2xyz_geocentricSpace.py -addheader -radius 1737400.0 -latBand 2 -lonBand 3 input.cub out.csv
* creates geocentric "Y, X, Radius" using lat,lon from bands 2,3 with a static radius 

% gdal2xyz_geocentricSpace.py -addheader -printLatLon input.cub out.csv
* just print Lat, Lon, Band number to out.csv 

% gdal2xyz_geocentricSpace.py -addheader -printLatLon -latBand 2 -lonBand 3 input.cub out.csv
* just print Lat, Lon, Band number to out.csv but lat,lon from defined bands 