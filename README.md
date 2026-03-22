# Gas Station Monitoring System

**Version 1.0.0** — Built with Java Swing  
**Publisher:** CTRL+ALT+WIN  
**Support:** https://callixasta-ui.github.io/GasSystemSupport/

---

## Overview

Gas Station Monitoring System is a desktop application for managing fuel station operations. It handles fuel inventory, sales recording, credit management, staff account management, and activity logging — all from a local, file-based system that requires no internet connection or database server.

---

## Features

| Area | What it does |
|---|---|
| **Dashboard** | Live overview of fuel stock levels, income, and daily totals with bar/pie charts |
| **Manage** | Record stock received, fuel sales, credits, own use, payments, set prices, add/remove fuel types |
| **Reports** | Monthly summaries with charts, tabular reports for each data type |
| **Records** | Full audit trail — edit, delete, or undo any entry with cascade handling |
| **Deleted / Undone** | Archive browser — restore deleted entries or redo/permanently remove undone entries |
| **Logs** | Read-only activity log, newest first, searchable |
| **Accounts** | Credential management — change username, password, 8-digit key, userstamp |

### User Levels

| Role | Access |
|---|---|
| **Developer** | Full access + DevDashboard (account management, backup/restore) |
| **Admin** | Full access to all pages including account creation |
| **User** | All transaction pages + own records only (cannot touch others' entries) |

---

## Default Developer Account

The installer pre-seeds one developer account so the system is usable immediately after installation:

| Field | Value |
|---|---|
| Username | `dev` |
| Password | `Dev@1234` |
| 8-Digit Key | `12345678` |
| Role | `developer` |
| Userstamp | `Developer` |

> **Important:** Change the default password and 8-digit key immediately after first login.  
> Go to **DevDashboard → Edit** to update credentials.

---

## System Requirements

- **Operating System:** Windows 10 or later (64-bit recommended)
- **Java:** JDK or JRE version 17 or later
  - [Download from Adoptium (free)](https://adoptium.net/)
  - [Download from Oracle](https://www.oracle.com/java/technologies/downloads/)
- **Storage:** ~50 MB for the application + data growth over time
- **RAM:** 256 MB minimum, 512 MB recommended

The application does **not** bundle its own Java runtime. It finds whichever JDK or JRE is already installed on your machine.

---

## Installation

1. Run `GasStationSystem_Setup_1.0.0.exe`
2. Follow the installer steps
3. The installer will warn you if Java is not detected
4. After installation, launch from the desktop shortcut or Start Menu

---

## Running Without the Installer

If you have the jar file directly:

```
java -Dapp.home="." -Dfile.encoding=UTF-8 -jar GasStationSystem.jar
```

Or double-click `launch.bat` — it automatically finds Java on your machine.

---

## File Structure

After installation, the application creates the following structure relative to the exe:

```
GasStationSystem.exe        ← main application
launch.bat                  ← fallback launcher
data\
  accounts.txt              ← user accounts (pre-seeded with dev account)
  fueltypes.txt             ← fuel type registry
  stocks.txt                ← stock received entries
  sales.txt                 ← fuel sales entries
  credits.txt               ← credit records
  payments.txt              ← credit payment records
  ownuse.txt                ← internal fuel use records
  prices.txt                ← price history
  deleted.txt               ← archived deleted entries
  undone.txt                ← archived undone entries
  logs.txt                  ← activity log
backups\
  <username>\               ← per-user timestamped backups
```

All data is stored as pipe-delimited plain text files (`|` separator). No database engine is required.

---

## Building from Source

### Prerequisites
- JDK 17 or later
- Launch4j (for exe wrapping): https://launch4j.sourceforge.net/
- Inno Setup (for installer): https://jrsoftware.org/isinfo.php

### Steps

```
1. Place all .java source files in the src\ directory
2. Run:  src\build.bat
         → produces src\GasStationSystem.jar
3. Open launch4j-config.xml in Launch4j and build
         → produces src\GasStationSystem.exe
4. Open GasStation.iss in Inno Setup Compiler and compile
         → produces installer\GasStationSystem_Setup_1.0.0.exe
```

---

## Developer Dashboard (DevDashboard)

The DevDashboard is only accessible with a `developer`-level account. It provides:

- **Create / Edit / Delete** accounts of any role
- **Download Backup (.devbak)** — exports an account row + all data entries attributed to that account (stocks, sales, credits, payments, own use, prices, deleted/undone entries, and logs)
- **Extract Backup (.devbak)** — imports an account and all its cascaded records; existing IDs are skipped to prevent duplicates

### Backup File Format (v2)

```
# DevDashboard Backup v2
# Exported: 2026-03-22 10:30:00
# Username:  john
# Userstamp: John Doe
[ACCOUNT]
john|password|12345678|user|John Doe|2026-01-01T09:00|admin
[STOCKS]
<id>|<fuelId>|<liters>|...
[SALES]
...
```

---

## Support

- GitHub: https://callixasta-ui.github.io/GasSystemSupport/
- Issues: https://callixasta-ui.github.io/GasSystemRelease/issues

---

## License

See `LICENSE.md` for full terms.

© 2026 CTRL+ALT+WIN. All rights reserved.
