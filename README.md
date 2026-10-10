<div align="center">

<img src="docs/img/iDryer_logo_small.png" width="220" alt="iDryer">

# iHeater

**An active heated chamber for any printer. Print engineering materials without failed parts.**

[![Documentation](https://img.shields.io/badge/docs-idryer.org-e7352c)](https://docs.idryer.org/en/projects/iheater/klipper/) [![Telegram](https://img.shields.io/badge/Telegram-iDryer-2ca5e0)](https://t.me/iDryer) [![Discord](https://img.shields.io/badge/Discord-join-5865f2)](https://discord.gg/jGce5eeHHz) [![License](https://img.shields.io/badge/license-GPL--3.0--or--later-blue)](LICENSE)

<img src="docs/img/iHeater_promo.png" width="480" alt="iHeater">

</div>

---

## What it is

A compact 200 W heater that turns an enclosed printer into an active heated chamber.

It runs from mains through its own inlet and connects over USB. You need no free connectors on the printer board, and the 200 W load never touches its power supply. Stock supplies often run close to their limit already.

## The problem it solves

ABS, PA, PC and other engineering filaments need a warm chamber. Without one, parts warp, layers split, and shrinkage is anyone's guess. Printers that ship with a heated chamber cost more, even though mechanically they are often identical to the ones that don't.

The catch is that you usually have no way to get heat into the chamber. On current machines from Creality, Bambu Lab and FlashForge the electronics are closed, and there are simply no spare connectors for a heater, a fan and a thermistor.

iHeater sidesteps all of it. It connects to nothing inside the printer and depends on nothing the printer board can or cannot do.

## Who it is for

- You print engineering filaments and want a result you can count on.
- You need strong parts: even shrinkage and real layer adhesion.
- You want a heated chamber on the printer already sitting on your bench, instead of buying a new one.
- You run a farm or print for customers, and a fleet of machines costs less at the same capability.

## What it looks like

<div align="center">

<img src="docs/img/iHeater_200_PCB.png" width="520" alt="iHeater 200 W board">

</div>

Everything is built from standard components. An enthusiast can put together an equivalent from an STM32 development board plus a couple of solid-state relays or off-the-shelf triac power modules. The finished board is more convenient and more compact, but the choice is yours.

## Three ways to control it

There is one board. How you drive it is up to you.

### Klipper

<div align="center">

<img src="docs/img/chamber_heating.jpg" width="440" alt="iHeater in the Klipper interface">

</div>

The board acts as a separate MCU and controls chamber heating and the fan on its own. Chamber temperature appears in the interface next to the bed and the nozzle, with macros and the full Klipper logic available.

→ [Klipper configuration](https://docs.idryer.org/en/projects/iheater/klipper/klipper/configuration/)

### Standalone firmware

The board is self-contained: it has everything needed to run without a host. You set the target temperature with successive presses of the MODE button, and three LEDs show the current setting. The printer is not involved at all.

→ [iHeater Standalone Firmware](https://github.com/pavluchenkor/iHeater-Standalone-Firmware)

### iHeater Link

A Wi-Fi module that takes the chamber setpoint from the printer itself, over MQTT on Bambu Lab, through Moonraker on Klipper, or from Home Assistant, and passes it to the heater. It also adds the portal, the mobile app and over-the-air updates.

This is the path for anyone whose printer firmware is sealed shut and who has no wish to dig into it.

→ [iHeater Link](https://github.com/pavluchenkor/iHeater-Link)

## What to expect from heating

The main heat source in the chamber is the printer bed. iHeater works together with it and evens out the heating, but on its own, with the bed off, it will usually not bring the chamber to working temperature.

Before you build, estimate what you will get in your specific enclosure: volume, losses through gaps, bed power. Use the [calculator](https://docs.google.com/spreadsheets/d/1u6XrWLFZGOUnRlFPjjGsJB_GLuFFIs3fFWLCp2-K8gc/edit?usp=sharing).

Preparing the enclosure matters as much as the heater itself: sealed gaps, closed vents, disabled exhaust fans. All of it is covered in the [usage](https://docs.idryer.org/en/projects/iheater/klipper/usage/) section.

## Place in the ecosystem

| Layer | What it does | Repository |
|---|---|---|
| Heater | Board, mechanics, diagrams: **this repository** | iHeater |
| Standalone firmware | Operation without a host, pulse protocol | [iHeater Standalone Firmware](https://github.com/pavluchenkor/iHeater-Standalone-Firmware) |
| Connectivity | Wi-Fi, portal, print-driven automation | [iHeater Link](https://github.com/pavluchenkor/iHeater-Link) |
| Cloud | Portal, app, integrations | [portal.idryer.org](https://portal.idryer.org/) |

## What you need

| Component | Qty | Note | Where to get it |
|---|---|---|---|
| iHeater 200 W board | 1 | | [store.idryer.org](https://store.idryer.org/) |
| Power cable | 1 | 110-230 V | — |
| USB cable | 1 | for the host connection when running under Klipper | — |
| Enclosure and mount | 1 | 3D printed | [models](https://docs.idryer.org/en/projects/iheater/klipper/cad/) |

The wiring diagram is in the [connection](https://docs.idryer.org/en/projects/iheater/klipper/connection/) section.

## Difficulty and cost

| | |
|---|---|
| Soldering | required for the wiring harness |
| 3D printing | enclosure and mount |
| **Hazardous voltage** | **yes, 110-230 V** |
| Skills | working with mains voltage, assembly from a diagram |
| Time | one evening |

## Safety

> **Heating elements and temperature control carry a risk of fire and equipment damage.** Follow safety precautions. Never leave the device running unattended.

Check separately that the printer's stock exhaust fans do not switch on by themselves while the chamber is heating, and that the electronics bay is isolated from hot air.

→ [Safety section](https://docs.idryer.org/en/projects/iheater/klipper/safety/)

## Quick start

1. **Estimate the result** for your enclosure with the [calculator](https://docs.google.com/spreadsheets/d/1u6XrWLFZGOUnRlFPjjGsJB_GLuFFIs3fFWLCp2-K8gc/edit?usp=sharing).
2. **Prepare the chamber**: seal the gaps, close the vents, isolate the electronics bay. See [usage](https://docs.idryer.org/en/projects/iheater/klipper/usage/).
3. **Assemble and connect** it following the [instructions](https://docs.idryer.org/en/projects/iheater/klipper/assembly/).
4. **Choose how to control it**: Klipper, standalone firmware or iHeater Link.
5. **Set up the slicer** with [profiles and parameters](https://docs.idryer.org/en/projects/iheater/klipper/slicer/).

## Status

The 200 W board is on sale, the 100 W version is archived. All three control methods work: Klipper, standalone firmware, iHeater Link.

## What is in this repository

| Path | What it is |
|---|---|
| `CAD/` | Enclosure and mount models |
| `printers/` | Ready configurations for specific printers |
| `*.cfg` | Klipper configuration |
| `User-mods/` | Community modifications |

## License

Code, CAD models, drawings and mechanics: [GNU GPL v3.0 or later](LICENSE), [NOTICE](NOTICE).

PCBs and schematics are not published.

The iDryer name is not covered by the license. See [TRADEMARKS.md](https://github.com/pavluchenkor/idryer-core/blob/main/TRADEMARKS.md).

## Help

- [Telegram](https://t.me/iDryer)
- [Discord](https://discord.gg/jGce5eeHHz)
- [Documentation](https://docs.idryer.org/en/projects/iheater/klipper/)

Guides and walkthroughs on the channel: [YouTube](https://www.youtube.com/@iDryerProject) · [Rutube](https://rutube.ru/channel/34401569/)

## Contributing

Got it running on your printer, put together a configuration, found an error in the instructions? Open an issue or send a pull request. Ready-made configurations live in `printers/`, community modifications in `User-mods/`.

## Next

[Run the numbers in the calculator](https://docs.google.com/spreadsheets/d/1u6XrWLFZGOUnRlFPjjGsJB_GLuFFIs3fFWLCp2-K8gc/edit?usp=sharing) and see what temperature your chamber will reach. It tells you right away whether this is worth it.
