**Linux** is a family of open-source **Unix-like** [[OS]] based on the Linux Kernel. It's widely used in [[server]], embedded systems, and increasingly on desktops.

Linux itself is just the **kernel** — the core that interfaces directly with [[hardware]]. A **Linux distribution** adds userland tools, libraries, package managers, and optionally a GUI.

# Kernel vs Distribution
- **Linux Kernel:**
    - The core part of the [[OS]].
    - Manages [[CPU]], memory, I/O devices, file systems, and process scheduling.
    - Written mainly in C.
- **Linux Distribution (Distro):**
    - A complete OS built around the Linux kernel.
    - Includes package managers, userland utilities, desktop environments (optionally).
    - Examples: Ubuntu, Fedora, Debian, Arch, Nix
# GUI vs CLI

- **Linux does not require a GUI** — many servers run **headless** (CLI-only).
- GUI support is **modular**:
    - **X11** or **Wayland** for windowing systems.
    - **Desktop environments:** GNOME, KDE Plasma, XFCE, etc.
    - You can boot into CLI or start a GUI session with commands like `startx`.
# Filesystem Structure

All Linux paths stem from the root `/`:

| Path     | Purpose                                                                  |
| -------- | ------------------------------------------------------------------------ |
| `/`      | Root of the file system. Everything begins here.                         |
| `/home/` | Home directories of users. `~` is shorthand for the current user's home. |
| `/etc/`  | Configuration files (system-wide). Example: `/etc/passwd`, `/etc/ssh/`.  |
| `/bin/`  | Essential user binaries (e.g., `ls`, `cp`, `bash`).                      |
| `/usr/`  | User-installed software and libraries.                                   |
| `/var/`  | Variable data (e.g., logs, mail, spool files).                           |
| `/tmp/`  | Temporary files. Cleared on reboot.                                      |
| `/dev/`  | Device files (e.g., `/dev/sda`, `/dev/null`).                            |
| `/proc/` | Virtual filesystem exposing kernel internals (e.g., `/proc/cpuinfo`).    |
| `/lib/`  | Shared libraries used by binaries in `/bin` and `/sbin`.                 |

# Essential Linux Commands

| Command                       | Description                                    |
| ----------------------------- | ---------------------------------------------- |
| `ls`                          | List files                                     |
| `cd`                          | Change directory                               |
| `pwd`                         | Print current directory                        |
| `cp`, `mv`, `rm`              | Copy, move, remove files                       |
| `touch`, `mkdir`              | Create files/directories                       |
| `cat`, `less`, `head`, `tail` | Read files                                     |
| `sudo`                        | Run command as superuser                       |
| `apt`, `dnf`, `pacman`        | Install packages (depending on distro)         |
| `top`, `htop`                 | Monitor system resources                       |
| `ps`, `kill`                  | View or terminate processes                    |
| `chmod`, `chown`              | Change permissions/ownership                   |
| `ssh`                         | Connect to a remote machine                    |
| `grep`, `find`                | Search for text/files                          |
| `tar`, `zip`, `unzip`         | Archive and compress files                     |
| `systemctl`                   | Manage services (start, stop, enable, disable) |
| `journalctl`                  | View system logs                               |
# Common Linux Distributions

| Distro     | Focus                                             | Package Manager |
| ---------- | ------------------------------------------------- | --------------- |
| **Ubuntu** | Beginner-friendly, widely supported               | `apt`           |
| **Debian** | Stable base for other distros                     | `apt`           |
| **Arch**   | Rolling release, minimal base                     | `pacman`        |
| **Fedora** | Cutting-edge software, Red Hat-backed             | `dnf`           |
| **CentOS** | Enterprise-like (replaced by CentOS Stream)       | `yum` / `dnf`   |
| **Alpine** | Lightweight, used mostly in [[Docker]] containers | `apk`           |
# Permissions model
Linux uses a `rwx` (read, write, execute) model applied to three categories: **user**, **group**, and **others**.  
Each permission has a numeric value:

|Permission|Symbol|Value|
|---|---|---|
|Read|`r`|4|
|Write|`w`|2|
|Execute|`x`|1|

Permissions are combined per category. For example:
- `rwxr-xr--` → `754`:
    - User: `rwx` = 4+2+1 = 7
    - Group: `r-x` = 4+0+1 = 5
    - Others: `r--` = 4+0+0 = 4
Common examples:

- `chmod 755 file`: Full permissions for user, read/execute for group/others.
- `chmod 644 file`: Read/write for user, read-only for group/others (common for config files).
- `chmod +x script.sh`: Adds execute permission (useful for scripts).

You can view permissions with `ls -l` and change ownership with `chown`.
# Extra

- **Everything is a file** in Linux — even hardware devices and processes.
- You can write powerful shell scripts using `bash`, `zsh`, or `fish`.
- Linux is highly customizable and modular — ideal for learning and control.