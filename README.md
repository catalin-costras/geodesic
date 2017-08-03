
# Geodesic [![Build Status](https://travis-ci.org/cloudposse/geodesic.svg?branch=master)](https://travis-ci.org/cloudposse/geodesic)

## Introduction

Geodesic is the fastest way to get up and running with a rock solid, production grade cloud platform. 

It provides a fully customizable framework for defining and building world-class cloud infrastructures backed by [AWS](https://aws.amazon.com/) and powered by [kubernetes](https://kubernetes.io/). It couples best-of-breed technologies with engineering best-practices to equip organizations with the tooling that enables clusters to be spun up in record time without compromising security.

Geodesic is composed of two parts:

1. It is an interactive command-line shell. The shell includes the *ultimate* mashup of cloud orchestration tools. Those tools are then integrated to work in concert with each other using a consistent framework. Installation of the shell is as easy as running a docker container.  
2. It is a distribution of essential services. The distribution includes a collection of Helm charts for CI/CD, VPN, SSH Bastion, Automatic DNS, Automatic TLS,  Automatic Monitoring, Account Management, Log Collection, Load Balancing/Routing, Image Serving, and much more. What makes these charts even more valuable is that they were designed from the ground up work well with each other and integrate with external services for authentication (SSO/OAuth2, MFA).

An organization may chose to leverage all of these components, or just the parts the make their life easier.

## Features
* **Secure** - TLS/PKI, OAuth2, MFA Everywhere, remote access VPN, [ultra secure bastion/jumphost](https://github.com/cloudposse/bastion) with audit capabilities and slack notifications, [IAM assumed roles](https://github.com/cloudposse/aws-assume-role/), automatic key rotation, encryption at rest, and VPCs;
* **Repeatable** - 100% Infrastructure-as-Code with change automation and support for scriptable admin tasks in any language, including terraform;
* **Extensible** - A framework where everything can be be extended to work the way you want to to;
* **Comprehensive** - our [helm charts library](https://github.com/cloudposse/charts) are designed to tightly integrate your cloud-platform with Github Teams and Slack Notifications and CI/CD systems like TravisCI, CircleCI or Jenkins;
* **OpenSource** - Permissive [APACHE 2.0](LICENSE) license means no lock-in and no on-going license fees


## Technologies

At its core, Geodesic is a framework for provisioning cloud infrastructure and the applications that sit on top of it. We leverage as many existing tools as possible to facilitate cloud fabrication and administration. We're like the connective tissue that sits between all of the components of a modern cloud.

* [`kops`](https://github.com/kubernetes/kops/) for kubernetes cluster orchestration 
* [`aws-cli`](https://github.com/aws/aws-cli/) for interacting directly with the AWS APIs
* [`helm`](https://github.com/kubernetes/helm/) for installing packages like varnish or apache on the kubernetes cluster
* [`terraform`](https://github.com/hashicorp/terraform/) for provisioning miscellaneous resources on pretty much any cloud
* [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl-overview/) for controlling kubernetes resources like deployments or load balancers
* [`ansible`](http://docs.ansible.com/ansible/latest/index.html) Ansible is an IT automation tool. It can configure systems, deploy software, and orchestrate more advanced IT tasks.
* [`s3fs`](https://github.com/s3fs-fuse/s3fs-fuse) for mounting encrypted S3 buckets that store cluster configurations and secrets
* [`gcloud`, `gsutil`](https://cloud.google.com/sdk/) for integration with Google Cloud (e.g. GKE, GCE, Google Storage)

## Demo

![](https://media.giphy.com/media/26FmS6BRnPVPo2FDq/source.gif)

## Prerequisites

### Install Docker

Docker can be easily installed by following the instructions for your OS:

* [Linux](https://docs.docker.com/linux/step_one/) (Or simply run  `curl -fsSL https://get.docker.com/ | sh`)
* [Windows](https://docs.docker.com/windows/step_one/)
* [Mac OS](https://docs.docker.com/mac/step_one/)

## Quick Start

1. Install the geodesic client, if you haven't already: (feel free to inspect the shell script!)

   ```
   curl -s https://geodesic.sh | sudo bash
   ```
2. Create a `Dockerfile` that defines your environment

   ```
   FROM cloudposse/geodesic:latest
   ENV AWS_PROFILE=ops
   ENV AWS_DEFAULT_PROFILE=ops
   ENV CLUSTER_PREFIX=aws                                # Short name of cluster (e.g. foobar)
   ENV CLUSTER_DNS_ZONE=example.com                      # Parent zone for cluster (e.g. example.com)
   ENV AWS_REGION=us-west-2

   COPY conf/ /conf/
   WORKDIR /conf/
   ```

3. Build your cluster image

   ```
   docker build -t aws.example.com
   ```


4. Run `geodesic use aws.example.com` to start the geodesic shell for that cluster
5. Run `cloud create` to run through configuration steps
6. Run `cloud up` to provision the cluster

All done. Your cloud is now up and running.

## Help

**Got a question?** 

Review the [docs](docs/), file a GitHub [issue](https://github.com/cloudposse/geodesic/issues), send us an [email](mailto:hello@cloudposse.com) or reach out to us on [Gitter](https://gitter.im/cloudposse/).


## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/bastion/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing Geodesic, we would love to hear from you! Shoot us an [email](mailto:hello@cloudposse.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull request** so that we can review your changes

**NOTE:** Be sure to merge the latest from "upstream" before making a pull request!

## License

[APACHE 2.0](LICENSE) © 2016-2017 [Cloud Posse, LLC](https://cloudposse.com)

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at
     
      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.

## About

Geodesic is maintained and funded by [Cloud Posse, LLC][website]. Like it? Please let us know at <hello@cloudposse.com>

We love [Open Source Software](https://github.com/cloudposse/)! 

See [our other projects][community]
or [hire us][hire] to help build your next cloud-platform.

  [website]: http://cloudposse.com/
  [community]: https://github.com/cloudposse/
  [hire]: http://cloudposse.com/contact/
  
### Contributors


| [![Erik Osterman][erik_img]][erik_web]<br/>[Erik Osterman][erik_web] | [![Igor Rodionov][igor_img]][igor_web]<br/>[Igor Rodionov][igor_web] |
|-------------------------------------------------------|------------------------------------------------------------------|

  [erik_img]: http://s.gravatar.com/avatar/88c480d4f73b813904e00a5695a454cb?s=144
  [erik_web]: https://github.com/osterman/
  [igor_img]: http://s.gravatar.com/avatar/bc70834d32ed4517568a1feb0b9be7e2?s=144
  [igor_web]: https://github.com/goruha/


