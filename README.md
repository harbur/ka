# ka - Kubernetes Anywhere

Launch Kubernetes in Docker in one `ka up` command.

```
➜  ~ ka up
Starting Weave Network.... [PASS]
Starting Kubernetes....... [PASS]
Setup Kubernetes Addons... [PASS]
Starting SOCKS proxy...... [PASS]
Configure Kube client..... [PASS]
➜  ~ kubectl cluster-info
Kubernetes master is running at http://localhost:8080
KubeDNS is running at http://localhost:8080/api/v1/proxy/namespaces/kube-system/services/kube-dns
```

It works with `Docker for Mac` and is blazzing fast.

This script automates the process described [here](https://github.com/weaveworks/kubernetes-anywhere/blob/master/DOCKER_FOR_MAC.md)

# Prerequisites

You'll need Docker and Weave Net to bootstrap Kubernetes using this script. This works best using [Docker for Mac](https://blog.docker.com/2016/03/docker-for-mac-windows-beta/).

* [Install Docker](https://www.docker.com/)

* [Install Weave Net](https://www.weave.works/install-weave-net/)

```
sudo curl -L git.io/weave -o /usr/local/bin/weave
sudo chmod +x /usr/local/bin/weave
```

* [Kubectl client](http://kubernetes.io/docs/getting-started-guides/binary_release/)

```
brew install kubernetes-cli
```

# Process

The script will check and launch Weave Net for you, Kubernetes as a single-node, Add `kube-system` namespace and DNS Addon, launch a SOCKS 
proxy to get Pod and Service IPs connectivity and configure your kubectl client `kubernetes-anywhere` context and set it as default.

After launching the script you simply use the `kubectl` to manage your cluster from your machine.

# Configure Proxy


`ka` launches a SOCKS proxy automatically that you can use to get visibility of the Pod and Service IPs.

To use it simply add the following `proxy.pac` to your Network configuration:

```
function FindProxyForURL(url, host) {
    PROXY = "SOCKS 127.0.0.1:1080"

    // Kubernetes via Proxy
    if (isInNet(host, "10.0.0.0", "255.0.0.0")) {
        return PROXY;
    }

    // Everything else directly!
    return "DIRECT";
}
```

The configuration is stored [here](https://gist.githubusercontent.com/spiddy/e54ef788c516e935daeba2a5cb80a2d7/raw/3203f6213ec39b6f5cce2ad28cdce0ff1e4a3ebe/proxy.pac
) you can reference the URL directly.

# Inspired by

* [k8s-anywhere-local.sh](https://gist.github.com/errordeveloper/e46a67c819c92016225353cb7a17891e)
* [kid](https://github.com/vyshane/kid) 
