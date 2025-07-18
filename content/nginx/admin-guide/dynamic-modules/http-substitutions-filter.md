---
description: Replace text in response bodies, using regular expressions and fixed
  strings, with the HTTP Substitutions Filter dynamic module supported by NGINX, Inc.
nd-docs: DOCS-389
title: HTTP Substitutions Filter
toc: true
weight: 100
type:
- how-to
---

The HTTP Substitutions Filter dynamic module replaces text in response bodies, using regular expressions and fixed strings.

## Installation

1. Check the [Technical Specifications]({{< ref "/nginx/technical-specs.md#dynamic-modules" >}}) page to verify that the module is supported by your operating system.

2. Make sure that your operating system is configured to retrieve binary packages from the official NGINX Plus repository. See installation instructions for your operating system on the [Installing NGINX Plus]({{< ref "/nginx/admin-guide/installing-nginx/installing-nginx-plus.md" >}}) page.

3. Install the HTTP Substitutions Filter module package `nginx-plus-module-subs-filter` from the official NGINX Plus repository.

   For Amazon Linux 2, CentOS, Oracle Linux, and RHEL:

   ```shell
   sudo yum update && \
   sudo yum install nginx-plus-module-subs-filter
   ```

   For Amazon Linux 2023, AlmaLinux, Rocky Linux:

   ```shell
   sudo dnf update && \
   sudo dnf install nginx-plus-module-subs-filter
   ```

   For Debian and Ubuntu:

   ```shell
   sudo apt update && \
   sudo apt install nginx-plus-module-subs-filter
   ```

   For SLES:

   ```shell
   sudo zypper refresh && \
   sudo zypper install nginx-plus-module-subs-filter
   ```

   For FreeBSD:

   ```shell
   sudo pkg update && \
   sudo pkg install nginx-plus-module-subs-filter
   ```

## Configuration

After installation you will need to enable and configure the module in F5 NGINX Plus configuration file `nginx.conf`.

1. Enable dynamic loading of the module with the [`load_module`](https://nginx.org/en/docs/ngx_core_module.html#load_module) directive specified in the top-level (“`main`”) context:

   ```nginx
   load_module modules/ngx_http_subs_filter_module.so;

   http {
       # ...
   }
   ```

2. Perform additional configuration as required by the [module](https://github.com/yaoweibin/ngx_http_substitutions_filter_module).

3. Test the NGINX Plus configuration. In a terminal, type-in the command:

    ```shell
    nginx -t
    ```

    Expected output of the command:

    ```shell
    nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    nginx: configuration file /etc/nginx/nginx.conf is successful
    ```

4. Reload the NGINX Plus configuration to enable the module:

    ```shell
    nginx -s reload
    ```

## More info

- [NGINX Substitution Filter GitHub project](https://github.com/yaoweibin/ngx_http_substitutions_filter_module)

- [NGINX dynamic modules]({{< ref "dynamic-modules.md" >}})

- [NGINX Plus technical specifications]({{< ref "/nginx/technical-specs.md" >}})

- [Uninstalling a dynamic module]({{< ref "uninstall.md" >}})
