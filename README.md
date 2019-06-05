# Homework6_team3

1. Take video


2. Make visual effect using ORB-SLAM2
使用這個方法必須先把影片切成好幾個frame，並且把每個timestamp對應的frame記錄在一個txt檔，再用下面的指令產生結果。
```
./Examples/Monocular/mono_tum Vocabulary/ORBvoc.txt Examples/Monocular/TUM2.yaml MY_PATH
```
以下是我們產生的結果：
https://drive.google.com/open?id=1c7B0Iapxr4W5J0VX-1D0xfsu3pINywL2

除了這個結果，ORB-SLAM2還會產生估測出來的point cloud，可以用來重建3D model，但我們在這次作業中並沒有做這項實作。

3. Make visual effect using another post-production software
使用Adobe After Effect的3D Camera Tracker解析影片
解析完成後會在畫面上看到許多追蹤點,並構築出一些平面


![](https://i.imgur.com/HjkGyzW.png)

產生的結果
https://drive.google.com/open?id=1gVVko-pOfWyM3NNFpwAA4sx3HoeyTXiW


4. Compare above methods


5. Make some special effects based on the pose information


6. Insert a 3D model




* BONUS:
基於Hololens跟Unity製作的虐待小人遊戲
一開始要等游標浮上來是為了確保地板的部分已經被辨認出來,確保小人能站在地板上
https://drive.google.com/open?id=160KFF9x1_I94X-daM-o9yxDXU_PCn4fP

HoloLens的感測器,包含一個IMU(Inertial measurement unit),4個灰階環境感知相機,1個深度照相機以及一個RGB相機(圖1)。主要是透過IMU取得面向，環境感知相機取得相對位置，深度相機用於感知環境。
![](https://i.imgur.com/b5ORA2k.png)

SLAM技術:
HoloLens使用的是單目視覺RGBD類。單目視覺指的是使用特徵的計算出相機運動的軌跡，RGBD類指的是HoloLens使用TOF(Time of flight:透過發射特定波長的紅外線，藉由計算來回的時間差進而得到圖像中各像素與相機之間的距離的技術)技術測出個像素與相機的距離。HoloLens的場景建模採用Richard Newcombe發明的Kinect Fusion，重建的方法如(圖1)，而得到的結果如(圖2)
(圖1)
![](https://i.imgur.com/RZH3klT.png)

a.	讀取深度圖建立point cloud以及各點的法向量
b.	相機追蹤
c.	根據現在相機的位置，將當前幀的點融入網格模型中
d.	根據當前相機位置，得到當前幀的point cloud和法向量，用來和下一幀的輸入圖匹配。
(圖2)
![](https://i.imgur.com/7bsafqX.png)

## Conclusion

ORB_SLAM2

ORB_SLAM2是由四個部分組成，前三個部份是，

1.跟踪（Tracking）：通過尋找對局部地圖特徵進行匹配)。
2.局部建图（LocalMapping） ：通過執行局部BA管理局部地圖並優化。
3.回環檢測（LoopClosing）：檢測大的環並通過執行位姿圖優化更正漂移誤差。
而最後一個是全局BA，是用來計算整個系統最優結構和運動結果。

ORB_SLAM2的優點是LoopClosing做的好，基本上只要見過的場景都能找回來。

