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
