 

## **Lite BMC Firmware Flash Utility** 
it provides to update the LiteBMC firmware on SAMRC ARM & x86-64 platforms. It uses I2C (for arm) / SMBUS(for x86) to communicate with the Lite BMC. This document will help to understand the Flash Firmware Utility supported features and how user can use it.



## How to Build & Install  

1. Install required dependencies.


| Supported Hardware                                           | **Architecture** | **Build Environmental details**                              |
| ------------------------------------------------------------ | ---------------- | ------------------------------------------------------------ |
| **1. SMARC LEC-PX30** with [Yocto Linux](https://docs.ipi.wiki/smarc-ipi/ipi-smarc-px30/YoctoImages.html#Binary-Image-download-Link), [Debian](https://docs.ipi.wiki/smarc-ipi/ipi-smarc-px30/DebianImages.html#Binary-Image-download-Link), [Ubuntu 18.04](https://docs.ipi.wiki/smarc-ipi/ipi-smarc-px30/UbuntuImages.html#Binary-Image-download-Link) images <br>(gcc 7.4.0 already inside) <BR>**2. SMARC LEC-iMX8M** with [Yocto Linux](https://github.com/ADLINK/meta-adlink-nxp/blob/zeus/README.md#lec-imx8m-smarc-module) image (gcc 7.4.0 already inside) | ARM-64 bit       | Install required packages:<BR>        - install i2c-tools for Debian Image |
| **SMARC LEC-iMX6R2** with [Yocto Linux](https://github.com/ADLINK/meta-adlink-nxp/blob/zeus/README.md#lec-imx6r2-smarc-module) image | ARM-32 bit       | gcc version :  7.4.0                                         |
| **1. IMB-M45/M45H** with [Ubuntu 18.04 LTS](https://ubuntu.com/download/desktop) <br>**2. AMITX-CF-G** with [Ubuntu 18.04 LTS](https://ubuntu.com/download/desktop)<br>**3. ADi-SA3X-CL** with [Ubuntu 20.04 LTS](https://ubuntu.com/download/desktop) <br> | x86-64           | Install required packages:<BR>      - gcc version :  7.5.0  <br>      - i2c-tools |

2. Git clone the source from https://github.com/adlink/litebmc-fwupd on your target device

3. please compile the source code using below command.

   ```
   $ cd ad-litbmc-fwupd
   $ gcc ad-litbmc-fwupd-src.c -o ad-litbmc-fwupd 
   ```



## How to Use 

The command **ad-litbmc-fwupd** is used in Linux to flash LiteBMC firmware on your target device.

**Usage**  

* Firmware Update:

  The utility will validate your file is valid or not. Once done, it will start to flash this firmware. 

  ```
  $ ad-litbmc-fwupd -u your_file.bin
  ```

    **Note**: 

  * it will give the below output with **the valid .bin file**:

    > Firmware file validation is in progress
    > Firmware file validation done successfully
    > Firmware updating in normal mode.
    > Firmware flashing in progress, please don't abort the application
    > Updating ….100%
    > Flashing done!
    > Firmware version on target device: BMC PX-30 0v11 Dec 17 2019 (c) ADLINK Technology Inc.
    > Firmware version on your bin file BMC PX-30 0v11 Dec 17 2019 (c) ADLINK Technology Inc.
    > Updated successfully and please reboot the system.
    
  * it will give the below output with **the invalid .bin file**:

    > Validating the bin file is in progress...
    > Firmware file is not valid. please provide valid firmware file to update BMC.
    
  * it will give the below output with **the incompatible .bin file**:
  
    > Validating the bin file is in progress... 
    > Firmware file is not suitable for current BMC, Tool expecting PX-30. But user provided Firmware file is for LEC-iMX8M.
  
  <br>


* Firmware update in Recovery Mode. 

  Please use this command to flash when BMC firmware is not in your target device

  ```
  $ ad-litbmc-fwupd -r your_file.bin
  ```

  **Note: Please provide respective firmware file to the target otherwise board will not boot again**

<br>


* Display the BMC version of .bin binary:

  ```
  $ ad-litbmc-fwupd -d -f your_file.bin
  ```

  **Note:**

  * it will give the below output with the valid .bin file:
  
    > **Output format: BMC [MODULE_NAME](#_Module_Details_:) [VERSION](#_Module_Details_:) [DATE](#_Module_Details_:) © ADLINK Technology Inc.**

<br> 

* Display the BMC version on your target device

  ```
  $ ad-litbmc-fwupd -d -t
  ```

  **Note:**

  * it will give the below output when the firmware is in your target,

    > **Output format: BMC [MODULE_NAME](#_Module_Details_:) [VERSION](#_Module_Details_:) [DATE](#_Module_Details_:) © ADLINK Technology Inc.**

  * it will give the below output when the firmware is NOT in your target

    > **Output format: Firmware is corrupted, please update the firmware in recovery mode.**
  



 



 

 

