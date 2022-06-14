## OpenCR1.0 ファームウェアリカバリー手順
TurtleBot3が正常に動作しない場合、セットアップ中にOpenCR1.0のファームウェア書き込みに失敗した際には、以下の手順に従ってふopenCR1.0のファームウェアリカバリーを行ってください。

### 前提条件
- OpenCR1.0はRaspberry Piに予めUSBケーブルで接続されていること。<br>
※このドキュメントはTurtleBot3内蔵のRaspberry PiとOpenCR1.0が接続されている前提で書かれています。
- リモートPCからTurtlebot3のRaspberry Piにリモート接続していること。

### OpenCR1.0 ブートローダーの起動
1. **PUSH SW2**を押したままにする。
2. **PUSH SW2**を押したまま**RESET**を押す。
3. **PUSH SW2**は押したまま**RESET**を離す。
4. 最後に**PUSH SW2**を離す。
5. OpenCR1.0上のステータスLED(緑)が100ms周期で点滅したらブートローダーの起動成功です。

![image](https://user-images.githubusercontent.com/5852451/173596559-43dbc98e-3875-4a34-84b7-4028c453e606.png)
![image](https://user-images.githubusercontent.com/5852451/173597002-115b362b-2ef3-406e-9347-25017e1fb58d.png)

上記の手順により、OpenCRはリセット後にブートローダーが起動します。ブートローダー動作中は、OpenCR上のステータスLED（緑）が100msごとに点滅します。
ブートローダーが起動している間に、下記のコマンドを実行しOpenCR1.0にファームウェアを書き込んでください。

### OpenCR1.0ファームウェアリカバリーコマンド(RaspberryPiの操作)※ブートローダー動作中に行う
```
$ sudo dpkg --add-architecture armhf
$ sudo apt-get update
$ sudo apt-get install libc6:armhf
$ export OPENCR_PORT=/dev/ttyACM0
$ export OPENCR_MODEL=burger
$ rm -rf ./opencr_update.tar.bz2
$ wget
https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/op
encr_update.tar.bz2
$ tar -xvf opencr_update.tar.bz2
$ cd ./opencr_update
$ ./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr　
```

以下のようなメッセージが表示されれば、ファームウェアのリカバリーは成功です。
![image](https://user-images.githubusercontent.com/5852451/173600231-e9768b8c-5bf1-4b36-a91f-bd907511909b.png)

### 参考資料
OpenCRのファームウェアリカバリー手順は、[OpenCR1.0公式マニュアル(日本語)](https://emanual.robotis.com/docs/en/parts/controller/opencr10_jp/#%E3%83%AA%E3%83%95%E3%82%A1%E3%83%AC%E3%83%B3%E3%82%B9)に記載しています。

