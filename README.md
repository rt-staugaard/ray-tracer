****3D RELATIVISTC RAY-TRACER:**** 

The idea behind this project was to capture the phenomena of gravitational lensing using a ray-tracer. 

https://github.com/user-attachments/assets/302f0e94-0b05-40e0-8f15-b43c9e987750 

This essentially functions by shooting out rays from the camera position in all directions of its FOV and tracking whether these light rays eventually hit the source. 
Updating the movement of the light is done through the Geodesic Equation. For a Schwarzchild like object, this equation takes on its simplest form in Spherical coordinates. 
The main procedure is thus this:

Calculate all the initial velocities in spherical coordinates. Update the position of each ray until it is far away from the centre of the black hole. Then look if it is heading
towards / has hit the target source, which is taken a sphere. If it hits the source, the pixel will have a brightness, otherwise it will be given a generic background colour. 

I have included a few early stopping condition to make it run more smoothly, so for instance, any ray heading straight into the black hole can be disregarded. All of this logic is found
within the shaders/light.frag

The relevant modules are the Camera module and the Graphics module (the physics module was used in an early version).

****Camera module:****
This module contains the logic of how the camera moves and how it should change the world through different transformations based on this movement.

****Graphics module:****
This module contains how the program sets up a window through GLFW and how it paints this window using OpenGL.
