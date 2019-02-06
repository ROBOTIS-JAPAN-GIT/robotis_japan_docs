## Raspberry Pi 3 B+ へ UbuntuMATEをインストール


### 1. はじめに
2019/01/31では、UbuntuMATE(16.04.2)がRaspBerry Pi 3 Model B +へ対応していない。
Raspberry Pi 3 Model B+ へ UbuntuMATE(16.04.2)のイメージを書き込んだSDカードを挿入して起動するとブートせず、 虹色のテストパターンの画面で止まってしまう。
そのため、UbuntuMATEを起動するためにRaspbianから必要な起動イメージをコピーし起動する手順を記載する。
<br>
※1 弊社、e-manualではRaspbianを推奨しており、やむを得なくUbuntuMATE(16.04.2)を使用したい場合に限ります。
<br>
※2 本手順でのイメージ作成は、保証の限りではないため自己責任で実施してください。
### 2. 事前準備
以下のリンクからRaspbianをダウンロードし、イメージを作成する。
<br>
[Raspbian](https://www.raspberrypi.org/downloads/raspbian/)

インストール手順は、下記を参考。
<br>
[Installing operating system images](https://www.raspberrypi.org/documentation/installation/installing-images/)

作成したイメージから、以下のファイルをコピーしておく。
<br>
boot
- bootcode.bin
- fixup.dat
- start.elf
- kernel7.img
- bcm2710-rpi-3-b-plus.dtb

rootfs
- /lib/modules/*-v7+
- /lib/firmware/brcm
### 3. 使用環境
- Linux PC(Ubuntu 16.04.5 LTS)
- Raspberry Pi 3 Model B+
- SDカード(16GB)
- Raspberry Pi用の電源 5V 3.0A(AD-K50P300)

### 4. 手順
#### 4.1. UbuntuMATEのイメージ作成
以下のリンクからUbuntuMATEのイメージをダウンロードする。
<br>
[Ubuntu MATE 16.04.2(Xenial)](https://ubuntu-mate.org/download/)

ダウンロード後、以下のコマンドで解凍する。
```
$ unxz ubuntu-mate-16.04.2-desktop-armhf-raspberry-pi.img.xz
```

イメージをSDカードへ書き込むためのツールをインストールする。
```
$ sudo apt-get install gnome-disk-utility
```

GNOME Disksを起動する。
```
$ gnome-disks
```
以下の動画を参考に、SDカードにUbuntuMATEのイメージを書き込む。

[Using GNOME Disks](https://www.youtube.com/embed/V_6GNyL6Dac)

#### 4.2. 必要なファイルをコピー
#### 4.2.1. PI_BOOTへのコピー
取得した firmware-master/boot の以下のファイルをPI_BOOTへコピーする。
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

#### 4.2.2. PI_ROOTへのコピー
取得した firmware-master/modules/*-v7+ を PI_ROOT/lib/modules にコピーする。
```
$ cp -r *-v7+/ /media/user_name/PI_ROOT/lib/modules/
$ cp -r brcm /media/user_name/PI_ROOT/lib/firmware
```
### 5. おわりに
上記の手順で作成したイメージでUbuntuMATEが起動できる。

### 6. 参考
[Ubuntu image for the new Raspberry Pi 3 B+](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=208538)
<br>
[[SOLVED] Raspberry Pi 3 B+ Wifi NIC not found](https://www.linuxquestions.org/questions/slackware-arm-108/raspberry-pi-3-b-wifi-nic-not-found-4175627137/)

