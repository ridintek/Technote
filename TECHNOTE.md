# **TECHNOLOGY NOTES**

| Information |                             |
| ----------- | --------------------------- |
| Author      | Riyan Widiyanto             |
| Description | Catatan Teknologi Informasi |
| Date        | 2017-11-11 03:06 +7         |
| Location    | Jakarta / Semarang          |
| Modified    | 2024-01-28 09:47 +7         |
| Version     | 2024                        |

# ELECTRONIC & CIRCUIT/DIAGRAM
## ESP32
ESP has some variants:
- ESP32-WROOM-32E (built-in antenna, newer)
- ESP32-WROOM-32UE (external antenna, newer)
- ESP32-WROOM-32D (NRND)
- ESP32-WROOM-32U (NRND)
- ESP32-WROOM-32 (NRND)

`NRND = Not Recommended for New Design (Obsolete)`

### Enter Download Mode
Press BOOT (IO0) to LOW and then press Reset (EN) to LOW.

If you are using serial, connect Serial pin to ESP pin to automatic enter Download mode.
| ESP Pin | Serial Pin |
| ------- | ---------- |
| EN      | RTS        |
| IO0     | DTR        |

### Pin Layout
```
  +----------------------------------------------------+
  |                                                    |
  |             WIFI Antenna / Keepout Zone            |
  |                                                    |
  +----------------------------------------------------+
 1| GND                                            GND |38
 2| 3V3                                           IO23 |37
 3| EN                                            IO22 |36
 4| SENSOR_VP                                     TXD0 |35
 5| SENSOR_VN                                     RXD0 |34
 6| IO34                 +-----+                  IO21 |33
 7| IO35                 |  39 |                    NC |32
 8| IO32                 | GND |                  IO19 |31
 9| IO33                 +-----+                  IO18 |30
10| IO25                                           IO5 |29
11| IO26                                          IO17 |28
12| IO27                                          IO16 |27
13| IO14                                           IO4 |26
14| IO12                                           IO0 |25
  |                                                    |
  | GND|IO13| NC | NC | NC | NC | NC | NC | IO15 | IO2 |
  +----------------------------------------------------+
    15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 |
```

