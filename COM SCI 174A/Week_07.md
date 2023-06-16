# Week 7
### Polygon vs. Vertex Attributes
* Polygon Attributes
    * Color
    * Normal
* Vertex Attributes
    * Coordinates (position)
    * Color
    * Normal
    * Texture coords


### Flat or Constant or Faceted Shading
* Use N of poly
* Find I at center or at any vertex of poly
* Apply that same color to all points inside poly
* In essence, it means:
    * N is constant across poly
    * Light is at infinity, N * L is constant across poly
    * Viewer is at infinity, N * V is constant across poly
* Which space to compute N and illuminate?
    * Either WS or ES, not in PS

### Problem with Flat Shading
* Mach bands is an optical illusion named after the physicist Ernst Mach.  It exaggerates the contrast between edges of slightly differing shades of gray, as soon as they contact one another, by triggering edge-detection in the human visual system.<br>

![image](https://github.com/ajan890/Notes/assets/66571533/d4b195f7-e50e-4865-88a3-4b7ac82929a8)<br>

### Gouraud Smooth Shading
* Also called “Intensity” interpolation or “Color” interpolation shading
* WS: Find I at each vertex and illuminate vertex
* SS: Interpolate across poly face
* Store normals at vertices
    * Average normals of polygons sharing vertex
    * During tessalation, e.g., sphere
    * What about hard edges?
* Uses bilinear interpolation (described below)<br>
![image](https://github.com/ajan890/Notes/assets/66571533/8d7ff9e7-d553-4159-b003-0f20a80945c3)<br>

* Issues with Gouraud Shading
    * Rotating polygons
    * Specular reflection with large polygons
        * At poly’s center
        * At poly’s vertex
    * Mach banding not completely eliminated

### Interpolation
#### Barycentric Interpolation

![image](https://github.com/ajan890/Notes/assets/66571533/fb0da6de-5ea7-4203-889f-f9f4b62a83c1)<br>

The further _t_ is from the red point, the more blue we want.  The further _t_ is from the blue point, the more red we want.<br>

* Percent blue = _t_
* Percent red = 1 - _t_
* Value at $t = (1 - t) \cdot x_1 + t \cdot x_2$<br>

This can be expanded to two dimensions:<br>
![image](https://github.com/ajan890/Notes/assets/66571533/56c1e929-9873-4941-84fe-c536b3833d6d)

### Bilinear Interpolation
* Can be used to interpolate z, color, normal, texture, etc.
* Interpolate along two edges
* Interpolate along scanline
* Incremental calculations<br>
![image](https://github.com/ajan890/Notes/assets/66571533/cdfd8575-b3dd-41bb-a567-0b98e965a521)<br>

### Phong Smooth Shading
* Also called “Normal Vector” interpolation shading
* Calculate intensity at each pixel
* Interpolate normals similar to others, then normalize
* Much more computation, but much better looking images<br>
![image](https://github.com/ajan890/Notes/assets/66571533/aeacf020-e1f9-443c-8e4f-8cb322792148)<br>

### Smooth Shadings
* Issues with interpolated shading
    * Polygon silouhette
    * Orientation dependence (trianges ok)
    * Problems at shared vertices
    * Unrepresentative vertex normals<br>
![image](https://github.com/ajan890/Notes/assets/66571533/837c2880-671d-4137-901e-5230e76ae34a)<br>
* We can’t smooth shade everything, since smooth shading removes hard edges.
* A cube would look like this, if it was shaded with smooth shading:<br>
![image](https://github.com/ajan890/Notes/assets/66571533/0d1ec35c-60ea-4963-b9c1-5b3c64714d07)<br>

#### Flat vs Smooth Shading
* Problem with this step:
    * Distribute it to all three vertices identically
* **What if some vertices are shared by more than one triangle?**
    * Could happen when we are summating our triangles using lists of “indices” into a list of (non-repeating, unique, more compact) vertices
    * A vertex can’t have two normals at once, logistically!
    * Other triangles will fight over assigning normals to a vertex
    * Conclusion: Sometimes we <span style="text-decoration:underline;">should</span> put repeats in our vertex list.  We shouldn’t try to re-use indices at seams.
        * Instead, store extra/duplicate vertices at a position, with differing normals

### GuerrillaCG Series: Flat vs Gouraud Shading
* For this to work, shapes must be modeled a certain way (“seams”)
* Must store multiple vertices touching the same position
* Must be able to store conflicting normal data even if position data matches
* [https://www.youtube.com/watch?v=PMgjVJogIbc&t=6s](https://www.youtube.com/watch?v=PMgjVJogIbc&t=6s)

### Shading Recap
#### Flat Shading
* Illuminate a poly only once
* No interpolation
#### Gouraud Shading
* Illuminate vertices of poly
* Interpolate colors at vertices
#### Phong Shading
* Illuminate each point inside poly
* Interpolate normals at vertices
#### Illumination in World/Eye Space, interpolation in Screen Space

### Illumination Recap
* $I = k_a \cdot I_a \cdot O_d + f_{att} \cdot k_d \cdot I_p \cdot (N \cdot L) \cdot O_d + f_{att} \cdot k_s \cdot I_p \cdot (R \cdot V)^n$

#### Material Properties:
* k<sub>a</sub>, k<sub>d</sub>, k<sub>s</sub>: ambient, diffuse, specular reflection coefficients of object
* O<sub>d</sub>: color of object
* I<sub>a</sub>: intensity of ambient light
* I<sub>p</sub>: intensity of point light
* n: specular exponent

#### Geometric Properties:
* N: orientation of object at point being illuminated
* L: depends on location of point and light
* R: depends on N and L
* V: depends on location of point and eye
* f<sub>att</sub>: depends on distance between point and light
* A<sub>att</sub>: depends on distance between point and eye

### Non-Photorealistic Shading
* Cartoon like effects
* Color = (N·L > 0.5) ? Color1 : Color2
* Color changes with object’s shape and light’s position
* Silhouette: (N·V &lt; 0.01) ? Black : Color<br>
![image](https://github.com/ajan890/Notes/assets/66571533/da7c5eef-78e0-40d2-b5fa-a76b48c99133)<br>

### Global Illumination
* Ray Tracing: shadows, reflections, refractions
* Radiosity
    * Based upon light energy conservation
    * Requires solution of a large set of equations involving all surfaces<br>
![image](https://github.com/ajan890/Notes/assets/66571533/7699b8f5-96e8-41ef-9276-fc4eed19b861)<br>

### Mappings
* Texture Mapping
* Bump Mapping
* Displacement Mapping
* Environment Mapping
* Procedural Mapping

### Texture Mapping
* AKA Pattern mapping
* Map a digitized image onto a poly face
* Individual elements are called Texels
* u, v and s, t coordinates
* Use texel color as diffuse color
* Texture replication (as in A4)<br>

![image](https://github.com/ajan890/Notes/assets/66571533/8e6681aa-3aee-4884-9986-2e71139766ab)<br>

### Texture Mapping: Aliasing
* Due to high-frequency patterns
* Mip Mapping (as in A4)<br>

![image](https://github.com/ajan890/Notes/assets/66571533/7471a6be-e7d2-437e-8ca5-079824e162bc)<br>

### Multi-Texturing
* Apply multiple textures on the same object - blend<br>
![image](https://github.com/ajan890/Notes/assets/66571533/475ec59b-a4d3-4890-824c-117600a360b2)<br>

### Bump and Displacement Mappings
* Displacement Mapping:
    * Displace point on surface of object
    * Change object’s geometry
    * _P’ = P + B * N_
* Bump mapping
    * Distort normal to simulate bump without altering object’s geometry
    * $N' = \frac{B_u (N \cdot P_t) - B_v (N \cdot P_s)}{|N|}$

* B<sub>u</sub>, B<sub>v</sub> = ∂B/∂u, ∂B/∂v, respectively
* P<sub>s</sub>, P<sub>t</sub> =∂P/∂s, ∂P/∂t, respectively
* **Displacement mapping changes the object’s geometry, while bump mapping is just a texture that gives the illusion.**

### Displacement Mapping
* Points actually move
* Requires hidden surface removal
* [Bump vs. Displacement 1](https://www.youtube.com/watch?v=1mdR2imNeZI&ab_channel=GuerrillaCG)
* [Bump vs. Displacement 2](https://www.youtube.com/watch?v=xpEUdGoyTGI&ab_channel=MHTutorials%2CtheModelingHub)
* Notice that the shadows are different.<br>
![image](https://github.com/ajan890/Notes/assets/66571533/b9a2504c-09a4-4450-b9be-d9ba8eaa3e4d)<br>


### Environmental Mapping
* AKA Reflection Mapping
* Use polar (or spherical) coordinates of reflected ray to map
* Map defined usually on 6 faces of a box (cube map) or a sphere<br>
![image](https://github.com/ajan890/Notes/assets/66571533/03dc6f98-5a76-4161-a07f-7efcca130e7d)<br>
* More examples
* **I = ambient + diffuse + specular + k<sub>r</sub> * I<sub>r</sub>**
    * k<sub>r</sub>: coefficient of reflection
    * I<sub>r</sub>: reflection intensity<br>
![image](https://github.com/ajan890/Notes/assets/66571533/f202c0e1-a242-44f6-a5dc-7e7cd74abdd1)<br>
* These mappings can be used to do reflections:
    * Imagine a camera at that point to fill in the sides of the sphere or the cube
    * Apply that texture on the reflective object.

### Shadow Algorithms
* Types
    * Object precision: shadow volume method
    * Image precision: 2-pass z-buffer method
* Main Idea
    * P is not visible fom light source implies P is in shadow
* Strategy
    * Identify areas on polys which are not directly visible from light source
    * Mark these areas
    * Do HSR (hidden surface removal) from eye position
    * Areas marked for shadow are rendered only with ambient light.
#### Shadow Volume Method
1. Create a shadow volume for each front facing polygon
2. Put shadow volume in polygon database
3. Do parity test to determine if a visible point is in shadow
    1. Initial value = # of shadow volumes containing eye position
    2. Increment for front-facing shadow polygon
    3. Decrement for back-facing shadow polygon
    4. If parity > 0 ⇒ point is in shadow<br>
![image](https://github.com/ajan890/Notes/assets/66571533/27378500-9b6f-4cff-8d17-4d8d14fe97d4)<br>

![image](https://github.com/ajan890/Notes/assets/66571533/52cc70d7-0f2c-48d6-b8c4-80c1c0adc002)<br>

Whenever an object is rendered, create volumes behind it.  Increment areas where covered, decrement areas if the object is removed.  0 means no shadows.<br>

### 2-Pass Z-Buffer Method (aka Shadow Map method)
1. Do z-buffer (full) from light position
    1. store results in shadow buffer
2. Do z-buffer (scanline or full) from eye position
    2. for each (visible) pixel in scanline
        1. Do inverse map point to WS
        2. Map to SS of shadow buffer
        3. Compare z with that of shadow buffer at x, y
        4. If shadow_buf[x][y] &lt; z, then point is in shadow<br>
![image](https://github.com/ajan890/Notes/assets/66571533/1c90c2d8-e8fb-4530-bc0a-e313518ff4ca)<br>
![image](https://github.com/ajan890/Notes/assets/66571533/8d9f8d34-ee1f-44e5-aa89-603e764ab946)<br>

* **Advantages**
    * Simple to implement
* **Disadvantages**
    * Shadow distant from light source may appear blocky
    * A large size of shadow-buffer is required
    * Depth buffer bit resolution- usually 8-bit
    * Umbra vs. penumbra<br>

![image](https://github.com/ajan890/Notes/assets/66571533/115d8887-b6a3-48c0-8a57-666cd45afb6c)<br>
