# STM32F4 Peripheral Library Set

## Description

This repository includes some libraries for the STM32F4xx series of microcontrollers and was created for fast use as a submodule in any other repositories. The content list is as follows:
1. CMSIS library;
2. SPL library;
3. Third-party USB device library;
4. CMakeLists.txt file for quick and easy building process.


## How to use

The best way to use this repository is to add it to any of your STM32 projects as a submodule (for example in some "third-party" folder) and then to compile it as a static library.

>>>
**`NOTE:`** Don't forget to use [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads) for compiling process (the same as for all your project).
>>>

To fine tune SPL to your desired microcontroller settings (clock, etc.) use `adjust_sys.h` file.

## Important notice:

Be aware that this repository was designed for compiling as a static library only. Therefore, the directories here **do not include** Startup and Linker files (they must be found in some third-party sources and imported into your main project separately).

