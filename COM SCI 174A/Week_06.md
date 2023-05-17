## Lighting


### Global Illumination

![image](https://github.com/ajan890/Notes/assets/66571533/c9aef5a1-ddf2-417f-9bae-b05f3ff6750c)

*  A scene may contain one or multiple light sources.  Each light source has a brightness, or **radiocity** which essentially describes how much light bounces off an object when a light ray hits it.
* Types of Lighting
    * Ambient
        * Background light
        * You can still see in a very dark room
        * Typically a very dim light that is just there in the background.
        * Often creates silhouettes
    * Diffuse
        * Light bouncing off an object
        * Illuminates color
    * Specular
        * Bright spots are created on an object
        * Usually for shiny objects


### Lighting/Illumination



* _Geometric Properties_
    * **Object:** position, orientation (normal)
    * **Light:** position, direction, point vs. spot vs. area
    * **Eye:** position, orientation
* _Material Properties_
    * **Object: **color, reflectivity, shininess, bumpiness, translucency
    * **Light:** color
    * **Eye:** filler, color blindness


### Ambient Lighting



* **Properties**
    * Background light
    * Unrealistic
    * Works as a good approximation of scattered light
    * Does NOT depend on position/orientation of light, object, or eye
    * Only depends on obkect and light’s material property
    * k<sub>a</sub> = ambient reflection coefficient, values [0, 1], may be different for R, G, B
    * I<sub>a</sub> = intensity of ambient light source, values [0, 1], different for R, G, B
    * **Ambient light reflected off object = k<sub>a</sub> * I<sub>a</sub>**


### Diffuse Lighting



* **Properties**
    * Point light source
    * Lambertian (or diffuse) reflection for dull, matte surfaces
    * Surfaces look equally bright from all directions
    * Reflect light **equally** in all directions
    * **Lambert’s Law:** _amount of light refleted from a differential unit area dA toward a viewer is proportional to the cosine of the angle between the incident light and the normal (θ)_
        * Think about the sun: At sunrise, the sun is perpendicular to the normal, so you get nearly no light where you are standing.  The amount of light increases towards noon, when the angle is 0°.  It begins decreasing past noon until sunset, when there is again little to no light.
    * k<sub>d</sub> = diffuse reflection coefficient, values [0, 1]
    * l<sub>p</sub> = intensity of point light source, values [0, 1]
    * **Diffuse light reflected off object = k<sub>d</sub> * l<sub>p</sub> * cos(θ) = k<sub>d</sub> * l<sub>p</sub> * (N * L)**

![image](https://github.com/ajan890/Notes/assets/66571533/39ecdf8c-171c-47b1-8f9e-e3755b3b1a8c)

#### Incident Angle θ



* θ < 90° → some light based on angle θ
* θ = 0° → max light
* θ > 90° → self occlusion


#### Directional light source



* The light source only has a direction, but no definite location
* A light at sufficient distance from object (e.g., sun)
    * Assumed to be infinitely far away, so all light rays pointing from the scene to the sun are parallel
* L remains the same for entire scene
* N remains the same for entire polygon
* Therefore, N, L = constant on polygon; L = constant everywhere


#### Attenuated light source



![image](https://github.com/ajan890/Notes/assets/66571533/fa7f9aec-2352-4740-a2de-ebe90dd8f960)
![image](https://github.com/ajan890/Notes/assets/66571533/323a5f88-4531-4038-a116-5b2b626e4c26)
* We tend to not use the first (simple) fraction because:
  * If d = 0, then we have problems
  * If the light is very close such that d &lt; 1, then it amplifies the light
  * Thus, we use the second fraction, plus the min() function to ensure light is not amplified.


#### Colored Light and Objects

![image](https://github.com/ajan890/Notes/assets/66571533/0b2d0f27-419b-40ac-9a85-357c33ee82b4)

#### Atmospheric Attenuation or Blending



* Depth cueing or fog (fog color = ![image](https://github.com/ajan890/Notes/assets/66571533/8fcc8b2f-9ea1-4637-8391-e36fd6bf8778))


![image](https://github.com/ajan890/Notes/assets/66571533/80585665-e71a-4dc2-b6ef-0953f20cd037)

* z represents the distance between the camera and the object
    * z<sub>b</sub> represents the close bound and z<sub>f</sub> represents the far bound
    * We do this because we want fog to be at a constant high after a certain distance from an object, and at a constant low when close to the object.
* s<sub>0</sub> represents the amount of fog at a given point.  
    * s<sub>b</sub> represents the minimum fog, or the amount of fog at z<sub>b</sub>
    * s<sub>f</sub> represents the maximum fog, or the amount of fog at z<sub>f</sub>


### Specular Lighting



* **Properties**
    * Shiny surfaces
    * Color of light, not object
    * Does depend on position of light, object, and eye
    * Light reflects **unequally** in different directions (e.g., perfect reflector: mirror)
    * For non-perfect reflectors
        * k<sub>s</sub> = specular reflection coefficient, values [0, 1], may be different for R, G, B
        * n = material’s specular reflection exponent, values [1..100s], perfect reflector n = infinity

        * **Specular light reflected off object** = ![image](https://github.com/ajan890/Notes/assets/66571533/451a816c-e2e7-4a84-85d1-03360f48a11b)

        * ![image](https://github.com/ajan890/Notes/assets/66571533/ebcd4616-b40a-467c-ac4b-5ef2e91cc935)

* **_Specular Term: Smoothness Exponent Effect_**
    * Exponentiating a term that has values &lt; 1 draws it closer to 0
    * Higher exponent ⇒ smaller region where point light’s reflection is considered aligned with the viewer ⇒ smaller shiny spot
    * -ve values of ![image](https://github.com/ajan890/Notes/assets/66571533/63e7f24f-b98e-465b-b193-9c8c63cbf829) is clamped to ![image](https://github.com/ajan890/Notes/assets/66571533/17ff9854-b147-45e6-b090-4a3d407801d8)
    * Max specular reflection when ![image](https://github.com/ajan890/Notes/assets/66571533/bf6c7f5b-81f7-4810-8f3a-a8ab682cbefb)

![image](https://github.com/ajan890/Notes/assets/66571533/c71379ca-1d74-4dfa-8867-abd0dc8bc7a6)

#### Reflection Equation
![image](https://github.com/ajan890/Notes/assets/66571533/1e24c0f3-f09e-409b-91b1-34be1112559c)

* We are given the direction of the light and the normal vector of the surface.  We want to find the vector that represents the direction the light is reflected off the surface.
* To do this, we use a projection of the incoming light ray vector, L, onto the normal vector.  The resulting vector is n’.  From here, L + N yields vector u, which represents the distance from the tip of the light vector to the n’ vector.  Adding n’ and u yields R, the reflection vector.
* Thus, the reflection vector is ![image](https://github.com/ajan890/Notes/assets/66571533/62824e47-c93e-4727-8b40-8c189eff0c43)




#### Halfway Vector: Alternate Formulation of ![image](https://github.com/ajan890/Notes/assets/66571533/e716256d-4e8f-4ecf-a6bd-1beb8cc7fe1d)

* We don’t want to calculate r and v because it is computationally expensive.  Thus, we use the angle between n and h instead, which is considerably cheaper.  It does not yield exactly the same result as calculating the reflection, but it allows the program to run much faster.
* In a video game, the player is most likely not going to notice the difference.
    * Halfway vector (H) between L and V = normalize(L + V)
    * Replace ![image](https://github.com/ajan890/Notes/assets/66571533/6bf6eb09-336d-4b48-848a-1c53fef49785) with ![image](https://github.com/ajan890/Notes/assets/66571533/e3e2edac-e479-44b6-b02a-23292b75c47f)
    * This alternate is referred to as Blinn-Phong illumination
![image](https://github.com/ajan890/Notes/assets/66571533/f7c02c51-9d75-44e0-814b-4b57707283ca)

### Final Light Equation

![image](https://github.com/ajan890/Notes/assets/66571533/2f5aa2d3-19e3-426f-9647-594622fa54ee)
**I = emissive + ambient + diffuse + specular**

![image](https://github.com/ajan890/Notes/assets/66571533/72f879c8-ff57-4c8e-a91d-4da05b7d0fce)

## Lighting: Miscellaneous Improvements



* Multiple Light Sources
    * Sum the light terms over all light sources
* Clamping
    * ![image](https://github.com/ajan890/Notes/assets/66571533/26b1ad0d-f002-4b9a-be9c-2d73b0ee6b9c)
    * ![image](https://github.com/ajan890/Notes/assets/66571533/86cf1fcf-b876-4bf6-9f10-7452778587cd) wrt to max value of color in entire image
* Fast Alternative to Phong Illumination
    * ![image](https://github.com/ajan890/Notes/assets/66571533/3f7220c4-4619-4237-82d1-1f830f46ba78)
    * ![image](https://github.com/ajan890/Notes/assets/66571533/921baa6a-9484-4a87-b5bc-2c9bb4602e4f)
* Spot Lights
    * Smooth spot silhouette

### Types of Lights: Summary
![image](https://github.com/ajan890/Notes/assets/66571533/de0deca8-995c-4773-a3b6-d5c8b9518a6f)
