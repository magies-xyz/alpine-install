# alpine-install

Automated setup scripts for Alpine Linux with DWM (Dynamic Window Manager) and essential development tools.

## Overview

This repository contains a modular installation script that sets up a minimal Alpine Linux system with:
- **DWM** - Suckless dynamic window manager
- **X11** - Xorg display server and utilities
- **Development tools** - Build essentials, git, and text editors
- **System services** - dbus and elogind for session management

Inspired by [tony-btw's tonarchy installer](https://github.com/tonybanters).

## Prerequisites

- Alpine Linux system
- Root access
- Internet connectivity

## Installation

1. Clone this repository:
```bash
git clone https://github.com/magies-xyz/alpine-install.git
cd alpine-install
```

2. Run the setup script:
```bash
sudo sh dwmsetup [USERNAME]
```

### Arguments

| Argument | Default | Description |
|----------|---------|-------------|
| `USERNAME` | `lima` | Username for the new user account |

### Examples

```bash
# Create user "lima" (default)
sh dwmsetup

# Create user "john"
sh dwmsetup john
```

## What the Script Does

### System Updates
- Updates package lists
- Upgrades existing packages

### Package Installation
Installs the following packages:
- **Display**: `xorg-server`, `xinit`, `xf86-video-intel`, `xf86-input-libinput`
- **Window Manager**: `dwm` (via git clone and compilation)
- **Terminal/Applications**: `st`, `rofi`, `vim`
- **System**: `doas`, `dbus`, `elogind`
- **Development**: `build-base`, `git`, `wget`, `curl`

### User Setup
- Creates user account (if not exists)
- Adds user to wheel, audio, video, and input groups
- Generates `.xinitrc` for X11 startup

### Service Configuration
- Enables dbus and elogind services
- Configures doas for privilege escalation

### DWM Compilation
- Clones from [tonybanters/dwm](https://github.com/tonybanters/dwm)
- Builds and installs from source

## Post-Installation

After the script completes, log in as your created user and start X11:

```bash
startx
```

## Keyboard Layout

Currently hardcoded to Brazilian Portuguese (`br`). To change:

Edit the `.xinitrc` file in your user's home directory:
```bash
vim ~/.xinitrc
```

Change `setxkbmap br` to your desired layout (e.g., `setxkbmap us`).

## Customization

### Change DWM Source
Edit the script to change the DWM repository:
```bash
DWM_REPO="https://github.com/your-fork/dwm"
```

### Modify Package List
Update the `INSTALL_PKGS` variable with additional packages as needed.

## Troubleshooting

### Build failures
If `make` fails during DWM compilation, ensure you have build tools installed:
```bash
apk add build-base
```

### Permission denied on startx
Ensure elogind is running:
```bash
rc-service elogind status
```

### Missing graphics drivers
The script installs Intel drivers by default. For other GPUs, install the appropriate driver:
- AMD: `xf86-video-amdgpu`
- NVIDIA: Requires additional setup (not included)

## Known Issues

- Keyboard layout is hardcoded to Brazilian Portuguese
- Intel graphics driver assumed; others require manual installation
- DWM source is fixed; no option to use custom forks

## Contributing

Feel free to fork and submit pull requests for improvements!

## License

This project is provided as-is. See individual component licenses.

## References

- [Alpine Linux](https://www.alpinelinux.org/)
- [DWM](https://dwm.suckless.org/)
- [Suckless Tools](https://suckless.org/)
- [tony-btw/tonarchy](https://github.com/tonybanters)
