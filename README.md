---
title: Quick Start Guide
layout: rancher-default-v2.0
version: v2.0
lang: en
redirect_from:
  - /rancher/quick-start-guide/
---

## Quick Start Guide
---

In this guide, you'll learn how to get started with Rancher v2.0, including:

* Preparing a Linux Host
* Launching Rancher Server and Accessing the Rancher UI
* Adding a Host through the Rancher UI
* Importing an Existing Kubernetes Cluster
* Adding a Container through the Rancher UI

### Preparing a Linux Host
Before you begin, you'll need a single Linux host with Docker v17.06 installed.

#### To Prepare a Linux Host:
1. Prepare a Linux host with 64-bit Ubuntu 16.04, at least 4GB of memory, and a kernel of 3.10+.
2. Install Docker v16.07 on the host. To install Docker on the server, follow the instructions from [Docker](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/).

### Launching Rancher Server
It only takes one command and a few minutes to install and launch Rancher Server. Once installed, you can open a web browser to access the Rancher UI.

#### To Launch Rancher Server:
1. Run this Docker command on your host:

```bash
$ sudo docker run -d –restart=unless-stopped -p 8080:8080 rancher/server:stable
```
>**Note:** This process might take several minutes to complete. For the Rancher v2.0 tech preview, we'll be replacing `stable` with a different string.

2. To access the Rancher UI, go to `http://<SERVER_IP>:8080`, replacing `<SERVER_IP>` with the IP address of your host. The Welcome page displays.

>**Note:** Initially, Rancher creates a **Default** cluster and environment for you.

3. Rancher automatically deploys and manages Kubernetes. Select one of these options for adding hosts:
  * **Add Hosts** -- Select this option if you want to manage hosts in Rancher. To add an existing host with Docker installed or a new host through a supported cloud provider, continue to the **Adding Hosts** section below.
  * **Use existing Kubernetes** -- Select this option if you want the cluster provider to manage hosts outside Rancher. To import an existing Kubernetes installation, continue to the **Importing Kubernetes** section below.

### Adding Hosts
You can either add a host from a cloud hosting provider that Rancher v2.0 supports, or you can add a custom host. If we do not support your particular cloud provider, don't worry. Simply use the custom host option.

If you're adding a custom host, note these requirements:
* Typically, Rancher automatically detects the IP address to register the host.
  * If the host is behind a NAT or the same machine that is running the `rancher/server` container, you might need to explicitly specify its IP address by clicking **Show advanced options**.
* The host agent initiates a connection to the server, so make sure firewalls or security groups allow it to reach the URL in the command.
* All hosts in the environment must to allow traffic between each other for cross-host networking
  * IPSec: `500/udp` and `4500/udp`
  * VXLAN: `4789/udp`

#### To Add a Host from a Supported Cloud Provider:
1. On the Add Hosts page, select your cloud hosting provider:
   * Amazon EC2
   * Microsoft Azure
   * DigitalOcean
   * Packet

2. Follow the instructions in the Rancher UI to add your host. This process might take a few minutes to complete. Once your host is ready, you can view its status on the Hosts page.

#### To Add a Custom Host:
1. On the Add Hosts page, click **Custom**. A `docker` command displays. For example:
   ```bash
   sudo docker run --rm --privileged -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/rancher:/var/lib/rancher rancher/agent:v2.0-alpha2
   http://<SERVER_IP>:8080/v3/scripts/D5433C26EC51325F9D98:1483142400000:KvILQKwz1N2MpOkOiIvGYKKGdE
   ```

   >**Note:** The IP address in the command must match your `<SERVER_IP>` and must be reachable from inside your host.

2. To register your host with Rancher, copy, paste, and run the `docker` command on your host. This process might take a few minutes to complete.
3. Click **Close**. On the Hosts page, you can view the status of your host.

### Importing Kubernetes Clusters

In Rancher v2.0, you can import an existing, external installation of Kubernetes v1.7+. In this scenario, the cluster provider manages your hosts outside of Rancher. We support hosted services like Google Container Engine, Azure Container Service, IBM Bluemix, and bring-your-own-Kubernetes installations.

#### To Import a Kubernetes Cluster:
1. A `kubectl` command displays in the UI. Copy, paste, and execute this command against your Kubernetes cluster. This process might take a few minutes to complete.
2. Click **Close**. On the Hosts page, you can view the status of your Kubernetes nodes.

### Adding Containers

After adding at least one host or cluster to your environment, you're ready to create your first container.

#### To Add a Container:
1. On the Rancher UI menu, click **Containers**.
2. Click **Add Container**. The Add Container page displays.
3. Enter a **Name**, such as "first-container."
4. Enter a **Docker Image** hosted on Docker Hub.
5. Click **Launch**. This process might take a few minutes to complete. Once your container starts running, you can view its status on the Containers page.

Now that you've added hosts and your first container is up and running, you can check out the rest of our new features in Rancher v2.0.
