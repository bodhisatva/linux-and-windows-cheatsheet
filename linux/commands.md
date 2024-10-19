# Linux commands

| Command | Description                                                        |
| ------- | ------------------------------------------------------------------ |
| `ls`    | Lists directory contents                                           |
| `cd`    | Changes the current directory                                      |
| `pwd`   | Prints the current working directory                               |
| `cp`    | Copies files or directories                                        |
| `mv`    | Moves or renames files or directories                              |
| `rm`    | Removes files or directories                                       |
| `mkdir` | Creates a new directory                                            |
| `rmdir` | Removes an empty directory                                         |
| `touch` | Creates an empty file or updates the timestamp of an existing file |
| `chmod` | Changes file permissions                                           |
| `chown` | Changes file owner and group                                       |
| `cat`   | Concatenates and displays file content                             |
| `echo`  | Displays a line of text                                            |
| `grep`  | Searches for patterns in files                                     |
| `find`  | Searches for files in a directory hierarchy                        |
| `tar`   | Archives files                                                     |
| `zip`   | Compresses files                                                   |
| `unzip` | Decompresses files                                                 |
| `df`    | Displays disk space usage                                          |
| `du`    | Displays directory space usage                                     |
| `ps`    | Displays currently running processes                               |
| `kill`  | Terminates processes                                               |
| `top`   | Displays real-time system information                              |
| `man`   | Displays the manual for a command                                  |

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
