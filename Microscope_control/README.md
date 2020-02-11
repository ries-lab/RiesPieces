# Microscope control

We control our localization microscope with [Micro-manager](https://micro-manager.org/) (MM). In order to interact with our devices, we developed device adapters now distributed with the MM software. Other device adapters can be found [here](https://github.com/jdeschamps/MM-ownAdapters).



### Easier Micro-manager User interfaces (EMU)

In order to provide better user experience, tailored user interfaces (UI) are often an important, albeit regularly overlooked, feature of a microscope. In Micro-Manager, UIs can be implemented as plugins and should modify the state of device properties whenever the user interacts with the UI controls (buttons, sliders...etc..). Because similar devices might have different types of properties (e.g. power percentage vs absolute power) and states (e.g. "On" vs "1"), great efforts should be spent to accommodate various devices. Otherwise, the interface will not be easily transferable and shared with other groups.

[EMU](https://github.com/jdeschamps/EMU) provides a mechanism to build flexible and reconfigurable user interfaces. In the user point of view, EMU delivers a choice of UIs that are rapidly ready to use thanks to an intuitive configuration menu. In particular, the configuration menu allows mapping the device properties to the various functions of the interface in few clicks. EMU also simplifies the task for programmers, as implementing a new UI can be as simple as using a drag and drop software (such as Eclipse WindowBuilder) to create the interface and writing few lines of code for compatibility. EMU then takes care of the configuration and all interactions with the devices.

In summary, with EMU:

- Users have access to a bank of UIs
- The interfaces are rapidly configured and ready to use
- The UIs are easily be transferred between similar set-ups
- New UIs can be designed with drag and drop softwares and few extra lines of code

EMU is part of Micro-Manager 2-gamma.



##### Useful links:

- [EMU source code on Github](https://github.com/jdeschamps/EMU)
- [EMU quick manual in Micro-Manager](https://micro-manager.org/wiki/EMU)
- [EMU user and programming guide](https://jdeschamps.github.io/EMU-guide/)
- [EMU tutorial](https://github.com/jdeschamps/EMU-guide/tree/master/tutorial): how to implement an interface for EMU.



### htSMLM

[htSMLM](https://github.com/jdeschamps/htSMLM) is the Ries group user interface for their automated single-molecule localization microscopes. htSMLM is an EMU plugin, it provides an intuitive interface to control an SMLM microscope, as well as tools to automatically adjust UV laser power and an advanced experiment designer allowing unsupervised experiments (z-stack, localization microscopy, multi-slice localization, bright-field, single-shot...).

Refer to the [Github repository](https://github.com/jdeschamps/htSMLM) on how to install and use it.