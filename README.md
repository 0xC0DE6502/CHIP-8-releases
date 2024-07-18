# CHIP-8 emulator

CHIP-8 (and S-CHIP) emulator by [0xC0DE](https://twitter.com/0xC0DE6502) for the Acorn Electron.

Download and use for free. Please [donate](https://ko-fi.com/S6S33YYQ7) to support me: [![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/S6S33YYQ7)

![CHIP-8 emulator - Loading screen](https://github.com/0xC0DE6502/CHIP-8-releases/blob/main/res/screenshot1.png?raw=true)

## Prerequisites

The CHIP-8 emulator works on an Acorn Electron, real or emulated. You need DFS or MMFS with `PAGE` at &E00 to run the emulator. 

## Quickstart

If you want to quickly fire up the CHIP-8 emulator and play one of the included games, follow these steps:

1. Download the [disk image](https://github.com/0xC0DE6502/CHIP-8-releases/raw/main/CHIP-8.ssd)
2. Boot the disk on your Acorn Electron, or in one of the Electron emulators
3. On the ROMs selection screen, select one of the included game ROMs
4. Play the game using the CHIP-8 hexpad, which is mapped to the `1` `2` `3` `4` | `Q` `W` `E` `R` | `A` `S` `D` `F` | `Z` `X` `C` `V` keys on the Electron
5. Press `ESCAPE` to return to the ROMs selection screen

## What is CHIP-8?

[CHIP-8](https://en.wikipedia.org/wiki/CHIP-8) is known as the original fantasy game console. It is an interpreted programming language designed in the 1970s by [Joseph Weisbecker](https://en.wikipedia.org/wiki/Joseph_Weisbecker) for the [COSMAC VIP](https://en.wikipedia.org/wiki/COSMAC_VIP) 8-bit computer.

[S-CHIP](https://en.wikipedia.org/wiki/CHIP-8#CHIP-8_extensions_and_variations) (SUPER-CHIP) was created by Erik Bryntse. It is one of many extensions to CHIP-8. S-CHIP has additional opcodes and a higher resolution.

My CHIP-8 emulator is written in 6502 assembler for the Acorn Electron and can play any CHIP-8 or S-CHIP game. Please note: I did not attempt to make my emulator cycle perfect. Also, sprite flicker is a typical CHIP-8 'feature'.

## Game ROMs

The emulator comes with a few CC0 or Public Domain game ROMs. Find more game ROMs online, for example from these 2 sources:
* [John Earnest chip8Archive](https://github.com/JohnEarnest/chip8Archive)
* [Chip-8 Public Domain ROMs](https://www.zophar.net/pdroms/chip8.html)

## Preparing your own games disk

A typical CHIP-8 emulator games disk looks like this:

![CHIP-8 emulator - Typical games disk contents](https://github.com/0xC0DE6502/CHIP-8-releases/blob/main/res/screenshot5.png?raw=true)

A games disk consists of 4 parts:

1. The 4 core emulator files: `!BOOT`, `SCREEN`, `CHIP-8` and `README`
2. A maximum of 13 CHIP-8 ROMs in the `C` directory
3. A maximum of 13 S-CHIP ROMs in the `S` directory
4. Optional [configuration files](#configuration-files) in the `Q` directory

Note that a DFS disk is limited to 31 files in total.

### Adding a game

Follow these 4 steps to add a game to a games disk:

1. Start with the default [games disk](https://github.com/0xC0DE6502/CHIP-8-releases/raw/main/CHIP-8.ssd)
2. Find and download a CHIP-8 or S-CHIP game ROM, e.g. `myfavouritegame.rom`
3. Copy it to the games disk using a correct DFS filename, e.g. `C.MYGAME` for a CHIP-8 game, and `S.MYGAME` for an S-CHIP game
4. Optionally, create and add a [configuration file](#configuration-files), e.g. `Q.MYGAME`

## Playing a game

After preparing your games disk, boot the disk on your Acorn Electron. You should see a loading screen for a few seconds, before entering the ROMs selection screen, e.g.:

![CHIP-8 emulator - ROMs selection screen](https://github.com/0xC0DE6502/CHIP-8-releases/blob/main/res/screenshot2.png?raw=true)

This menu shows all the games found on the disk. It lists CHIP-8 games (if any) first, in alphabetical order. Followed by S-CHIP games (if any). Type a letter to start the corresponding game, e.g. `S.ROCKTO`:

![CHIP-8 emulator - Playing the game Rockto](https://github.com/0xC0DE6502/CHIP-8-releases/blob/main/res/screenshot3.png?raw=true)

### Keys during gameplay

Originally, CHIP-8 games were controlled by the 16-key hexpad of the COSMAC VIP. It may feel a little awkward to use these controls at first. The hexpad keys are mapped to a 'square' of Electron keys, as follows:

| Hexpad key | Electron key |
| :--- | ---: |
| `1` `2` `3` `C` | `1` `2` `3` `4` |
| `4` `5` `6` `D` | `Q` `W` `E` `R` |
| `7` `8` `9` `E` | `A` `S` `D` `F` |
| `A` `0` `B` `F` | `Z` `X` `C` `V` |

Other keys:

`ESCAPE` - Quit the game and return to the ROMs selection screen  
`RETURN`/`DELETE` - Soft reset the emulator  
`CTRL`+`RETURN`/`DELETE` - Hard reset the emulator  
`COPY` - Show or hide game information  
`M` - Mute or unmute sound  
`SPACE` - Pause emulator (hold `SPACE` to single-step through a game)  

### Keys for finetuning a game

Games may sometimes need specific configuration. Or you may want to slow down or speed up a particular game. Use the following keys for that:

`SHIFT`+`1`..`7` - Toggle configuration options ([quirks](#quirks))  
`UP` - Increase emulator speed  
`DOWN` - Decrease emulator speed  

[Quirks](#quirks) and other game information, like emulator speed and ROM name, can be shown or hidden by pressing the `COPY` key, e.g. in the S-CHIP game Blinky:

![CHIP-8 emulator - Showing game information while playing Blinky](https://github.com/0xC0DE6502/CHIP-8-releases/blob/main/res/screenshot4.png?raw=true)

## Quirks

Most games work with the default emulator settings. But some games need to have specific configuration options (quirks) enabled or disabled to work properly. The emulator supports 7 quirks which can be toggled during gameplay (press keys `SHIFT`+`1`..`7`). They can also be set permanently in an optional [configuration file](#configuration-files) for each game. 

The 7 quirks are:
1. **`CZ`** - When enabled, the **C**arry flag is set to **Z**ero after `AND`/`OR`/`XOR` instructions
2. **`II`** - When enabled, the **I**-register is **I**ncremented after certain instructions
3. **`VS`** - When enabled, wait for **V**ertical **S**ync before drawing each sprite
4. **`CL`** - When enabled, **CL**ip sprites at screen edges, otherwise wrap around
5. **`SH`** - When enabled, the bit**SH**ift instructions `SHL`/`SHR` operate on different registers
6. **`JV`** - When enabled, the **J**ump instruction uses the **V**0-register
7. **`LE`** - When enabled, the S-CHIP mode switches to **LE**gacy instead of Modern style

## Configuration files

Quirks and other configuration options can be set permanently by creating a configuration file for a game. When no configuration file is found, the emulator uses its default settings. A configuration file must have the same name as the game and it must be placed in the `Q` directory. Example: the `Q.BLINKY` configuration file belongs to the `S.BLINKY` game ROM.

### Syntax of a configuration file

Configuration files may be created in a plain text editor (e.g. Notepad) on a host machine and then transferred to the games disk. Alternatively, create a configuration file directly on the Electron using the `*BUILD` command.

A configuration file must be plain text, with a maximum of 64 bytes. For instance, here is the `Q.EATY` configuration file for the S-CHIP game Eaty the Alien (`S.EATY`):

```
II,SH,JV
B3,F0
P3,I4
SC8
```

This instructs the emulator to toggle the `II`, `SH` and `JV` quirks (in relation to their default setting). It sets the emulator speed to &C8 (200 instructions per frame). And finally, it defines a few custom colours. Spaces, commas and line-endings function as separators for these commands. Therefore, the entire configuration file could have been written on a single line, e.g. `IISHJVB3F0P3I4SC8`.

Here are the valid commands in a configuration file:

`CZ`, `II`, `VS`, `CL`, `SH`, `JV`, `LE` - Toggle this specific quirk (in relation to its default setting)  
`SNN` - Set emulator speed to &NN (&00..&C8, i.e. 0..200)  
`BN` - Set background colour of gameplay area to N (0..7), default is black (0)  
`FN` - Set foreground colour of gameplay area to N (0..7), default is white (7)  
`PN` - Set background colour (paper) of the rest of the screen to N (0..7), default is black (0)  
`IN` - Set foreground colour (ink) of the rest of the screen to N (0..7), default is white (7)  

The 8 available colours are: 0=black, 1=red, 2=green, 3=yellow, 4=blue, 5=magenta, 6=cyan, 7=white.

---

CHIP-8 emulator - Copyright (C) 2024 [0xC0DE](https://twitter.com/0xC0DE6502)  
