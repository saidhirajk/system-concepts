# Linux Boot Process (Step-by-Step Process)

Understanding the Linux boot process is crucial for troubleshooting and system administration.  
Here’s the sequence:

1. **BIOS/UEFI**
   - Performs POST (Power-On Self-Test) to check hardware.
   - Locates the boot device and reads the first sector (MBR or GPT).
   - Passes control to the boot loader.

2. **MBR (Master Boot Record) / GPT (GUID Partition Table)**
   - MBR: Located in the first sector (512 bytes) of the boot disk. Contains the primary boot loader code and partition table.
   - GPT: Modern standard used with UEFI. Supports larger disks and stores partition info robustly.
   - Both help locate and load the bootloader (e.g., GRUB).

3. **GRUB (GRand Unified Bootloader)**
   - Loads the Linux kernel into memory.
   - Presents a boot menu (if configured) for OS/kernel selection.
   - Passes boot parameters to the kernel.  
   - Config files: `/etc/default/grub`, `/boot/grub/grub.cfg`.

4. **Kernel Initialization**
   - Kernel image is loaded into RAM.
   - Decompresses itself and initializes CPU, memory, and devices.
   - Mounts the root filesystem.

5. **Initramfs (Initial RAM Filesystem)**
   - Temporary root FS loaded by GRUB before the real one.
   - Provides required drivers/modules (e.g., disk controllers).
   - Helps kernel access the actual root FS.

6. **Init / systemd**
   - Kernel starts the first user-space process (traditionally `init`, now mostly `systemd`).
   - Initializes rest of the system → mounts filesystems, starts services, sets runlevel/target.

7. **Runlevels / Targets**
   - **Runlevels (init)**: Define system states (single-user, multi-user, graphical).  
   - **Targets (systemd)**: Modern equivalent, e.g., `multi-user.target`, `graphical.target`.

8. **User Login**
   - Once services are started & default target is reached, login prompt appears.

![Linux Boot Process](images/linux_boot_process.png)


📌 *This entire flow completes within seconds every time you boot your Linux machine!*
