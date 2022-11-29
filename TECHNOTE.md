# TECHNOLOGY NOTES

| Information | |
-------|----------------
Author | Riyan Widiyanto
Description | Catatan Teknologi Informasi
Date | 2017-11-11 03:06 +7
Location | Jakarta / Semarang
Modified | 2021-12-30 13:06:23
Version | 2022

# ELECTRONIC CIRCUIT/DIAGRAM
## HEADSET
### Jack 3.5mm Combo (IPhone/Android)
```
----+---+---+---\
 4  | 3 | 2 | 1  |
----+---+---+---/

1. Left Earphone
2. Right Earphone
3. Mic (Nokia: GND)
4. GND (Nokia: Mic)
```
> Short pin `Mic` (3) & `GND` (4) to receive call.

### Jack 3.5mm Mono
```
------------+---\
      2     | 1  |
------------+---/

1. Left & Right Earphone
2. GND
```

### Jack 3.5mm Stereo
```
--------+---+---\
    3   | 2 | 1  |
--------+---+---/

1. Left Earphone
2. Right Earphone
3. GND
```

## USB
### USB 2.0 A Standard
```
+---------+
| 1 2 3 4 |
+---------+
USB Female:
1: VCC
2: Data (-)
3: Data (+)
4: GND

+---------+
| 4 3 2 1 |
+---------+
USB Male:
1: VCC
2: Data (-)
3: Data (+)
4: GND
```

### USB 2.0 B Standard
```
+-----+
| 2 1 |
|     |
| 3 4 |
+-----+
USB Female:
1: VCC
2: Data (-)
3: Data (+)
4: GND

+-----+
| 1 2 |
|     |
| 4 3 |
+-----+
USB Male:
1: VCC
2: Data (-)
3: Data (+)
4: GND
```

### USB 2.0 A/B Micro
```
+/---------\+
| 5 4 3 2 1 |
+-----------+
USB Female:
1: VCC
2: Data (-)
3: Data (+)
4: ID (On-The-Go)
5: GND

+/---------\+
| 1 2 3 4 5 |
+-----------+
USB Male:
1: VCC
2: Data (-)
3: Data (+)
4: ID (On-The-Go)
5: GND
```
> USB OTG device usually short pin `ID OTG` (4) & `GND` (5) to make device as **USB Host**.

# OpenSSL
## Self-Signed Certificate for Server
### Windows
```
C:\> set OPENSSL_CONF=C:\YourPath\openssl.cnf
```

### Linux
```
$ OPENSSL_CONF=/usr/local/ssl/openssl.cnf
```

### Edit `openssl.cnf` file
```
[ CA_Default ]
copy_extensions = copy
...

[ v3_ca ]
subjectAltName = @Alternate_Names
...

[ Alternate_Names ]
DNS.1 = localhost
DNS.2 = app1.localhost
...
```

### Create Certificate Request and Private Key
```
$ openssl req -x509 -nodes -days 365 -keyout privkey.pem -out pubkey.cert
```

# PROGRAMMING LANGUAGE
## x86 Assembly
### General Purpose Registers
Name | 8-bit | 16-bit | 32-bit | 64-bit
-----|-------|--------|--------|-------
Accumulator Register | `AH` and `AL` | `AX` | `EAX` | `RAX`
Counter Register | `CH` and `CL` | `CX` | `ECX` | `RCX`
Data Register | `DH` and `DL` | `DX` | `EDX` | `RDX`
Base Register | `BH` and `BL` | `BX` | `EBX` | `RBX`
Stack Pointer || `SP` | `ESP` | `RSP`
Base Pointer Register || `BP` | `EBP` | `RBP`
Source Index Register || `SI` | `ESI` | `RSI`
Destination Index Register || `DI` | `EDI` | `RDI`

### Syntax
Description | AT&T | INTEL
------------|------|------
Copy immediate value to register EAX | `movl $0x10, %eax` | `mov eax, 10h`
Copy immediate value to register AX | `movw $0x10, %ax` | `mov ax, 10h`
Copy immediate value to register AH | `movb $0x10, %ah` | `mov ah, 10h`
Copy register ECX to register EAX | `movl %ecx, %eax` | `mov eax, ecx`
Copy register CX to register AX | `movw %cx, %ax` | `mov ax, cx`
Copy register CH to register AL | `movb %cl, %al` | `mov al, ch`