### PINOUT
| Name      | No. | Type | Function                                                                                       |
| --------- | --- | ---- | ---------------------------------------------------------------------------------------------- |
| GND       | 1   | P    | Ground                                                                                         |
| 3V3       | 2   | P    | Power supply                                                                                   |
| EN        | 3   | I    | High: On; enables the chip Low: Off; the chip shuts down. Note: Do not leave the pin floating. |
| SENSOR_VP | 4   | I    | GPIO36, ADC1_CH0, RTC_GPIO0                                                                    |
| SENSOR_VN | 5   | I    | GPIO39, ADC1_CH3, RTC_GPIO3                                                                    |
| IO34      | 6   | I    | GPIO34, ADC1_CH6, RTC_GPIO4                                                                    |
| IO35      | 7   | I    | GPIO35, ADC1_CH7, RTC_GPIO5                                                                    |
| IO32      | 8   | I/O  | GPIO32, XTAL_32K_P (32.768 kHz crystal oscillator input), ADC1_CH4, TOUCH9, RTC_GPIO9          |
| IO33      | 9   | I/O  | GPIO33, XTAL_32K_N (32.768 kHz crystal oscillator output), ADC1_CH5, TOUCH8, RTC_GPIO8         |
| IO25      | 10  | I/O  | GPIO25, DAC_1, ADC2_CH8, RTC_GPIO6, EMAC_RXD0                                                  |
| IO26      | 11  | I/O  | GPIO26, DAC_2, ADC2_CH9, RTC_GPIO7, EMAC_RXD1                                                  |
| IO27      | 12  | I/O  | GPIO27, ADC2_CH7, TOUCH7, RTC_GPIO17, EMAC_RX_DV                                               |
| IO14      | 13  | I/O  | GPIO14, ADC2_CH6, TOUCH6, RTC_GPIO16, MTMS, HSPICLK, HS2_CLK, SD_CLK, EMAC_TXD2                |
| IO12      | 14  | I/O  | GPIO12, ADC2_CH5, TOUCH5, RTC_GPIO15, MTDI, HSPIQ, HS2_DATA2, SD_DATA2  FEMAC_TXD3             |
| GND       | 15  | P    | Ground                                                                                         |
| IO13      | 16  | I/O  | GPIO13, ADC2_CH4, TOUCH4, RTC_GPIO14, MTCK, HSPID, HS2_DATA3, SD_DATA3, EMAC_RX_ER             |
| NC        | 17  | -    | SD2, GPIO19, Used by SPI Flash                                                                 |
| NC        | 18  | -    | SD3, GPIO10, Used by SPI Flash                                                                 |
| NC        | 19  | -    | CMD, GPIO11, Used by SPI Flash                                                                 |
| NC        | 20  | -    | CLK, GPIO6, Used by SPI Flash                                                                  |
| NC        | 21  | -    | SD0, GPIO7, Used by SPI Flash                                                                  |
| NC        | 22  | -    | SD1, GPIO8, Used by SPI Flash                                                                  |
| IO15      | 23  | I/O  | GPIO15, ADC2_CH3, TOUCH3, MTDO, HSPICS0, RTC_GPIO13, HS2_CMD, SD_CMD, MAC_RXD3                 |
| IO2       | 24  | I/O  | GPIO2, ADC2_CH2, TOUCH2, RTC_GPIO12, HSPIWP, HS2_DATA0, SD_DATA0                               |
| IO0       | 25  | I/O  | GPIO0, ADC2_CH1, TOUCH1, RTC_GPIO11, CLK_OUT1, EMAC_TX_CLK                                     |
| IO4       | 26  | I/O  | GPIO4, ADC2_CH0, TOUCH0, RTC_GPIO10, HSPIHD, HS2_DATA1, SD_DATA1, MAC_TX_ER                    |
| IO163     | 27  | I/O  | GPIO16, HS1_DATA4, U2RXD, EMAC_CLK_OUT                                                         |
| IO17      | 28  | I/O  | GPIO17, HS1_DATA5, U2TXD, EMAC_CLK_OUT_180                                                     |
| IO5       | 29  | I/O  | GPIO5, VSPICS0, HS1_DATA6, EMAC_RX_CLK                                                         |
| IO18      | 30  | I/O  | GPIO18, VSPICLK, HS1_DATA7                                                                     |
| IO19      | 31  | I/O  | GPIO19, VSPIQ, U0CTS, EMAC_TXD0                                                                |
| NC        | 32  | -    | -                                                                                              |
| IO21      | 33  | I/O  | GPIO21, VSPIHD, EMAC_TX_EN                                                                     |
| RXD0      | 34  | I/O  | GPIO3, U0RXD, CLK_OUT2                                                                         |
| TXD0      | 35  | I/O  | GPIO1, U0TXD, CLK_OUT3, EMAC_RXD2                                                              |
| IO22      | 36  | I/O  | GPIO22, VSPIWP, U0RTS, EMAC_TXD1                                                               |
| IO23      | 37  | I/O  | GPIO23, VSPID, HS1_STROBE                                                                      |
| GND       | 38  | P    | Ground                                                                                         |

`P = Power Supply, I = Input, O = Output`

