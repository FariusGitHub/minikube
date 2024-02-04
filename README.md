# Minikube<br>
Minikube is an open-source tool that allows developers to run a single-node Kubernetes cluster on their local machine. It is designed to simplify the process of setting up and managing a Kubernetes environment for development and testing purposes. Minikube provides a lightweight and isolated Kubernetes environment, allowing developers to quickly deploy and test their applications without the need for a full-scale production cluster. It supports various features of Kubernetes, such as creating and managing pods, services, and deployments. Minikube is widely used by developers to learn, experiment, and develop applications for Kubernetes.

![](/images/06-image01.jpg)
<br><br>

## INSTALLATION
Let's start with installation which usually located at minikube.sigs.k8s.io/docs/start/

```txt
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                  Dload  Upload   Total   Spent    Left  Speed
  100 89.3M  100 89.3M    0     0  20.8M      0  0:00:04  0:00:04 --:--:-- 20.8M

minikube start
W0131 22:57:06.541855   12098 main.go:291] Unable to resolve the current Docker CLI context "default": context "default": context not found: open /home/devops/.docker/contexts/meta/37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f/meta.json: no such file or directory
😄  minikube v1.32.0 on Ubuntu 23.10
✨  Automatically selected the docker driver. Other choices: qemu2, none, ssh
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.28.3 preload ...
    > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 27.86 M
    > gcr.io/k8s-minikube/kicbase...:  453.90 MiB / 453.90 MiB  100.00% 19.42 M
🔥  Creating docker container (CPUs=2, Memory=3900MB) ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

We can also using a dashboard like below

```txt
minikube dashboard
🔌  Enabling dashboard ...
    ▪ Using image docker.io/kubernetesui/dashboard:v2.7.0
    ▪ Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
💡  Some dashboard features require the metrics-server addon. To enable all features please run:

	minikube addons enable metrics-server	


🤔  Verifying dashboard health ...
🚀  Launching proxy ...
🤔  Verifying proxy health ...
🎉  Opening http://127.0.0.1:44309/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
Opening in existing browser session.
```

![](/images/06-image02.png)
<br>
Figure 2: Example of Minikube Dashboard
<br>

Last thing, let's try to deploy simple yaml file below
```txt
nano deployment.yaml ## copy paste below deployment.yaml 
cat deployment.yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: hello-world
    namespace: default
  spec:
    replicas: 3
    selector:
      matchLabels:
        app: main
    template:
      metadata:
        labels:
          app: main
      spec:
        containers:
        - name: hello-world
          image: psk8s.azurecr.io/hello-app:2.0
          ports:
          - containerPort: 8080

kubectl create -f deployment.yaml
deployment.apps/hello-world created

kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
hello-world-645c45876d-2xb2g   1/1     Running   0          48s
hello-world-645c45876d-4vd6v   1/1     Running   0          48s
hello-world-645c45876d-shsjd   1/1     Running   0          48s
```
And let's see the dashboard again
![](/images/06-image03.png)
<br>
Figure 3: Example of Minikube Dashboard after a deployemnet above 
<br>

## SUMMARY

Minikube is a powerful Kubernetes cluster comparable to K3S and Docker-Desktop Kubernetes cluster. It may not provide all the full functional features for production but a practical tool for proof of concept.

| Feature                | Minikube                            | K3S                                 | Docker-Desktop Kubernetes          |
|------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Installation           | Requires installation of VirtualBox  | Lightweight installation            | Requires installation of Docker     |
| Resource Usage         | High resource usage                  | Low resource usage                   | Moderate resource usage              |
| Cluster Management     | Single-node cluster management       | Single-node or multi-node cluster    | Single-node or multi-node cluster    |
| Scalability            | Limited scalability                 | Scalable                            | Scalable                            |
| High Availability      | Not suitable for high availability   | Supports high availability           | Supports high availability           |
| Networking             | Limited networking options           | Supports multiple networking options | Supports multiple networking options |
| Storage                | Limited storage options              | Supports multiple storage options    | Supports multiple storage options    |
| Monitoring and Logging | Limited monitoring and logging tools | Supports monitoring and logging      | Supports monitoring and logging      |
| Ease of Use            | Easy to use                          | Easy to use                          | Easy to use                          |
| Community Support      | Large community support              | Growing community support            | Large community support              |
| Platform Support       | Supports multiple platforms          | Supports multiple platforms          | Supports multiple platforms          |
| Updates and Upgrades   | Manual updates and upgrades          | Automatic updates and upgrades       | Automatic updates and upgrades       |
| Cost                   | Free                                | Free                                | Free                                |
