# Linux Basics

Metropolia Linux-Basics course notes.

## Typical Directory Structure in Debian Linux

```
/           # The root directory, the top level of the filesystem hierarchy
├── bin     # Essential command binaries that need to be available in single-user mode; for all users (e.g., `ls`, `cp`).
├── boot    # Static files of the boot loader (e.g., kernels, initrd).
├── dev     # Device files (e.g., `/dev/sda1` for the first partition on the first hard drive).
├── etc     # Host-specific system-wide configuration files (e.g., `/etc/passwd` for user accounts).
├── home    # User home directories (e.g., `/home/username`).
├── lib     # Essential shared libraries and kernel modules.
├── media   # Mount points for removable media (e.g., `/media/cdrom` for a CD-ROM).
├── mnt     # Mount point for temporarily mounting filesystems.
├── opt     # Optional application software packages
├── proc    # Virtual filesystem providing process and kernel information as files (e.g., `/proc/uptime`).
├── root    # Home directory for the root user.
├── run     # Runtime variable data (e.g., PID files, sockets).
├── sbin    # Essential system binaries (e.g., `fsck`, `reboot`).
├── srv     # Data for services provided by the system (e.g., web server data).
├── sys     # Virtual filesystem providing system information.
├── tmp     # Temporary files (cleared on reboot).
├── usr     # Secondary hierarchy for read-only user data; contains the majority of (multi-)user utilities and applications.
│   ├── bin     # Non-essential command binaries (not needed in single-user mode).
│   ├── lib     # Libraries for `/usr/bin` and `/usr/sbin`.
│   ├── local   # Tertiary hierarchy for local data specific to this host.
│   ├── sbin    # Non-essential system binaries (e.g., `daemon` programs for various services).
│   └── share   # Architecture-independent data (e.g., documentation, icons).
└── var     # Variable data files (e.g., logs, spool files).
    ├── cache   # Application cache data.
    ├── lib     # State information
    ├── log     # Log files
    ├── mail    # User mailbox files
    ├── run     # Information about the running system since the last boot
    ├── spool   # Spool for tasks waiting to be processed (e.g., print jobs).
    └── tmp     # Temporary files preserved between reboots
```

## APT Toolset

- A package manager to retrieve and install package dependencies from repositories.
- Uses `dpkg` to install, upgrade, and remove packages.

| Command       | Description                         |
| ------------- | ----------------------------------- |
| `apt install` | Install a package                   |
| `apt update`  | Update package lists                |
| `apt search`  | Search for a package by name        |
| `apt show`    | Display information about a package |

## Hardware Settings

| Command       | Description                                                           |
| ------------- | --------------------------------------------------------------------- |
| `uname`       | Print info about the system                                           |
| `uname -m`    | Machine hardware name                                                 |
| `uname -n`    | Network hostname                                                      |
| `hostname`    | Hostname (with sudo can create a new transient hostname)              |
| `hostnamectl` | Control the system hostname                                           |
| `lshw`        | List all information about hardware (install with `apt install lshw`) |
| `lscpu`       | Display information about the CPU architecture                        |
| `lsusb`       | List USB devices                                                      |
| `inxi`        | Display system information                                            |

- There are three types of hostnames:

1. **Static**: Used to initialize the kernel hostname during boot time.
2. **Transient**: A value received from network configuration.
3. **Pretty**: A high-level hostname.

- To set a new transient hostname:
  ```sh
  sudo hostname new_name
  ```

## UEFI

- BIOS is limited, and a replacement called **Extensible Firmware Interface (EFI)** was developed.
- The current standard is **Unified EFI (UEFI)**.
- Booting is different on **UEFI** compared to **MBR**.

| Command      | Description                                                          |
| ------------ | -------------------------------------------------------------------- |
| `efibootmgr` | Shows info if the system uses BIOS or UEFI (`dmesg \| grep "EFI v"`) |

- If a list of boot targets is shown, then the system uses UEFI.

## Init

- Starts and stops the essential service processes on the system.
- The standard init implementation is `systemd`.
- `man init`: Tells the init version.
- `systemd` is one of the newest init implementations.
- Handles the regular boot process, can track individual service daemons, and group together multiple processes associated with a service.

| Command    | Description                                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `man init` | Tells the init version                                                                                                                |
| `systemd`  | Handles the regular boot process, tracks individual service daemons, and groups together multiple processes associated with a service |

## Systemd Configuration

