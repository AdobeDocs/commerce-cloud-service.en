---
title: Build and Deploy Process
description: Learn about the build and deploy process for Commerce on AEC.
exl-id: 6e98f6ac-5b35-4c36-9eea-f1dfe223364b
---
# Build and Deploy Process

There are three, distinct phases of the Commerce deployment process: build, deploy, and post-deploy.

- **Build**
- **Deploy**
- **Post-deploy**

Cloud Manager (CM) UI request → CM self-service gateway APIs → Skyline cloud controller (SCC) lifecycle trigger → k8s Operator → SCC state reflector → CM self-service gateway APIs → CM UI response
