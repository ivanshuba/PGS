# Changelog

All notable changes to PGS will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html). Dates are *YYYY-MM-DD*.

## **1.3.0** *(2022-10-20)*

### Added
#### Classes
* **`PGS_Hull`** — a dedicated class for convex and concave hulls of polygons and point sets.
* **`PGS_SegmentSet`** — a class that generates random sets of <i>non-intersecting</i> line segments.

#### Methods
* `equalPartition()` to `PGS_Processing`. Partitions a shape into N approximately equal area polygons.
* `trapezoidPartition()` to `PGS_Processing`. Partitions a shape into axis-aligned trazepoids.
* `fromChildren()` to `PGS_Conversion`. Creates a single GROUP parent shape from a list of child shapes.
* `WKT` and `WKB` conversion methods to `PGS_Conversion`. Converts PShapes to and from their *Well-Known Text* / *Well-Known Binary* representation.
* `Encoded Polyline` conversion methods to `PGS_Conversion`. Converts PShapes to and from a Google Encoded Polyline representation.
* `GeoJSON` conversion methods to `PGS_Conversion`. Converts PShapes to and from a GeoJSON representation.
* `toJava2D()` and `fromJava2D()` to `PGS_Conversion`. Converts PShapes to and from Java2D/java.awt shape objects.
* `originScale()` to `PGS_Transformation`. Scales a shape relative to the origin (0, 0).
* `resizeByWidth()` and `resizeByHeight()` to `PGS_Transformation`. Resizes a shape to a given width/height, whilst resizing the height/width to maintain the original aspect ratio.
* `resizeByMajorAxis()` to `PGS_Transformation`. Resizes a shape (based on the longest axis of its envelope) to a given size.
* `translateEnvelopeTo()` and `translateCornerTo()` to `PGS_Transformation`. These methods translate a shape based on its envelope.
* A new mesh-coloring algorithm: `GENETIC`, which finds a coloring via a genetic algorithm.
* `toGraph()` to `PGS_Conversion`. Converts a shape to a (jGraphT) graph, representing its dual-graph (this method was previously private).
* `fromGraph()` to `PGS_Conversion`. Converts a (jGraphT) graph to a shape, using a Force-Directed placement algorithm.
* `sphericity()`, `elongation()` and `maximumInteriorAngle()` to `PGS_ShapePredicates`.
* `findContainingShape()` to `PGS_ShapePredicates`. Finds the child shape in a GROUP shape that contains a query point.
* `overlap()` to `PGS_ShapePredicates`. Measures the degree of mutual overlap between two shapes.
* `equalsExact()`, `equalsNorm()` and `equalsTopo()` to `PGS_ShapePredicates`. These methods test for equality between two shapes according to different criteria.
* `createRectangularSpiral()` to `PGS_Construction`. Creates a rectangular-shaped spiral.
* `createBlobbie()` to `PGS_Construction`. Creates a "blob"-like shape.
* `largestEmptyCircle()` to `PGS_Optimisation`. Finds the largest empty circle in a set of obstacle geometries.
* `hilbertSort()` to `PGS_PointSet`. Sorts a list of points according to their location on a Hilbert curve.
* `tangentAngle()` to `PGS_Processing`. Finds the angle a the line tangent to a shape at a certain point on its perimeter.
* `variableBuffer()` to `PGS_Morphology`. Buffers a shape with a buffer whose distance varies along the shape's perimeter.
* `toGraph()` and `toDualGraph()` to `PGS_Triangulation`. Converts a triangulation mesh to a direct, or dual, (jGraphT) graph representation.
* `chordalAxis()` to `PGS_Contour`. Finds the chordal axis (a type of skeleton) of a shape.
* `tangencyPack()` to `PGS_CirclePacking`. Generates a circle packing having a pattern of tangencies specified by a triangulation.
* Added methods for Hilbert Curve, Sierpinski Carpet, Koch Snowflake and Sierpinski Tri-Curves to `PGS_Construction`.
* `poissonN()` to `PGS_PointSet`. Produces as Poisson distribution having exactly N points.
* `removeHiddenLines()` to `PGS_Processing`. Removes hidden lines from a set of overlapping/occluded polygons.
* `relativeNeighborFaces()` to `PGS_Meshing`. Finds the relative neighbour faces of a triangulation.
* `spannerFaces()` to `PGS_Meshing`. Finds the relative neighbour faces of a greedy sparse spanner of a triangulation.
* `minimumSpanningTree()` to `PGS_PointSet`. Finds the Euclidean minimum spanning tree of a set of points.
* `repulsionPack()` to `PGS_CirclePacking`. Generates a circle packing of a shape via iterative pair-repulsion.
* `simplifyDCE()` to `PGS_Morphology`. Simplifies a shape using *Discrete Curve Evolution*.
* `compoundVoronoi()` to `PGS_Voronoi`. Creates a Voronoi diagram for a set of disjoint shapes.
* Additional method signature for `buffer()` that accepts a buffer style parameter.
* Additional method signature for `offsetCurvesInward()` that accepts a curves number parameter.
* `intersectMesh()` and `subtractMesh()` to `PGS_ShapeBoolean`. Performs the associated boolean operations on mesh-like shapes, preserving individual faces during the operation (rather than dissolving remaining elements).
* `dilationErosion()` to `PGS_Morphology`. Applies a positive followed by a negative buffer (in a single operation).
* `eliminateSlivers()` to `PGS_Processing`. Removes narrow areas ("slivers") from a shape.
* `reducePrecision()` to `PGS_Morphology`. Reduces the precision of a shape, whilst ensuring the output shape is valid.
* `distanceField()` to `PGS_Contour`. Generates a contour map based on a distance field of a shape.
* `hatchSubdivision()` to `PGS_Tiling`. Randomly subdivides the plane into equal-width strips having varying lengths.
* `squareTriangleTiling()` to `PGS_Tiling`. Generates a non-periodic tiling, comprising squares and equilateral triangles.
* `cleanCoverage()` to `PGS_Processing`. Removes gaps and overlaps from meshes/polygon collections.
* `sineWarp()` to `PGS_Morphology`. Warps/perturbs a shape by displacing vertices according to a sine wave following the perimeter.
* `hilbertSortFaces()` to `PGS_Optimisation`. Sorts the faces of a GROUP shape according to hilbert curve index of each face's centroid coordinate.

