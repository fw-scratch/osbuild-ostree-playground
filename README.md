# Vagrant setup to build ostree images using osbuild

## Setup steps

Run `vagrant up` and `vagrant ssh`

Inside the vagrant vm, run:

1. In `~/osbuild`:

```
make rpm
sudo dnf install ./rpmbuild/RPMS/noarch/*.rpm
```

2. In `~/centos-automotive-sample-images/osbuild-manifests`:

```
make cs9-qemu-minimal-ostree.x86_64.qcow2
```