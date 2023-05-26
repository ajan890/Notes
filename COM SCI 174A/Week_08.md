# Week 8
### HSR: Ray Casting Algorithm
* Forward vs. backward ray casting<br>
![image](https://github.com/ajan890/Notes/assets/66571533/19e3d7c9-8ccb-4d41-a1ae-cc604c1b4c45)<br>
* Ray Casting is a World Space or Eye Space visible surface algorithm
* Window is divided into a rectangular array of pixels

#### Algorithm
```
for (each pixel in viewport):
  generate ray from Eye (O) through pixel
  find intersection between ray and objects
  pick intersection point closest to Eye (O)
  Illuminate the closest intersection point
  plot pixel with illuminated color of closest object
```
![image](https://github.com/ajan890/Notes/assets/66571533/398141e7-091d-4d10-a147-511ccb314eb2)<br>
### Ray Casting Pipeline
![image](https://github.com/ajan890/Notes/assets/66571533/81ce5e8d-5504-441c-a9b3-23ecb4d2c1fd)<br>

### Ray Casting Algorithm
#### Step 1: Generate ray emanating from Eye (O) through pixel
* Superimpose a grid (representing viewport) onto the area defined by $(-\tan(\theta), -\tan(\theta)/A_r)$, $(\tan(\theta), \tan(\theta)/A_r)$ on $z=1$ plane.
* Width of a pixel on the $z = 1$ plane will be $\frac{2 \cdot \tan(\theta)}{X_{res}}$
* Point corresponding to center of pixel (i, j) is $P = (x_p, y_p, 1)$
```math
  x_p = -\tan(\theta) + (i + 0.5) \cdot \frac{2 \tan(\theta)}{X_{res}} \:\:\:\:\:\:\:\:\:\:\:\: y_p = \frac{1}{A_r}\cdot (\tan(\theta) - (j + 0.5) \cdot \frac{2\tan(\theta)}{Y_{res}})
```
* Parametric ray emanating from eye (origin) through pixel P:
  * $x = x_e + t(x_p - x_e), y = y_e + t(y_p - y_e), z = z_e + t(z_p - z_e)$
  * For ES $(x_e = y_e = z_e = 0)$: $x = tx_p, y = ty_p, z = t$ <br>
![image](https://github.com/ajan890/Notes/assets/66571533/85b906da-9f70-4270-b172-f2c979a3a081)<br>
#### Step 2: Find intersection between ray and objects
a. Intersection test: if no intersection, skip part b <br>
b. Intersection calculation: for spheres and for polygons

**Ray Casting Spheres**
1. Transform center of sphere to Eye Space (radius remains same)
2. Equation of sphere: $(x - x_c)^2 + (y - y_c)^2 + (z - z_c)^2 - R^2 = 0$
3. Parametric equation of ray (ES): $x = tx_p, y = ty_p, z = t$
4. Find intersection of ray with sphere: plug in equation of ray in equation of sphere $At^2 + Bt + C = 0$
    * No real solution $\implies$ ray does not intersect sphere
    * 1 real solution $\implies$ ray grazes sphere
    * 2 real solutions $\implies$ entering and exiting points, pick lower +ve t, and calculate P 
5. Find normal at intersection point P: $N = P - P_c$
6. Illuminate using P, N, E of closest +ve t

**Ray Casting Polygons**
1. Transform polygon to Eye Space
2. Equation of the plane containing polygon: $Ax + By + Cz + D = 0$
3. Parametric equation of ray (ES):  $x = tx_p, y = ty_p, z = t$
4. Find intersection of ray with plane: plug in equation of ray in equation of plane
    * If denominator = 0, ray is parallel to plane $\implies$ no intersection
5. Check if intersection point P is contained inside the polygon
    * Project polygon and point ontl one of the primary planes (use max of N components)
    * Use one of the "point inside polygon" tests
6. Find normal N at intersection point using pilinear interpolation
7. Illuminate using P, N, e of closest +ve t

**Ray Casting in World Space**
* Vectors
  * $V_z = \text{normalize}(COI - OBS)$
  * $V_x = V_z \times <0,1, 0>$
  * $V_y = V_x \times V_Z$

* Ray
  * Parametric equation: $OBS + t(P - OBS)$, where P is given by
```math
\begin{align*}
x_p &= -\tan(\theta) + (i + 0.5) \cdot \frac{2 \tan(\theta)}{X_{res}} \cdot V_x\\
y_p &= \frac{1}{A_r} \cdot (\tan(\theta) - (j + 0.5) \cdot \frac{2 \tan(\theta)}{Y_{res}} \cdot V_y)\\
z_p &= V_z
\end{align*}
```
* Rest of calculations are similar to ray casting in ES<br>
![image](https://github.com/ajan890/Notes/assets/66571533/168a0b20-e60e-4299-8af1-cea343211c00)<br>

### Ray Tracing
* Also referred to as Recursive Ray Tracing
* Handles reflections, refractions, shadows
* Primary ray: ray from eye into the world
* Secondary rays: reflected, refracted, shadow
* Illumination for ray tree:
  * **I = ambient + diffuse + specular + $k_rI_r$ + $k_tI_t$**
  * $k_r$: coefficient of reflection
  * $k_t$: coefficient of transmission
* Attennuate $I_r$ and $I_t$ by distance the ray travels<br>
![image](https://github.com/ajan890/Notes/assets/66571533/71e1c902-4605-479b-b18a-120e342dc5ed)<br>

#### Equations
* Reflected Ray Direction
  * $r = i - 2(i \cdot n) n$
* Refracted Ray Direction
  * Snell's Law: $\eta_1\sin(\theta_i) = \eta_2\sin(\theta_t)$
  * $t = \frac{\eta_1}{\eta_2} i + \left(\frac{\eta_1}{\eta_2} \cos(\theta_i) - \sqrt{1 - \sin^2(\theta_t)}\right) \cdot n$
  * $\sin^2(\theta_t) = \left(\frac{\eta_1}{\eta_2}\right)^2\sin^2(\theta_i) = \left(\frac{\eta_1}{\eta_2}\right)^2 (1 - \cos^2(\theta_i))$

![image](https://github.com/ajan890/Notes/assets/66571533/66e09111-9c5e-44c5-b104-8859d641c75d)

### Ray Tracing: Illumination
* Ray Tree
  * Formed of primary, secondary, shadow rays
  * Evaluated bottom up

![image](https://github.com/ajan890/Notes/assets/66571533/3145c7e9-db15-410b-ba47-007723437ae1)
* Tree terminates if
  * Nointersection for a ray
  * Tree depth has reached a specified level
  * Intensity of I<sub>r</sub> or I<sub>t</sub> becomes very low
  * Ray has traveled a maximum distance

### Ray Tracing: Speed
* There is a ray for every pixel on the screen.
* Efficiency Considerations
  * Total # of shadow rays spawned = $m(2^n - 1)$
    * m = number of light sources; n = depth of ray-tree
    * This assumes that 2 rays are spawned per ray at intersection.  
    * 1 splits into 2, which splits into 4.
  * Total number of rays = $(m + 1)(2^n - 1)$
  * Back faces cannot be culled
  * Clipping cannot be done for view volume or behind eye
  * 75%-95% of the time is spent in intersection calculations
  * Use bounding box/sphere testing or hierarchies (octrees)

#### Space Subdivision
* If a part of the screen has a lot of items, we can divide the screen into multiple regions.
  * 4 regions = "Quartree" (screen height and width are cut down the middle for 4 regions)
  * If a region still has a lot of items, the region can be divided into 4 regions again, in a similar manner.  8 regions = "Octree".  Divisions can continue indefinitely as needed.<br>
![image](https://github.com/ajan890/Notes/assets/66571533/1d6862c8-2233-4d13-a00a-7d020aad9800)<br>
Source: Wikipedia<br>
  * In this case, the screen is divided into 64 main regions, which are subdivided into even smaller subregions.
* Suppose a ray began in the bottom corner and travels diagonally up-left.  The ray will pass through many regions.
  * However, if the ray intersects an object in the first region, then there is no need to check the other regions.
  * Therefore, if there are a lot of items, this can dramatically speed up ray tracing since the entire screen of objects would not have to be checked for every ray.

#### Aliasing
* Aliasing in RT
  * Spatial aliasing
  * Temporal aliasing: for small objects
* Anti-Aliased Ray Tracing
  1. Super-sampling (eye has 1.44M photoreceptors)
  2. Adaptive super-sampling (along edges of objects)
  3. Stochastic RT

### Stochastic Ray Tracing
AKA Distributed Ray Tracing
* **Antialiasing**: distribute over pixel sampling area
* **Gloss**: distribute reflected rays
* **Translucency**: distribute refracted rays
* **Penumbra**: distribute shadow rays
* **Depth of Field**: distribute over lens diameter
* **Motion Blur**: distribute across frames<br>

![image](https://github.com/ajan890/Notes/assets/66571533/7b0308db-1cf5-44e5-be9f-3466c0003da3)<br>
* Specular takes one light sample at the exact point it hits.
* Glossy uses a 5x5 grid (or finer, depending on how glossy the object is)
* Diffuse uses a jittered 5x5 grid (randomly selected 25 points near a 5x5, or finer)<br>
![image](https://github.com/ajan890/Notes/assets/66571533/da6625ed-7bbb-4e46-8981-f3e52b4d3607)<br>
* The larger area sampled, the more blurry the image gets.


![image](https://github.com/ajan890/Notes/assets/66571533/936bbd06-f0b7-422e-adfe-51a8700fd472)<br>
* Notice that Stochastic Ray Tracing allows for shadows, translucency, glossiness, etc.

![image](https://github.com/ajan890/Notes/assets/66571533/94e135a1-b40e-4f89-a774-6e782d5cbfc0)<br>
* Far-away objects appear more blurry since rays diverge as you get farther away, so a larger area is sampled in that pixel.

![image](https://github.com/ajan890/Notes/assets/66571533/aec3015f-c571-42f6-8441-3131e2cc0a3e)<br>
* In this case, the focus is on further objects, so the closer objects are blurred due to larger area sampling

![image](https://github.com/ajan890/Notes/assets/66571533/8ab145d3-b1b6-402e-8858-a6ac80c8deb4)<br>
* For motion blur, pixels for multiple frames of an animation are averaged together.







