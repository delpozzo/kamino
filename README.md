# Kamino

## About

Kamino is an integrity-based disk imaging utility for Linux.

![Kamino Screenshot](src/screenshots/main_menu.png?raw=true)

### Features

+ Drive-To-Drive Cloning
+ Capture Image File from Drive
+ Deploy Image File to a Single Drive
+ Deploy Image File to Multiple Drives Simultaneously
+ Wipe a Single Drive
+ Wipe Multiple Drives Simultaneously
+ Automated Integrity Checking of Image Files
+ Image File Manager

## Compatibility

### Operating System

Kamino is written in bash and will run on most modern Linux distributions with a kernel version of 2.6 or higher. Kamino relies mainly on `dd`, `gzip`, and `sha256sum` which are bundled with most distros. Kamino has been verified to work on Ubuntu 16.04 thru 18.04, Arch, Debian, RHEL 6.7, and Fedora 25 but will likely run on many others.

### Supported Devices

Kamino supports most block devices such as USB Drives, SATA HDDs and SSDs, SD Cards, etc. The rule of thumb is if it shows up under `/dev` as `sda` through `sdz`, the device will most likely be supported. Optical devices (CD/DVD/BD) are not supported at this time.

## Installation

**Step 1:** Download the latest Kamino tarball from the [release folder](https://github.com/delpozzo/kamino/blob/master/release).


**Step 2:** Verify the integrity of the Kamino tarball by running the following command and comparing the output to the [expected hash totals](https://github.com/delpozzo/kamino/blob/master/release/HASHTOTALS.md):

`sha256sum kamino-1.x.y.tgz` (where x.y corresponds to the version that you downloaded)

If the sha256sum output matches the [expected hash totals](https://github.com/delpozzo/kamino/blob/master/release/HASHTOTALS.md), proceed to Step 3.


**Step 3:** Extract the tarball with the following command:

`tar -xzvf kamino-1.x.y.tgz -C <destination directory>`(where x.y corresponds to the version that you downloaded)

This will create a folder titled "kamino" inside the `<destination directory>`

Example: `tar -xzvf kamino-1.0.1.tgz -C /home/mike`

## Usage

+ [Running Kamino](#running-kamino)
+ [Capture Image](#capture-image)
+ [Clone Drive](#clone-drive)
+ [Deploy Image (Single Drive)](#deploy-image-single-drive)
+ [Deploy Image (Multi-Drive)](#deploy-image-multi-drive)
+ [Zeroize (Single Drive)](#zeroize-single-drive)
+ [Zeroize (Multi-Drive)](#zeroize-multi-drive)
+ [Manage Images](#manage-images)
+ [About Kamino](#about-kamino)
+ [Exiting Kamino](#exiting-kamino)
+ [kamino.config](#kaminoconfig)

### Running Kamino

From a terminal, `cd` into the "kamino" folder. Execute `kamino` via `sudo` or as root:

`sudo ./kamino`

Kamino will start and you will be brought to the Main Menu.

![Main Menu Screenshot](src/screenshots/main_menu.png?raw=true)

**Important:** On your first run of Kamino, make sure you set the directory you'd like to use for image files via "Manage Images" by entering `m` into the Main Menu selection followed by `c` to configure the directory.

**Note:** If you cloned this repo and are running Kamino from the `src` directory, make sure the execute bit is set for the scripts:

```
cd kamino
chmod +x kamino
chmod +x res/scripts/*
```

### Capture Image

Enter `1` into the Main Menu selection to capture an image of a drive attached to the system.

A list of available drives will be displayed. Choose a `source drive` by entering the corresponding number into the selection prompt. In the example below, `/dev/sdg` is selected by entering `5`

![Capture Image Screenshot 1](src/screenshots/capture-1.png?raw=true)

Enter a name for the image file. Do not include any file extensions since `.img.gz` will be automatically appended.

![Capture Image Screenshot 2](src/screenshots/capture-2.png?raw=true)

The command to capture the image will be displayed based off of your input from the previous steps. Carefully review the output from this screen and enter `y` to begin the image capture process.

![Capture Image Screenshot 3](src/screenshots/capture-3.png?raw=true)

Capturing a drive image can take anywhere from a minute to many hours depending on the size of the drive and the speed of your hardware. During the image capture process, the `dd` command output will display to show the progress.

![Capture Image Screenshot 4](src/screenshots/capture-4.png?raw=true)

When the image capture is complete, a `sha256` hash will be generated and saved as `<image_name>.img.gz.sha256` in  `images_directory`. Press enter to return to the main menu.

![Capture Image Screenshot 5](src/screenshots/capture-5.png?raw=true)

### Clone Drive

Enter `2` into the Main Menu selection to clone one drive directly to another. 

### Deploy Image (Single Drive)

Enter `3` into the Main Menu selection to deploy an image file to a single target drive. 

### Deploy Image (Multi-Drive)

Enter `4` into the Main Menu selection to deploy an image file to multiple target drives at the same time.

**Note:** For multi-drive operations, the target drives you select must all be the same size.

### Zeroize (Single Drive)

Enter `5` into the Main Menu selection to wipe a single target drive by writing all zeroes.

### Zeroize (Multi-Drive)

Enter `6` into the Main Menu selection to wipe multiple target drives at the same time by writing all zeroes.

**Note:** For multi-drive operations, the target drives you select must all be the same size.

### Manage Images

Enter `m` into the Main Menu selection to manage images and configure which directory you would like to use for image files.

### About Kamino

Enter `a` into the Main Menu selection to see information about Kamino.

### Exiting Kamino

Enter `q` into the Main Menu selection to exit Kamino.


### kamino.config

The `kamino.config` file is located under the `kamino/res` directory. The various options (and defaults) are described below. 

**Note:** the `images_directory` option should be set via "Manage Images" within Kamino. All others can be edited in this file directly.

```
# Block size which is utilized for dd operations
# Default: 64K
block_size 64K

# Directory where image files are stored
images_directory /path/to/images

# Directory where temporary pids are stored 
# Default: /tmp
tmp_directory /tmp

# gzip compression level [1-9]
# Default: 6
# 1 = fastest, lowest compression (produces largest image files)
# 9 = slowest, highest compression (produces smallest image files)
compression_level 6
```

## License

Kamino Copyright (C) 2019 Mike Del Pozzo

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or any later version.

See [LICENSE](LICENSE) for details.
