
.. _geometry:

Geometry Handling
=================

Points, linestrings, polygons that represent a spatial feature are commonly referred to as geometries.
In QGIS they are represented with :class:`QgsGeometry` class.
All possible geometry types are nicely shown in `JTS discussion page <http://www.vividsolutions.com/jts/discussion.htm#spatialDataModel>`_.

Sometimes one geometry is actually a collection of simple (single-part) geometries. Such a geometry is called
multi-part geometry. If it contains just one type of simple geometry, we call it multi-point, multi-linestring or multi-polygon.
For example, a country consisting of multiple islands can be represented as a multi-polygon.

The coordinates of geometries can be in any coordinate reference system (CRS). When fetching features from a layer, associated geometries
will have coordinates in CRS of the layer.


Geometry Construction
---------------------

There are several options how to create a geometry:

* from coordinates::

    gPnt = QgsGeometry.fromPoint(QgsPoint(1,1))
    gLine = QgsGeometry.fromPolyline( [ QgsPoint(1,1), QgsPoint(2,2) ] )
    gPolygon = QgsGeometry.fromPolygon( [ [ QgsPoint(1,1), QgsPoint(2,2), QgsPoint(2,1) ] ] )

  Coordinates are given using :class:`QgsPoint` class.

  Polyline (Linestring) is represented by a list of points. Polygon is represented by a list of linear rings (i.e. closed linestrings).
  First ring is outer ring (boundary), optional subsequent rings are holes in the polygon.

  Multi-part geometries go one level further: multi-point is a list of points, multi-linestring is a list of linestrings and multi-polygon is a list of polygons.

* from well-known text (WKT)::

    gem = QgsGeometry.fromWkt("POINT (3 4)")

* from well-known binary (WKB)::

    g = QgsGeometry()
    g.setWkbAndOwnership(wkb, len(wkb))


Access to Geometry
------------------

First, you should find out geometry type, :func:`wkbType` method is the one to use --- it returns a value from QGis.WkbType enumeration::

  >>> gPnt.wkbType() == QGis.WKBPoint
  True
  >>> gLine.wkbType() == QGis.WKBLineString
  True
  >>> gPolygon.wkbType() == QGis.WKBPolygon
  True
  >>> gPolygon.wkbType() == QGis.WKBMultiPolygon
  False

As an alternative, one can use :func:`type` method which returns a value from QGis.GeometryType enumeration.
There is also a helper function :func:`isMultipart` to find out whether a geometry is multipart or not.

To extract information from geometry there are accessor functions for every vector type. How to use accessors::

  >>> gPnt.asPoint()
  (1,1)
  >>> gLine.asPolyline()
  [(1,1), (2,2)]
  >>> gPolygon.asPolygon()
  [[(1,1), (2,2), (2,1), (1,1)]]

Note: the tuples (x,y) are not real tuples, they are :class:`QgsPoint` objects,
the values are accessible with :func:`x` and :func:`y` methods.

For multipart geometries there are similar accessor functions: :func:`asMultiPoint`, :func:`asMultiPolyline`, :func:`asMultiPolygon()`.


Geometry Predicates and Operations
----------------------------------

QGIS uses GEOS library for advanced geometry operations such as geometry predicates (:func:`contains`, :func:`intersects`, ...)
and set operations (:func:`union`, :func:`difference`, ...)


**TODO:**

* :func:`area`, :func:`length`, :func:`distance`
* :func:`transform`
* available predicates and set operations
