**TurtleBot3 Mobile Manipulator (TB3MM) SW動作確認手順**

**リモートPC セットアップ**

`　`以下の手順を参考にリモートPCのセットアップを行ってください。

`　`<https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup>

`　`※リモートPC側には、TB3MMのパッケージの他にTB3とOM-Xの各パッケージが必要です。

`　`ネットワーク設定は必ず確認してください。

`　`<https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#network-configuration>

**TurtleBot3 MM セットアップ**

` `**1. Raspi image (raspbian)**

`　`以下のサイトからラズパイのイメージを取得し、SDカードに書き込んでください。

`　`<https://www.robotis.com/service/download.php?no=1738>

`　`**SHA256 (image\_rpi\_20190429.img)** :

`　`eb8173f3727db08087990b2c4e2bb211e70bd54644644834771fc8b971856b97

`　`**デフォルトユーザー名：pi**

`　`**デフォルトパスワード：turtlebot**

`　`起動前と起動後に以下のコマンドを入力して、TB3MMのIPを調べることができます。（増えたIPがTB3MMのIP）

`　`ラズパイをディスプレイに接続して、IPアドレスを確認する方法でも問題ありません。


|echo <TurtleBot3が接続されているIP>.{1..254} | xargs -P256 -n1 ping -s1 -c1 -W1 | grep ttl|
| :- |


例


|<p>起動前</p><p>$ echo 192.168.1.{1..254} | xargs -P256 -n1 ping -s1 -c1 -W1 | grep ttl</p><p>9 bytes from 192.168.1.1: icmp\_seq=1 ttl=255</p><p>9 bytes from 192.168.1.2: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.3: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.7: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.11: icmp\_seq=1 ttl=128</p><p>9 bytes from 192.168.1.13: icmp\_seq=1 ttl=128</p><p>9 bytes from 192.168.1.18: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.91: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.200: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.210: icmp\_seq=1 ttl=64</p><p></p><p></p><p>起動後</p><p>$ echo 192.168.1.{1..254} | xargs -P256 -n1 ping -s1 -c1 -W1 | grep ttl</p><p>9 bytes from 192.168.1.1: icmp\_seq=1 ttl=255</p><p>9 bytes from 192.168.1.2: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.3: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.7: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.11: icmp\_seq=1 ttl=128</p><p>9 bytes from 192.168.1.13: icmp\_seq=1 ttl=128</p><p>9 bytes from 192.168.1.17: icmp\_seq=1 ttl=64  <-- これがTB3 MMのIP</p><p>9 bytes from 192.168.1.18: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.91: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.200: icmp\_seq=1 ttl=64</p><p>9 bytes from 192.168.1.210: icmp\_seq=1 ttl=64</p>|
| :- |

`　`イメージは、以下のツールで書き込みができます。Ubuntuに標準で搭載されているDisks（ディスク管理ツール）を使用しても問題ありません。

`　`<https://www.balena.io/etcher/>

` `**2. CPG鍵アップデート**

`　`ROSのCPG鍵が古いため、アップデートしてください。

|$ sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654|
| :- |


|$ sudo apt-get update|
| :- |

` `**3. ssh インストール**

`　`以下のコマンドでsshをインストールしてください。

|$ sudo apt-get install ssh -y|
| :- |



` `**4. ntpdate インストール**

|<p>$ sudo apt-get install ntpdate</p><p>$ sudo ntpdate ntp.ubuntu.com</p>|
| :- |

` `**5. ファイルシステムの拡張**

|$ sudo raspi-config|
| :- |

` `**6. OpenCR1.0 セットアップ**

`　`以下のコマンドを入力してください。

|<p>$ sudo dpkg --add-architecture armhf</p><p>$ sudo apt-get update</p><p>$ sudo apt-get install libc6:armhf</p><p>$ export OPENCR\_PORT=/dev/ttyACM0</p><p>$ export OPENCR\_MODEL=om\_with\_tb3</p><p>$ rm -rf ./opencr\_update.tar.bz2</p><p>$ wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/opencr\_update.tar.bz2</p><p>$ tar -xvf opencr\_update.tar.bz2</p><p>$ cd ./opencr\_update && ./update.sh $OPENCR\_PORT $OPENCR\_MODEL.opencr && cd ..</p>|
| :- |