### Changed
* **NOTE**: Moved all hull methods from `PGS_Processing` to `PGS_Hull`.
* Renamed `partition()` to `convexPartition()`.
* `PGS_Conversion.fromPShape()` (a major method used internally) now applies any shape affine transformations (such as `rotate()`, `scale()`, `translate()`) to the resulting geometry.
* `earCutTriangulation()` now uses JTS' implementation which supports inputs with holes.
* `PGS_Morphology.smoothGaussian()` now uses a higher default resolution.
* `PGS_Contour.straightSkeleton()` now supports multi-polygonal inputs and outputs faces (in addition to bones and branches, as before).
* `PGS_Contour.straightSkeleton()` uses a different implementation that is ~50x faster!
* Renamed `maximumInscribedRectangle()` to `maximumInscribedAARectangle()` ("axis-aligned").
* `PGS_Optimisation.maximumInscribedRectangle()` now finds the maximum-area inscribed rectangle of arbitrary orientation.
* `PGS_Transformation.touchScale()` now scales shapes that are contained within a larger shape.
* Reimplemented `PGS_CirclePacking.maximumInstribedPack()`. New algorithm is perfectly accurate and is ~10x faster!
* `PGS_Conversion.fromPVector()` now outputs an unclosed path shape if the input vertices are unclosed (rather than always treating the input as a closed polygon).
* `PGS_Transformation.resize()` now resizes a shape with respect to its center.
* `PGS_Morphology.smoothGaussian()` now supports polygons with holes.
* Reimplemented `PGS_PointSet.poisson()`. New algorithm is faster and produces better quality point set outputs.
* Styling methods in `PGS_Conversion()` (such as `setAllFillColor()`) now return the (mutated) input (rather than being `public void`), to help method chaining.
* GROUP PShapes having different child types (paths and polygons for instance) are now fully preserved during PShape<->Geometry conversion.
* `snapHull()` now uses a JTS-based implementation which improves the range of output and meaningfulness of the snap parameter (now 0...1).
* All methods in `PGS_ShapePredicates()` now output `double`.

