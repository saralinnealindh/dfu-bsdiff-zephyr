# About
This is a module implementing [DETools](https://github.com/eerimoq/detools) for [Zephyr](https://www.zephyrproject.org/). It allows for incremental firmware updates, or [delta updates](https://en.wikipedia.org/wiki/Delta_update), as an alternative to the standard procedure of downloading new firmware in its entirety.

### Key features 
The module is based on my [bachelor´s thesis](https://hdl.handle.net/20.500.12380/302598), which one may look through for implementation details, descriptions of the algorithms used, methodology, and suggestions for further research, among other things. For a brief overview one may refer to the list below:

* Only tested on [nRF52840 DK](https://www.nordicsemi.com/Products/Development-hardware/nrf52840-dk). However, it will likely very easily be ported to other [Zephyr supported boards](https://docs.zephyrproject.org/latest/boards/index.html).
* Zephyr v3.3.
* The delta encoding algorithm used is the DETools implementation of [BSDiff](http://www.daemonology.net/bsdiff/) using [heat-shrink](https://github.com/atomicobject/heatshrink) for compression.
* The program utilizes the Device Firmware Upgrade features facilitated by the [MCUBoot](https://www.mcuboot.com/) bootloader, and is therefore dependent on its usage. Most notably it takes advantage of the [flash map layout](https://github.com/mcu-tools/mcuboot/blob/main/docs/readme-zephyr.md).
* The patching process makes use of three partitions: the primary partition, the secondary partition, and the patch partition. The current firmware runs on the primary partition, the new firmware is created on the secondary partition, and the patch is downloaded to the patch partition. Naturally, this means that the size of the patch partition puts an upper limit to the size of the patch. When the new firmware has been created, the device requests a swap of the primary and the secondary partition and reboots, as in the [normal upgrade scanario](https://www.mcuboot.com/documentation/design/#high-level-operation).
* Limited testing has resulted in patch sizes of 1.6 to 6.4 percent of target image size depending on the types of changes made. However, more extended testing has to be performed in order to make any generalized claims.

### Purpose 
Many resource-constrained IoT units are used in a manner which makes them inaccessible via cable and at the same time unable to receive large amounts of data using radio transmissions. Upgrading firmware is hence difficult or in some cases impossible. Integrating support for delta updates in the unit is a potential solution to this problem, as it significantly reduces the payload during an upgrade scenario. However, as of now there is no open-source solution for delta upgrades in embedded systems. The purpose of the application is to show that such a solution is achievable and that it causes a significant payload reduction.