- Files are spread across the system.
- `systemctl -p UnitPath show`: Shows the current systemd configuration search path.
- Unit: Refers to any resource that the system knows how to operate on and manage.
- `/lib/systemd/system`: A place where installed software puts unit files (set of rules).
- `/etc/systemd/system`: A place where to modify files.

| Command                      | Description                                         |
| ---------------------------- | --------------------------------------------------- |
| `systemctl -p UnitPath show` | Shows the current systemd configuration search path |
| `systemctl start <unit>`     | Starts a unit                                       |
| `systemctl stop <unit>`      | Stops a unit                                        |
| `systemctl restart <unit>`   | Restarts a unit                                     |

## System V Init

- A base set of processes of the machine is called its runlevel (0-6).
- To check runlevel: `who -r`.
- Runlevels distinguish states between system startup, shutdown, single-user mode, and console mode.
- Runlevels are becoming a thing of the past.

| Command  | Description                 |
| -------- | --------------------------- |
| `who -r` | Checks the current runlevel |

## Shutdown

- Init also controls how the system shuts down and reboots.
- A proper way to shut down a Linux machine is to use the `shutdown` command.
- `shutdown -h now`: Immediately shuts down the system.
- `shutdown -r +10`: Reboots the system in 10 minutes.
- Tells the init to begin the shutdown process.
- On systemd, this means activating the shutdown units.
- On System V, this means setting the runlevel to 0.

| Command           | Description                       |
| ----------------- | --------------------------------- |
| `shutdown -h now` | Immediately shuts down the system |
| `shutdown -r +10` | Reboots the system in 10 minutes  |

## Grep

- Prints the lines that match an expression.
- Understands regular expressions.

| Symbol | Description                                                 |
| ------ | ----------------------------------------------------------- |
| `^`    | Matches the beginning of the line                           |
| `$`    | Matches the end of the line                                 |
| `*`    | Matches zero or more occurrences of the previous character  |
| `+`    | Matches one or more occurrence(s) of the previous character |
| `.`    | Matches exactly one character                               |

### Examples

1. To find lines that start with "text" in a file:

   ```sh
   grep '^text' filename
   ```

2. To find lines that end with "text" in a file:

   ```sh
   grep 'text$' filename
   ```

3. To find lines that contain zero or more occurrences of "a" followed by "bc":

   ```sh
   grep 'a*bc' filename
   ```

4. To find lines that contain one or more occurrences of "a" followed by "bc":

   ```sh
   grep 'a+bc' filename
   ```

5. To find lines that contain "a" followed by any character and then "c":
   ```sh
   grep 'a.c' filename
   ```

## Process Management

- Every process is a running program.
- Each process on the system has a numeric process ID (PID).

- Background process: When running a command from the shell, you don't get the shell prompt back until it finishes executing.
- With `&` you can detach the process and put it in the background.

| Command      | Description                                           |
| ------------ | ----------------------------------------------------- |
| `kill <PID>` | Terminates a process                                  |
| `ctrl + c`   | Terminates the current process                        |
| `top`        | Lists processes, most active ones at the top          |
| `M`          | Sorts by memory usage (within `top` command)          |
| `T`          | Sorts by total CPU usage (within `top` command)       |
| `u`          | Displays only user's processes (within `top` command) |
| `q`          | Quit the `top` command                                |

### Examples

1. To run a command in the background:

   ```sh
   command &
   ```

2. To terminate a process with a specific PID:

   ```sh
   kill <PID>
   ```

## Devices

- All Linux devices are located at `/dev`, which is an integral part of the root (`/`).
- Must be available during the boot process.
- Device files aren't device drivers (sometimes called nodes).

| Command      | Description                                |
| ------------ | ------------------------------------------ |
| `ls -l /dev` | Identify a device and view its permissions |

### Device Types

| Symbol | Description                                                                                                                     |
| ------ | ------------------------------------------------------------------------------------------------------------------------------- |
| `b`    | **Block device**: Programs access data in fixed chunks (e.g., hard drives, file systems)                                        |
| `c`    | **Character device**: Work with data streams, only read and write operations (e.g., `/dev/null`)                                |
| `p`    | **Pipe**: Allow two or more processes to communicate with each other, sending data to another process                           |
| `s`    | **Socket**: Facilitate communication between processes, similar to pipe devices but can communicate with many processes at once |

### Examples

1. To identify a device and view its permissions:

   ```sh
   ls -l /dev
   ```

2. Example of a character device operation:
   ```sh
   echo "Hello" > /dev/null
   ```

## Partition Table

- Most newer systems use Globally Unique Identifier Partition Table (GPT).
- Some Linux partitioning tools:

