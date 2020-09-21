---
title: "HOWTO install Prometheus & Grafana on a single host with microk8s"
subtitle: ""
date: 2020-09-18T15:00:29-07:00
lastmod: 2020-09-18T15:00:29-07:00

tags:
  - Devops

featuredImage: ""
featuredImagePreview: ""

toc:
  enable: false
lightgallery: false
---
I wanted to get Prometheus and Grafana up and running on a development machine but I didn't want to get bogged down by the specifics of how to run Kubernetes.

I found [`microk8s` by Canonical](https://microk8s.io/) and I was pleased to find out that it made things really simple to set up the entire k8s stack and Prometheus and Grafana on a single machine.
<!--more-->

# Getting Started
I did my setup on  a fresh install of Ubuntu 20.04.1 LTS, but these instructions should work on any recent version of Ubuntu.

First, install the microk8s snap package
```bash
$ sudo snap install microk8s --classic
```

Then, you can list all of the add-ons that are shipped with microk8s.
```bash
$ microk8s.status
```

None of these are enabled by default. So to run Prometheus and Grafana, you will have to enable them.
```bash
$ microk8s.enable dashboard prometheus
```

That should install the Kubernetes dashboard as well as Prometheus & Grafana.

$ Optional Alias
The next step is completely optional, but it makes me type less so I'm going to do it:
```bash
$ sudo snap alias microk8s.kubectl kubectl
```
Most of the upcoming commands are going to be `microk8s.kubectl` commands, so the above alias allows us to just use `kubectl` instead of typing out the entire `microk8s.kubectl` command.

# Accessing the Kubernetes Dashboard
To access the dashboard, you need to get your access token. To do so:
```bash
$ kubectl describe secret
Name:         default-token-8vptq
Namespace:    default
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: default
              kubernetes.io/service-account.uid: 4c6fbee3-beca-4ecb-9ea5-91a30c1b77dc

Type:  kubernetes.io/service-account-token

Data
====
token:      XXXXXXXXXXXXXXXX
```
With a fresh installation of Kubernetes, there should only be one secret: the default token.
You want to copy the `token` field into your clipboard.

Finally, you want open up a secure channel to the cluster:
```bash
$ kubectl proxy &
```

Finally, going to:
```
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
```
Should give you access to the dashboard. Use the token in your clipboard to login!

{{< admonition type=tip title="If you're SSHed into a machine, then you need to port forward" open=true >}}
If you're going through this HOWTO on a remote host via SSH, you're going to need to forward the port via SSH like so:
```
$ ssh -L 8001:localhost:8001 hostname
```
Then the above link in your browser should work!
{{< /admonition >}}

# Exploring kubectl commands
Here are some commands to get you started exploring the Kubernetes CLI:
```
$ kubectl get services -n monitoring
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
prometheus-operator     ClusterIP   None             <none>        8443/TCP                     2d19h
alertmanager-main       ClusterIP   10.152.183.141   <none>        9093/TCP                     2d19h
grafana                 ClusterIP   10.152.183.237   <none>        3000/TCP                     2d19h
kube-state-metrics      ClusterIP   None             <none>        8443/TCP,9443/TCP            2d19h
node-exporter           ClusterIP   None             <none>        9100/TCP                     2d19h
prometheus-adapter      ClusterIP   10.152.183.70    <none>        443/TCP                      2d19h
prometheus-k8s          ClusterIP   10.152.183.137   <none>        9090/TCP                     2d19h
alertmanager-operated   ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP   2d19h
prometheus-operated     ClusterIP   None             <none>        9090/TCP                     2d19h
$ kubectl get pods -n monitoring
NAME                                   READY   STATUS    RESTARTS   AGE
prometheus-adapter-557648f58c-z8jf5    1/1     Running   0          2d19h
prometheus-operator-5b7946f4d6-5jkbw   2/2     Running   0          2d19h
grafana-7c9bc466d8-r6b88               1/1     Running   0          2d19h
node-exporter-hnvfl                    2/2     Running   0          2d19h
kube-state-metrics-66b65b78bc-mjj5q    3/3     Running   0          2d19h
alertmanager-main-0                    2/2     Running   0          2d19h
prometheus-k8s-0                       3/3     Running   1          2d19h
```

# Accessing Prometheus
You need to port-forward to enable external access:
```bash
$ kubectl port-forward -n monitoring service/prometheus-k8s --address 0.0.0.0 9090:9090
```
Then you should be able to access the Prometheus UI on `http://localhost:9090`. No username/password is required.

# Accessing Grafana
You need to port-forward to enable external access:
```bash
$ kubectl port-forward -n monitoring service/grafana --address 0.0.0.0 3000:3000 
```
Then you should be able to access the Grafana UI on `http://localhost:3000`. The default credentials are:
```
username: admin
password: admin
```
Grafana should come pre-configured with Prometheus as a data source.

# References:
- https://readyspace.co.id/en/remote-monitoring-at-the-edge-with-microk8s/
- https://www.server-world.info/en/note?os=Ubuntu_20.04&p=microk8s&f=8
