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
