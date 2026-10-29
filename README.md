# Arch Linux + Hyprland Setup

My personal Arch Linux desktop configuration, package lists, and restoration instructions.

## What's included

- **Window manager:** Hyprland (Lua configuration)
- **Bar:** Waybar
- **Terminal:** foot with Iosevka
- **Shell:** Fish
- **Application launcher:** Rofi
- **Wallpaper:** swaybg
- **File manager:** Dolphin
- **Appearance:** GTK, Qt, icon, font, and cursor settings
- **Packages:** official Arch repository packages and foreign/AUR packages

## Repository structure

```text
arch-setup/
├── README.md
├── config/
│   ├── hypr/
│   ├── waybar/
│   ├── foot/
│   ├── fish/
│   └── rofi/
├── packages/
│   ├── official.txt
│   └── aur.txt
└── system/
    ├── enabled-services.txt
    ├── hyprland-info.txt
    └── installed-versions.txt
```

Some folders or files may be absent if they are not used on a particular installation.

## Restore on a fresh Arch Linux installation

### 1. Install prerequisites

Install Git and update the system:

```bash
sudo pacman -Syu git
```

Clone this repository:

```bash
git clone https://github.com/YOUR_USERNAME/arch-setup.git
cd arch-setup
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Install official packages

Review `packages/official.txt` first. This list reflects explicitly installed packages on the original computer, and may contain hardware-specific or unnecessary packages.

```bash
sudo pacman -S --needed - < packages/official.txt
```

If a package is no longer available, skip it and investigate separately.

### 3. Install AUR packages

Install an AUR helper such as `paru` or `yay` if you need packages from the AUR.

Review `packages/aur.txt`, then install the packages with your helper. For example, with `yay`:

```bash
xargs -r yay -S --needed < packages/aur.txt
```

Check that each package is still available and compatible before installing.

### 4. Restore configuration files

Back up any existing configurations before restoring:

```bash
mkdir -p ~/.config-backup
cp -a ~/.config/. ~/.config-backup/
```

Copy the repository configurations into your home directory:

```bash
cp -an config/. ~/.config/
```

The `-n` option avoids overwriting existing files. Review any conflicts manually and copy updated files into place as needed.

### 5. Review system-specific settings

The old PC's settings may not work unchanged on different hardware.

- Check display resolution and monitor configuration.
- Install the correct graphics drivers.
- Configure audio, networking, Bluetooth, and power management.
- Review enabled system services before enabling them.
- Check scripts, executable permissions, file paths, and environment variables.
- Verify cursor themes, fonts, GTK themes, and Qt settings.

Do not blindly copy the old machine's entire `/etc` directory or enable all its services.

### 6. Restart and test

Log out and back into Hyprland after restoring the relevant configurations.

Verify that:

- Hyprland starts correctly.
- Keybindings and the application launcher work.
- Waybar and wallpaper start.
- foot uses Iosevka.
- Fish loads the expected configuration.
- Your file manager and appearance settings work.

## Updating this repository

After changing configurations on your main computer:

```bash
cd ~/arch-setup
git status
git add config packages system README.md
git commit -m "Update desktop configuration"
git push
```

To refresh the package lists:

```bash
pacman -Qqen > packages/official.txt
pacman -Qqem > packages/aur.txt
```

Review changes before committing.

## Privacy and security

Never commit passwords, access tokens, private SSH keys, browser profiles, authentication cookies, or other secrets. Review configuration files and shell history before publishing.

This repository is intended to reproduce the desktop environment, not clone an entire machine. Hardware, bootloader, disk layout, drivers, and some system services must be configured separately.
