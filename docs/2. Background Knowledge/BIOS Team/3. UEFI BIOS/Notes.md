# Study Notes

## Topic 1 : UEFI Firmware and Tools

UEFI or Unified Extensible Firmware Interface is a modern firmware interface for computers aimed to replace legacy BIOS. UEFI offers faster boot times, better security, support for lager disks, and a modular design.

Boot Flow Overview
Firmware (UEFI) -> Boot Manager -> OS Loader -> OS Kernel

UEFI Initialization System
- SEC (Security Phase) = Initializes temporary memory (cache) and authenticates firmware
- PEI (Pre-EFI Initialization) = Discovers memory and initializes essential hardware (RAM and chipset)
- DXE (Driver Execution Environment) = Loads drivers, installs protocols, and builds Boot Services
- BDS (Boot Device Selection) = Selects OS loader and initiates handoff
- RT (Run Time) = Keeps runtime services alive after OS boot

UEFI Shell Environment
A command line interface that can be accessed before the OS boots up. It can be used for scripting boot behavior, inspecting variables, and running .efi formatted apps.
[Common shell commands and fuctions](https://docstore.mik.ua/manuals/hp-ux/en/5991-1247B/ch04s13.html#google_vignette) 

Building UEFI with [EDK II](https://github.com/tianocore/edk2)
Specifications and other resources needed : 
- Linux Ubuntu 20.04 BTS running OS
- GCC or VS Toolchain
Example of script compiled into .efi file and run in UEFI shell : 
```
#include <Uefi.h>
#include <Library/UefiLib.h>
EFI_STATUS EFIAPI UefiMain(IN EFI_HANDLE ImageHandle, IN EFI_SYSTEM_TABLE *SystemTable) {
    Print(L"Hello, UEFI World!\n");
    return EFI_SUCCESS;
}
```

## Topic 2

## Topic 3
