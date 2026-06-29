# Blackfin Project Notes

This tree contains deployable artifacts, packaging helpers, and field utility
scripts for LCO Blackfin mechanism controllers, including Superfin boards.

Important top-level directories:

- repository root: TFTP-ready bootloaders, Linux images, application packages,
  and checksums.
- `utility_scripts`: upgrade, downgrade, and package-building helpers.
- `package-overrides`: overlay files used to build patched application
  packages.
- `SPARES.md`: bench inventory for prepared spare controllers.

## Software Generations

There are two incompatible Blackfin software generations in use. The newer
generation is sometimes referred to casually as "3.1", but the deployed kernel
seen in the field is Linux 3.10.10.

### Legacy uClinux 2.6

Legacy systems run uClinux/Linux 2.6.24.7 with an application-specific OS image.
The `uImage-*` files whose `file` output says `uClinux Kernel and ext2` are
legacy 2.6 images. Examples include:

- `uImage-floyds`
- `uImage-floydscal`
- `uImage-fw0m4`
- `uImage-fw1m0`
- `uImage-mirrorcell1m0`
- `uImage-mirrorcover1m0`
- `uImage-nres`
- `uImage-ots0m4`
- `uImage-ots1m0`
- `uImage-oxfocus`
- `uImage-wost`

In this generation, the Linux image contains the base root filesystem and an
application-specific `/etc/rc`. The application package on `/mnt/flash` overlays
additional binaries, libraries, and web files at boot.

Typical legacy 2.6 partition layout:

```text
mtd0: 00040000 "Bootloader"
mtd1: 000c0000 "jffs2"
mtd2: 00300000 "uImage"
mtd3: 01000000 "ROMfs"
```

For this layout, `/mnt/flash` is `/dev/mtdblock1`.

Legacy application packages in this repository include:

- `bosbox-*.tgz`
- `floyds-*.tgz`
- `floydscal-*.tgz`
- `fw0m4-*.tgz`
- `fw1m0-*.tgz`
- `fw75a-*.tgz`
- `inscrate-*.tgz`
- `mirrorcell1m0-*.tgz`
- `mirrorcover1m0-*.tgz`
- `mres-*.tgz`
- `nres-*.tgz`
- `nres-agu-*.tgz`
- `nres-tc-*.tgz`
- `ots0m4-*.tgz`
- `ots1m0-*.tgz`
- `oxfocus-*.tgz`

Use packages built for the same legacy runtime. Do not assume that a package
built or modified recently is compatible with the old runtime just because its
name matches. For example, a package with a rebuilt `post` binary can fail on
2.6 with unresolved runtime symbols if it was built with the wrong toolchain.

A safe syslog-only FLOyDS package can be built from known-good
`floyds-0.3.2.tgz` by adding only a `bin/syslogd` wrapper to forward to
`syslog:514`. Do not replace `usr/bin/post` unless it is built with the legacy
2.6 toolchain and tested on a 2.6 controller.

### Buildroot Linux 3.10

Newer systems run Buildroot/Linux 3.10.10. In this generation, the OS image is
generic rather than application-specific.

The 3.10 image in this repository is:

- `uImage-1.1.0`

Typical 3.10 partition layout:

```text
mtd0: 00040000 "bootloader(nor)"
mtd1: 00100000 "linux kernel(nor)"
mtd2: 00100000 "root file system(nor)"
mtd3: 001c0000 "flash file system(nor)"
```

For this layout, `/mnt/flash` is `/dev/mtdblock3`.

Buildroot-compatible application packages have a different layout from legacy
packages. For example, `wost-3.0.0.tgz` installs under `/srv/www` and
includes a `tmp/deploy` script. Legacy packages usually install web files under
`/home/httpd`.

Do not deploy legacy uClinux packages such as `floyds-0.3.2.tgz` onto a 3.10
Buildroot system unless the package has been rebuilt and verified for
Buildroot. Runtime symbol errors such as
`post: can't resolve symbol '___thenan_sf'` indicate an ABI/toolchain mismatch.

For spare-board preparation, WOST remains on Buildroot/Linux 3.10 using
`wost-3.0.1.tgz`, which is built from `wost-3.0.0.tgz` by patching only
`tmp/deploy` so `/sbin/syslogd` forwards to `syslog:514`.

