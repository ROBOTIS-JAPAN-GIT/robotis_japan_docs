## Raspberry Pi 3 B+ へ UbuntuMateをインストール


### 1. はじめに
2019/01/31では、UbuntuMate(16.04.2)がRaspBerry Pi 3 Model B +へ対応していない.
そのためRaspberry Pi 3 Model B+ へ UbuntuMate(16.04.2)のイメージを書き込んだSDカードを挿入して起動するとブートせず, 虹色のテストパターンの画面で止まってしまう. 
そのため,UbuntuMATEを起動するためにRaspbianから必要な起動イメージをコピーし起動する手順を記載する.

※本手順で作成したイメージは、保証の限りではない。
### 2. 事前準備
以下のリンクからRaspbianをダウンロードし,イメージを作成する.

[Raspbian](https://www.raspberrypi.org/downloads/raspbian/)

インストール手順は、下記を参考.

[Installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/)

作成したイメージから,以下のファイルをコピーしておく.

boot
- bootcode.bin
- fixup.dat
- start.elf
- kernel7.img
- bcm2710-rpi-3-b-plus.dtb

rootfs
- /lib/modules/*-v7+
- /lib/firmware/brcm


### 2. 使用環境
・Linux PC(Ubuntu 16.04.5 LTS)

・Raspberry Pi 3 Model B+

・SDカード(16GB)

・Raspberry Pi用の電源 5V 3.0A(AD-K50P300)

### 3. 手順
#### 3.1. UbuntuMateのイメージ作成

以下のリンクからUbuntuMateのイメージをダウンロードする.

[Ubuntu MATE 16.04.2(Xenial)](https://ubuntu-mate.org/download/)

ダウンロード後、以下のコマンドで解凍する.
```
$ unxz ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz
```

イメージをSDカードへ書き込むためのツールをインストールする.
```
$ sudo apt-get install gnome-disk-utility
```

GNOME Disksを起動する。
```
$ gnome-disks
```
以下の動画を参考に、SDカードにUbuntuMATEのイメージを書き込む.

[Using GNOME Disks](https://www.youtube.com/embed/V_6GNyL6Dac)

### 3.2. 必要なファイルをコピー
#### 3.2.1. PI_BOOTへのコピー

取得した firmware-master/boot の以下のファイルをPI_BOOTへコピーする.
- bootcode.bin
- fixup.dat
- start.elf
- kernel7.img
- bcm2710-rpi-3-b-plus.dtb
```
$ cp bootcode.bin /media/user_name/PI_BOOT/
$ cp fixup.dat /media/user_name/PI_BOOT/
$ cp start.elf /media/user_name/PI_BOOT/
$ cp kernel7.img /media/user_name/PI_BOOT/
$ cp bcm2710-rpi-3-b-plus.dtb /media/user_name/PI_BOOT/
```

#### 3.2.2. PI_ROOTへのコピー

取得した firmware-master/modules/*-v7+ を PI_ROOT/lib/modules にコピーする.
```
$ cp -r *-v7+/ /media/user_name/PI_ROOT/lib/modules/
$ cp -r brcm /media/user_name/PI_ROOT/lib/firmware
```
### 4. おわりに
上記の手順で作成したイメージでUbuntuMATEが起動できる.

### 5. 参考
[Ubuntu image for the new Raspberry Pi 3 B+](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=208538)

[[SOLVED] Raspberry Pi 3 B+ Wifi NIC not found](https://www.linuxquestions.org/questions/slackware-arm-108/raspberry-pi-3-b-wifi-nic-not-found-4175627137/)

