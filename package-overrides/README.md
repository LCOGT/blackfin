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
