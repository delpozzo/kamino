# Kamino

## About

Kamino is an integrity-based disk imaging utility for Linux.

### Features
Drive-To-Drive Cloning

Capture Image File from Drive

Deploy Image File to a Single Drive

Deploy Image File to Multiple Drives Simultaneously

Wipe a Single Drive

Wipe Multiple Drives Simultaneously

Automated Integrity Checking

Image File Manager

## Compatibility

### Operating System

Kamino is written in bash and will run on most modern Linux distributions with a kernel version of 4.0 or higher. Kamino relies mainly on `dd`, `gzip`, and `sha256sum` which are bundled with most distros. Kamino has been verified to work on Ubuntu 16.04 thru 18.04, Arch, and Debian but will likely run on many others.

### Supported Devices

Kamino supports most block devices such as USB Drives, SATA HDDs and SSDs, SD Cards, etc. The rule of thumb is if it shows up under `/dev` as `sda` through `sdz`, the device will most likely be supported. Optical devices (CD/DVD/BD) are not supported at this time.

## Installation

**Step 1** Download the latest Kamino tarball from the [release folder](https://about:blank).

**Step 2** Verify the integrity of the Kamino tarball by running the following command and comparing the output to the [expected hash totals](https://about:blank):

`sha256sum kamino-1.x.y.z.tgz` (where x.y.z corresponds to the version that you downloaded)

If the sha256sum output matches, proceed to Step 3.

**Step 3** Extract the tarball with the following command:

`tar -xzvf kamino-1.x.y.z.tgz -C <destination directory>`

This will create a folder titled "kamino" inside the `<destination directory>`

Example: `tar -xzvf kamino-1.0.0.0.tgz -C /home/mike`

## Usage

### Running Kamino

From a terminal, `cd` into the `kamino` folder. Execute `kamino` via `sudo` or as root:

`sudo ./kamino`

Kamino will start and you will be brought to the Main Menu.

**Important:** On your first run of Kamino, make sure you set the directory you'd like to use for image files via "Manage Images" by entering `m` into the Main Menu selection followed by `c` to configure the directory.

### Capture Image

Enter `1` into the Main Menu selection to capture an image. 

### Clone Drive

Enter `2` into the Main Menu selection to clone one drive directly to another. 

### Deploy Image (Single Drive)

Enter `3` into the Main Menu selection to deploy an image file to a single target drive. 

### Deploy Image (Multi-Drive)

Enter `4` into the Main Menu selection to deploy an image file to multiple target drives at the same time.

**Note** For multi-drive operations, the target drives you select must all be the same size.

### Zeroize (Single Drive)

Enter `5` into the Main Menu selection to wipe a single target drive by writing all zeroes.

### Zeroize (Multi-Drive)

Enter `6` into the Main Menu selection to wipe multiple target drives at the same time by writing all zeroes.

**Note** For multi-drive operations, the target drives you select must all be the same size.

### Manage Images

Enter `m` into the Main Menu selection to manage images and configure which directory you would like to use for image files.

### About

Enter `a` into the Main Menu selection to see information about Kamino.

### Exit

Enter `q` into the Main Menu selection to exit Kamino.

### kamino.config

The `kamino.config` file is located under the `kamino/res` directory. The various options (and defaults) are described below. 

**Note:** the `images_directory` parameter should be set via "Manage Images" within Kamino. All others can be edited in this file directly.

&#35; Block size which is utilized for dd operations

&#35; Default: 64K

block_size 64K

&#35; Directory where image files are stored

images_directory /path/to/images

&#35; Directory where temporary pids are stored 

&#35; Default: /tmp

tmp_directory /tmp

&#35; gzip compression level [1-9]

&#35; Default: 6

&#35; 1 = fastest, lowest compression (produces largest image files)

&#35; 9 = slowest, highest compression (produces smallest image files)

compression_level 6

&#35; Root filesystem protection [yes, no]

&#35; Default: yes

&#35; Prevents Kamino from listing the drive which the root

&#35; filesystem is currently mounted to as a selectable option

protect_root_filesystem yes

## License

Kamino Copyright (C) 2019 Mike Del Pozzo

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or any later version.

See [LICENSE](LICENSE) for details.
