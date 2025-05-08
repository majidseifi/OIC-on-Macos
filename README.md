# Oracle Instant Client on macOS

A step-by-step video tutorial showing how to install and configure the Oracle Instant Client (Basic, SQL\*Plus, and SDK) on macOS (ARM64 & Intel).

🎥 Watch the full tutorial on YouTube: [Oracle Client Setup on macOS](https://youtu.be/U_mFVr5vPas)

---

## Table of Contents

- [Prerequisites](#prerequisites)  
- [Installation Steps](#installation-steps)  
  - [1. Determine Architecture](#1-determine-architecture)  
  - [2. Download Instant Client Packages](#2-download-instant-client-packages)  
  - [3. Mount & Install DMGs](#3-mount--install-dmgs)  
  - [4. Eject Volumes](#4-eject-volumes)  
  - [5. Move to Permanent Location](#5-move-to-permanent-location)  
  - [6. Configure Environment Variables](#6-configure-environment-variables)  
  - [7. Reload Your Shell](#7-reload-your-shell)  
  - [8. Verify Installation](#8-verify-installation)  
- [Commands Used](#commands-used)  

---

## Prerequisites

- A macOS machine (Apple Silicon or Intel)  
- Oracle Instant Client DMG files downloaded from Oracle’s website  
- Basic familiarity with the Terminal and editing your `~/.zshrc`

---

## Installation Steps

### 1. Determine Architecture
```bash
uname -m
# arm64 → Apple Silicon
# x86_64 → Intel
```

### 2. Download Instant Client Packages
From Oracle’s Instant Client download page, get the DMG files for:

* Basic (or Basic Light)
* SQL*Plus
* SDK

Each package corresponds to your architecture (ARM64 or x86_64).

### 3. Mount & Install DMGs
Repeat for each DMG you downloaded:

```bash
hdiutil mount ~/Downloads/instantclient-*.dmg
cd /Volumes/instantclient-*/
sh ./install_ic.sh
```

### 4. Eject Volumes
```bash
hdiutil unmount /Volumes/instantclient-*/
```

### 5. Move to Permanent Location
```bash
mkdir -p ~/oracle
mv ~/Downloads/instantclient_23_3/ ~/oracle/
```

### 6. Configure Environment Variables
Edit your Z shell profile:

```bash
code ~/.zshrc
```

Add these lines (adjust values as needed):

```bash
# Instant Client version
export ORACLE_HOME=/Users/[userName]/oracle/instantclient_23_3
export DYLD_LIBRARY_PATH=$ORACLE_HOME:$DYLD_LIBRARY_PATH
export PATH=$ORACLE_HOME:$PATH

# Optional: for OCCI/C++ development
export OCI_LIB_DIR="$ORACLE_HOME"
export OCI_INC_DIR="$ORACLE_HOME/sdk/include"
```

### 7. Reload Your Shell
```bash
source ~/.zshrc
```

### 8. Verify Installation
Run SQL*Plus:

```bash
sqlplus $ORA_USER/$ORA_PASS@//host:server/service
```

### Commands Used
```bash
uname -m
hdiutil mount ~/Downloads/instantclient-basic-macos.arm64-23.3.0.23.09.dmg
cd /Volumes/instantclient-basic-macos.arm64-23.3.0.23.09/
sh ./install_ic.sh
cd ~/Downloads/
hdiutil unmount /Volumes/instantclient-basic-macos.arm64-23.3.0.23.09/
hdiutil mount ~/Downloads/instantclient-sqlplus-macos.arm64-23.3.0.23.09.dmg
cd /Volumes/instantclient-sqlplus-macos.arm64-23.3.0.23.09/
sh ./install_ic.sh
cd ~/Downloads/
hdiutil unmount /Volumes/instantclient-sqlplus-macos.arm64-23.3.0.23.09/
hdiutil mount ~/Downloads/instantclient-sdk-macos.arm64-23.3.0.23.09.dmg
cd /Volumes/instantclient-sdk-macos.arm64-23.3.0.23.09/
sh ./install_ic.sh
cd ~
hdiutil unmount /Volumes/instantclient-sdk-macos.arm64-23.3.0.23.09/
mkdir -p ~/oracle
mv ~/Downloads/instantclient_23_3/ ~/oracle/
code ~/.zshrc
source ~/.zshrc
sqlplus $ORA_USER/$ORA_PASS@//host:server/service
```