### GPIO
| GPIO   | Analog Function | RTC GPIO   | Comments            |
| ------ | --------------- | ---------- | ------------------- |
| GPIO0  | ADC2_CH1        | RTC_GPIO11 | Strapping pin       |
| GPIO1  |                 |            | TXD                 |
| GPIO2  | ADC2_CH2        | RTC_GPIO12 | Strapping pin       |
| GPIO3  |                 |            | RXD                 |
| GPIO4  | ADC2_CH0        | RTC_GPIO10 |
| GPIO5  |                 |            | Strapping pin       |
| GPIO6  |                 |            | SPI0/1              |
| GPIO7  |                 |            | SPI0/1              |
| GPIO8  |                 |            | SPI0/1              |
| GPIO9  |                 |            | SPI0/1              |
| GPIO10 |                 |            | SPI0/1              |
| GPIO11 |                 |            | SPI0/1              |
| GPIO12 | ADC2_CH5        | RTC_GPIO15 | Strapping pin; JTAG |
| GPIO13 | ADC2_CH4        | RTC_GPIO14 | JTAG                |
| GPIO14 | ADC2_CH6        | RTC_GPIO16 | JTAG                |
| GPIO15 | ADC2_CH3        | RTC_GPIO13 | Strapping pin; JTAG |
| GPIO16 |                 |            | SPI0/1              |
| GPIO17 |                 |            | SPI0/1              |
| GPIO18 |                 |            |
| GPIO19 |                 |            |
| GPIO21 |                 |            |
| GPIO22 |                 |            |
| GPIO23 |                 |            |
| GPIO25 | ADC2_CH8        | RTC_GPIO6  |
| GPIO26 | ADC2_CH9        | RTC_GPIO7  |
| GPIO27 | ADC2_CH7        | RTC_GPIO17 |
| GPIO32 | ADC1_CH4        | RTC_GPIO9  |
| GPIO33 | ADC1_CH5        | RTC_GPIO8  |
| GPIO34 | ADC1_CH6        | RTC_GPIO4  | GPI                 |
| GPIO35 | ADC1_CH7        | RTC_GPIO5  | GPI                 |
| GPIO36 | ADC1_CH0        | RTC_GPIO0  | GPI                 |
| GPIO37 | ADC1_CH1        | RTC_GPIO1  | GPI                 |
| GPIO38 | ADC1_CH2        | RTC_GPIO2  | GPI                 |
| GPIO39 | ADC1_CH3        | RTC_GPIO3  | GPI                 |

- Strapping pin: GPIO0, GPIO2, GPIO5, GPIO12 (MTDI), and GPIO15 (MTDO) are strapping pins.
- SPI0/1: GPIO6-11 and GPIO16-17 are usually connected to the SPI flash and PSRAM integrated on the module and therefore should not be used for other purposes.
- GPI: GPIO34-39 can only be set as input mode and do not have software-enabled pullup or pulldown functions.
- ADC2 pins cannot be used when Wi-Fi is used. So, if you are having trouble getting the value from an ADC2 GPIO while using Wi-Fi, you may consider using an ADC1 GPIO instead, which should solve your problem.
- Please DO NOT USE the interrupt of GPIO36 and GPIO39 when using ADC or Wi-Fi and Bluetooth with sleep mode enabled.
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

> Short pin `Mic` (3) & `GND` (4) once to receive call.

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

```ini
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
## Assembly x86
### General Purpose Registers
| Name                       | 8-bit         | 16-bit | 32-bit | 64-bit |
| -------------------------- | ------------- | ------ | ------ | ------ |
| Accumulator Register       | `AH` and `AL` | `AX`   | `EAX`  | `RAX`  |
| Counter Register           | `CH` and `CL` | `CX`   | `ECX`  | `RCX`  |
| Data Register              | `DH` and `DL` | `DX`   | `EDX`  | `RDX`  |
| Base Register              | `BH` and `BL` | `BX`   | `EBX`  | `RBX`  |
| Stack Pointer              |               | `SP`   | `ESP`  | `RSP`  |
| Base Pointer Register      |               | `BP`   | `EBP`  | `RBP`  |
| Source Index Register      |               | `SI`   | `ESI`  | `RSI`  |
| Destination Index Register |               | `DI`   | `EDI`  | `RDI`  |

### Syntax
| Description                          | AT&T               | INTEL          |
| ------------------------------------ | ------------------ | -------------- |
| Copy immediate value to register EAX | `movl $0x10, %eax` | `mov eax, 10h` |
| Copy immediate value to register AX  | `movw $0x10, %ax`  | `mov ax, 10h`  |
| Copy immediate value to register AH  | `movb $0x10, %ah`  | `mov ah, 10h`  |
| Copy register ECX to register EAX    | `movl %ecx, %eax`  | `mov eax, ecx` |
| Copy register CX to register AX      | `movw %cx, %ax`    | `mov ax, cx`   |
| Copy register CH to register AL      | `movb %cl, %al`    | `mov al, ch`   |

### Example Code
- **DIV** (Unsigned Divide)

Using `DIV` mnemonic as divider
the register `EDX` must be zero before using `DIV` mnemonic, otherwise `INTEGER_OVERFLOW` error will occurred.
After `DIV` operation succeeded, `EDX` will return modulus.

> Syntax: DIV [reg]

Example:

```asm
mov eax, 10h ; =16
mov ecx, 2h  ; =2
xor edx, edx ; Must be zero before div
div ecx ; Result EAX = 8h; ECX = 2h; EDX = 0h
```

- **MUL** (Unsigned Multiply)

Using `MUL` mnemonic as multiplier
`MUL` mnemonic will multiply `EAX` register with destination register and store value in `EAX` register.

`Syntax: MUL [reg]`

Example:

```asm
mov ecx, 2h
mov eax, 4h
mul ecx ; Result EAX = 8h; ecx = 2h
```
## C / C++
### Minimal Hello World application.

```c
#include <stdio.h>

