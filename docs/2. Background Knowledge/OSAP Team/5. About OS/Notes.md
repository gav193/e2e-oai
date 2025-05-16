# Study Notes

## Topic 1 
###[Windows Hardware and Drivers](https://learn.microsoft.com/en-us/windows-hardware/get-started/?view=windows-11)
From the reference, it gives an overview about building, customizing, and deploying Windows 10 and Windows 11 devices along with its drivers. 
Building and Customizing Windows Devices : 
- Device development = selecting appropriate hardware components to meet both the minimum and optimal requirements
- Driver development = driver creation using Windows Driver Kit (WDK) with support for both Kernel-Mode Driver Framework (KMDF) and User-Mode Driver Framework (UMDF)
- Universal windows drivers = driver development that are compatible across multiple device types (embedded to desktop)

Deployment and Customization Tools : 
- Windows Assessment and Deployment Kit (ADK) = customizes Windows images, assessing system performance, and deploying Windows at scale
- Windows Preinstallation Environment (WinPE) = lightweight OS used for deploying PCs, workstations, servers, or troubleshoot an OS when it's offline
- Unattended Installation = utilizes "Unattend.xml" files to automate Windows installations, allows for consistent and efficient deployments

Testing and Validation : 
- Test Authoring and Execution Framework (TAEF) = creates and runs automated tests to ensure hardware and software reliability
- Windows Hardware Lab Kit (HLK) = validates hardware and drivers to ensure meeting Windows certification requirements
- WIndows Performance Toolkit = analyzes system and application performance to identify potential bottleneck or issues

Manufacturing and Deployment : 
- Image Customization = build customized Windows images tailored to speciic markets or needs
- IoT Device Deployment = build and deployment of Windows IoT Core devices (including apps, drivers, settings)

###[Windows Driver Kit (WDK) Documentation](https://learn.microsoft.com/en-us/windows-hardware/drivers/)
This documentation explains about the aim to design, develop, test, and deploy hardware and device drivers for Windows devices.
Development Tools and Resources : 
- Windows Driver Kit (WDK) = essential for building Windows drivers, integrates Visual Studio and provides headers, libraries, and tools necessary for driver development
- Driver Samples = Collection of drivers illustrating scenarios to understand implementation patterns
- Debugging Tools for Windows = provides tools to debug drivers and system code (includes WinDbg)

Driver Installation and Deployment : 
- Device and Driver Installation = creating driver packages, about INF files, and managing driver installation process
- Driver Security Checklist = practices to ensure drivers are secure including code signing and adherence to security protocols

Testing and Certification : 
- Hardware Lab Kit (HLK) = framework to test hardware and drviers to ensure meeting WIndows certification requirements
- Partner Center for Windows Hardware = submits drivers for certification and management of hardware submissions

Driver Frameworks and Models
- Windows Driver Frameworks (WDF) = Comprises KMDF and UMDF, provides structured models for writing both kernel-mode and user-mode respectively
- Kernel-Mode Driver Architecture = Driver development operating in kernel mode



### [Windows 11 IoT Enterprise LTSC](https://www.microsoft.com/zh-tw/evalcenter/evaluate-windows-11-iot-enterprise-ltsc)
Key Features : 
- Long-Term (10 year) support cycle with 5 years mainstream support + 5 years of extended support
- High stability and security fom Windows 11 core with enterprise-grade security and management features
- Minimal System Requirements supporting x64 and ARM64 with low hardware requirements (1 GHz dual-core CPU, 2 GB RAM, 16 GB storage)
- Customizable Lockdown by restricting the user actions based on the device's capabilities for security

Important Notes : 
- Back up data before installation since process will reformat your drive
- Unable to revert to previous version of Windows after installing
- Once evaluation period ends, the system will shut down automatically every hour and display software watermark


## Topic 2
### Kernel Mode Drivers
Contains two types of drivers which is : 
- Function Drivers = primary driver for a device, communicates directly with device
-> Working principle : 
  - Initializes and manages the hardware
  - Handles read/write/control requests (I/O operations)
  - Interfaces with Windows driver stacks
- Filter Drivers = optional driver, sits above or below function drivers to modify behavior (antivirus, encryption)
-> Types
  - Upper filter driver = intercept I/O requests before they reach function driver
  - Lower filter driver = intercept I/O requests after the function driver processes them
->  Roles
  - Logging
  - Encryption
  - Antivirus scan
  - Custom command filtering



### User Mode Drivers
Based on [User-Mode Driver Framework (UMDF)](https://learn.microsoft.com/en-us/windows-hardware/drivers/wdf/overview-of-the-umdf) 
Runs in user space, outside the Windows kernel, hence :
- Its comparatively safer since it won't crash the entire OS
- Essier to debug
- Slightly slower then KMDF due to context-switching between user and kernel space
- Used to write drivers for simpler or less latency-sensitive devices

Benefits of UMDF : 
- Stability = Since crashes in UMDF drivers don't crash the entire OS
- Security = Isolated and less direct access to hardware corresponds to lower risks of exploits (less prone to backdoors)
- Ease of development = No need to directly deal with kernel APIs

Features : 
- Asynchronous I/O model
- Simplified plug-and-play with power management
- COM-based interface for programmin

Limitations : 
- No suitable for high-speed, low-latency device interactions
- Cannot be used for drivers that must run in kernel mode

## Topic 3
OS Concepts 
### Process
-> instance of a running program containing :
- Code
- Data
- Resources
- Execution context
- Virtual address space

Processes are isolated from each other to provide security or stability. The OS manages processes using a Process Control Block (PCB) which tracks process state, memory, CPU registers, etc.

### Threads
-> smallest unit of execution within a process
Each process has at least one thread and threads within a process share the same memory space and resources to execute instructions independently but share the same data
Threads enables for multitasking wihtin a single process hence leading to a more efficient system rather than creating multiple processes. (because threads share the same address space, while processes does not)
Types of Threads: 
- User-level = managed by user libraries and not visible to OS scheduler
- Kernel-level = managed by the OS scheduler directly

### Memory
Virtual memory : 
- Each process gets its own virtual address space which maps to a physical memory
- Virtual memory allows isolation and protection between processes
- Enables programs larger than physical RAM to run by swapping memory to disk

Memory Management Units (MMU) = hardware that traslates virtual address to physical address

Types of Memory : 
- Heap = dynamic memory for runtime allocation
- Stack = stores local variables and call return addresses
- Code/Text Segment = contains executable instructions
- Data Segment = Global and static variables

### File System
-> Manages how data is stored, organized, and accessed on storage devices 
Responsible for : 
- File creation, reading, writing, deletion
- Directory management
- Metadata storage (file size, permissions, timestamps)

Common Windows File Systems : 
- NTFS = Default Windows file system, supports permissions, encryption, journaling (to recover from crashes by saving log of changes before committed)
- FAT32/exFAT = Older file system, commonly used on USB drives and SD cards
- ReFS = Newer Microsoft file system optimized for resilience and large data
