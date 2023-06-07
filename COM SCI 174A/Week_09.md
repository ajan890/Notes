# Week 9
## Transparency / Opacity
* Matte: coverage info
* Add a $4^{\text{th}}$ channel to color: $\alpha$ = opacity (RGBA), range [0, 1]
* $\alpha = 0 \implies$ fully transparent; $a = 1 \implies$ fully opaque
* Transparency = 1 - Opacity
* Applications
  * Image compositing, e.g., combining computer-rendered images with live footage
  * Particle rendering, e.g., smoke, snow, fire
  * Volume rendering

### Blending
* Pre-multiplied vs. straight alpha
* **Operators: over, in, out, atop, xor**
* Alpha blending or alpha compositing (**over operator**)
  * Straight<br>
  $C_0 = \frac{C_f \alpha_f + C_b \alpha_b (1 - \alpha_f)}{\alpha_f + \alpha_b (1 - \alpha_f)}$<br>
  * Pre-multiplied<br>
  $c_0 = c_f + c_b(1 - \alpha_f)$<br>
  $\alpha_0 = \alpha_f + \alpha_b (1 - \alpha_f)$<br>
    * Final color ($c_0$) = Front color plus back color times $(1 - \alpha)$, essentially "how much do you see the back color through the front color."
    * Final opacity ($\alpha_0$) = Front opacity plus back opacity times transparency of front layer
    * These are affine combinations on a function of $\alpha_f$.

###  Procedural Models
* For modeling cloud, smoke, water, crowd, flock, waves: using behavior
* Describe objects in an algorithmic manner (e.g., spheres and ellipsoids), generate polygons only when necessary
* Combine computer graphics with physical laws or for modeling solid objects
  * Particle systems obeying Newton's Laws, e.g., fireworks, smoke, flame
  * Language based models for natural objects, e.g., plants, snowflakes
  * Fractal geometry for natural phenomenon, using level of detail, e.g., mountains
    * Level of detail: use more detail (more tessellation) for closer objects, less for further objects
  * Procedural noise for realistic motion, e.g., clouds, fluid motion

### Particle Modeling
* Used for simulating fuzzy phenomena
* Examples: chaotic, natural, or chemical systems
  * Like fire, smoke, explosions, snow, dust, etc.
* Modeled as an emitter, like sphere or box
* Particle behavior parameters
  * Spawning rate
  * Initial velocity vector
  * Lifetime
  * Color, etc.
  * Collision?

### Particle Rendering
* Rendered usually as textured bill-boarded quads
  * Sprites vs. billboards
    * You don't want to rerender the entire screen just because one object moved
    * Difference between the two: billboards always face the camera; they have depth.  sprites are just images.
  * Integrate with z-buffer
* In games, as a single pxel
* Examples: 
  * Particles and Billboards
  * Interactive 3D Graphics

### Volume Rendering
* 2D projection of 3D sampled dataset
* Volume rendering algorithms:
  * Usually no illumination or shadows, just compositing
  * Therefore only ray-casting, no recursive ray-tracing
  * No perspective, only parallel projection

#### Voxels
* **Volume dataset:** 3D regular grid of voxels
  * Like a 2D grid is divided into pixels, a 3D grid is divided into cubes, or voxels.
* **Voxel:** a small cube at i, j, k, with sides $\Delta x, \Delta y, \Delta z$
* Each grid point has a scalar value f(x, y, z)
* For example, density, intensity, CT scan, MRI
* Voxelize more complex implicit surfaces
* If $\Delta x = \Delta y = \Delta z \implies$ structured volume dataset
* Transfer function: to map lattice scalar values to RGBA
* Based on viewer location, there's a natural ordering of voxels<br>

