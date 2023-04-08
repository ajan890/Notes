# Week 1
## Computer Graphics
* The Art and Science of creating imagery by computer
### Applications of Computer Graphics
* **Entertainment**
    * Films
    * Computer games
    * Virtual reality
* **Visualization**
    * Scientific visualization
    * Medical visualization
    * Flight simulation
    * Architecture
* **Education, etc.**
### History
* 2000 B.C.E.
    * Orthographic projection
* 1400’s (C.E.)
    * Perspective: Italian Renaissance
* 1600’s
    * Coordinate systems: Descartes
    * Optics: Huygens
    * Optics, calculus, physics: Newton
* 1897
    * Oscilloscope: Braun
* 1950-1970:
    * Computers with vector displays
* 1966:
    * First true raster display
* 1993:
    * 1200x1200, 500k triangles/sec, 36-bit color, stereo texture mapping... all at 60Hz (fps)
* Today:
    * Still rapidly evolving
#### Genesis of Computer Graphics and Interactive Techniques
* A PhD project at MIT in the early 1960s
* _Ivan E. Sutherland, 1963_
	> “Sketchpad, a man-machine graphical communication system”<br>
#### First Computer Game?
* Spacewar!, PDP-1, MIT, 1961,1972
* The **First** “Computer” Game - 1958
    * “Tennis for Two”
#### Movies
* Show how graphics evolve over time.
    * Toy Story 1 (1995) -> Toy Story 4 (2019)
    * Lion King: 1994 -> 2019
* Special effects
* Digital Compositing.
* Cartoons
* etc.
#### Modeling
* **Computer-Aided Design (CAD)**
    * Precision modeling
    * Engineering
    * **It’s not just about visualization, simulation is also useful**
#### Visualization
* Scientific
    * Weather reports, microscopic visualization, etc.
* Architectural
    * Buildings, blueprints, etc.
* Informational
    * Maps, Covid-19 tracker, etc.
* Graphical User Interfaces (GUI)
    * Windows, etc.
* Art and Digital Art
## Basic Elements of Computer Graphics
* Modeling
* Animation
* Rendering
* Interaction
### Modeling
* How do we model (mathematically represent) objects?
* How do we construct models of specific objects?
#### Primitives
* 3D points
* 3D lines and curves
* Surfaces (BNREPs): polygons, patches
* Volumetric representations
* Image-based representations
#### Attributes
* Color, texture maps
* Lighting properties
#### Geometric Transformations
* Representing objects geometrically on a computer
* Point clouds
* Polygon meshes
* Parametric curves
* Surface patches NURBS
* Texture maps
#### Alternative Representations
* Subdivision surfaces
* Voxels
* Blobs
#### Altering Geometric Models
* Affine transform
#### Volume Modeling
* CT Scans
* MRI
* Ultrasound
* PET Scans
* Atmosphere
### Animation
*  How do we represent the motions of objects?
*  How do we give animators control of this motion?
#### Keyframe Animation
* Flipbook animation
#### Motion Capture
* Men in Black
#### Procedural Animation
* Cloth Simulation
* Fluid Simulation
    * Incompressibility
    * Viscocity
* Smoke Simulation
    * Photon maps
    * Multiple scattering
* Other Physics Simulations
#### Modeling Transformations
* Assembly
* Viewing
    * Orthographic
    * Perspective
* Clipping
    * Remove what is not visible
### Rendering
*  How do we simulate the real-world behavior of light?
*  How do we simulate the formation of images?
#### Visibility - Simulating Light Propagation
* Reflection
* Absorption
* Scattering
* Emission
* Interference
#### Key Elements:
* Camera (angles and position)
* Illumination
    * Compute normals and color at vertices
    * Per vertex operations
* Shading
* Geometric and Reflectance Shape
* Subsurface Scattering
    * Translucency and varied levels of light penetration can be created using subsurface scattering effects
* Texture
    * Multilevel texture synthesis
    * Texture mapping
