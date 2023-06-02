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
* **Voxel:** a small cube at i, j, k, with sides $\Delta x, \Delta y, \Delta z$
* Each grid point has a scalar value f(x, y, z)
* For example, density, intensity, CT scan, MRI
* Voxelize more complex implicit surfaces
* If $\Delta x = \Delta y = \Delta z \implies$ structured volume dataset
* Transfer function: to map lattice scalar values to RGBA
* Based on viewer location, there's a natural ordering of voxels




