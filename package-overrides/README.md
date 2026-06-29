# Package Overrides

This directory contains small overlay trees that can be applied to existing
Blackfin application packages without rebuilding the application binaries.

## `syslog`

`syslog` adds `bin/syslogd`, a wrapper that starts the BusyBox syslog daemon
with remote logging enabled:

```sh
/bin/busybox syslogd -R syslog:514
```

Legacy uClinux application packages overlay files onto the RAM root filesystem
at boot. If a package contains `bin/syslogd`, it replaces the base `/bin/syslogd`
symlink to BusyBox after deploy. Existing startup scripts that run `syslogd`
will then use this wrapper and send logs to host `syslog` on UDP port 514.

Use `utility_scripts/apply_package_override` to build patched packages from
known-good application packages.

## `mirrorcell1m0-syslog`

`mirrorcell1m0-syslog` adds the same `bin/syslogd` wrapper and also replaces
`etc/config/crontab/root` with the original hourly `ntpcheck` entry plus a
`0-59` minute-range cron guard that runs `/bin/start_syslogd`; that helper starts
`/bin/syslogd` only when it is not already running. This is needed because the legacy mirrorcell1m0 2.6 image does not
start syslog from `/etc/rc`.

## WOST Buildroot Package

`wost-3.0.0.tgz` is a Buildroot/Linux 3.10 package and uses `tmp/deploy` rather
than the legacy `/bin/deploy` flow. Use
`utility_scripts/apply_wost_syslog_patch` to build `wost-3.0.1.tgz`; it patches
only the syslog startup line in `tmp/deploy`.
