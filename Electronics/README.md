# Electronics

This page provides links and files of various electronics board used on our microscopes.



### Laser diode electronics

We built a custom electronics system to control multiple affordable laser diodes. For more details, visit the [laser engine repository](https://github.com/ries-lab/LaserEngine).



### MicroFPGA: a Hobby FPGA to control microscope elements

We use a hobby FPGA (Au, Alchitry) to trigger our lasers, control our servos, flip-mirrors and LEDs, as well as reading-out analog signals. You can find the project in the [MicroFPGA](https://github.com/jdeschamps/MicroFPGA) on Github. It features:

- Code for [Micro-Manager](https://micro-manager.org/), Java, Python and LabView

- Flexible triggering of multiple lasers in parallel using a camera trigger signal. The lasers can be pulsed with us resolution and follow complex patterns.

- Multiple servos (e.g.: filter-wheel, 3D lens, beam-blocks). Check out the microscopy section of this repository for example applications.

- TTLs signals (e.g.: flip-mirror, bright-field LEDS)

- PWM signals (e.g.: coupled with a low-pass filter, this signal is used for AOM)

- 8x analog read-out signals (e.g.: focus-lock signals, power meter, temperature)  

  

### Custom electronics

In the present section, we provide Altium projects and Gerber files to reproduce electronics used on our microscope together with our FPGA (see MicroFPGA above). The following boards are currently described:

- [Analog divider](Analog_divider) converts a 5 or 10 V analog signal to 1 V, while providing an upper voltage limit for safety.
- [Low-pass and digital divider](LowPass_divider) is a multi-channel bi-directional digital voltage conversion (3.3, 4 and 5 V), that features additionally a low-pass filter on some of the channels in order to produce an analog signal from a PWM input.
- [Servomotor distribution board](Servo_distribution) is a simple distribution hub for servomotor signals.

Note that an updated version of the low-pass and digital divider (renamed signal conversion board) is available in the [MicroFPGA](https://github.com/jdeschamps/MicroFPGA) repository.



### Powermeter

We use a simple home-made [powermeter](Powermeter) to measure the laser power during experiments without loosing too much power or stopping acquisitions.