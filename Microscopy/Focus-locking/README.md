# Focus-locking

For a fully documented and open-source system, please check out [pgFocus](http://big.umassmed.edu/wiki/index.php/PgFocus) from Karl Bellvé (UMass).

Our system is similar to pgFocus, but based on different hardware and not fully documented. We only outline here the principles and how to roughly put the components together.

### Main parts

- P-726 z-stage (PI) with its E-709 controller (PI). The controller accepts a 0-10 V analog input.
- WSLP-785-050-4-PD 785 nm laser (Laser components). This laser has been discontinued but a 70 mW version seems to be available. We observed mode jumps and we therefore switched to the alternative.
  or
  iBeamSmart 785 nm 150 mW laser (Toptica).

- QP50-6 TO quadrant photo-diode (First Sensor).
- LC-301DQD-PV amplifier 0-10 V (Laser Components).
- SLC2445-me linear stage (SmarAct) or similar.



### Principle

A near infra-red (IR) laser is reflected at the coverslip. The reflected beam is monitored by a QPD sensor. The QPD electronics produces three 0-10 V signals. The X signal is at 5 V and the Sum signal maximized when the laser is in the center of the QPD (see electronics). The X signal is used as an external analog control for the z stage. When the z stage is set to external sensor (i.e. when it listens to the external analog signal), the stage will compensate any movement to maintain the X signal at 5 V. 

Note that we use this system for high-NA objectives (TIRF objectives) as well as with water objectives, silicon objectives and with index-matched samples. The strength of the signal might vary, but the focus-locking has proven to be working well with all these conditions.

### Optics alignment

- 750 short-pass dichroic mirror (AHF)

From Thorlabs:

- Posts and post holders
- 19 mm 1/2" cemented achromatic doublet
- 1/2" fiber adapter (make sure it matches the optical: FC/PC vs FC/APC)
- 1/2" lens tube
- adjustable 1/2" lens and its locking ring
- 1" round silver mirror and its mirror mount (x1 or x2)
- 1/2" half-mirror and its mirror mount

Our microscopes all feature an entrance port with a 750 short-pass dichroic mirror (AHF). The fluorescence collected by the objective is transmitted through the dichroic, while the 785 nm focus-lock laser is reflected upon its surface. It is then transmitted through the main dichroic before entering the objective.

The IR laser is coupled in a single-mode fiber. The output of the single-mode fiber is then mounted in an 1/2" optical fiber adapter within a 1/2" lens tube.  On the lens tube, we screw an adjustable 1/2" lens tube holding a 19 mm achromatic lens (Thorlabs). The adjustable 1/2" lens tube can be fixed by using a locking ring (sold with the lens tube).

The QPD sensor (QP50-6 TO) is mounted on a custom aluminum holder and screwed on top of the linear stage. 

Here are the rough alignment steps, they might involve some playing around.

:warning: Please wear appropriate laser protection. :warning: 

1. Collimate the laser beam by moving inward/outward the 19 mm lens with the adjustable lens tube. This step can be done approximatively.
2. Place a mirror (or two mirrors to have an easier alignment procedure) in front of the laser so that it is reflected on the 750 SP dichroic mirror and to the objective. We find placing a piece of paper on top of the objective useful to determine when the sweet spot where the laser exits the microscope.
3. Move the 19 mm lens away from the laser until the shape of the beam exiting the objective transitions from a large blurry profile to a well-defined central sport with a ring (i.e. collimated after the objective lens). This corresponds to the laser being focused in the back-focal plane (BFP) of the objective. We usually use the mirror knobs to have the laser exit vertically from the objective.
4. Place a coverslip on the microscope. We find it useful to have fluorescence beads to find the focus. Use the mirror knobs (sometimes we need to translate directly the mirror, this is not necessary if you are using two mirrors) to move the focus of the laser in the back-focal plane. The goal is to translate laterally the focus of the laser in the BFP (which corresponds to the laser exiting at a higher and higher angle from the microscope) until it is no longer transmitted but reflected at the coverslip. Stop when you observe the laser reflection coming back parallel to the laser beam.
5. Place a 1/2" half mirror and its holder (Thorlabs) on the path of the reflected beam, while making sure the entrance beam is not obstructed. Reflect the exit beam onto the QPD.
6. Once everything is aligned, verify that the QPD electronics signals have the proper response to a change in focus (see electronics). If not, adjust the mirror sending the beam into the microscope to make sure the beam sweeps laterally the QPD when taking a z stack with the objective.

We often use a 750 short pass in the detection beam path as well to prevent near-IR signals going to the camera.

### Electronics

The LC-301DQD QPD amplifier has three output signals: X, Y and Sum (refer to the datasheet for more details). The output signals are between 0 and 10 V. Note that in order to produce the signals in the right laser power range, you probably need to exchange resistors on the electronics (see the LC-301DQD-PV datasheet).

When the system is well aligned, focusing through z with the objective stage should yield the following graph (here as a cartoon):

![QPD](X:\users\Joran\Illustrator\QPD.png)

The QPD amplifier should be connected to the QPD. The X signal should be connected to the external analog input of the z-stage controller. Finally, you should also monitor the X and Sum signals.



### Computer control

The PI stage is controlled using a modified PI device adapter in [Micro-Manager](https://micro-manager.org/). The device adapter is available [on Github](https://github.com/jdeschamps/MM-ownAdapters/tree/ownAdapters/DeviceAdapters/PI_FocusLock), refer to Micro-Manager "How to build device adapter" to compile it or contact us directly. 

:warning: The device adapter set some internal controller parameter values. These values might be only safe for our z stage. Please contact PI or your device manufacturer to the exact procedure to switch from internal to external sensor (and inversely). ​Us​e​ th​i​s ​d​e​vi​ce ​a​dap​te​r ​a​t ​y​o​ur​ ​ow​n ​ri​sk​.​ :warning:

Note that the PI internal parameters must also be set to translate the 0-10 V input range to -1/+1 um (see manual).



### How to use the focus-lock system

1. Find the focus on your sample.
2. Turn on the focus-lock laser.
3. Move the QPD using its stage until the X signal is about 5 V and the Sum signal maximum.
4. Lock the system by setting the z-stage to external sensor (in Micro-manager: set external sensor to 1 in the device property browser).
5. Re-focus using the QPD stage.