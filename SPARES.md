# Blackfin Spare Inventory

Record every prepared spare before it leaves the bench. Keep factory MAC
addresses unique; do not clone a failed controller MAC unless a site-specific
replacement plan explicitly requires it.

## Preparation Batch

| Qty | Application | Kernel Generation | OS Image | Package | Status |
| ---: | --- | --- | --- | --- | --- |
| 7 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 7 prepared |
| 7 | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 7 prepared |
| 4 | floyds | uClinux 2.6 | `uImage-floyds` | `floyds-0.3.4.tgz` | 4 prepared |
| 4 | floydscal | uClinux 2.6 | `uImage-floydscal` | `floydscal-0.2.3.tgz` | 4 prepared |
| 3 | nres | Buildroot/Linux 3.10 | `uImage-nres` | `nres-2.1.0.tgz` | 3 prepared |
| 3 | nres-tc | Buildroot/Linux 3.10 | `uImage-1.1.0` | `nres-tc-1.0.0.tgz` | 3 prepared |

## Board Records

Fill one row per physical board after final reboot verification.

| Board ID | MAC Address / `ethaddr` | Application | Kernel Generation | OS Image | Package | Prepared Date | Verification | Ship To | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| MIRRORCELL1M0-01 | 4C:43:4F:00:01:85 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-02 | 4C:43:4F:00:01:7F | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-03 | 4C:43:4F:00:01:80 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-04 | 4C:43:4F:00:01:81 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-05 | 4C:43:4F:00:01:82 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-06 | 4C:43:4F:00:01:83 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| MIRRORCELL1M0-07 | 4C:43:4F:00:01:84 | mirrorcell1m0 | uClinux 2.6 | `uImage-mirrorcell1m0` | `mirrorcell1m0-0.4.7.tgz` | 2026-06-26 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports mirrorcell1m0; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-01 | 4C:43:4F:00:01:86 | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after repeated reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-02 | 4C:43:4F:00:01:71 | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-03 | 4C:43:4F:00:01:6E | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-04 | 4C:43:4F:00:01:6D | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-05 | 4C:43:4F:00:01:70 | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-06 | 4C:43:4F:00:01:6F | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| WOST-07 | 4C:43:4F:00:01:72 | wost | Buildroot/Linux 3.10 | `uImage-1.1.0` | `wost-3.0.1.tgz` | 2026-06-26 | Boots after reboot; checksum OK; hostname OK; web API reports wost; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  | formatted mtd3 JFFS2 before install |
| FLOYDS-01 | 4C:43:4F:00:01:89 | floyds | uClinux 2.6 | `uImage-floyds` | `floyds-0.3.4.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floyds with status -1 on bench; syslogd and boa OK; board cannot resolve syslog |  |  |
| FLOYDS-02 | 4C:43:4F:00:01:88 | floyds | uClinux 2.6 | `uImage-floyds` | `floyds-0.3.4.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floyds with status -1 on bench; syslogd and boa OK; board cannot resolve syslog |  |  |
| FLOYDS-03 | 4C:43:4F:00:01:79 | floyds | uClinux 2.6 | `uImage-floyds` | `floyds-0.3.4.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floyds with status -1 on bench; syslogd and boa OK; board cannot resolve syslog |  |  |
| FLOYDS-04 | 4C:43:4F:00:01:7A | floyds | uClinux 2.6 | `uImage-floyds` | `floyds-0.3.4.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floyds with status -1 on bench; syslogd and boa OK; board cannot resolve syslog |  |  |
| FLOYDSCAL-01 | 4C:43:4F:00:01:7E | floydscal | uClinux 2.6 | `uImage-floydscal` | `floydscal-0.2.3.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floydscal with status 0 on bench; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| FLOYDSCAL-02 | 4C:43:4F:00:01:7D | floydscal | uClinux 2.6 | `uImage-floydscal` | `floydscal-0.2.3.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floydscal with status 0 on bench; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| FLOYDSCAL-03 | 4C:43:4F:00:01:7C | floydscal | uClinux 2.6 | `uImage-floydscal` | `floydscal-0.2.3.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floydscal with status 0 on bench; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| FLOYDSCAL-04 | 4C:43:4F:00:01:7B | floydscal | uClinux 2.6 | `uImage-floydscal` | `floydscal-0.2.3.tgz` | 2026-06-29 | Devolved from 3.10 to 2.6; boots after reboot; checksum OK; hostname OK; web API reports floydscal with status 0 on bench; syslogd and boa OK; post exits on bench; board cannot resolve syslog |  |  |
| NRES-01 | 4C:43:4F:00:01:78 | nres | Buildroot/Linux 3.10 | `uImage-nres` | `nres-2.1.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksum OK; hostname OK; web API reports nres with status 0; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd currently points at `log:1028`, not `syslog:514` |
| NRES-02 | 4C:43:4F:00:01:77 | nres | Buildroot/Linux 3.10 | `uImage-nres` | `nres-2.1.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksum OK; hostname OK; web API reports nres with status 0; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd currently points at `log:1028`, not `syslog:514` |
| NRES-03 | 4C:43:4F:00:01:76 | nres | Buildroot/Linux 3.10 | `uImage-nres` | `nres-2.1.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksum OK; hostname OK; web API reports nres with status 0; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd currently points at `log:1028`, not `syslog:514` |
| NRES-TC-01 | 4C:43:4F:00:01:73 | nres-tc | Buildroot/Linux 3.10 | `uImage-1.1.0` | `nres-tc-1.0.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksums OK; hostname OK; web root reports NRES Temperature Controller; /cgi-bin/status is not provided; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd is local only: `/sbin/syslogd -n -s 1024 -b 3` |
| NRES-TC-02 | 4C:43:4F:00:01:75 | nres-tc | Buildroot/Linux 3.10 | `uImage-1.1.0` | `nres-tc-1.0.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksums OK; hostname OK; web root reports NRES Temperature Controller; /cgi-bin/status is not provided; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd is local only: `/sbin/syslogd -n -s 1024 -b 3` |
| NRES-TC-03 | 4C:43:4F:00:01:74 | nres-tc | Buildroot/Linux 3.10 | `uImage-1.1.0` | `nres-tc-1.0.0.tgz` | 2026-06-29 | Read-only bench verification; no reboot or configuration changes; checksums OK; hostname OK; web root reports NRES Temperature Controller; /cgi-bin/status is not provided; boa OK; post and expose absent on bench; board cannot resolve syslog |  | syslogd is local only: `/sbin/syslogd -n -s 1024 -b 3` |

## Bench Verification

For each board, record the result of these checks in the `Verification` field.
Use short phrases such as `checksum OK`, `web API reports wost`, or
`board cannot resolve syslog` so the record captures both passes and caveats.

Required bench checks:

- Boots from flash without serial intervention after at least one reboot.
- Package checksum passes from `/mnt/flash`, for example `md5sum -c wost-3.0.1.md5`.
- `hostname` matches the installed application.
- `uname -a` matches the expected kernel generation.
- `cat /proc/mtd` matches the expected partition layout.
- Web/API status responds when the board has a bench IP; `/cgi-bin/status`
  should report the expected `hostname` and `status:0`.
- Syslog startup command points at `syslog:514`:
  - legacy 2.6 packages use the `bin/syslogd` wrapper from the package.
  - WOST 3.10 should show `/sbin/syslogd -n -R syslog:514 -s 1024 -b 3`.
- `boa` is running where applicable.

Hardware/site-dependent checks:

- `post` should be running when the board is attached to suitable mechanism
  hardware. On the bench, record if it exits but the web API still responds.
- End-to-end syslog delivery should be verified when the board can resolve
  `syslog`; if bench DNS does not provide that name, record
  `board cannot resolve syslog` and rely on the syslog command-line check.
