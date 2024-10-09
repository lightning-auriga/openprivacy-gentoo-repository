# openprivacy-gentoo-repository

## Overview

This is a draft gentoo ebuild repository for openprivacy software.

## Local Configuration

### openprivacy gentoo repository

Add the repository with [eselect repository](https://wiki.gentoo.org/wiki/Eselect/Repository):

```bash
## if needed
root # emerge -a dev-vcs/git app-eselect/eselect-repository

root # eselect repository add openprivacy git https://github.com/lightning-auriga/openprivacy-gentoo-repository
root # emaint sync --repo openprivacy ## or the standard emerge --sync
```

### optional features

For the initial draft version of these ebuilds, the only optional feature is backend use of the NetworkManager
D-Bus interface; this is enabled by default, and can be disabled as follows:

```bash
root # echo 'net-im/cwtch-autobindings -networkmanager' > /etc/portage/package.use/cwtch.conf
```

## Installation of [cwtch](https://docs.cwtch.im)

To install cwtch with portage:

```bash
## unmask on amd64
root # echo 'net-im/cwtch-autobindings ~amd64' > /etc/portage/package.accept_keywords/cwtch.conf
root # echo 'net-im/cwtch-bin ~amd64' >> /etc/portage/package.accept_keywords/cwtch.conf
root # emerge -a net-im/cwtch-bin
```

## Removal of cwtch

To uninstall cwtch with portage:

```bash
root # emerge --depclean -a net-im/cwtch-bin
root # emerge --depclean -a
```

## Repository Maintenance

To update an ebuild for a new upstream version, approximately follow these steps:

- copy the existing ebuild under `net-im/cwtch*` to the appropriate new version number
- as needed, update the `SRC_URI` string in the new ebuild file to match the appropriate upstream tarball
- check upstream for new installation patterns or dependencies and update as needed
- from inside the appropriate `net-im` subdirectory, run `GENTOO_MIRRORS="" ebuild ./cwtch*ebuild manifest`
- commit changes and push
