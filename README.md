# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Change into the local copy and download required software: 
   `cd CarND-PID-Control-Project`
   `./install-ubuntu.sh`
3. Make a build directory: `mkdir build && cd build`
4. Compile: `cmake .. && make`
5. Run it: `./pid`. 


![Build Screen](images/build.png)

For Step #5 before and for the next steps you must be in the GPU mode of the environment if you are in the UDACITY Workspace! 


![run default](./images/run_default.png)


Run the Simulator and choose the PID Simulator.
Using the right arrow, you need to go to the "PID Controller" project!
![Simulator PID Controller](images/Simulator PID Controller.png) 

As the default parameters are use, the result will be bad and not acceptable for a real car, as can bee seen in this Video:
[![Failed Run](http://img.youtube.com/vi/DxWku4wbNKk/0.jpg)](http://www.youtube.com/watch?v=DxWku4wbNKk "Failed Run")

Stop the Simulator by hitting ESC (this will stop the current run and will bring the Simulator to the initial Screen)

Run again with optimized parameter: `./pid -0.1 0 -0.8` :

![run tuned](./images/run_tuned.png)

Again you need the right arro to go to the "PID Controller" project!

[![Successful Run](http://img.youtube.com/vi/5-FI0BBsW5g/0.jpg)](http://www.youtube.com/watch?v=5-FI0BBsW5g "Sucesful Run")

Using the right arrow, you need to go to the Project 4: PID Controller project:

![Simulator PID controller project](./images/Simulator_PID_Controller.png)

Click the "Select" button, and the car starts driving. You will see the debugging information on the PID controller terminal. 

# [Rubric Points](https://review.udacity.com/#!/rubrics/824/view) 

## Compilation

### Your code should compile.

The code compiles without errors or warnings. No modifications were done on the provided setup.

## Implementation

### The PID procedure follows what was taught in the lessons.

The PID implementation is done on the [./src/PID.cpp](./src/PID.cpp). 
The [PID::UpdateError](./src/PID.cpp#L24) method calculates proportional, integral and derivative errors and the [PID::TotalError](./src/PID.cpp#L33) calculates the total error using the appropriate coefficients.

## Reflection

### Describe the effect each of the P, I, D components had in your implementation.

- The proportional portion of the controller tries to steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly.  

- The integral portion tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present.

- The differential portion helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it.  

### Describe how the final hyperparameters were chosen.

The parameters were chosen manually by try and error. First, make sure the car can drive straight with zero as parameters. Then add the proportional and the car start going on following the road but it starts overshooting go out of it. Then add the differential to try to overcome the overshooting. The integral part only moved the car out of the road; so, it stayed as zero. After the car drove the track without going out of it, the parameters increased to minimize the average cross-track error on a single track lap. The final parameters where [P: -0.1, I: 0.0, D: -0.8].

## Simulation

### The vehicle must successfully drive a lap around the track.

Running the track with good parameters is shown [here](https://youtu.be/5-FI0BBsW5g).
