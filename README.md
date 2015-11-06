This project is a Ubuntu DKMS package for the Broadcom wireless
driver found at http://www.broadcom.com/support/?gid=1

The patches are applied on install of the Ubuntu package. This means you
have to build the Ubuntu package.

## Ubuntu repository (PPA)

I keep built packages at my [bcmwl PPA](https://launchpad.net/~longsleep/+archive/ubuntu/bcmwl).

```bash
sudo add-apt-repository ppa:longsleep/bcmwl
sudo apt-get update
sudo apt-get install bcmwl-kernel-source
```

## Build instructions

The repository uses [git-buildpackage](http://honk.sigxcpu.org/projects/git-buildpackage/manual-html/gbp.html)
with pristine-tar and upstream branch. It follows closely the original
Ubuntu packaging and updates the driver to latest version with patches to make
it compile on modern Kernels.

```bash
sudo apt-get install git-buildpackage
mkdir bcmwl-ubuntu
cd bcmwl-ubuntu
git clone https://github.com/longsleep/bcmwl-ubuntu.git bcmwl-ubuntu-master
cd bcmwl-ubuntu-master
gbp buildpackage -b -uc -us
ls ../*.deb
../bcmwl-kernel-source_6.30.223.271+bdcom-1longsleep0_amd64.deb
sudo dpkg -i ../bcmwl-kernel-source_6.30.223.271+bdcom-1longsleep0_amd64.deb
```

This will build a Ubuntu package for Ubuntu 14.04 or later. The Kernel module
will build automatically for all your installed Kernel versions with the
help of DKMS and apply patching as required after the package is installed
on the target system.

If you have problems or questions add them to the GitHub tracker
at https://github.com/longsleep/bcmwl-ubuntu/issues - i will try to reply.
