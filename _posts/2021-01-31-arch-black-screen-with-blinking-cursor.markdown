---
layout: post
title:  "[Arch Linux] GNOME 설치 후 로그인 화면이 나타나지 않는 문제"
date:   2021-01-31 15:00:00 +0900
categories: linux
---

# 환경
- GPU: AMD Radeon RX 5700XT
- OS: Arch Linux

# 증상
- GNOME 설치 후 아래의 화면과 같이 로그인 화면이 나타나지 않음
![Screenshot from 2021-02-01 07-52-07](https://user-images.githubusercontent.com/67717313/106400675-32197080-6463-11eb-8ebc-4a107dc21b9a.png)

- tty2(Ctrl+Alt+F2)로 변경 후 다시 tty1(Ctrl+Alt+F1)로 변경 시 GUI 로그인 화면이 나옴

# 해결
tty2 진입 후 KMS(Kernel mode stting)를 변경하여 initramfs 단계에서 KMS가 활성화 되도록 수정

- tty2 진입
	- Ctrl+Alt+F2

- /etc/mkinitcpio.conf 파일 열기
	- sudo vim /etc/mkinitcpio.conf
-  7번 라인의 MODULES에 Driver 추가 
	- AMD : amdgpu
	- Intel : i915

```
  1 # vim:set ft=sh
  2 # MODULES
  3 # The following modules are loaded before any boot hooks are
  4 # run.  Advanced users may wish to specify all system modules
  5 # in this array.  For instance:
  6 #     MODULES=(piix ide_disk reiserfs)
  7 MODULES=() -> MODULES=(amdgpu)
  8 

```

- initramfs 재생성
	- sudo mkinitcpio -P 


```shell
[hello@archlinux]$ sudo mkinitcpio -P
[sudo] password for hello: 

==> Building image from preset: /etc/mkinitcpio.d/linux.preset: 'default'
  -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux.img
==> Starting build: 5.10.11-arch1-1
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [autodetect]
  -> Running build hook: [modconf]
  -> Running build hook: [block]
==> WARNING: Possibly missing firmware for module: xhci_pci
  -> Running build hook: [filesystems]
  -> Running build hook: [keyboard]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating gzip-compressed initcpio image: /boot/initramfs-linux.img
==> Image generation successful
==> Building image from preset: /etc/mkinitcpio.d/linux.preset: 'fallback'
  -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-fallback.img -S autodetect
==> Starting build: 5.10.11-arch1-1
  -> Running build hook: [base]
  -> Running build hook: [udev]
  -> Running build hook: [modconf]
  -> Running build hook: [block]
==> WARNING: Possibly missing firmware for module: wd719x
==> WARNING: Possibly missing firmware for module: aic94xx
==> WARNING: Possibly missing firmware for module: xhci_pci
  -> Running build hook: [filesystems]
  -> Running build hook: [keyboard]
  -> Running build hook: [fsck]
==> Generating module dependencies
==> Creating gzip-compressed initcpio image: /boot/initramfs-linux-fallback.img
==> Image generation successful
```

- reboot

# 참고
- [Kernel mode setting](https://wiki.archlinux.org/index.php/kernel_mode_setting#Early_KMS_start)
- [mkinitcpio](https://wiki.archlinux.org/index.php/Mkinitcpio#Image_creation_and_activation)
