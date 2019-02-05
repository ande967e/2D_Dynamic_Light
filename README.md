# 2D_Dynamic_Light

The idea with this 2D dynamic lighting is it should be easy to implement in ones projekt.

There is two components in the project, VisibilityPolygon and DynamicLightController:

VisibilityPolygon
This component is placed upon the gameobject which should act as a lightsource. This component finds points which togehter makes up a visibility polygon. These points are saved in a list. Furthermore this component has data on the light's color, intensity, range and if it should be a point light or spotlight.

DynamicLightController
This component is the one which actually draws the light in the scene, which is done by the use of several fragment shaders.
The overall process for generating the light is as follows:
1) The visibility polygon of a light can be split into several triangles. For each of these triangle a texture is drawn, a blank texture with a white triangle. All these white triangles are combined intoo one texture, which gives a texture that is white on the area of the visibility polygon. This texture for each of the light sources I call a complete LightTexture.
2) If any circle colliders has been a part of the visibility poolygon, then it is ensured that the complete LightTexture follows the circlecolliders form.
3) The alpha value is increased the further away a pixel in a complete LightTexture is from the given light source, as to replicate the faling intensity of light away from its lightsource. In this process the color of the light is also implemented.
4) The different complete LightTextures are combined into one texture.
5) The combined complete LightTextures are put over the scene. It's also in this process the shadow is implementet, how dark it is where the light doesn't shine.


--The shaders--
1) LightTextures: Generates a texture which is white inbetween three coordinates, generating a white triangle and otherwise blank texure.
2) Combiner: Puts two textures together.
3) CircleLightRemover: Takes a coordinate and a radius, and then blanks out the pixels in a circle around this point with the given radius. 
4) FallOff: Increases the alpha value the further away a pixel is from a given point, and colors all pixels in a given color.
5) CombineLightSources: Combines twoo complete LightTextures together, and ensures that the light color and intensity mixes correct.
6) CombineWithSource: This puts the final light texture atop the source texture, and applies darkness to the unlit area with a given shadow intensity.