int main (int argc, char **argv)
{
  printf("Hello World\r\n");
  return 0;
}
```
## CSS (Cascading Style Sheets)
- Pseudo-class `hover`, `focus` and `active`[^csshfa]

Pseudo-class `active` MUST BE AT THE END of all Pseudo-classes.

It won't work:
```css
div:active {}
div:focus {}
div:hover {}
```

It works:
```css
div:hover {}
div:focus {}
div:active {}
```
## Javascript
### Hoisting
```js
console.log(avgFunc(2, 8)); // => 5
console.log(avgCons(2, 8)); // Uncaught ReferenceError

const avgConst = (a, b) => (a + b) / 2;

function avgFunc(a, b) {
  return (a + b) / 2;
}
```

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

```xml
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
| Distro        | Command           |
| ------------- | ----------------- |
| Debian/Ubuntu | `sudo apt update` |
| RHEL/CentOS   | `sudo yum update` |

## Update Package
| Distro        | Command            |
| ------------- | ------------------ |
| Debian/Ubuntu | `sudo apt upgrade` |
| RHEL/CentOS   | `sudo yum upgrade` |

# MacOSX
## Clean Install MacOSX
1. Shutdown Macbook by long press power button.
2. Turn on Macbook and press `Command` + `R` to enter Recovery Mode.
3. Insert USB Flashdrive to Macbook.
4. Use `Disk Utilities` to format USB.
5. `Utilities > Terminal`
6. Access from another PC https://support.apple.com/en-us/HT211683 to get link download.
7. Enter this command to download image:

```
# cd /tmp/
# curl -O http://updates-http.cdn-apple.com/2019/cert/061-41424-20191024-218af9ec-cf50-4516-9011-228c78eda3d2/InstallMacOSX.dmg
# pkgutil --expand /Volumes/Install\ OS\ X/InstallMacOSX.pkg /tmp/El\ Capitan
# diskutil eject Install\ OS\ X
# cd /tmp/El\ Capitan
# hdiutil attach InstallMacOSX.pkg/InstallESD.dmg  -noverify -nobrowse -mountpoint /Volumes/esd
# asr restore -source /Volumes/esd/BaseSystem.dmg -target /Volumes/MyVolume -noprompt -noverify -erase
# diskutil rename OS\ X\ Base\ System Install\ El\ Capitan
# rm /Volumes/Install\ El\ Capitan/System/Installation/Packages
# cp -rpv /Volumes/esd/Packages /Volumes/Install\ El\ Capitan/System/Installation
# cp -rp /Volumes/esd/BaseSystem.chunklist /Volumes/Install\ El\ Capitan/
# cp -rp /Volumes/esd/BaseSystem.dmg /Volumes/Install\ El\ Capitan/
# hdiutil detach /Volumes/esd
# bless --folder /Volumes/Install\ El\ Capitan/System/Library/CoreServices --label Install\ El\ Capitan
# cp /Volumes/Install\ El\ Capitan/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/InstallAssistant.icns /Volumes/Install\ El\ Capitan/.VolumeIcon.icns
# cd "$HOME"
# rm -r /tmp/El\ Capitan
# diskutil eject Install\ El\ Capitan
```
6. Done. Restart and press Alt to boot the USB Flashdrive.

# MySQL
## Database Replication
In database replication. Clients or second Masters must import from main Master first before start replication.
1. Dump all databases from main master to SQL.
```
mysqldump -h masterhost -u user -p"Password" dbname > dbname.sql
```
1. Import all dumped databases to client.
```
mysql -h clienthost -u user -p"Password" dbname < dbname.sql
```