## Safety Rules

- Keep serial access connected for any bootloader or OS image operation.
- Do not run flash erase commands from memory. Verify `cat /proc/mtd` every time.
- Never substitute `/dev/mtd*` numbers between 2.6 and 3.10 systems.
- On 2.6, `/dev/mtd1` is the flash app/config filesystem.
- On 3.10, `/dev/mtd3` is the flash app/config filesystem.
- On 3.10, `/dev/mtd1` is the Linux kernel partition.
- Avoid manually erasing U-Boot flash address ranges unless following a known
  script for the exact bootloader/kernel generation.
- The first 256 KiB of flash contains U-Boot. If U-Boot is corrupted and there
  is no serial output at power-up, recovery requires JTAG/dev-board flashing.

## Application Deployment

### Persistent deployment to `/mnt/flash`

Use this when the flash filesystem is mounted read-write and has enough space.
The package name must match the running image's hostname because legacy
`/bin/deploy` looks for `$(hostname)-*.tgz`.

Example for legacy FLOyDS:

```sh
cd /mnt/flash
pkg=floyds-0.3.2
tftp -g -l ${pkg}.tgz -r blackfin/${pkg}.tgz 10.0.0.15
tftp -g -l ${pkg}.md5 -r blackfin/${pkg}.md5 10.0.0.15
md5sum -c ${pkg}.md5
/bin/deploy
```

Restart the app processes or reboot after a successful deploy.

Common legacy process restart:

```sh
killall post
post &
killall boa
boa -c /etc &
```

### Temporary RAM-only deployment

Use this when `/mnt/flash` cannot be written but the controller must run until
the next reboot.

```sh
cd /tmp
pkg=floyds-0.3.2
tftp -g -l ${pkg}.tgz -r blackfin/${pkg}.tgz 10.0.0.15
tftp -g -l ${pkg}.md5 -r blackfin/${pkg}.md5 10.0.0.15
md5sum -c ${pkg}.md5
tar zxvf ${pkg}.tgz -C /
```

This modifies the RAM root filesystem only. It is lost on reboot.

If the application needs config and flash is not mountable, create temporary RAM
directories and place the needed files there:

```sh
mkdir -p /mnt/flash/config
mkdir -p /etc/config
```

Then restart `post` so it reads the current config.

## Spare Board Preparation

The planned spare inventory is tracked in `SPARES.md`. Record each board's
factory MAC address, installed application, kernel generation, OS image,
application package, preparation date, verification result, and shipping
destination before it leaves the bench.

Build syslog-forwarding packages without overwriting the original artifacts:

```sh
utility_scripts/apply_package_override mirrorcell1m0-0.4.3.tgz mirrorcell1m0-0.4.7.tgz package-overrides/mirrorcell1m0-syslog
utility_scripts/apply_package_override floyds-0.3.2.tgz floyds-0.3.4.tgz
utility_scripts/apply_package_override floydscal-0.2.2.tgz floydscal-0.2.3.tgz
utility_scripts/apply_wost_syslog_patch wost-3.0.0.tgz wost-3.0.1.tgz
```

The current spare targets are:

- 7 `mirrorcell1m0` boards: legacy 2.6, `uImage-mirrorcell1m0`,
  `mirrorcell1m0-0.4.7.tgz`
- 7 `wost` boards: Buildroot/Linux 3.10, `uImage-1.1.0`, `wost-3.0.1.tgz`
- 4 `floyds` boards: legacy 2.6, `uImage-floyds`, `floyds-0.3.4.tgz`
- 4 `floydscal` boards: legacy 2.6, `uImage-floydscal`,
  `floydscal-0.2.3.tgz`

Keep each board's factory MAC address unless a site-specific replacement plan
explicitly requires cloning an address. Label the board with application,
kernel generation, package version, MAC address, and preparation date.

## Updating Applications Only

`utility_scripts/update` downloads an application package and its checksum from
TFTP and verifies the checksum. It does not deploy the package and does not
flash the OS.

Example:

```sh
cd /mnt/flash
sh /path/to/update floyds-0.3.2
/bin/deploy
```

## Evolve: 2.6 to 3.10

`utility_scripts/evolve` upgrades a legacy 2.6 controller to the newer
Buildroot 3.10 generation.

