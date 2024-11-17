
> [!NOTE]
> This document is written based on the `Docker version 27.3.1, build ce12230`.

## Install

### MAC

It can be installed via `brew`.

```
brew install --cask docker
```

> [!NOTE]
> Before using the `docker` command in the CLI, you need to start the Docker daemon by launching the Docker Desktop application.
> When launching the Docker Desktop application for the first time, it will prompt for the installation of the Docker Desktop application.
> During the installation, it will ask to install in whether under the user home or the system directory.

## Add custom registry

Add the endpoint to the `~/.docker/daemon.json` file.

For example, add the [microk8s's built-in `registry`](https://microk8s.io/docs/registry-built-in):

```
$ microk8s kubectl get services -n container-registry 
NAME       TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
registry   NodePort   10.152.183.133   <none>        5000:32000/TCP   10d
```

If it is running in `microk8s-vm` launched by `multipass`, use the IPv4 address of `microk8s-vm`, else, use `localhost`.

```
$ multipass info
Name:           microk8s-vm
State:          Running
Snapshots:      0
IPv4:           192.168.64.1
                10.1.254.64
...
```

Add the endpoint to the `insecure-registries` property in the `~/.docker/daemon.json` file.

```
{
  ...
  "insecure-registries": [
    "localhost:32000" // if it's an ubuntu host
    "192.168.64.1:32000" // for multipass + microk8s-vm
  ]
}
```

Finally, restart the docker daemon by restarting the Docker Desktop application.
