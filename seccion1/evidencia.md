cat > seccion1/evidencia.md << 'EOF'
# Sección 1 - Evidence of Debian Installation
## Answers 
- Question 1 
LUKS or Linux Unified Key Setup refers to a standard specification of how to store both the metadata and the encryption keys used to encrypt disks in Linux. It is intended that encrypted disks can be read consistently across a variety of systems, by using a common format when they are created.
The actual encryption and decryption of the data stored on the block devices is done by the dm-crypt kernel module in Linux. When an application attempts to read data from an encrypted disk it issues a read request, which is then translated into an I/O request for the underlying physical device using the mapping established in the device mapper layer. The dm-crypt module will then decrypt the data from the target disk on-the-fly as it is being read and will also encrypt any new data written back to the disk before it is committed to permanent storage.

- Question 2

   Aspect               ||           FDE (Full Disk Encryption)                                       ||          Filesystem-level Encryption
What it encrypts        || Everything on the disk (boot sector, partitions, metadata, logs, swap).    || Only files and directories within a specific filesystem.
Metadata visibility     || All metadata is hidden and encrypted.	                              || Metadata like directory structure remains visible.
Advantage 1	        || Protects sensitive system information (logs, swap files, temporary data).  || Offers granularity - you can encrypt only sensitive directories like /home.
Advantage 2	        || Transparent to applications - no changes needed.	                      || Allows selective recovery of encrypted files without affecting the whole system.
Limitation 1	        || If you lose the encryption password, the entire disk is unrecoverable.     || More complex to configure when using multiple keys for different filesystems.
Limitation 2 	        ||Constant CPU overhead from continuous encryption/decryption.	              || Attackers can see directory structure and file sizes, allowing pattern analysis.
When password is needed || During boot (before OS starts).	                                      || After system boots, when accessing encrypted directories.
 
Our installation uses FDE: All data on /dev/sda5 is encrypted, and the password is requested during boot before GRUB loads the kernel. 

-Question 3 
The LVM (Logical Volume Manager) provides a level of abstraction that separates physical disks from filesystems. LVM allows you to manage storage more flexibly than would be possible through traditional partitioning of disks using disk partitions directly. LVM features three levels of abstraction: 
(1) the Physical Volume (PV) – the location on which your data lives physically in a storage device, such as a disk or partition, is the actual physical storage where your data will be physically stored. An example of our PV is /dev/mapper/sda5_crypt, which is the decrypted LUKS container. The PV is where your real data resides in the storage device.
 

The installer shows the main partitioning options. We selected option 3: "Guided - use entire disk and set up encrypted LVM". This option automatically creates LVM volumes inside a LUKS encrypted container, which is exactly what we need for this project. Volume Groups (VGs) are logical containers that can include more than 1 physical volume (PV). VGs provide a virtual "hard disk" that groups the total size of multiple P/V's into one single entity. In our case, there is one VG called daniel-vg that provides 19.05 GB of total available storage from the P/V (/dev/mapper/sda5_crypt) managed by that VG. 
3. LV (Logical Volume): Virtual partitions created in the volume group created by the user to use (use) LVs, but not PVs or VGs. The logical volumes can be mounted to directories as filesystems. There are 3 logical volumes created in our system:
1. root (7.5 GB) - mounted on / for the operating system
2. home (10.5 GB) - mounted on /home for user files
3. swap_1 (1 GB) - used as virtual memory.

Advantages of LVM over traditional partitioning:
Increase without losing access: You can increase /home partition space while still using the computer. Most systems would require you to unmount your /home partition (e.g., boot from CD) in order to resize it. Flexibility: You can add additional physical devices (hard drives/SSDs) without needing to repartition existing partitions (i.e., you can continue using the same VG). Taking snapshots of the entire system: LVM gives instant access to a snapshot of the entire system. This is helpful for taking backups or reverting changes. Most traditional partitions do not allow snapshots. 

- Question 4 
There are 7 steps involved in the booting of a system configured with LUKS and LVM encryption. These steps include the BIOS/UEFI initialization, where the hardware is initialized and a search is done for the bootloader; GRUB loading from the unencrypted partition /boot; GRUB prompting for the LUKS passphrase; dm-crypt decrypting /dev/sda5 and mapping the data inside of it to /dev/mapper/sda5_crypt; Linux Kernel scanning for the VG 'daniel-vg' and the 3 logical volumes (root, home, swap) within it; Linux kernel loading from /dev/mapper/daniel--vg-root (the decrypted root volume) and executing the init system (systemd); and finally, systemd starting up the rest of the file systems (/home, /var, etc.) as well as their respective services.
Role of GRUB: The GRUB program is responsible for providing a request for an encryption password and loading the kernel. GRUB does not perform any decryption but instead passes on the entered password to the dm-crypt program, which will perform the actual decryption of data after unlocking the encrypted files with the entered password before the kernel starts up. 

## Screenshots

Screenshot 1: Partitioning Method Selection 
EOF
