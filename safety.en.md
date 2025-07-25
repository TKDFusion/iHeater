## Safety
The iHeater controller can operate both as part of the Klipper firmware and autonomously under its own built-in firmware (standalone). In both modes, advanced protection algorithms are implemented, with the standalone mode utilizing the same protections as in Klipper:

- Temperature control using thermistors;
- Checking for the presence of sensor connections;
- Protection against temperature exceeding safe limits;
- Use of timers in case the system hangs;
- Automatic shutdown in case of sensor or controller errors.

Additionally, hardware protection is implemented:

A KSD9700 thermal switch (135°C) is installed to provide physical disconnection of the heater power in case of overheating. Once the temperature drops below the threshold, the device automatically restores the connection, re-enabling power to the heater.

This type of protection is especially important in the event of software errors or hardware malfunctions, as it operates independently of the controller logic.

!!! note warning "Using a Thermal Fuse"
    In situations where the iHeater is used without continuous operator supervision, it is recommended to replace the KSD9700 thermal switch with a thermal fuse, providing hardware protection against overheating.


    One suitable option is the RH130 model, which has similar dimensions and can be installed in the standard iHeater housing position or mounted directly on the heatsink.

    Upon reaching the critical temperature, the fuse irreversibly opens the circuit, completely de-energizing the system and preventing overheating. Note that such devices are single-use and require replacement after activation.



The controller is equipped with a 2A fuse, which protects the device, and in case of an emergency, it blows, completely cutting off the system's power.

A PTC heating element with full electrical insulation is used. Unlike most heating solutions, the PTC heater's casing is not energized, eliminating the risk of electric shock during installation or maintenance of the 3D printer chamber.

This multi-layered protection system makes the iHeater a safe solution for active heating of 3D printer chambers, including during long continuous operation.