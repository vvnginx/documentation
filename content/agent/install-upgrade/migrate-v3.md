---
title: Upgrade from v2.x to v3.0
weight: 500
docs: DOCS-000
---

This topic describes how to migrate from F5 NGINX Agent v2 to NGINX Agent v3.

## Overview

---

## Before you begin

To begin this task, you will require the following:

- A [working NGINX Agent instance]({{< relref "/agent/install-upgrade/install.md" >}}).
- A NGINX Agent connected to NGINX One. For a quick guide on how to connect to NGINX One Console see: [Connect to NGINX One Console]({{< relref "/nginx-one/how-to/nginx-configs/add-instance" >}})

---

## Migrate from NGINX Agent v2 to v3
The migration from NGINX Agent v2 to v3 is handled automatically by the package manager on your OS during the installation of NGINX Agent v3.

To install NGINX Agent v3 see : [Install NGINX Agent]({{< relref "agent/install-upgrade/install" >}})

To migrate NGINX Agent containers, there is a script that can be run to convert a NGINX Agent V2 config file to a NGINX Agent V3 config file which is located here [NGINX Agent Config Upgrade Script](https://github.com/nginx/agent/blob/v3/scripts/packages/upgrade-agent-config.sh).

Here is an example of how to upgrade the configuration:

```shell
wget https://github.com/nginx/agent/blob/v3/scripts/packages/upgrade-agent-config.sh
./upgrade-agent-config.sh --v2-config-file=./nginx-agent-v2.conf --v3-config-file=nginx-agent-v3.conf
```

If your NGINX Agent container was apart of a config sync group, then your NGINX Agent config needs to be manually updated to add the config sync group label. 
See [Add Config Sync Group]({{< relref "/nginx-one/how-to/config-sync-groups/manage-config-sync-groups" >}}).

---

## Rolling back from NGINX Agent v3 to v2
If a rollback to v2 is required, there is a backup of the NGINX Agent v2 config located here `/etc/nginx-agent/nginx-agent-v2-backup.conf`.

Replace `/etc/nginx-agent/nginx-agent.conf` with the contents of `/etc/nginx-agent/nginx-agent-v2-backup.conf` and then re-install NGINX Agent to an older version.
