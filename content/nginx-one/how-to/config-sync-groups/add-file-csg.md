---
docs: null
title: Add a file to a Config Sync Group
toc: true
weight: 400
type:
- how-to
---

## Overview

{{< include "nginx-one/add-file/overview.md" >}}

## Before you start

Before you add files in your configuration, ensure:

- You have access to the NGINX One Console.
- Config Sync Groups are properly registered with NGINX One Console

## Important considerations

This page applies when you want to add a file to a Config Sync Group. Any changes you make here apply to all [Instances]({{< relref "/nginx-one/glossary.md" >}}) of that Config Sync Group.

## Add a file

You can use the NGINX One Console to add a file to a specific Config Sync Group. To do so:

1. Select the Config Sync Group to manage.
1. Select the **Configuration** tab.

   {{< tip >}}

   {{< include "nginx-one/add-file/edit-config-tip.md" >}}

   {{< /tip >}}

1. Select **Edit Configuration**.
1. In the **Edit Configuration** window that appears, select **Add File**.

You now have multiple options, described in the sections which follow.

### New Configuration File

Enter the name of the desired configuration file, such as `abc.conf` and select **Add**. The configuration file appears in the **Edit Configuration** window.

### New SSL Certificate or CA Bundle

{{< include "nginx-one/add-file/new-ssl-bundle.md" >}}

  {{< tip >}}

  Make sure to specify the path to your certificate in your NGINX configuration,
  with the `ssl_certificate` and `ssl_certificate_key` directives.

  {{< /tip >}}

### Existing SSL Certificate or CA Bundle

{{< include "nginx-one/add-file/existing-ssl-bundle.md" >}}
With this option, You can incorporate [Managed certificates]({{< relref "/nginx-one/how-to/certificates/manage-certificates.md#managed-and-unmanaged-certificates" >}}).

## See also

- [Create and manage data plane keys]({{< relref "/nginx-one/how-to/data-plane-keys/create-manage-data-plane-keys.md" >}})
- [View and edit NGINX configurations]({{< relref "/nginx-one/how-to/nginx-configs/view-edit-nginx-configurations.md" >}})
- [Manage certificates]({{< relref "/nginx-one/how-to/certificates/manage-certificates.md" >}})
