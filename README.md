# HP Omen 17 Autoinstall Project

This repository contains configuration files for automated installation of Ubuntu Server 24.04.2 LTS on an HP Omen 17 ck1xxx laptop using cloud-init's autoinstall feature.

## Overview

Autoinstall provides a way to perform automated, unattended Ubuntu Server installations with custom configurations. This project specifically targets the HP Omen 17 laptop with optimized settings.

## Repository Contents

- **user-data**: Main configuration file for the autoinstall process
- **meta-data**: Contains instance identification information
- **vendor-data**: Required empty file for cloud-init

## Features

- **Hardware-Enabled Kernel (HWE)**: Better support for newer hardware
- **LVM Storage Layout**: Configured without swap and with reset partitioning
- **Network Configuration**: Set up for both wired and wireless connections
- **Custom Package Selection**: Includes essential software components
- **Post-installation Commands**: Configure system settings after installation

## Usage Instructions

### Server Setup

1. Host the three configuration files (user-data, meta-data, vendor-data) on an HTTP server.
2. Ensure the server serves the proper Content-Type headers for these files.

### Apache2 Configuration

To ensure proper MIME types for files without extensions:

```bash
sudo vim /etc/apache2/conf-available/yaml-mime.conf
```

Add the following content to the file:

```markdown
<IfModule mod_mime.c>
    # Apply MIME type to files with no extension
    <FilesMatch "^(user-data|meta-data|vendor-data)$">
        ForceType text/plain
    </FilesMatch>
</IfModule>
```

```markdown
# HP Omen 17 Autoinstall Project

This repository contains configuration files for automated installation of Ubuntu Server 24.04.2 LTS on an HP Omen 17 ck1xxx laptop using cloud-init's autoinstall feature.

## Overview

Autoinstall provides a way to perform automated, unattended Ubuntu Server installations with custom configurations. This project specifically targets the HP Omen 17 laptop with optimized settings.

## Repository Contents

- **user-data**: Main configuration file for the autoinstall process
- **meta-data**: Contains instance identification information
- **vendor-data**: Required empty file for cloud-init

## Features

- **Hardware-Enabled Kernel (HWE)**: Better support for newer hardware
- **LVM Storage Layout**: Configured without swap and with reset partitioning
- **Network Configuration**: Set up for both wired and wireless connections
- **Custom Package Selection**: Includes essential software components
- **Post-installation Commands**: Configure system settings after installation

## Usage Instructions

### Server Setup

1. Host the three configuration files (user-data, meta-data, vendor-data) on an HTTP server.
2. Ensure the server serves the proper Content-Type headers for these files.

### Apache2 Configuration

To ensure proper MIME types for files without extensions:

```bash
sudo vim /etc/apache2/conf-available/yaml-mime.conf
```

Add the following content:

```apache
<IfModule mod_mime.c>
    # Apply MIME type to files with no extension
    <FilesMatch "^(user-data|meta-data|vendor-data)$">
        ForceType text/plain
    </FilesMatch>
</IfModule>
```

Enable and apply the configuration:

```bash
sudo a2enconf yaml-mime.conf
sudo systemctl reload apache2
```

### Boot Command

At the Ubuntu Server installation boot menu, press F6, then ESC to edit the boot command. Replace the existing boot parameters with:

```
linux /casper/vmlinuz autoinstall ip=dhcp cloud-init-delay=15 ds="nocloud;s=http://cdaboot.abiwot-lab.com/cloud-init/hpomen17-c1k/server/"
```

Adjust the URL path to match your HTTP server location.

## Customization

The user-data file contains all installation parameters and can be modified to:

- Change username and password settings
- Modify partition layout
- Adjust package selections
- Edit network settings
- Customize post-installation commands

## Requirements

- Ubuntu Server 24.04.2 installation media
- HTTP server to host configuration files
- Network connection during installation

## License

This project is open source and available under the MIT License.
```
