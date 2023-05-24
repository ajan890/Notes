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