### Master To Client (M2C)
- Server A (Master)
```bash
mysql> CREATE USER replica_a IDENTIFIED BY 'PassA';
mysql> GRANT REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO replica_a;
mysql> FLUSH PRIVILEGES;
```
- Server B (Client)
```bash
mysql> CHANGE REPLICATION SOURCE TO SOURCE_HOST='hostname.com', SOURCE_USER='replica_a', SOURCE_PASSWORD='PassA';
mysql> RESET REPLICA;
mysql> START REPLICA;
mysql> SHOW REPLICA STATUS\G
```
### Master To Master (M2M)
- Server A (Master)
```bash
mysql> CREATE USER replica_a IDENTIFIED BY 'PassA';
mysql> GRANT REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO replica_a;
mysql> FLUSH PRIVILEGES;
mysql> CHANGE REPLICATION SOURCE TO SOURCE_HOST='hostname_b.com', SOURCE_USER='replica_b', SOURCE_PASSWORD='PassB';
mysql> RESET REPLICA;
mysql> START REPLICA;
mysql> SHOW REPLICA STATUS\G
```
- Server B (Master)
```bash
mysql> CREATE USER replica_b IDENTIFIED BY 'PassB';
mysql> GRANT REPLICATION CLIENT, REPLICATION SLAVE ON *.* TO replica_b;
mysql> FLUSH PRIVILEGES;
mysql> CHANGE REPLICATION SOURCE TO SOURCE_HOST='hostname_a.com', SOURCE_USER='replica_a', SOURCE_PASSWORD='PassA';
mysql> RESET REPLICA;
mysql> START REPLICA;
mysql> SHOW REPLICA STATUS\G
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
## Office GVLK (Generic Volume License Key)[^officegvlk]
### **Office 2021**
| Product                            | GVLK                          |
| ---------------------------------- | ----------------------------- |
| Office LTSC Professional Plus 2021 | FXYTK-NJJ8C-GB6DW-3DYQT-6F7TH |
| Office LTSC Standard 2021          | KDX7X-BNVR8-TXXGX-4Q7Y8-78VT3 |
| Project Professional 2021          | FTNWT-C6WBT-8HMGF-K9PRX-QV9H8 |
| Project Standard 2021              | J2JDC-NJCYY-9RGQ4-YXWMH-T3D4T |
| Visio LTSC Professional 2021       | KNH8D-FGHT4-T8RK3-CTDYJ-K2HT4 |
| Visio LTSC Standard 2021           | MJVNY-BYWPY-CWV6J-2RKRT-4M8QG |
| Access LTSC 2021                   | WM8YG-YNGDD-4JHDC-PG3F4-FC4T4 |
| Excel LTSC 2021                    | NWG3X-87C9K-TC7YY-BC2G7-G6RVC |
| Outlook LTSC 2021                  | C9FM6-3N72F-HFJXB-TM3V9-T86R9 |
| PowerPoint LTSC 2021               | TY7XF-NFRBR-KJ44C-G83KF-GX27K |
| Publisher LTSC 2021                | 2MW9D-N4BXM-9VBPG-Q7W6M-KFBGQ |
| Skype for Business LTSC 2021       | HWCXN-K3WBT-WJBKY-R8BD9-XK29P |
| Word LTSC 2021                     | TN8H9-M34D3-Y64V9-TR72V-X79KV |

### **Office 2019**
| Product                       | GVLK                          |
| ----------------------------- | ----------------------------- |
| Office Professional Plus 2019 | NMMKJ-6RK4F-KMJVX-8D9MJ-6MWKP |
| Office Standard 2019          | 6NWWJ-YQWMR-QKGCB-6TMB3-9D9HK |
| Project Professional 2019     | B4NPR-3FKK7-T2MBV-FRQ4W-PKD2B |
| Project Standard 2019         | C4F7P-NCP8C-6CQPT-MQHV9-JXD2M |
| Visio Professional 2019       | 9BGNQ-K37YR-RQHF2-38RQ3-7VCBB |
| Visio Standard 2019           | 7TQNQ-K3YQQ-3PFH7-CCPPM-X4VQ2 |
| Access 2019                   | 9N9PT-27V4Y-VJ2PD-YXFMF-YTFQT |
| Excel 2019                    | TMJWT-YYNMB-3BKTF-644FC-RVXBD |
| Outlook 2019                  | 7HD7K-N4PVK-BHBCQ-YWQRW-XW4VK |
| PowerPoint 2019               | RRNCX-C64HY-W2MM7-MCH9G-TJHMQ |
| Publisher 2019                | G2KWX-3NW6P-PY93R-JXK2T-C9Y9V |
| Skype for Business 2019       | NCJ33-JHBBY-HTK98-MYCV8-HMKHJ |
| Word 2019                     | PBX3G-NWMT6-Q7XBW-PYJGG-WXD33 |

### **Office 2016**
| Product                       | GVLK                          |
| ----------------------------- | ----------------------------- |
| Office Professional Plus 2016 | XQNVK-8JYDB-WJ9W3-YJ8YR-WFG99 |
| Office Standard 2016          | JNRGM-WHDWX-FJJG3-K47QV-DRTFM |
| Project Professional 2016     | YG9NW-3K39V-2T3HJ-93F3Q-G83KT |
| Project Standard 2016         | GNFHQ-F6YQM-KQDGJ-327XX-KQBVC |
| Visio Professional 2016       | PD3PC-RHNGV-FXJ29-8JK7D-RJRJK |
| Visio Standard 2016           | 7WHWN-4T7MP-G96JF-G33KR-W8GF4 |
| Access 2016                   | GNH9Y-D2J4T-FJHGG-QRVH7-QPFDW |
| Excel 2016                    | 9C2PK-NWTVB-JMPW8-BFT28-7FTBF |
| OneNote 2016                  | DR92N-9HTF2-97XKM-XW2WJ-XW3J6 |
| Outlook 2016                  | R69KK-NTPKF-7M3Q4-QYBHW-6MT9B |
| PowerPoint 2016               | J7MQP-HNJ4Y-WJ7YM-PFYGF-BY6C6 |
| Publisher 2016                | F47MM-N3XJP-TQXJ9-BP99D-8K837 |
| Skype for Business 2016       | 869NQ-FJ69K-466HW-QYCP2-DDBV6 |
| Word 2016                     | WXY84-JN2Q9-RBCCQ-3Q3J3-3PFJ6 |

## Windows GVLK (Generic Volume License Key)
### **Windows 7**
| Product                  | GVLK                          |
| ------------------------ | ----------------------------- |
| Professional             | FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4 |
| Windows 7 Professional N | MRPKT-YTG23-K7D7T-X2JMM-QY7MG |
| Windows 7 Professional E | W82YF-2Q76Y-63HXB-FGJG9-GF7QX |
| Windows 7 Enterprise     | 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH |
| Windows 7 Enterprise N   | YDRBP-3D83W-TY26F-D46B2-XCKRJ |
| Windows 7 Enterprise E   | C29WB-22CC8-VJ326-GHFJW-H9DH4 |

### **Windows 8**
| Product                   | GVLK                          |
| ------------------------- | ----------------------------- |
| W8 Core                   | BN3D2-R7TKB-3YPBD-8DRP2-27GG4 |
| W8 Core Single Language   | 2WN2H-YGCQR-KFX6K-CD6TF-84YXQ |
| W8 Professional           | NG4HW-VH26C-733KW-K6F98-J8CK4 |
| W8 Professional N         | XCVCF-2NXM9-723PB-MHCB7-2RYQQ |
| W8 Professional WMC       | GNBB8-YVD74-QJHX6-27H4K-8QHDG |
| W8 Enterprise             | 32JNW-9KQ84-P47T8-D8GGY-CWCK7 |
| W8 Enterprise N           | JMNMF-RHW7P-DMY6X-RF3DR-X2BQT |
| W8.1 Core                 | M9Q9P-WNJJT-6PXPY-DWX8H-6XWKK |
| W8.1 Core N               | 7B9N3-D94CG-YTVHR-QBPX3-RJP64 |
| W8.1 Core Single Language | BB6NG-PQ82V-VRDPW-8XVD2-V8P66 |
| W8.1 Professional         | GCRJD-8NW9H-F2CDX-CCM8D-9D6T9 |
| W8.1 Professional N       | HMCNV-VVBFX-7HMBH-CTY9B-B4FXY |
| W8.1 Professional WMC     | 789NJ-TQK6T-6XTH8-J39CJ-J8D3P |
| W8.1 Enterprise           | MHF9N-XY6XB-WVXMC-BTDCT-MKKG7 |
| W8.1 Enterprise N         | TT4HM-HN7YT-62K67-RGRQJ-JFFXW |

### **Windows 10/11**
| Product               | GVLK                          |
| --------------------- | ----------------------------- |
| Home                  | TX9XD-98N7V-6WMQ6-BX7FG-H8Q99 |
| Home N                | 3KHY7-WNT83-DGQKR-F7HPR-844BM |
| Home Single Language  | 7HNRX-D7KGG-3K4RQ-4WPJ4-YTDFH |
| Home Country Specific | PVMJN-6DFY6-9CCP6-7BKTT-D3WVR |
| Professional          | W269N-WFGWX-YVC9B-4J6C9-T83GX |
| Professional N        | MH37W-N47XK-V7XM9-C7227-GCQG9 |
| Education             | NW6C2-QMPVW-D7KKK-3GKT6-VCFB2 |
| Education N           | 2WH4N-8QGBV-H22JP-CT43Q-MDWWJ |
| Enterprise            | NPPR9-FWDCX-D2C8J-H872K-2YT43 |
| Enterprise N          | DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4 |

### **Windows Server 2008**
| Product                                        | GVLK                          |
| ---------------------------------------------- | ----------------------------- |
| Windows Web Server 2008                        | WYR28-R7TFJ-3X2YQ-YCY4H-M249D |
| Windows Server 2008 Standard                   | TM24T-X9RMF-VWXK6-X8JC9-BFGM2 |
| Windows Server 2008 Standard without Hyper-V   | W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ |
| Windows Server 2008 Enterprise                 | YQGMW-MPWTJ-34KDK-48M3W-X4Q6V |
| Windows Server 2008 Enterprise without Hyper-V | 39BXF-X8Q23-P2WWT-38T2F-G3FPG |
| Windows Server 2008 HPC                        | RCTX3-KWVHP-BR6TB-RB6DM-6X7HP |
| Windows Server 2008 Datacenter                 | 7M67G-PC374-GR742-YH8V4-TCBY3 |
| Windows Server 2008 Datacenter without Hyper-V | 22XQ2-VRXRG-P8D42-K34TD-G3QQC |
| Windows Server 2008 for Itanium-Based Systems  | 4DWFP-JF3DJ-B7DTH-78FJB-PDRHK |

### **Windows Server 2008 R2**
| Product                                          | GVLK                          |
| ------------------------------------------------ | ----------------------------- |
| Windows Server 2008 R2 Web                       | 6TPJF-RBVHG-WBW2R-86QPH-6RTM4 |
| Windows Server 2008 R2 HPC edition               | TT8MH-CG224-D3D7Q-498W2-9QCTX |
| Windows Server 2008 R2 Standard                  | YC6KT-GKW9T-YTKYR-T4X34-R7VHC |
| Windows Server 2008 R2 Enterprise                | 489J6-VHDMP-X63PK-3K798-CPX3Y |
| Windows Server 2008 R2 Datacenter                | 74YFP-3QFB3-KQT8W-PMXWJ-7M648 |
| Windows Server 2008 R2 for Itanium-based Systems | GT63C-RJFQ3-4GMB6-BRFB9-CB83V |

### **Windows Server 2012**
| Product                                 | GVLK                          |
| --------------------------------------- | ----------------------------- |
| Windows Server 2012                     | BN3D2-R7TKB-3YPBD-8DRP2-27GG4 |
| Windows Server 2012 N                   | 8N2M2-HWPGY-7PGT9-HGDD8-GVGGY |
| Windows Server 2012 Single Language     | 2WN2H-YGCQR-KFX6K-CD6TF-84YXQ |
| Windows Server 2012 Country Specific    | 4K36P-JN4VD-GDC6V-KDT89-DYFKP |
| Windows Server 2012 Server Standard     | XC9B7-NBPP2-83J2H-RHMBY-92BT4 |
| Windows Server 2012 MultiPoint Standard | HM7DN-YVMH3-46JC3-XYTG7-CYQJJ |
| Windows Server 2012 MultiPoint Premium  | XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G |
| Windows Server 2012 Datacenter          | 48HP8-DN98B-MYWDG-T2DCC-8W83P |

### **Windows Server 2012 R2**
| Product                                | GVLK                          |
| -------------------------------------- | ----------------------------- |
| Windows Server 2012 R2 Server Standard | D2N9P-3P6X9-2R39C-7RTCD-MDVJX |
| Windows Server 2012 R2 Datacenter      | W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9 |
| Windows Server 2012 R2 Essentials      | KNC87-3J2TX-XB4WP-VCPJV-M4FWM |

### **Windows Server 2016**
| Product                        | GVLK                          |
| ------------------------------ | ----------------------------- |
| Windows Server 2016 Datacenter | CB7KF-BWN84-R7R2Y-793K2-8XDDG |
| Windows Server 2016 Standard   | WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY |
| Windows Server 2016 Essentials | JCKRF-N37P4-C2D82-9YXRT-4M63B |

## **COMMAND & UTILITIES**
### **WINDOWS ACTIVATION SCRIPT**

```bat
@echo off
cscript /nologo slmgr.vbs /ipk <ProductKey>
cscript /nologo slmgr.vbs /skms <Host:Port>
cscript /nologo slmgr.vbs /ato
```

### **CONVERT OFFICE RETAIL TO VL SCRIPT**

```bat
@echo off
setlocal EnableDelayedExpansion

