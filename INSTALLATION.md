# Installation

We have two different ways to experience Pouch, one for end-users, the other for developers. In the former one, installation can help you with Pouch installing out of box. The latter one is for those who wish to get involved in Pouch with hacking.

If you wish to experience Pouch, please choose [End User Quick-Start](#end-user-quick-start). And if you are looking forward to becoming a hacker, [Developer Quick-Start](#developer-quick-start) is a must-read for you.

## End User Quick-Start

You can install Pouch automatically on your machine with very few steps. Currently we support two kinds of Linux Distribution: Ubuntu and CentOS.

## Ubuntu

To be added.

## CentOS

To be added.

## Developer Quick-Start

As a developer, you may need to build and test Pouch binaries via source code. To build pouchd which is so-called "pouch daemon" and pouch which is so-called "pouch cli", the following build system dependencies are required:

* Go 1.9.x or above
* Linux Kernel 3.10+ 

First, clone the repository and checkout whichever branch you like (in the following example, checkout branch master):

``` shell
$ git clone https://github.com/alibaba/pouch.git
$ cd pouch
$ git checkout master
```

Second, build and install pouch binaries (pouchd and pouch). With the required dependencies installed, the Makefile target named build will compile the pouch and pouchd binaries in current work directory. Or you can just execute `make install` to build binaries and install them in destination directory (/usr/local/bin by default).

``` shell
$ make install
```

Third, install containerd, runc and runv binaries. Since pouchd is a kind of container engine, and pouch is a cli tool, if you hope to experience container management ability via Pouch, there are several additional binaries needed:

* [containerd](https://github.com/containerd/containerd): an industry-standard container runtime;
* [runc](https://github.com/opencontainers/runc): a CLI tool for spawning and running containers according to the OCI specification;
* [runv](https://github.com/hyperhq/runv): a hypervisor-based runtime for OCI.

Here are the versions of these binaries which we suggest you should lock to:

```
containerd: 1.0.0-beta.3 
runc: 1.0.0-rc4
runv: 1.0.0
```

You can use the following command to install containerd:

``` shell
$ wget https://github.com/containerd/containerd/releases/download/v1.0.0-beta.3/containerd-1.0.0-beta.3.linux-amd64.tar.gz
$ tar -xzvf containerd-1.0.0-beta.3.linux-amd64.tar.gz -C /usr/local
```

You can refer to [runV installation](https://github.com/hyperhq/runv#build) and [runC installation](https://github.com/opencontainers/runc#building)

Forth, with all needed binaries installed, we could start pouchd via:

``` shell
$ pouchd
INFO[0000] starting containerd                           module=containerd revision=a543c937eb0a05e1636714ee2be70819d745b960 version=v1.0.0-beta.2
INFO[0000] setting subreaper...                          module=containerd
INFO[0000] loading plugin "io.containerd.content.v1.content"...  module=containerd type=io.containerd.content.v1
INFO[0000] loading plugin "io.containerd.snapshotter.v1.btrfs"...  module=containerd type=io.containerd.snapshotter.v1
WARN[0000] failed to load plugin io.containerd.snapshotter.v1.btrfs  error="path /var/lib/containerd/io.containerd.snapshotter.v1.btrfs must be a btrfs filesystem to be used with the btrfs snapshotter" module=containerd
INFO[0000] loading plugin "io.containerd.snapshotter.v1.overlayfs"...  module=containerd type=io.containerd.snapshotter.v1
INFO[0000] loading plugin "io.containerd.metadata.v1.bolt"...  module=containerd type=io.containerd.metadata.v1
WARN[0000] could not use snapshotter btrfs in metadata plugin  error="path /var/lib/containerd/io.containerd.snapshotter.v1.btrfs must be a btrfs filesystem to be used with the btrfs snapshotter" module="containerd/io.containerd.metadata.v1.bolt"
INFO[0000] loading plugin "io.containerd.differ.v1.walking"...  module=containerd type=io.containerd.differ.v1
INFO[0000] loading plugin "io.containerd.grpc.v1.containers"...  module=containerd type=io.containerd.grpc.v1
```

After pouchd's running, you could interact with pouchd by pouch cli:

```
$ pouch images ls
IMAGE ID             IMAGE NAME                                               SIZE
3e8fa85ddfef         docker.io/library/busybox:latest                         2699
504cf109b492         docker.io/library/redis:alpine                           2035
```

## Feedback

We hope this guide would help you get up and run with Pouch. And feel free to send feedback via [ISSUE](https://github.com/alibaba/pouch/issues/new), if you have any questions. If you wish to contribute to Pouch on this guide, please just submit a pull request.