* Non-Photorealistic Rendering
* Rasterization
    * Converting vectors to individual pixels
    * Causing **aliasing**, or if you zoom in far enough, you will notice that the line isn’t smooth.  You can see the pixels.
        * This is caused by the pixels being a fixed shape and size.
* Shadoes
* Participating media
* Motion blur
* Etc.
### Interaction
*  How do we enable humans and computers to interact?
*  How do we design human-computer interfaces?
## What is Academic about all this?
* The full collection of techniques and “hacks” known to the industry?  **No.**
* The history of the techniques?  **No.**
* The skill of getting code working?  **Yes.**
* Well-understood math concepts that separate graphics from other programming?  **Yes.**
* Tying into graphics research sometimes.
## A Basic Graphics System
![image](https://user-images.githubusercontent.com/66571533/230695216-d05e1751-f719-4172-a6d6-8bd7b53d772f.png)<br>
* CPU vs. GPU
* Computing and rendering system
* Input and Output
### Input Devices
* Keyboard
* Mouse
* Game controller
* Tablet and Pen
* Other sensors
    * Data glove
    * Sound
    * Gestures
    * Etc.
### Output Devices
#### CRT (Cathode Ray Tube)
* Electrons strike Phosphor coating and emits light
* Direction of beam controlled by deflection plates
* Random-scan, calligraphic or vector CRT
* Moving beam to new location
* Refresh rate: 60 Hz - 85 Hz
* The single cathode ray only burns one pixel at a time.  Thus, it must move across all the pixels on the screen to create a frame.
#### Raster CRTs (n x m phosphor)
* Instead of having one electron gun like the CRT, Raster CRTs have three electron guns, one per color
* Framebuffer Depth
    * 1 bit: 2 levels only, b/w
    * 8 bits: gray scale, 256 gray levels or colors
    * 8 bits per color (RGB) = 24 bits = 16M colors
    * 12 bits per color: HD
* 3 different colored Phosphors: triads
* Shadow mask
* Interlaced vs. Non-Interlaced displays
    * Interlaced: On every frame, the pixel guns only mark even rows, and on the next frame switch to the odd rows.  Since frames are so fast, you can’t see the difference.  However, this halves the bandwidth needed to display frames since each frame only half of the display is updated.
    * Non-interlaced: On every frame, the entire frame is updated.
* Interlaced: used in commercial TV
* Single vs. double buffering
#### Screen Resolutions of Raster CRTs (n x m phosphor)
* TV: 640 x 480 px
* HD: 1920 x 1080 px
* 4K LCD: 3840 x 2160 px
* 35mm: 3000 x 2000 px
#### Memory Speed and Space Requirements
* Screen resolution = n x m
* Refresh rate = r Hz (frames/second)
* Interlaced vs. non-interlaced
* Color depth = b bits/pixel
* **Memory space per second = (n * m * b * r) / 8 bytes**
* **If non-interlaced, memory read time = 1 / (n * m * r) secs/pixel**
* **If interlaced, memory read time = 2 / (n * m * r) secs/pixel**
#### Flat Screen Displays
* **Raster Based:** active matrix with transistors at grid points
* **LEDs:** light emitting diodes
* **LCDs:** polarization of liquid crystals
* **Plasma:** energize gases to glow plasma
#### Other Output Devices
* Printers and Plotters: raster based, no refresh
* Stereo Displays: 3D TVs/movies, fast switching of left and right eye polarized images
#### Virtual Reality (VR)
* Flat panel technology
* Stereoscopic
* Track body, finger, and head locations
* **Foveated Rendering:** hi-res where viewer is focusing, lo-res everywhere else
* Other input devices: force sensing gloves, sound, etc.
#### Exotic Display Devices
* Immersive displays
* Head-Mounted displays
* Autostereoscopic
* Holographic
* Volumetric
* Etc.
### Aliasing in Raster Displays
#### Aliasing
* Lines
* Polygons
#### Reasons for Aliasing
* Location of pixels are fixed
* Size of pixels are fixed.
