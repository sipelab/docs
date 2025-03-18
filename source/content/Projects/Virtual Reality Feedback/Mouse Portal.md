A python based maze-running game for neuroscience closed-loop feedback behavioral experiments. 

# Major Features:
1. Packaged executable that can be easily run as a subprocess 
2. Panda3D engine backend for optimized graphical processing and python development environment with no-boilerplate graphical API control
3. Loads experimental parameters from a JSON configuration file
4. Real-time data logging and saving
5. Configurable IO for implementing custom controllers (arduino-encoders, for example)
6. Customizable texture loading
7. Experimental block design implemented via configurable Finite-State-Machine logic built into Panda3D

## Virtual Environment design
- Single point geometry
The controller input in a wheel encoder or a treadmill providing some velocity. There should be forward and backward movement based on whether the input is positive or negative, for example. The Virtual maze should be presented to a first-person camera and the hallway should be rendered from a 1 point perspective with "walls" that are textured and provide a visual flow based on movement. Build the design in such a way that data can be collected from the movement through the virtual maze. Make sure all parameters are loaded from a configuration file