![image](https://github.com/ajan890/Notes/assets/66571533/4c1b5966-b28a-49b2-9401-9fd5b2638fd9)<br>
* If needed, you can *voxelize* 3D objects into voxels.  (Like building a sphere in Minecraft)

#### Marching Cubes
* Object based volume rendering technique
* Create poly mesh by extracting iso-surfaces: $f_{i, j, k} = c$
* Color vertices: if $f_{i, j, k} < c$, then white, else black<br><br>
![image](https://github.com/ajan890/Notes/assets/66571533/c01d0cc4-7740-4600-bde2-10aa1a5f6492)<br>
![image](https://github.com/ajan890/Notes/assets/66571533/38cf2746-b3be-4a9b-92d0-9e1b88ec522f)<br>
**Aside: Marching Squares**
* 16 cases of vertex labeling, but only 4 unique cases
* Ambiguous cases
![image](https://github.com/ajan890/Notes/assets/66571533/b388dac4-5d8b-4af2-8dbe-7a7b47b00d3a)
  * Left: all 16 possible cases
  * Right-Up: 4 unique cases
  * Middle-Down: These two cases have two diagonal corners in the object.  You must decide which division is correct.  To do this, you use the information from neighboring squares/cubes. 
  * Right-Down: Both these cases are possible with one corner in the object (you lose detail).  We assume (a) would be the case rather than (b).  To prevent this, use smaller voxels!
* Can be extrapolated to cubes<br>
![image](https://github.com/ajan890/Notes/assets/66571533/430c907c-182d-4fa1-a1fb-5a76bc53a230)<br>
* There are 14 unique cases, but $2^8 = 256$ total cases.
* The planes show possible ways the 3D object may pass through the cube.
* This is called the "Marching Square/Cube" algorithm because you start from one square and go to neighboring squares.
  * Can be used to generate triangle meshes from a function.
  * Given the points, inside and outside an object defined by the implicit function, a triangle mesh to make up the surface can be created.
* **The vertices need not be binary, they can be on a gradient**
  * If we use for example an equation that gives every vertex a number between 0 and 16, then all the corners have some value between 0 and 16.  We then establish a threshold.  All values higher get set to 1 when using this algorithm, all values lower get set to 0.  Therefore, we can render a gradient of 3D meshes from different threshold values.
  * This can also be thought of as a 4D mesh, where the fourth dimension is the continuous gradient of the threshold.

#### Splatting
* Object-resolution volume rendering technique
* Each volume element (voxel) is splatted on screen as a snowball
* Voxels splatted in BTF order wrt to the viewer
* Splats are rendered and composited as disks on the screen
* Circular, ellipsoidal or Gaussian splats
* Aliasing
  * If each voxel is converted to one pixel on the screen, you get aliasing.  Therefore, each voxel should cover multiple pixels (which would blend multiple voxels) to prevent aliasing.<br>
![image](https://github.com/ajan890/Notes/assets/66571533/912a8c34-d294-46b7-81ac-23d1d4e43b1b)<br>
* If we are using parallel projection, we can generate a footprint for one voxel and use the same footprint for all the other voxels, since in parallel projection, every voxel will take up the same area.  The same does not apply in perspective projection.

#### V-Buffer
* Image based volume rendering technique
* Ray casting through volume
* Trilinear interpolation to determine RGBA at non-lattice point
* Accumulate color and opacity
* 3 levels of sampling:
  * Voxel lattice: $x_{i, j, k}$
  * Sampling along ray: $y_i$
  * Image plane: $z_{i, j}$
* 2 pipelines (color/opacity): $c = c_1 + c_2(1 - \alpha_1)$; $\alpha = \alpha_1 + \alpha_2(1 - \alpha_1)$
* Parametric equation of ray: $p + t \cdot d$
  * p: pixel location
  * d: ray direction
  * t: parameter along ray
* Step through ray by incrementing t<br>

![image](https://github.com/ajan890/Notes/assets/66571533/69426737-e18c-4fa8-a78a-7b02701af4b9)<br>
**Algorithm**<br>
![image](https://github.com/ajan890/Notes/assets/66571533/5f76b142-defc-4796-8489-0ed02e588247)<br>
**V-Buffer Transfer Function**<br>
* X-Ray density data for each voxel
* Assign different color to each peak in histogram
* Opacity values based on emphasis<br>
![image](https://github.com/ajan890/Notes/assets/66571533/40e5e426-1d71-4ff3-ac83-2e4f9a25b783)<br>
  * Top left: Example X-ray density and frequency
  * Others: Color graphs; for every frequency on frequency graph, assign a color based on the X-ray density associated with it<br>
**V-Buffer Speedups**<br>
* Early ray termination
  * Stop when opacity reaches 1
  * Or when ray exits volume
* Empty space skipping
* Octree or BSP trees
* Temporal use of voxels
### Aliasing
#### Rasterization
* Spatial aliasing in CG
  * Jagged lines while rasterization
  * Going from continuous representation to a sampled approximation, which has limited resolution
  * Pixels on screen have fixed number, size, shape and location
  * Splatting during volume rendering<br>
![image](https://github.com/ajan890/Notes/assets/66571533/f9d29677-8663-407a-ace0-f029d2cb316d)<br>
* To anti-alias, instead of making each pixel either colored or not, use shades.  For example, (row 0, col 3) shouldn't be completely blue or completely white; rather a shade of light blue calculated from the area the blue triangle covers the pixel.

#### Temporal
* Temporal aliasing in CG<br>
![image](https://github.com/ajan890/Notes/assets/66571533/d60d6b1d-0380-4028-9036-2145c6d100f3)<br>
* Suppose you have a very small object flying in the scene. 
  * If the object happens the be on one of the rays, it gets captured in one pixel.  However, on another frame, what if it misses two rays of two pixels?  Then it doesn't get captured.
  * This causes the small flying object to flicker in and out of view, a phenomenon called temporal aliasing.
* To prevent this:
  * Use stochastic ray tracing (multiple rays per pixel)
  * Increase frames per second (rays sample more often)
  * Use smaller pixels (smaller gaps between rays)

#### Mappings
* Due to high-frequency patterns
* Mip Mapping (as in A4)<br>
![image](https://github.com/ajan890/Notes/assets/66571533/5a3c9282-f00c-42af-8c04-2f422479ff28)<br>
* High frequency patterns may not display properly if the frequency is higher than the resolution.

#### Shadows
* Blocky shadow borders<br>
![image](https://github.com/ajan890/Notes/assets/66571533/5f0ce26b-a5bf-4125-b8df-f5dc7867979c)<br>

#### Splatting
* Shape of splat<br>
![image](https://github.com/ajan890/Notes/assets/66571533/912a8c34-d294-46b7-81ac-23d1d4e43b1b)<br>

#### Anti-Aliasing
* Area averaging<br>
![image](https://github.com/ajan890/Notes/assets/66571533/fc13b742-2307-4181-890b-39ce213dfdf6)<br>
* Super-sampling, then averaging or blending
* Stochastic (or distributed) super-sampling
* In h/w, use super-sampled offline buffer, then average to frame buffer

### Incremental Calculations
* Plane equation during z-buffering for depth
  * $z_x = -\frac{Ax + By + D}{C}$
  * $z_{x+1} = z_x - \frac{A}{C}$
* Bilinear interpolations during shading for colors, normals, depth, texture, or anything else provided at the vertices
  * $z_x = z_a + \frac{(x - x_a)}{(x_b - x_a)} \cdot (z_b - z_a)$
  * $z_{x+1} = z_x + \frac{(z_b - z_a)}{(x_b - x_a)}$
* Ray equation during ray casting for pixel location
  * $x_i = -\tan(\theta) + (i + 0.5) \cdot \frac{2 \cdot \tan(\theta)}{X_{res}}$
  * $x_{i+1} = x_i + \frac{2 \cdot \tan(\theta)}{X_{res}}$