# LINUX
## Compare between two files.
> `diff File1.txt File2.txt`

## Create `systemd` Service.[^systemd]
- Create and edit file `myservice.service`.
> `vim /etc/systemd/system/myservice.service`
```
[Unit]
Description=My Service

[Service]
Type=simple
ExecStart=/usr/bin/php /home/myname/example.php

[Install]
WantedBy=multi-user.target
```
- For application which create sub-process then exit parent process.
```
[Unit]
Description=My Service

[Service]
Type=forking
ExecStart=/usr/bin/yourapp -p /var/run/myservice.pid
PIDFile=/var/run/myservice.pid

[Install]
WantedBy=multi-user.target
```
- Enable start at boot.
> `systemctl enable myservice`
- Start service.
> `systemctl start myservice`
- View status.
> `systemctl status myservice`

## Fix Brightness Persistent (Linux Mint 19.3 Tricia)
> `sudo xed /etc/default/grub`

- Add `acpi_backlight=none` after `splash`
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_backlight=none"
```
> `sudo update-grub && reboot`

## Fix Font Rendering for Calibri (Linux Mint 20 Ulyana)

> `mkdir ~/.config/fontconfig`

> `xed ~/.config/fontconfig/fonts.conf`
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>
</fontconfig>
```
> `reboot`

## List Processes
> `ps -ejH`

## Update Repository
Distro | Command
-------|--------
Debian/Ubuntu | `sudo apt update`
RHEL/CentOS | `sudo yum update`

## Update Package
Distro | Command
-------|--------
Debian/Ubuntu | `sudo apt upgrade`
RHEL/CentOS | `sudo yum upgrade`

## C / C++
### Minimal Hello World Program
```
#include <stdio.h>
#include <stdlib.h>

int main (int argc, char **argv)
{
  printf("Hello World\r\n");
  return 0;
}
```
# PostgreSQL
## Windows Install
> `set PATH=%PATH%;C:\pgsql\bin`

> `initdb -D C:\pgsql\data -E utf8 -U postgres --locale=en_US`

- Edit `C:\pgsql\data\pg_hba.conf`:
  - Change IPv4 **ADDRESS** to `0.0.0.0/0` and IPv6 **ADDRESS** to `::/0`.
  - Change all **METHOD** to `scram-sha-256`. Save.

> `pg_ctl -D C:\pgsql\data -l C:\pgsql\logs\logfile.log start`

> `psql -U postgres -w`

> `ALTER ROLE postgres WITH PASSWORD 'YourPassword';`

> `REVOKE ALL ON DATABASE postgres FROM public;`

> `CREATE ROLE YourRoleName WITH LOGIN PASSWORD 'YourPassword';`

> `CREATE DATABASE YourDatabase;`

> `REVOKE ALL ON DATABASE YourDatabase FROM public;`

> `GRANT ALL ON DATABASE YourDatabase TO YourRoleName;`

# WINDOWS
## Enable 'Open Command Prompt here' (Windows 10)
- Open **REGEDIT** as **Administrator**

- Browse to `HKEY_CLASSES_ROOT\Directory\Background\shell\cmd`
- Right click `cmd`, choose **Permission...** > **Advanced** > **Owner**: **Administrators**
- Set Permissions: **Administrators** > **Allow: Full Control**
- Rename `HideBasedOnVelocityId` to `ShowBasedOnVelocityId`

## General DLL Files
- advapi32.dll
- advpack.dll
- comctl32.dll
- comdlg32.dll
- crypt32.dll
- dbghelp.dll
- kernel32.dll
- msvcrt.dll
- shell32.dll
- user32.dll
- gdi32.dll
- gdiplus.dll
- netapi32.dll
- ole32.dll
- oleaut32.dll
- opengl32.dll
- setupapi.dll
- shfolder.dll
- shlwapi.dll
- winspool.drv
- ws2_32.dll
- wsock32.dll

## Show WIFI Name and Password
- Run command prompt as **Administrator** then type:

> `netsh wlan show profile`

- Type one of WIFI name, example name **Home Wifi**:

> `netsh wlan show profile "Home Wifi" key=clear`

- Find **Security Settings** > **Key Content** as WIFI Password.

[^systemd]: https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files
