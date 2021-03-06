# GeoTrellis

*GeoTrellis* is a high performance geoprocessing engine and programming toolkit.  The goal of the project is to transform
user interaction with geospatial data by bringing the power of geospatial analysis to real time, interactive web applications.

GeoTrellis was designed to solve three core problems, with a focus on raster processing:

- Creating scalable, high performance geoprocessing web services
- Creating distributed geoprocessing services that can act on large data sets
- Parallelizing geoprocessing operations to take full advantage of multi-core architecture 

GeoTrellis is a project of Azavea (www.azavea.com), and was written by Josh Marcus (jmarcus@azavea.com) and Erik Osheim (eosheim@azavea.com).  Please contact us if you have any questions, find us on irc at #geotrellis on freenode, or join 
the user mailing list at [https://groups.google.com/group/geotrellis-user](https://groups.google.com/group/geotrellis-user).

Please see our 
[getting started guide](http://azavea.github.com/geotrellis/getting_started/GeoTrellis.html) for more information. 

## Features

- GeoTrellis is designed to help a developer create simple, standard REST services that return the results of geoprocessing models.
- Like an RDBS that can optimize queries, GeoTrellis will automatically parallelize and optimize your geoprocessing models where possible.  
- In the spirit of the object-functional style of Scala, it is easy to both create new operations and compose new 
operations with existing operations.

## Some sample GeoTrellis code

```scala
  // create a new operation that multiplies each cell of 
  // each raster by a weight, and then add those two new
  // rasters together
  val op = Add(MultiplyConstant(raster1, weight1),
               MultiplyConstant(raster2, weight2))

  // create a new operation that takes the result of the
  // previous operation and divide each cell by the average 
  // weight, creating a weighted overlay of our two rasters
  val op2 = DivideConstant(op, weight1 + weight2 / 2) 

  // or, we can use a simpler syntax:
  val avg = weight1 + weight2 / 2 
  val wo = (raster1 * weight1) + (raster2 * weight2) / avg

  // To this point, we've only been composing new operations.
  // To run an operation:
  val server = Server("example")
  val result = server.run(wo)

``` 
## API Reference

### Scaladocs

You can find *Scaladocs* for the latest version of the project here:

[http://azavea.github.com/geotrellis/latest/api/index.html#geotrellis.package](http://azavea.github.com/geotrellis/latest/api/index.html#geotrellis.package)