`　`OpenCRのファームウェア書き込みに失敗した際は、以下の手順に従って、ブートローダーを起動してください。

1. プッシュスイッチ2ボタンを押したままにする。
1. リセットボタンを押す。
1. リセットボタンを離す。
1. プッシュスイッチ2ボタンを離す。

![](Aspose.Words.d4d57a34-7c7d-4f90-b781-f5c11b9fc02f.001.png)　

`　`上記の手順により、OpenCRはリセット後にブートローダーに入ります。ブートローダーの動作中は、ステータスLEDが100msごとに点滅します。ブートローダーが起動している間に再度、ファームウェアを書き込んでください。



` `**7. ラズパイカメラ セットアップ**

`　`以下のコマンドを入力し、設定します。

|$ sudo raspi-config|
| :- |

`　`Interfacing Options > P1 Cameraを選択し、OKを押してください。

下記のコマンドを入力し、supported=1 detected=1の両方が1となっていれば、カメラが認識されています。

|<p>$ vcgencmd get\_camera</p><p>supported=1 detected=1</p>|
| :- |

` `**8. ラズパイカメラ ノードの設定**

`　`下記コマンドを入力して、githubからソースを取得し、ビルドしてください。

|<p>$ cd ~/catkin\_ws/src</p><p>$ git clone https://github.com/UbiquityRobotics/raspicam\_node.git</p><p>$ cd ~/catkin\_ws && catkin\_make</p>|
| :- |

` `**9. ネットワーク設定**

`　`下記のコマンドで.bashファイルを修正してください。

|$ nano ~/.bashrc|
| :- |


`　`下記の内容を追記してください。

|<p>export ROS\_MASTER\_URI=http://{リモートPCのIPアドレス}:11311</p><p>export ROS\_HOSTNAME={TB3MMのIPアドレス}</p>|
| :- |

**動作テスト**

**テスト1 RC-100**

`　`**確認項目**

`　　`・無線操作できる事を確認します。

`　`**手順**　

`　　`・RC-100で操作します。（前進：U、左旋回：L、右旋回：D、後進：R、全速前進：1、停止：5）

**テスト2 テレオペレーション**

`　`**確認項目**

`　　`・遠隔操作ができることを確認します。

`　`**手順**

`　　`・リモートPCで以下のコマンドを入力してください。

|$ roscore|
| :- |

`　　`・リモートPCからsshでTB3MMにログインしてください。

|$ ssh pi@<TB3MMのIPアドレス>|
| :- |
`　`※デフォルトパスワード：turtlebot

`　　`・TB3MMのターミナルで以下のコマンドを入力してください。

|$ roslaunch turtlebot3\_bringup turtlebot3\_robot.launch|
| :- |

`　`※この際、以下のような警告が表示されますが、動作が正常であれば問題ありません。

|<p>[ WARN] [1574853830.988542702]: This firmware(v2.0.1) isn't compatible with this software (v1.1.0)</p><p>[ WARN] [1574853830.988814629]: You can find how to update its in FAQ section(turtlebot3.robotis.com)</p>|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_teleop turtlebot3\_teleop\_key.launch</p>|
| :- |

`　　`・turtlebot3\_teleop\_key.launchを立ち上げたターミナルでa, w, d, s, x等で操作します。

**テスト3 SLAM**

`　`**確認項目**

`　　`・SLAMができる事を確認します。

`　`**手順**

`　　`・リモートPCで以下のコマンドを入力してください。

|$ roscore|
| :- |

`　　`・リモートPCからsshでTB3MMにログインしてください。。

|$ ssh pi@<TB3MMのIPアドレス>|
| :- |
`　`※デフォルトパスワード：turtlebot3



`　　`・TB3MMのターミナルで以下のコマンドを入力してください。

