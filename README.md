# Service creator | Ansible role

[![Build Status](https://travis-ci.org/rh-messaging-qe/ansible-service-creator.svg?branch=master)](https://travis-ci.org/rh-messaging-qe/ansible-service-creator)
[![GitHub Issues](https://img.shields.io/github/issues/rh-messaging-qe/ansible-service-creator.svg)](https://github.com/rh-messaging-qe/ansible-service-creator/issues)
[![GitHub Issues](https://img.shields.io/github/issues-pr/rh-messaging-qe/ansible-service-creator.svg)](https://github.com/rh-messaging-qe/ansible-service-creator/pulls)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Description

Create custom service for SystemD or SysV based operating systems.

## Requirements

- SystemD or Init.D on remote
- Ansible >2.5

## Role Variables

### ansible-service-creator options

| Name                               | Default Value  | Description                     |
|------------------------------------|----------------|---------------------------------|
| `service_opts`                     | {}             | Include settings for this role  |

### Common Supported service_opts for SystemD

| Name                  | Default Value                  | Description               |
|-----------------------|--------------------------------|---------------------------|
| `Enabled`             | False                          |                           |
| `Description`         | Service for {{ item.key }}     |                           |
| `After`               | ""                             |                           |
| `Before`              | ""                             |                           |
| `User`                | ""                             |                           |
| `Group`               | ""                             |                           |
| `Type`                | ""                             |                           |
| `PIDfile`             | ""                             |                           |
| `OOMScoreAdjust`      | ""                             |                           |
| `Nice`                | ""                             |                           |
| `ExecStart`           | ""                             |                           |
| `ExecStartPre`        | ""                             |                           |
| `ExecStartPost`       | ""                             |                           |
| `ExecStop`            | ""                             |                           |
| `ExecStopPost`        | ""                             |                           |
| `ExecReload`          | ""                             |                           |
| `Restart`             | ""                             |                           |
| `RestartSec`          | ""                             |                           |
| `TimeoutSec`          | '30'                           |                           |
| `Wants`               | ""                             |                           |
| `Requires`            | ""                             |                           |
| `Environment`         | ""                             |                           |
| `EnvironmentFile`     | ""                             |                           |
| `WorkingDirectory`    | ""                             |                           |
| `StandardInput`       | ""                             |                           |
| `StandardOutput`      | ""                             |                           |
| `StandardError`       | ""                             |                           |
| `WantedBy`            | ""                             |                           |
| `RequiredBy`          | ""                             |                           |

### Common supported service_opts for Init.D

| Name                  | Default Value                  | Description               |
|-----------------------|--------------------------------|---------------------------|
| `Enabled`             | False                          |                           |
| `User`                | ""                             |                           |
| `PIDFile`             | ""                             |                           |
| `ExecStart`           | ""                             |                           |
| `WorkingDirectory`    | ""                             |                           |
| `StandardOutput`      | ""                             |                           |
| `StandardError`       | ""                             |                           |

## Usage

```yaml
- hosts: node01
  roles:
    - role: ansible-service-creator
      services_opts:
        qdrouterd01:
          Enabled: Yes
          Started: Yes
          ExecStart: "qdrouterd -c /etc/qdrouterd/qdrouterd-01.conf"
          User: "qdrouterd"
          Group: "qdrouterd"
        qdrouterd02:
          Enabled: No
          Started: No
          ExecStart: "qdrouterd -c /etc/qdrouterd/qdrouterd-02.conf"
          User: "qdrouterd"
          Group: "qdrouterd"
```

## NOTICE

- Init.d based on [init-script-template](https://github.com/fhd/init-script-template)

## License

- Apache 2.0

## Author Information

Messaging QE team @ redhat.com

Initial work and current maintainer

- Dominik Lenoch <dlenoch@redhat.com>