### Fixed
* NPE when shapes created with `createShape()` in the P2D renderer were passed to `fromPShape()` (#55).
* `slice()` would sometimes fail to return some rectangular slices on a concave input (and it's more robust too now).
* Error if a GROUP shape was passed to `point(s)OnExterior()` methods.
* Triangulation methods now respect holes on shapes whose vertices wind opposite to convention (such as letter shapes created from `PFonts`).
* `fromPShape()` now properly converts singular shapes consisting of multiple contours that in turn represent multiple polygons (#67). (Note boolean flag `HANDLE_MULTICONTOUR` should be toggled to enabled this feature).
* Conversion error with shapes created via `createShape(TRIANGLE)`.
* `edgeCollapse` and `centroid` quadrangulation methods now respect shape/triangulation holes.

### Removed
* `earCutTriangulation(List<PVector> points)` from `PGS_Triangulation`.
* `isolinesFromGrid()` from `PGS_Contour` (dependency too large).
* `voronoiCirclesDiagram()` from `PGS_Voronoi` (achieved by `compoundVoronoi()`).
* `voronoiCells()` from `PGS_Voronoi` (replaced by `innerVoronoi()`).
* `voronoiDiagram(IncrementalTin tin)` from `PGS_Voronoi`.

## **1.2.0** *(2021-12-15)*

### Added
#### Classes
* **`PGS_PointSet`** — a class that generates sets of 2D points having a variety of different distributions and constraints.
* **`PGS_Coloring`** — a class for intelligent coloring of meshes (or mesh-like shapes) such that no two adjacent faces have the same color, while minimising the number of colors used.
* **`PGS_Tiling`** — a class for tiling, tessellation and subdivision of the plane using periodic or non-periodic geometric shapes.
* **`PGS_Meshing`** - a class to host mesh generation methods (excluding triangulation).

#### Methods
* `toPointsPShape()` to `PGS_Conversion`. Generates a `POINTS` type PShape from a list of PVector points.
* 3 additional method signatures (one  for each return type) for `delaunayTriangulation()` that accept a PShape only, returning a constrained triangulation.
* `minimumBoundingTriangle()` to `PGS_Optimisation`. Computes the minimum-area bounding triangle that encloses a shape or point set.
* `unionMesh()` to `PGS_ShapeBoolean`. Quickly and efficiently unions/merges the faces of a mesh-like shape together.
* `setAllStrokeToFillColor()` to `PGS_Conversion`. Sets the stroke color to the fill color for a PShape and all its descendants (separately).
* `copy()` to `PGS_Conversion`. Deep copies / clones a PShape.
* A number of new primitives to `PGS_Construction`: *serpinskiCurve*, *linearSpiral*, *fermatSpiral*.
* `extractPerimeter()` to `PGS_Processing`. Extracts a portion/subline of the perimeter of a shape between two locations.
* `interpolate()` to `PGS_Morphology`. Generates an intermediate shape between two shapes by interpolating/morphing between them.

### Changed
* `PGS_Construction` now preserves a PShape's *fillColor*, *strokeColor* and *strokeWeight* throughout forward-backward conversion. This behaviour can be toggle using the class's `PRESERVE_STYLE` flag (default = true). Note that PGS' methods will generally not preserve the style of the original PShape because JTS does not preserve geometry user data during its operations.
* `fieldWarp()` now supports `POINTS` and `GROUP` PShapes.
* `removeSmallHoles()`, `round()` and `chaikinCut()` now support `GROUP` PShape inputs.
* `partition()`, `split()` and `slice()` (from `PGS_Processing`) now output a single `GROUP` PShape (rather than a list of PShapes).
* During conversion, JTS MultiGeometries that contain a single geometry only will be converted to a first-class PShape (rather than a GROUP PShape containing one child).
* Output PShapes are now always created with a shape family of `PATH` (rather than `GEOMETRY`) to maximise compatibility with the `P2D` renderer.
* `PGS_Contour.isolines()` now accepts a contour smoothing parameter.
* `PGS_Processing.polygonizeLines()` is now more robust and faster.
* Moved `urquhartFaces()` and `gabrielFaces()` from `PGS_Triangulation` to `PGS_Meshing`.
* Renamed `micycle.pgs.utility` package to `micycle.pgs.commons`.

### Fixed
* Occasional out of bounds error with Poisson Distribution.
* Error when constrained voronoiDiagram called with `GROUP` PShape input.
* Removing duplicate vertices during PShape->Geometry conversion would remove every vertex (not just the duplicated ones).

### Removed
- `PGS_Contour.straightSkeletonSolub()` (didn't meet robustness standards).

## **1.1.3** *(2021-09-01)*
### Added
- `diameter()` to `PGS_ShapePredicates`. Computes the diameter of a shape.
- `width()` and `height()` to `PGS_ShapePredicates`.
- `createRing()` to `PGS_Construction`. Generates ring-shaped PShapes.
- `roundVertexCoords()` to PGS_Conversion. Rounds the x and y coordinates of all vertices belonging to a shape.
### Changed 
- The approach used by `PGS_Triangulation.urquhartFaces()`. The new approach is typically ~3.5x faster!
- `polygonizeLines()` now returns a `GROUP` PShape (where each face is a child shape), rather than `List<PShape>`.
- Reduced buffer line simplification applied during `offsetCurvesOutwards()`  (outer-most lines are now noticeably more smooth).
- `offsetCurvesOutward()` now supports multi polygons (GROUP PShapes).
- Algorithm used by `PGS_PointSet.poisson()`; poisson point outputs are now more densely packed and more regularly spaced.
- Triangulation methods now output `GROUP` PShapes, so individual triangles are more easily accessible.

### Fixed
- `PGS_Triangulation.gabrielFaces()` no longer retains some edges that should have been removed according to the Gabriel graph condition.
- Error that occurred during PShape conversion from very small `ELLIPSE` primitives. 
- Conversion now supports `GROUP` PShapes containing multiple shape types (such as line and polygon).
- `offsetCurvesInward()` applied to `GROUP` PShapes no longer has a line joining shape islands.

## **1.1.2** *(2021-08-10)*
### Added
- `polygonizeLines()` to `PGS_Processing`. Computes the polygonal faces formed by a set of intersecting line segments.
- Additional method signature for `PGS_Processing.generateRandomGridPoints()` that accepts a random seed.
- `fieldWarp()` to `PGS_Morphology`. Warps a shape by displacing vertices according to a 2D noise vector field.
- `radialWarp()` to `PGS_Morphology`. Warps a shape by displacing vertices along a line between each vertex and the shape centroid.
- Expand PGS_Conversion to support conversion between:
  - `TRIANGLES` PShape➜JTS `MultiPolygon`
  - `QUADS` PShape➜JTS `MultiPolygon`

### Fixed
- Issue with negative rotation values in `PGS_Transformation.rotateAroundCenter()`.

## **1.1.1** *(2021-07-28)*
### Added
- `voronoiCells()` to `PGS_Voronoi`. Generates Voronoi diagrams from shapes or point sets, outputting the diagram as polygonal cells (rather than lines only, as before).
- Additional method signature for `voronoiDiagram()` that accepts a list of points (rather than PShapes only, as before).
- `findContainedPoints()` to `PGS_ShapePredicates`. Tests each point in a given point set whether it is contained in a shape, returning only those points that are contained.

### Changed 
- Constrained Voronoi diagrams are now constrained to envelope of input shape, rather than a arbitrarily large area.
- Refactored `List<PVector>` method arguments to `Collection<PVector>` where possible.

### Fixed
- `generateRandomPoints()` no longer skips over small subsections of shapes when generating random points.

## **1.1.0** *(2021-06-13)*

### Added
#### Classes
- **`PGS_CirclePacking`** — a class for circle packings of shapes, subject to varying constraints and patterns of tangencies

#### Methods
- `closestPointPair()` to `PGS_Optimisation`. Efficiently computes the **closest** pair of points in a set of points.
- `farthestPointPair()` to `PGS_Optimisation`. Efficiently computes the **farthest** pair of points in a set of points.
- `chaikinCut()` to `PGS_Morphology`. Smoothes shapes via iterated corner cuts.
- `createHeart()` to `PGS_Construction`. Generates heart-shaped PShapes.
- `urquhartFaces()` to `PGS_Triangulation`. Tessellates a triangulation into polygons corresponding to the faces of an _Urquhart graph_.
- `gabrielFaces()` to `PGS_Triangulation`. Tessellates a triangulation into polygons corresponding to the faces of an _Gabriel graph_. 
- Additional method signature for `earCutTriangulation()` accepts a PShape argument (previously it accepted a list of points only).
- Additional method signature for `generateRandomPoints()` that accepts a random seed.
- Additional method signature for each of the existing 3 *Delaunay Triangulation* methods, accepting a collection of points only.
- Expand `PGS_Conversion` to support conversion between:
  - `PATH` PShape⟷JTS `LineString`
  - `POINTS` PShape⟷JTS `MultiPoint`
  - `LINES` PShape⟷JTS `MultiLineString`

### Changed 
- Split `PGS_Processing.concaveHull()` into `concaveHullDFS()` and `concaveHullBFS()` (the method previously used the BFS approach only).
- Compute (rather than ignore) circle sites of radius 0 (these are effectively points) in `PGS_Voronoi.voronoiCirclesDiagram()`.
- Replaced the algorithm used by `PGS_Processing.generateRandomPoints()` with a triangulation-based approach. The new approach is ~10x faster!
- Renamed `delaunayTriangulationTin()` to `delaunayTriangulationMesh()`.
- Renamed `poissonTriangulation()` to `poissonTriangulationPoints()` (the method of the same original name now outputs a PShape). 

### Fixed
- Error when `concaveHull2()` was called with alpha > 1.
- Concave hull methods no longer mutate the input point set.
- PShapes marked as closed and having less than 3 vertices could cause an error during conversion ([#22](https://github.com/micycle1/PGS/issues/22)).
- `PGS_Conversion.toPVector()` now handles [primitive](https://processing.org/examples/shapeprimitives.html) PShapes.
- Constrained Delaunay triangulations now respect shape holes.

### Removed
- `PGS_Processing.concaveHull()` (see *Changed*)

## **1.0.0** *(2021-05-06)*