## Turtlebot3 Burger用カスタムLiDARマウント使用方法(UST-10/20LX,TiM571,RPLidar A1M8)
### はじめに
このドキュメントではカスタムタイプのマウントを使って各種LiDARハードウェアをTurtlebot3 Burgerに取り付ける方法のみ記述します。
配線の接続やソフトウェアセットアップはLiDARメーカーのドキュメントや[TurtleBot3 e-manual](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)を参照して下さい。
<br>
### 取付方法 UST-10/20LX
  1.UST-10/20LXの底部にあるM3のねじ穴2箇所(画像の赤丸の箇所)を使用します。残りの2箇所はノック穴です。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141722947-0af0bc30-58ce-4a2a-9945-bae2c3fc1627.png)<br>
<br>
  2.M3x8皿ねじでマウントをUST-10/20LXに取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141723125-978d8610-a3b4-4b62-8a67-eb15344ae715.png)<br>
<br>
  3.マウントをM2.5x8皿ねじでTurtleBot3 Burgerの天板(4th Plate)に取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141723284-5aa33f84-9dcc-4a9a-bf9b-ba55c044d138.png)<br>
<br>
  4.完成状態<br>
  ![image](https://user-images.githubusercontent.com/5852451/141723338-47c43dc1-7f84-48fd-b44f-c5c98beb6224.png)<br>  
<br>

### 取付方法 SICK TiM571
  1.TiM571の底部にあるM3のねじ穴2箇所を使用します。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141720411-d9449e55-244e-43d2-9189-f1bda17599e4.png)<br>
<br>
  2.M3x8皿ねじでマウントをTiM571に取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141721818-badcccf7-4774-43a0-9764-1930fdfea107.png)<br>
<br>
  3.マウントをM2.5x8皿ねじでTurtleBot3 Burgerの天板(4th Plate)に取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141722698-3a0ddc4f-ca1a-4d0d-8204-a46fa00de6af.png)<br>
<br>
  4.完成状態<br>
  ![image](https://user-images.githubusercontent.com/5852451/141722098-19324061-2402-4be8-8216-b10fe8ebc4d6.png)<br>
<br>
### 取付方法 RPLidar A1M8
  1.RPLidar A1M8用マウント外観<br>
![image](https://user-images.githubusercontent.com/5852451/141723805-39bd35c3-55f6-472b-9df6-985b2ed465e8.png)<br>
<br>
  2.2x6タッピングねじでUSB変換基板をマウントに取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141724053-894d7bfa-8804-44f7-93f7-f6d5b1ce9f8c.png)<br>
<br>
  3.RPLidarとUSB変換基板を付属の接続ケーブルで接続します。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141724201-23bc28fb-a7b8-4f46-ad82-e68d2444055e.png)<br>
<br>
  4.M2.5x8皿ねじでマウントをRPLidarに取り付けます。このとき、接続ケーブルを慎重に折り曲げてLiDARとマウントの間に収まるようにしてください。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141724399-5ee780e0-399c-4775-b06f-3bf12ab2c446.png)<br>
<br>
  5.マウントをM2.5x8皿ねじでTurtleBot3 Burgerの天板(4th Plate)に取り付けます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141724756-9a5eb99c-dc96-4852-90e2-53f6c340b02f.png)<br>
<br>
  6.USBケーブルはTurtleBot3付属のものがそのまま使用できます。<br>
  ![image](https://user-images.githubusercontent.com/5852451/141724893-55689139-221a-4674-8e12-43843c4cdc42.png)<br>
<br>
  7.完成状態<br>
  ![image](https://user-images.githubusercontent.com/5852451/141725050-73f993f6-74aa-4fb1-854b-73bfb333d857.png)<br>
<br>
### ソフトウェアの修正 RPLidar A1M8
#### 動作環境
- TurtleBot3(waffle pi):Kinetic<br>
  https://github.com/ROBOTIS-GIT/turtlebot3<br>
- RP Lidar A1<br>
  https://github.com/Slamtec/rplidar_ros<br>

#### ソフトウェアの修正
![image](https://user-images.githubusercontent.com/5852451/141726455-a762d06b-f1a6-48f0-9a57-4cecf35fc643.png)<br>
※より正確に動作検証をする場合は、リモートPC側のturtlebot3_description/urdfを修正すること。<br>
<br>
- 上記の内容でTurtleBot3のSLAMが正常に動作することを確認しています。(24 Nov 2020)
![image](https://user-images.githubusercontent.com/5852451/141726591-c67dbb4a-acc9-4870-b244-c00cdc2c46c1.png)<br>

### マウントのCADデータ配布と販売について
  問い合わせ先 : ロボティズ日本支店 japan@robotis.com




