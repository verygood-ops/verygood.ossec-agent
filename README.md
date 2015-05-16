Role Name
=========

This roles setup a OSSEC Agent

Requirements
------------

This role is only tested on Ubuntu trusty. You need to have a OSSEC server running. The server needs to be
running before the client because the client needs to get the credentials from the server, otherwise it
won't be able to talk to the server until the next restart.

Role Variables
--------------

The role uses the Ubuntu package defaults. The below all the options with their defaults as examples, but list 
items are truncated. Please view `defaults/main.yml` for a full list.

Server

```yml
ossec_server: 127.0.0.1
```

Rules

```yml
ossec_rules:
  - rules_config.xml
```

Syscheck

```yml
ossec_syscheck_frequency: 7200
ossec_syscheck_directories:
  - check_all: yes
    directories: /etc,/usr/bin,/usr/sbin
ossec_syscheck_ignore_directories:
  - /etc/mtab
```

Rootcheck

```yml
ossec_rootcheck_rootkit_files: /var/ossec/etc/shared/rootkit_files.txt
ossec_rootcheck_rootkit_rojans: /var/ossec/etc/shared/rootkit_trojans.txt
```

Global whitelist

```yml
ossec_global_white_lists:
  - 127.0.0.1
```

Remote
```yml
ossec_remote_connection: secure
ossec_remote_port: 1514
ossec_remote_protocol: udp
ossec_remote_local_ip: 0.0.0.0
```

Alerts

```yml
ossec_alerts_log_alert_level: 1
ossec_alerts_email_alert_level: 7
```
Commands

```yml
ossec_commands:
  - name: host-deny
    executable: host-deny.sh
    expect: srcip
    timeout_allowed: yes
```

Active Responses

```yml
ossec_active_responses:
  - command: host-deny
    location: local
    level: 6
    timeout: 600
```

Localfile

```yml
ossec_localfile:
  - log_format: syslog
    location: /var/log/messages
```

Example Playbook
----------------

    - hosts: agents
      vars:
        ossec_server: 10.13.123.123
      roles:
         - verygood.ossec-agent

License
-------

BSD
