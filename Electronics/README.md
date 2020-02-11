# Electronics



### Laser diode electronics

For more details, visit the [laser engine repository](https://github.com/ries-lab/LaserEngine).



### Hobby FPGA to control microscope elements

We use a hobby FPGA (MojoV3 & Au, Alchitry) to trigger our lasers, control our servos, flip-mirrors and LEDs, as well as reading-out analog signals. The older version (MojoV3) has been [archived](https://github.com/jdeschamps/MicroMojo) due to the discontinuation of the FPGA. You can find the newest version (Au) of the project in the [MicroFPGA project](https://github.com/jdeschamps/MicroFPGA) on Github.

MicroFPGA features:

- Compatible with Micro-Manager
- Micro-second triggering of multiple lasers in parallel using the camera trigger signal.
- Multiple servos (e.g.: filter-wheel, 3D lens, beam-blocks). Check out the microscopy section of this repository for example applications.
- TTLs signals (e.g.: flip-mirror, bright-field LEDS)
- PWM signals (e.g.: coupled with a low-pass filter, this signal is used for AOM)
- 8x analog read-out signals (e.g.: focus-lock signals, power meter, temperature)  

