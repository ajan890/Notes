# Week 5
## Hidden Surface Removals
* **Object Types**
  * Polymesh
  * Volume
  * Free form surfaces
  * CSG
  * Implicit surfaces
* ** Basic Operations**
  * Establish priorities among polygons, objects, etc.
  * Collect overlapping elements and use priorities to resolve visibility

## Backface Culling
* N = outward normal vector of face
* P = a point on face
* E = eye vector (from a point on face to eye = Eye - P)<br>

* It is a front face if:
  * In World Space: N · E > 0
  * In Eye/Camera Space: N · (-P) > 0 or N · P < 0
  * In Projection Space (after perspective division): N<sub>z</sub> < 0
* All operations in backface culling is done in projection space.

## Hidden Surface Removals
* **Algorithm Types**
  * Object/World/Eye Space: operation 1 and 2 both at object resolution
  * Screen/Image Space: operations 1 and 2, both at pixel resolution
  * List-Priority: operation 1 at object resolution, operation 2 at pixel resolution
* **Evaluation Criteria**
  * Flexibility: what types of objects can it handle?
  * Special Effects: transparency, anti-aliasing
  * Memory Requirements
  * Speed
* **Object Space Algorithms**
  * Painter's Algorithm
    * Called this because it is similar to the process of painting: you paint the background first, then the foreground, etc.
* **Screen Precision Algorithms**
  * Z-Buffer
  * Scanline Z-Buffer
  * Ray Casting

## Painter's Algorithm
![image](https://github.com/ajan890/Notes/assets/66571533/fd39ca93-1c1d-44ed-beba-8d64397ef4ae)

1. Sort all polygons by z-depth
2. Scan-convert polygons in back-to-front order
   * So paint poly R first, then Q, then P 

**Cannot handle certain cases:**
1. Cyclic polygons
2. Intersecting polygons

![image](https://github.com/ajan890/Notes/assets/66571533/67afeb5d-fa27-4de5-bef8-f6103f8d7df8)

## Z-Buffer Algorithm
zb[X<sub>res</sub>][Y<sub>res</sub>] = ∞<br>
cb[X<sub>res</sub>][Y<sub>res</sub>] = background<br>
```
1. for each polygon
2.   for each pixel covered by polygon:
3.     calculate z for polygon at (x, y)
4.     if (z > zb[x][y])
5.       zb[x][y] = z
6.       cb[x][y] = color of polygon
```
* **Properties**
  * Image/screen precision algorithm
  * Easy to implement in software and hardware
  * Polygons scan-converted into framebuffer in random order
  * No pre-sorting of objects/polygons necessary

* **Disadvantages**
  * Memory requirements for storing color and depth for entire image
  * Aliasing issues
  * Complexity depends on polygon's protection area on the screen
  * Hard to handle transparency

* **Advantages**
  * Handles penetrating and cyclic objects 
  * Extends to various kinds of faces other than polygons
  * Simploicity and ease of software implementation
  * Easily implementable in hardware
  * Be modified to reduce memory requirements
  * Can be extended to A-buffer to reduce aliasing
  * Theoretically it can handle any number of polygons

## Scanline Z-Buffer Algorithm
* A **scanline** is an imaginary line across the screen
* Move the scanline from the bottom to top of the screen.
* When the scanline reaches a polygon (regardless of z-value), the polygon divides the scanline into sections where they intersect.
  * these sections are called **spans**, or **span segments**.
* If on a given line, there is only one polygon intersecting the scanline, it colors the pixels in the span created by the two sides of the polygon to the polygon's color.
* If there are two polygons, one on top of another (for example, the scan line crosses boundaries in the order: Red-Blue-Blue-Red), then it checks the z-value of the polygons and colors accordingly.
* Using this strategy, the computer only has to allocate memory for a single scanline.

zb[X<sub>res</sub>]; cb[X<sub>res</sub>];<br>
```
1. for each scanline (y = scanline, reset zb and cb)
2.   for each polygon which intersects scanline
3.     scan convert for specific scanline; determine span segment
4.     for each pixel in span segment (x = pixel location)
5.       calculate z for polygon at (x, y)
6.       if (z < zb[x])
7.         zb[h] = z
8.         cb[x] = color of polygon
```

* **Advantages**
  * Same as z-buffer
  * Less memory requirement than z-buffer
* **Disadvantages**
  * Multiple passes through polygon database

## Efficiency Considerations in Z-Buffer Algorithms
* **Speed Considerations**
  * Bounding box testing
    * Y<sub>min</sub>/Y<sub>max</sub> test: associate Y<sub>min</sub>/Y<sub>max</sub> with each face (Step 2)
    * Calculate left and right ends: x-intercept with scanline (Step 3)
  * Incremental calculation of Z or bilinear interpolation (Step 5)
    * Ax + By + Cz + D = 0
    * z = -(Ax + By + D) / C
    * z<sub>x+1</sub> - z<sub>x</sub> = - A / C => z<sub>x+1</sub> = z<sub>x</sub> + Δz (where Δz = -A / C)
    * Space subdivision
    * Hierarchical subdivision