| Tool      | Description                                      |
| --------- | ------------------------------------------------ |
| `parted`  | A text-based tool that supports both MBR and GPT |
| `gparted` | A graphical version of parted                    |
| `fdisk`   | Traditional text-based Linux partitioning tool   |

### Examples

1. To view the system partition table using `parted`:

   ```sh
   parted -l
   ```

2. To start `parted` and interactively manage partitions:

   ```sh
   sudo parted /dev/sda
   ```

3. To start `gparted` (requires a graphical environment):

   ```sh
   sudo gparted
   ```

4. To manage partitions using `fdisk`:
   ```sh
   sudo fdisk /dev/sda
   ```

## Mounting a Filesystem

- The process of attaching a filesystem to a running system is called mounting.
- When the system boots, the kernel reads some configuration data and mounts the root (`/`) based on the data.

### Requirements to Mount a Filesystem

- Filesystem's device, location, or identifier.
- Filesystem type.
- The mount-point, a place where the filesystem will be attached.

| Command                           | Description                                                       |
| --------------------------------- | ----------------------------------------------------------------- |
| `mount`                           | Show current filesystem status                                    |
| `mount -t type device mountpoint` | Manually mount a filesystem                                       |
| `umount mountpoint`               | Unmount a filesystem                                              |
| `blkid`                           | View a list of devices and the corresponding filesystem and UUIDs |
| `df`                              | View utilization of mounted filesystems                           |
| `du`                              | Estimate disk usage of files and directories                      |

### Examples

1. To show the current filesystem status:

   ```sh
   mount
   ```

2. To manually mount a filesystem:

   ```sh
   sudo mount -t ext4 /dev/sda1 /mnt
   ```

3. To unmount a filesystem:

   ```sh
   sudo umount /mnt
   ```

4. To view a list of devices and their corresponding filesystem and UUIDs:

   ```sh
   blkid
   ```

5. To view the utilization of mounted filesystems:

   ```sh
   df -h
   ```

6. To estimate disk usage of files and directories:
   ```sh
   du -sh /path/to/directory
   ```

### Mounting at Boot Time

- To mount a filesystem at boot time, Linux systems keep a permanent list of filesystems and options in `/etc/fstab`.

## Files

- Every file has permissions: read, write, and execute.
- `ls -l`: Display permissions.
- Permissions can be divided into four sections:  
  `-rw-r--r--`: type (first `-`, a regular file here), user permissions (`rw-`), group permissions (`r--`), other permissions (`r--`).

| Symbol | Description                               |
| ------ | ----------------------------------------- |
| `r`    | Read (4)                                  |
| `w`    | Write (2)                                 |
| `x`    | Execute (1)                               |
| `-`    | None (0)                                  |
| `s`    | Setuid/setgid (admin privileges required) |

- `chmod`: Modify permissions.
- `rw-r--r--` = `110100100` = `644`.

### Examples

1. To display file permissions:

   ```sh
   ls -l
   ```

2. To modify file permissions:
   ```sh
   chmod 644 filename
   ```

## Links

- Symbolic link: A file that points to another file or directory.
- To create a symbolic link: `ln -s target linkname`.

| Command                 | Description            |
| ----------------------- | ---------------------- |
| `ln -s target linkname` | Create a symbolic link |

### Examples

1. To create a symbolic link:
   ```sh
   ln -s /path/to/target /path/to/linkname
   ```

## Compression

- `gzip`: Unix compression program, `.gz` is GNU Zip archive.
- `gunzip`: To uncompress `.gz` file.

| Command          | Description             |
| ---------------- | ----------------------- |
| `gzip file`      | Compress a file         |
| `gunzip file.gz` | Uncompress a `.gz` file |

### Examples

1. To compress a file:

   ```sh
   gzip filename
   ```

2. To uncompress a file:
   ```sh
   gunzip filename.gz
   ```

## Archiving

- `tar`: Create an archive.
- `tar -cvf archive.tar file1 file2 ...`: Create a tar archive.
- Usually `.tar` suffix.
- To unpack: `tar -xvf archive.tar`.

| Command                      | Description          |
| ---------------------------- | -------------------- |
| `tar -cvf archive.tar files` | Create a tar archive |
| `tar -xvf archive.tar`       | Unpack a tar archive |

### Examples

1. To create a tar archive:

   ```sh
   tar -cvf archive.tar file1 file2
   ```

2. To unpack a tar archive:
   ```sh
   tar -xvf archive.tar
   ```