Command shape:

```sh
sh evolve u-boot-1.0.0 uImage-1.1.0
```

The script verifies:

```text
uname -r begins with 2.6
/dev/mtd0 size is 00040000
/dev/mtd1 size is 000c0000
/dev/mtd2 size is 00300000
/dev/mtd0 contains U-Boot 2011.
```

It downloads and verifies:

- `upgrade-utils.tgz`
- `u-boot-1.0.0.bin`
- `uImage-1.1.0`

It patches the new bootloader with the current `eth0` MAC address, stops
services, unmounts `/mnt/flash`, flashes the new bootloader, writes the 3.10
image across the banked flash layout, initializes the 3.10 flash filesystem, and
reboots.

This operation rewrites U-Boot. Do not run it without serial access and a known
recovery path.

## Update Linux: 3.10 to Newer 3.10

`utility_scripts/update_linux` updates the Linux image on systems
already running Buildroot 3.10.

Command shape:

```sh
sh update_linux uImage-1.1.0
```

The script verifies:

```text
uname -r begins with 3.10
/dev/mtd0 size is 00040000
/dev/mtd1 size is 00100000
/dev/mtd2 size is 00100000
```

It writes:

```text
image bytes 0x000000 - 0x0fffff -> /dev/mtd1
image bytes 0x100000 - 0x1fffff -> /dev/mtd2
```

Do not use this on legacy 2.6 systems.

## Devolve: 3.10 to 2.6

`utility_scripts/devolve` reverts a Buildroot 3.10 controller back to
legacy uClinux 2.6.

Command shape for FLOyDS:

```sh
sh devolve u-boot uImage-floyds
```

The script verifies:

```text
uname -r begins with 3.10
/dev/mtd0 size is 00040000
/dev/mtd1 size is 00100000
/dev/mtd2 size is 00100000
```

It downloads:

- `u-boot.bin`
- the target legacy `uImage-*`

It checks that the target image contains `uClinux Kernel and ext2`, patches the
old bootloader with the current `eth0` MAC address and `bootcmd=run localboot`,
then flashes the bootloader and splits the legacy image across the old layout:

```text
image bytes 0x000000 - 0x03ffff -> /dev/mtd1 offset 0x0c0000
image bytes 0x040000 - 0x13ffff -> /dev/mtd2
image bytes 0x140000 - 0x2fffff -> /dev/mtd3
```

After rebooting into 2.6, install the matching legacy application package onto
`/mnt/flash`.

Example for FLOyDS:

```sh
cd /mnt/flash
pkg=floyds-0.3.2
tftp -g -l ${pkg}.tgz -r blackfin/${pkg}.tgz 10.0.0.15
tftp -g -l ${pkg}.md5 -r blackfin/${pkg}.md5 10.0.0.15
md5sum -c ${pkg}.md5
/bin/deploy
```

## Network Notes

U-Boot network variables affect U-Boot `ping` and `tftp`:

```text
ipaddr
netmask
gatewayip
serverip
ethaddr
```

Linux usually runs DHCP. If DHCP assigns the wrong field IP, the usual cause is
that `ethaddr` differs from the failed controller's MAC. Only reuse a MAC if the
old controller is offline.

Temporary Linux IP assignment:

```sh
killall dhcpcd
ifconfig eth0 10.0.20.115 netmask 255.255.0.0 up
route add default gw 10.0.0.254
```

DHCP refresh:

```sh
killall dhcpcd
dhcpcd eth0 &
```

If the old `dhcpcd` does not accept an interface argument:

```sh
killall dhcpcd
dhcpcd &
```

## JTAG Recovery

If U-Boot is corrupted, there may be no serial output after reset. TFTP cannot
recover that state because TFTP requires U-Boot to run.

The documented recovery path uses:

- Bluetechnix DEV-BF5xxDA-Lite development board
- gnICE+ USB JTAG In-Circuit Emulator
- ADI/uClinux 2009R1.1 `bfin-jtag`

Minimal `flashit` script:

```text
cable gnICE+
detect
initbus bf53x
detectflash 0x20000000
flashmem 0x20000000 u-boot.bin
```

Run:

```sh
sudo /opt/uClinux-2009R1.1/bfin-elf/bin/bfin-jtag flashit
```
