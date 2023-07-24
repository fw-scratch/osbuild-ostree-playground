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
# Build minimal image
make cs9-qemu-minimal-ostree.$(arch).qcow2

# Build image with extra packages
make cs9-qemu-minimal-ostree.$(arch).qcow2 DEFINES='extra_rpms=["vim","wget","curl","zsh"]'

# Build repo to serve as a remote
make cs9-qemu-minimal-ostree.$(arch).repo DEFINES='extra_rpms=["strace"]'  OSTREE_REPO=ostree-repo
```

See [Updating an OSTree-based image](https://sigs.centos.org/automotive/building/updating_ostree/)

```
osbuild-mpp -I . -D image_type="\"ostree\"" -D arch=\"x86_64\" -D distro_name="\"cs9\"" -D target="\"qemu\""    images/minimal.mpp.yml _build/cs9-qemu-minimal-ostree.x86_64.json
sudo rm -rf _build/image_output/qcow2
mkdir -p _build/image_output/qcow2
sudo osbuild --checkpoint build --store _build/osbuild_store --output-directory _build/image_output --export qcow2 _build/cs9-qemu-minimal-ostree.x86_64.json

```
