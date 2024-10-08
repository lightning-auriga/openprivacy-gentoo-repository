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
root # emaint sync --repo openprivacy
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
root # echo 'net-im/cwtch ~amd64' >> /etc/portage/package.accept_keywords/cwtch.conf
root # emerge -a net-im/cwtch
```

## Removal of cwtch

To uninstall cwtch with portage:

```bash
root # emerge --depclean -a net-im/cwtch
root # emerge --depclean -a
```
