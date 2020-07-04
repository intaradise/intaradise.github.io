---
layout: post
title:  "Install RTL8812AU driver in Linux"
date:   2020-07-04 16:16:00 +0900
categories: linux
---

Compatible with RTL8814AU and RTL8821AU

```shell
sudo apt install git dkms
git clone https://github.com/aircrack-ng/rtl8812au.git
cd rtl8812au
sudo ./dkms-install.sh
sudo reboot -f

```