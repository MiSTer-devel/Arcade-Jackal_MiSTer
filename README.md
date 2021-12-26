# Jackal for [MISTer](https://github.com/MiSTer-devel/Main_MiSTer/wiki)
An FPGA implementation of Jackal/Top Gunner for the MiSTer platform

## Credits
- Sorgelig: MiSTer project lead
- Ace: Core design and Konami custom chip implementations
- ElectronAsh, Furrtek, SnakeGrunger: Assistance with Konami custom chip implementations
- brknglass: Obtaining a bootleg Jackal PCB for reverse-engineering
- Shane Lynch: SDRAM support
- JimmyStones: High score saving support & pause feature
- Kitrinx: ROM loader
- Porkchop Express: Finishing touches

## Features
- Logic modelled to match the original PCB design as closely as possible
- Standard joystick and keyboard controls
- High score saving (To save your scores, use the 'Save Settings' option in the OSD)
- Greg Miller's cycle-accurate MC6809E CPU core with modifications by Sorgelig and bugfixes by Arnim Laeuger and Jotego
- YM2151 implementation using JT51 by Jotego
- Modeling of bootleg PCBs' timing and graphical differences
- Fully-tuned audio filters matching both bootleg and original PCBs
- Option for normalized video timings to use with picky HDTVs and monitors (underclocks the game by ~1.8%)

## **NOTE**
This core requires SDRAM to function properly, which is used to hold tilemap data.  While the game will run without SDRAM, the tilemap layer will not be visible without it.

## Installation
Place `*.rbf` into the "_Arcade/cores" folder on your SD card.  Then, place `*.mra` into the "_Arcade" folder and ROM files from MAME into "games/mame".

### ****ATTENTION****
ROMs are not included. In order to use this arcade core, you must provide the correct ROMs.

To simplify the process, .mra files are provided in the releases folder that specify the required ROMs along with their checksums.  The ROM's .zip filename refers to the corresponding file in the M.A.M.E. project.

Please refer to https://github.com/MiSTer-devel/Main_MiSTer/wiki/Arcade-Roms for information on how to setup and use the environment.

Quick reference for folders and file placement:

/_Arcade/<game name>.mra
/_Arcade/cores/<game rbf>.rbf
/games/mame/<mame rom>.zip
/games/hbmame/<hbmame rom>.zip

## Controls
### Keyboard
| Key | Function |
| --- | --- |
| 1 | 1-Player Start |
| 2 | 2-Player Start |
| 5, 6 | Coin |
| 9 | Service Credit |
| Arrow keys | Movement |
| CTRL | Fire machine gun |
| ALT | Fire grenades/rockets |

### Joystick (buttons follow Super NES layout)
| Joystick action | Function |
| --- | --- |
| D-Pad | Movement |
| B | Fire machine gun |
| A | Fire grenades/rockets |
| L | Rotary left |
| R | Rotary right |

## Notes on the different software revisions
1) Each version of Jackal has different ways in which the machine gun fires:
- Most versions of Jackal, including bootlegs, fire the machine gun upwards at all times
- The Japanese version of Jackal fires the machine gun in the direction the player is facing
- A specific version of Jackal supports rotary controls to allow aiming the machine gun in 8 directions (bootlegs support this as well, but lack the hardware to handle it on the PCB)
2) Bootleg PCBs have faster VSync timings than original PCBs, resulting in the in-game music failing to start - this behavior is recreated for bootleg versions of Jackal.  To work around this, pause the game for a short while prior to being given control

## Known Issues
1) Sprites render one frame earlier than normal - this is not correct behavior and causes graphics rendered on both the sprite and tilemap layers partially split apart during scrolling
2) Although bootleg flaws are modeled, the score display is not correctly rendered when the screen is flipped and the slower clocks used by bootleg Jackal PCBs are missing - as such, the core behaves as if said bootlegs used the same clocks as the original PCB