|$ roslaunch turtlebot3\_bringup turtlebot3\_robot.launch|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_slam slam.launch</p>|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_teleop turtlebot3\_teleop\_key.launch</p>|
| :- |

`　`・リモートPCで以下のコマンドを入力してください。

|$ rosrun map\_server map\_saver -f ~/map|
| :- |



・turtlebot3\_teleop\_key.launchを立ち上げたターミナルでa, w, d, s等で操作します。

`　　`・地図が作成できたら、保存してください。

`　　`・RViz上のTurtleBot3MMでSLAMできている事を確認してください。

**テスト3 ナビゲーション**

`　`**確認項目**

`　　`・ナビゲーションができる事を確認します。



`　`**手順**

`　　`・リモートPCで以下のコマンドを入力してください。

|$ roscore|
| :- |

`　　`・リモートPCからsshでTB3MMにログインしてください。

|$ ssh pi@<TB3MMのIPアドレス>|
| :- |
`　　`※デフォルトパスワード：turtlebot3



`　　`・TB3MMのターミナルで以下のコマンドを入力してください。

|$ roslaunch turtlebot3\_bringup turtlebot3\_robot.launch|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_navigation navigation.launch　</p>|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_teleop turtlebot3\_teleop\_key.launch map\_file:=$HOME/map.yaml</p>|
| :- |

`　　`・RVizから、2D Pose Estimate（初期位置）、2D Nav Goal（目標地点）を指定してください。

`　　`・Rviz上のTurtleBot3MMでナビゲーションができている事を確認してください。


**テスト5 マニピュレーション**

`　`**確認項目**

`　　`・ OpenManipulator control GUIで動作すること。

`　　　`・ Init poseを押す

`　　　`・ Home poseを押す

`　　　`・ Gripper openを押す

`　　　`・ Gripper closeを押す

`　　`・ moveitで動作すること。



`　　`InterctiveMarkerを操作して、plan -> Excuteが実行できることを確認します。



`　`**手順**

`　　`・リモートPCで以下のコマンドを入力してください。

|$ roscore|
| :- |

`　　`・リモートPCからTB3MMにログインしてください。

|$ ssh pi@<TB3MMのIPアドレス>|
| :- |
`　`※デフォルトパスワード：turtlebot

`　　`・TB3MMのターミナルで以下のコマンドを入力してください。

|$ roslaunch turtlebot3\_bringup turtlebot3\_robot.launch|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_bringup turtlebot3\_manipulation\_bringup.launch</p>|
| :- |

`　　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_moveit\_config move\_group.launch</p>|
| :- |

`　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_moveit\_config moveit\_rviz.launch</p>|
| :- |

`　`・リモートPCで以下のコマンドを入力してください。

|<p>$ export TURTLEBOT3\_MODEL=waffle\_pi</p><p>$ roslaunch turtlebot3\_manipulation\_gui turtlebot3\_manipulation\_gui.launch</p>|
| :- |

`　`GUIが立ち上がったらTimer startを押してください。

`　　`・ OpenManipulator control guiを操作してください。

`　　`・ moveitのrvizを選択し、Interctive Markerを操作して動作させてください。

**テスト6 ラズパイカメラ**

`　`**確認項目**

`　　`・カメラ画像がTB3MMから送られてくる事を確認してください。

`　`**手順**
**
`　　`・リモートPCで以下のコマンドを入力してください。

|$ roscore|
| :- |

`　　`・リモートPCからsshでTB3MMにログインしてください。

|$ ssh pi@<TB3MMのIPアドレス>|
| :- |
`　`※デフォルトパスワード：turtlebot

`　　`・TB3MMのターミナルで以下のコマンドを入力してください。

|$ roslaunch turtlebot3\_bringup turtlebot3\_rpicamera.launch|
| :- |

`　　`・リモートPCでは以下のコマンドを入力してください。

|$ rqt\_image\_view|
| :- |

`　　`・モニタするトピックを/raspicam\_node/image/compressedにしてください。

`　　`・カメラ画像が送られてくる事を確認してください。
