## Assembly

# Before Assembly

## Documentation

Review the documentation, download and print the necessary parts. Ensure that all required parts and tools are available.

## Getting Started with Assembly

It is recommended to first assemble the entire system **on the table**, without mounting it into the enclosure, and perform testing:

* Connect **all** components.
* Verify the functionality of the heater, fan, and temperature sensors.
* Connect the system to **Klipper** or flash standalone firmware and ensure proper operation of the macros.

Video guide: [YouTube](https://youtu.be/1QMtVY0Vx-8?si=Ol1u4Ux9wALDcfe2)

### Installing the Board

![iHeater Assembly](imgweb/iHeater_5484.jpg)

### Installing the Thermistor and thermal fuse

!!! warning "Installing the thermistor"
    Make sure that the thermistor wires do not come into contact with the metal body of the heater. If you're unsure, insulate the thermistor - for example, by wrapping it with Kapton tape or placing it in any heat-resistant insulating material, such as a Teflon sleeve or heat-shrink tubing.
    
    Keep in mind that the heater temperature can reach up to 140°C.

!!! warning "Thermal Fuse Installation"
    You can install either a resettable thermal switch (such as the KSD9700) or a thermal fuse.

    Keep in mind that a thermal fuse is a one-time protection device: when the rated temperature is exceeded, it permanently breaks the circuit and must be replaced with an identical fuse.

    In contrast, the KSD9700 is a bimetallic thermal switch. It cuts off power when a set temperature is reached and automatically reconnects the circuit once the temperature drops below the threshold. This allows the system to recover without needing to replace the component.

    From a safety perspective, a thermal fuse offers more reliable protection, as it completely shuts down the system in case of overheating and prevents it from turning back on automatically.

    Since this is a DIY project, and working with heating elements requires a clear understanding of electrical safety, it’s recommended to first test your setup using a KSD9700, and once everything is working correctly, replace it with an appropriate thermal fuse(one suitable option is the RH130 model) for maximum safety.

![iHeater Assembly](imgweb/iHeater_5489.jpg)

### Installing the Heater

![iHeater Assembly](imgweb/iHeater_5491.jpg)

### Wiring

![iHeater Assembly](imgweb/iHeater_5494.jpg)

### Installing


![iHeater Assembly](imgweb/iHeater_5496.jpg)

### Wiring Connections

![iHeater Assembly](imgweb/iHeater_5498.jpg)

### Final Assembly

![iHeater Assembly](imgweb/iHeater_5500.jpg)

### Finished Product

![iHeater Assembly](imgweb/iHeater_5506.jpg)
