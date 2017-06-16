# lora-feed
Semtech packages for OpenWRT/LEDE.
This repository is originated from [this](https://github.com/JiapengLi/OpenWrt-lora)

## Table of Contents

- [Patch](#patch)
- [Install](#install)
- [Contribute](#contribute)
- [License](#license)

## Patch
packet-forwarder requires function qsort_r which is not avaiable in neither musl library 1.1.15 nor 1.1.16.
We need [patch](https://github.com/xueliu/lora-feed/blob/master/101-added_qsort_r.patch) the toolchain to support qsort_r.

    $ cp 101-added_qsort_r.patch $SOURCE_TREE/toolchain/musl/patches
    $ make toolchain/clean
    $ make toolchain/compile
    $ make toolchain/install
Note: Please make sure that the musl library is updated in the file system.

## Install

Edit your feeds.conf or feed.conf.default and add the following to it:

    # Semtech
    src-git lora https://github.com/asd268/lora-feed

Update your build environment and install the package:

    $ scripts/feeds update lora
    $ scripts/feeds install lora
    $ make menuconfig

Go to Utilities, select lora-gateway and packet-forwarder;

Exit, save and build

    $ make package/lora-gateway/install
    $ make package/packet-forwarder/install

Following two packages are only working on Raspberry Pi
 
    $ make package/wiringpi/install
    $ make package/single_chan_pkt_fwd/install

## Contribute

Found a bug? Please create an issue on GitHub:
    https://github.com/xueliu/lora-feed/issues

Further tests and PR's are welcome and appreciated.

## License

GPLv2
