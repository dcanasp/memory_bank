## BIOS (Basic Input/Output System)

- BIOS is a firmware embedded on a chip on a computer's [[Motherboard]]. It initializes and tests hardware components during the booting process and provides runtime services for operating systems and programs.
- Acts as an interface between the computer's firmware and its operating system at the boot moment
- It loads the [[OS]] to ram 

- **Booting Process**:
    - **Power-On Self-Test (POST)**: Checks the hardware's functionality and compatibility.
    - **Bootstrap Loader**: Locates the operating system's bootloader and hands over control.

## UEFI (Unified Extensible Firmware Interface)

- UEFI is a modern replacement for the traditional BIOS, providing a more versatile and user-friendly interface.
- **Advantages Over BIOS**:
    - Supports larger hard drives (over 2 TB).
    - Faster boot and resume times.
    - More advanced security features like Secure Boot.
- Like BIOS, it initializes system components and loads the operating system. However, it comes with a more flexible pre-boot environment.
- **Booting Process**:
    - **Initialization**: Performs a similar function to BIOS POST but with more advanced diagnostic capabilities.
    - **EFI Bootloaders**: More flexible, can read from a variety of file systems, allowing multi-boot setups.


## Booting Process Overview

- **Initial System Check**. Upon power-up, the system firmware (BIOS or UEFI) checks the hardware's integrity.
- **Detection of Boot Device**. Identifies and prioritizes available boot devices (hard drives, SSDs, USB drives, network boot, etc.).
- **Loading the OS**. Executes the bootloader from the selected boot device, which then loads the operating system into memory.
- **Handover to OS**. Control is transferred to the operating system, initiating the system startup.
## present

- UEFI is considered the successor to BIOS, addressing many of the older system's limitations.
- Modern systems are **predominantly** equipped with **UEFI**, though some may still offer a legacy BIOS mode for compatibility with older systems.
- You can **access** this **BIOS/UEFI** as in the software, in this window you can change what [[OS]] to use, the drivers, and more. Normally to do that you hit one key when turning up the device (f1,f2,f12 depends on the computer, you can google `how to enter bios`) 
![[Bios.png]]