if exist "!ProgramFiles(x86)!\Microsoft Office\Office16\ospp.vbs" (
  set "OSPP=!ProgramFiles(x86)!\Microsoft Office\Office16\ospp.vbs"
  set "LICENSE=!ProgramFiles(x86)!\Microsoft Office\root\Licenses16"
) else if exist "!ProgramFiles!\Microsoft Office\Office16\ospp.vbs" (
  set "OSPP=!ProgramFiles!\Microsoft Office\Office16\ospp.vbs"
  set "LICENSE=!ProgramFiles!\Microsoft Office\root\Licenses16"
)

rem Office 2016 Retail
for /f %%a in ('dir /b "!LICENSE!\ProPlusVL_kms*.xrm-ms"') do cscript "!OSPP!" /inslic:"!LICENSE!\%%a"

rem Office 2019 Retail
for /f %%a in ('dir /b "!LICENSE!\ProPlus2019VL*.xrm-ms"') do cscript "!OSPP!" /inslic:"!LICENSE!\%%a"
```

### **OFFICE ACTIVATION SCRIPT**

```bat
@echo off
setlocal EnableDelayedExpansion

if exist "!ProgramFiles(x86)!\Microsoft Office\Office16\ospp.vbs" (
  set "OSPP=!ProgramFiles(x86)!\Microsoft Office\Office16\ospp.vbs"
) else if exist "!ProgramFiles!\Microsoft Office\Office16\ospp.vbs" (
  set "OSPP=!ProgramFiles!\Microsoft Office\Office16\ospp.vbs"
)

cscript "!OSPP!" /inpkey:<ProductKey>
cscript "!OSPP!" /sethst:<Host>
cscript "!OSPP!" /setprt:1688
cscript "!OSPP!" /act
```

## **BYPASS WIN11 RESTRICTIONS**
On select Windows version, press `SHIFT` + `F10`. Command prompt will popup then type these:

```bat
reg add HKLM\SYSTEM\Setup\LabConfig /v BypassCPUCheck /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\Setup\LabConfig /v BypassRAMCheck /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\Setup\LabConfig /v BypassSecureBootCheck /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\Setup\LabConfig /v BypassStorageCheck /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\Setup\LabConfig /v BypassTPMCheck /t REG_DWORD /d 1 /f

```

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

[^officegvlk]: https://docs.microsoft.com/en-us/deployoffice/vlactivation/gvlks

[^csshfa]: https://bitsofco.de/when-do-the-hover-focus-and-active-pseudo-classes-apply/