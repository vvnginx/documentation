---
title: Which Ingress Controller Do I Need?
toc: true
draft: true
weight: 400
nd-content-type: reference
nd-product: NIC
nd-docs: DOCS-610
---

This document describes the key differences between the community Ingress-NGINX Controller and F5 NGINX Ingress Controller.

There are two NGINX-based Ingress Controller implementations out there: the one made by NGINX ([nginx/kubernetes-ingress](https://github.com/nginx/kubernetes-ingress)) and the one made by Kubernetes ([kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx)). In this document, we explain the key differences between those implementations. This information should help you to choose an appropriate implementation for your requirements or move from one implementation to the other.

## Which One Am I Using?

If you are unsure about which implementation you are using, check the container image of the Ingress Controller that is running. For the nginx/kubernetes-ingress Ingress Controller its Docker image is published on [DockerHub](https://hub.docker.com/r/nginx/nginx-ingress/) and available as *nginx/nginx-ingress*.

## The Key Differences

The table below summarizes the key difference between nginx/kubernetes-ingress and kubernetes/ingress-nginx Ingress Controllers. Note that the table has two columns for the nginx/kubernetes-ingress Ingress Controller, as it can be used both with NGINX and NGINX Plus. For more information about nginx/kubernetes-ingress with NGINX Plus, read the [Extensibility with NGINX Plus]({{< ref "/nic/overview/nginx-plus.md" >}}) documentation.

{{% table %}}
| Aspect or Feature | kubernetes/ingress-nginx | nginx/kubernetes-ingress with NGINX | nginx/kubernetes-ingress with NGINX Plus |
| --- | --- | --- | --- |
| **Fundamental** |
| Authors | Kubernetes community | NGINX Inc and community |  NGINX Inc and community |
| NGINX version | [Custom](https://github.com/kubernetes/ingress-nginx/tree/main/images/nginx) NGINX build that includes several third-party modules | NGINX official mainline [build](https://github.com/nginx/docker-nginx) | NGINX Plus |
| Commercial support | N/A | N/A | Included |
| **Load balancing configuration via the Ingress resource** |
| Merging Ingress rules with the same host | Supported | Supported via [Mergeable Ingresses](https://github.com/nginx/kubernetes-ingress/tree/v{{< nic-version >}}/examples/ingress-resources/mergeable-ingress-types) | Supported via [Mergeable Ingresses](https://github.com/nginx/kubernetes-ingress/tree/v{{< nic-version >}}/examples/ingress-resources/mergeable-ingress-types) |
| HTTP load balancing extensions - Annotations | See the [supported annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/) | See the [supported annotations]({{< ref "/nic/configuration/ingress-resources/advanced-configuration-with-annotations.md" >}}) | See the [supported annotations]({{< ref "/nic/configuration/ingress-resources/advanced-configuration-with-annotations.md#summary-of-annotations" >}})|
| HTTP load balancing extensions -- ConfigMap | See the [supported ConfigMap keys](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/) | See the [supported ConfigMap keys]({{< ref "/nic/configuration/global-configuration/configmap-resource.md" >}}) | See the [supported ConfigMap keys]({{< ref "/nic/configuration/global-configuration/configmap-resource.md" >}}) |
| TCP/UDP | Supported via a ConfigMap | Supported via custom resources | Supported via custom resources |
| Websocket  | Supported | Supported via an [annotation](https://github.com/nginx/kubernetes-ingress/tree/v{{< nic-version >}}/examples/ingress-resources/websocket) | Supported via an [annotation](https://github.com/nginx/kubernetes-ingress/tree/v{{< nic-version >}}/examples/ingress-resources/websocket) |
| TCP SSL Passthrough | Supported via a ConfigMap | Supported via custom resources | Supported via custom resources |
| JWT validation | Not supported | Not supported | Supported |
| Session persistence | Supported via a third-party module | Not supported | Supported |
| Canary testing (by header, cookie, weight) | Supported via annotations | Supported via custom resources | Supported via custom resources |
| Configuration templates *1 | See the [template](https://github.com/kubernetes/ingress-nginx/blob/main/rootfs/etc/nginx/template/nginx.tmpl) | See the [templates](../internal/configs/version1) | See the [templates](../internal/configs/version1) |
| **Load balancing configuration via Custom Resources** |
| HTTP load balancing | Not supported | See [VirtualServer and VirtualServerRoute]({{< ref "/nic/configuration/virtualserver-and-virtualserverroute-resources.md" >}}) resources | See [VirtualServer and VirtualServerRoute]({{< ref "/nic/configuration/virtualserver-and-virtualserverroute-resources.md" >}}) resources |
| TCP/UDP load balancing | Not supported | See [TransportServer]({{< ref "/nic/configuration/transportserver-resource.md" >}}) resource | See [TransportServer](({{< ref "/nic/configuration/transportserver-resource.md" >}}) resource |
| TCP SSL Passthrough load balancing | Not supported | See [TransportServer]({{< ref "/nic/configuration/transportserver-resource.md" >}}) resource | See [TransportServer]({{< ref "/nic/configuration/transportserver-resource.md" >}}) resource |
| **Deployment** |
| Command-line arguments *2 | See the [arguments](https://kubernetes.github.io/ingress-nginx/user-guide/cli-arguments/) | See the [arguments]({{< ref "/nic/configuration/global-configuration/command-line-arguments.md" >}}) | See the [arguments]({{< ref "/nic/configuration/global-configuration/command-line-arguments.md" >}}) |
| TLS certificate and key for the default server | Required as a command-line argument/ auto-generated | Required as a command-line argument | Required as a command-line argument |
| Helm chart | Supported | Supported | Supported |
| Operator | Not supported | Supported | Supported |
| **Operational** |
| Reporting the IP address(es) of the Ingress Controller into Ingress resources | Supported | Supported | Supported |
| Extended Status | Supported via a third-party module | Not supported | Supported |
| Prometheus Integration | Supported | Supported | Supported |
| Dynamic reconfiguration of endpoints (no configuration reloading) | Supported with a third-party Lua module | Not supported | Supported |
{{% /table %}}

Notes:

*1 -- The configuration templates that are used by the Ingress Controllers to generate NGINX configuration are different. As a result, for the same Ingress resource the generated NGINX configuration files are different from one Ingress Controller to the other, which in turn means that in some cases the behavior of NGINX can be different as well.

*2 -- Because the command-line arguments are different, it is not possible to use the same deployment manifest for deploying the Ingress Controllers.

## How to Swap an Ingress Controller

If you decide to swap an Ingress Controller implementation, be prepared to deal with the differences that were mentioned in the previous section. At minimum, you need to start using a different deployment manifest.
