# ka - Kubernetes Anywhere

Launch Kubernetes in Docker in one `ka up` command.

```
> ka up

```
It works with `Docker for Mac` and is blazzing fast.

This script automates the process described [here](https://github.com/weaveworks/kubernetes-anywhere/blob/master/DOCKER_FOR_MAC.md)

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
