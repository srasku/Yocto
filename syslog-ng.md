"Next generation" system logging daemon.

# Configuration
Configuration file is in `/etc/syslog-ng/syslog-ng.conf`.  Five types of entries:
- `options`
- `source` - where to collect log entries from
- `destination` - where to send logs to
- `filter` - Combines `source`s amd `destintation`s and allows you to specify facilities and log levels.
- `log` - precisely where the information is logged.