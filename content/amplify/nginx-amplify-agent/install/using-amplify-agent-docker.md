---
title: Use NGINX Amplify Agent with Docker
description: Learn how to use F5 NGINX Amplify Agent with Docker.
weight: 500
toc: true
docs: DOCS-971
---

You can use F5 NGINX Amplify Agent in a Docker environment. Although it's still work-in-progress, NGINX Amplify Agent can collect most of the metrics and send them over to the Amplify backend in either "standalone" or "aggregate" mode. The standalone mode of operation is the simplest one, with a separate "host" created for each Docker container. Alternatively, the metrics from NGINX Amplify Agents running in different containers can be aggregated on a "per-image" basis — this is the aggregate mode of deploying NGINX Amplify Agent with Docker.

For more information, please refer to our [Amplify Dockerfile](https://github.com/nginxinc/docker-nginx-amplify) repository.
