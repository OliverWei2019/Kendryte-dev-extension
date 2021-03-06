# Kendryte Dev Tool for Visual Studio Code

[![License](https://img.shields.io/badge/license-Apache%202-blue)](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/LICENSE)
![Version](https://img.shields.io/badge/Version-0.1.0-green)

[中文版](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/README.md)

- [Prepare](#Prepare)
- [Quick Start](#QuickStart)
- [Directory Structure](#DirectoryStructure)
- [Features](#Features)
- [Questions](#Questions)
  - [Windows](#Windows)
  - [MacOS](#MacOS)
  - [Linux](#Linux)
- [Roadmap](#Roadmap)

## Prepare

Install [VSCode](https://code.visualstudio.com/) on your computer. Search `Kendryte` on VSCode Extension Market and install. This development tool only support `Kendryte KD233` board for now.

### MacOS environment

1.Install Homebrew

``` bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

2.Install dependencies

``` bash
brew install libusb mpfr
```

### Linux environment

#### Install dependencies

``` bash
sudo apt install libftdi-dev libhidapi-dev libusb-dev
```

or

``` bash
sudo yum install libftdi hidapi libusb
```

#### Debugger permission

1.Download [60-openocd.rules](https://mirrors-kendryte.s3.cn-northwest-1.amazonaws.com.cn/60-openocd.rules) and put it on `/etc/udev/rules.d`

2.Reload `udev`

  ``` bash
    sudo udevadm control --reload
  ```

3.Add user to `plugdev` group

  ``` bash
    sudo usermod -aG plugdev $USER
  ```

## QuickStart

1.Kendryte controller will open after installed, click `Examples` tag to switch to the examples store.

![image](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/resources/readme/en/quick-start/quick-1.png)

2.Select an example and download.

![image](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/resources/readme/en/quick-start/quick-2.png)

3.Click the `build and upload` button for build and upload to board.

![image](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/resources/readme/en/quick-start/quick-3.png)

4.Check the board

## DirectoryStructure

``` Bash  
.
├── .vscode # The contents of this directory are automatically generated, include debug option, build commands and extension's config.
├── CMakeLists.txt # This file is automatically generated when build.
├── README.md
├── build # The contents of this directory are compiled product.
│   ├── CMakeCache.txt
│   ├── CMakeFiles
│   ├── Makefile
│   ├── ai_image
│   ├── camera-standalone-driver
│   ├── cmake_install.cmake
│   ├── compile_commands.json
│   ├── ${Project-name} # Target file
│   ├── ${Project-name}.bin # Target file
│   ├── lcd-nt35310-standalone-driver
│   ├── standalone-sdk
│   └── w25qxx-standalone-driver
├── config # The content of this directory include pin definitions and model address assignment. It can be overwrited.
│   ├── device-manager.json # Model address assignment
│   ├── flash-manager.h # Model address assignment
│   ├── flash-manager.json # Model address assignment
│   ├── fpioa-config.c # Pin definitions
│   ├── fpioa-config.h # Pin definitions
│   └── ide-hook-main.c
├── detect.kmodel # Kendryte model file. You can use nncase to convert tensorflow lite model to kmodel.
├── kendryte-package.json # The config file of project. Include project name, source files and so on. It can be overwrited.
├── kendryte_libraries # This directory is dependencies installation directory. All of dependencies will download on this directory. You shouldn't modify the contents of this directory most of the time.
│   ├── ai_image
│   ├── camera-standalone-driver
│   ├── lcd-nt35310-standalone-driver
│   ├── standalone-sdk
│   └── w25qxx-standalone-driver
└──  src # Source files.
     └── main.c
```

## Features

![image](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/resources/readme/en/full-screen.png)

![image](https://raw.githubusercontent.com/kendryte/Kendryte-dev-extension/master/resources/readme/en/status-bar.png)

## Questions

### Windows

1. Q: Openocd report error: libusb_error_not_supported?

    A: Please download [Zadig](https://zadig.akeo.ie/) and switch `JLink` driver to `Libusb`。

### MacOS

### Linux

1. Q: Openocd report error: libusb_error_access?

    A: Please read [Debugger permission](#Debugger\ permission) to get the debugger permission and plug in device again. If you still have this problem, please contact us on [issue](https://github.com/kendryte/Kendryte-dev-extension/issues).

2. Q: Why extension request sudo permission on upload?

    A: If current don't have permission to read serialport device, it will request sudo permission. You can also config serialport devices permission by yourself.

## Roadmap

- [x] Release `0.1.0` version. (2019.12.09)
- [ ] Serialport arguments configurable.
- [ ] Move `serialport` and `bindings` lib from `node_modules` to `src`.
- [ ] Webview panel listen to React local development server on development mode.
- [ ] Add pin visual configuration.
- [ ] Add CI/CD
- [ ] Release `0.2.0` version. (2020.02)
- [ ] Support `K510`. (2020 Q2)
