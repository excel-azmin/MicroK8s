# MicroK8s Quickstart with Kubectl

* Install MicroK8s on Linux

```
sudo snap install microk8s --classic
```  

* Check the status while Kubernetes starts

```
microk8s status --wait-ready
```

* Turn on the services you want

```
microk8s enable dashboard
microk8s enable dns
microk8s enable registry
microk8s enable istio
```

* Start using Kubernetes

```
microk8s dashboard-proxy
```

* Start and stop Kubernetes to save battery

  Kubernetes is a collection of system services that talk to each other all the time. If you don't need them running in the background then you will save battery by stopping them. `microk8s start` and `microk8s stop` will do the work for you.

# Install and Set Up kubectl on Linux

  * Download the latest release with the command:
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

**Note:**

To download a specific version, replace the $(curl -L -s https://dl.k8s.io/release/stable.txt) portion of the command with the specific version.

For example, to download version 1.30.0 on Linux x86-64, type:

```
curl -LO https://dl.k8s.io/release/v1.30.0/bin/linux/amd64/kubectl
```

And for Linux ARM64, type:

```
curl -LO https://dl.k8s.io/release/v1.30.0/bin/linux/arm64/kubectl
```

* Validate the binary (optional)
  
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
```

* If valid, the output is:

```
kubectl: OK
```

* If the check fails, sha256 exits with nonzero status and prints output similar to:

```
kubectl: FAILED
sha256sum: WARNING: 1 computed checksum did NOT matc
```

* Install kubectl

```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

**Note:**

If you do not have root access on the target system, you can still install kubectl to the `~/.local/bin` directory:

```
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
# and then append (or prepend) ~/.local/bin to $PATH
```

**To use MicroK8s with your existing kubectl:**

```
sudo microk8s kubectl config view --raw > $HOME/.kube/config
```

* Now use the MicroK8s with kubectl

```
kubectl get ns
```

```
azmin@excel:~$ kubectl get ns
NAME              STATUS   AGE
default           Active   24m
kube-node-lease   Active   24m
kube-public       Active   24m
kube-system       Active   24m

``



