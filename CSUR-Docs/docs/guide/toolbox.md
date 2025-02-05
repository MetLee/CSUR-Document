---
sidebarDepth: 3
---
# ToolBox 说明书

## 1. 简介

CSURToolBox 是 CSUR2.0 的重要辅助工具合集。主要有下面 6 个功能：<br>
1. 提供一个 UI 辅助快速选择 CSUR 道路；<br>
2. 往游戏中加入了 CSUR 的偏移量，更方便选中道路（点选实际路面选中 CSUR 偏移路）；<br>
3. CSUR 偏移路桥墩自动偏移；<br>
4. 车道平滑偏移；<br>
5. 去除 CSUR Shift Ramp Transition and Express 道路的 Zone；
6. 调用 TMPE laneconnector 对复杂 CSUR 路口划线；

其余一些 BUG 的修复：<br>
1. 当 CSUR 8DR 以上路作为地图出入口时，部分出入口只能用 1 个车道；<br>
2. CSUR 大路直接互相直连时，居民会停在直连路口；<br>
3. 修复了 TMPE 道路连线时，无法读取部分 CSUR 路的车道连接点的问题；<br>
4. 修复了一些巨大的路口；
5. 解决了 CSUR 路 zone 不对齐的问题；

下面主要介绍一下 CSUR UI 的具体用法。<br>

## 2. UI 入口

进入主界面后，在内容管理器内，模组界面下找到 CSURToolBox，并启用即可生效。<br>

进入游戏后，在画面右侧能找到 UI 按钮如右图: ![按钮图](/assets/img/wiki/Button.png) <br>

左键按住可以拖动该按钮至任意你喜欢的位置<br>
左键单击可以呼出 UI 界面<br>

## 3. UI 界面

呼出的 UI 界面如图，按从左到右，从上到下分为七个部分：<br>
![](/assets/img/wiki/overview.jpg) <br>

|序号|名称|作用|
|:---:|:---:|:---:|
|1|标题栏|拖动 UI 位置|
|2|预览框|查看选中情况|
|3|状态面板|切换同类型路不同样式|
|4|目标车道面板|选择道路末端车道接口|
|5|起始车道面板|选择道路首端车道接口|
|6|调整面板|调整 4、5 所选车道|
|7|关闭按钮|关闭 UI 面板|

### 3.1 标题栏

左键按住可以拖动该界面的位置。<br>

### 3.2 预览框

当选中的按钮有对应的道路，则显示该道路的图标，否则显示 Not found（无匹配项）<br>

### 3.3 状态面板

|按钮图案|名称|作用|
|:---:|:---:|:---:|
|![](/assets/img/wiki/single.png)|单向|按车道面板**原样**产生单向的道路|
|![](/assets/img/wiki/dual.png)|双向|按车道面板原样产生双向的道路(对向是**镜像**的)|
|![](/assets/img/wiki/asym1.png)|不对称+1|产生在**双向**基础上，前进方向增加 **1** 个车道的类型|
|![](/assets/img/wiki/asym2.png)|不对称+2|产生在**双向**基础上，前进方向增加 **2** 个车道的类型|
|![](/assets/img/wiki/uturn.png)|调头车道|产生在**双向**基础上，前进方向增加**调头**车道的类型|
|![](/assets/img/wiki/bike.png)|人行道和自行车道|同时带有非机动车道和人行道|
|![](/assets/img/wiki/human.png)|仅人行道|仅带有人行道无非机动车道|
|![](/assets/img/wiki/nohuman.png)|纯路面|无人行道无非机动车道|

### 3.4 目标车道面板，选择路段末端对应的车道

### 3.5 起始车道面板，选择路段首端对应的车道

此二面板为该 UI 的核心。上有多个按钮，分别对应 CSUR 道路的每一个车道。<br>
![](/assets/img/wiki/example4.png) <br>
**注意：该面板选取的车道都是单向部分的，所有双向类型通过类型面板的按钮衍生<br>**

本 UI 从左侧的 L2 开始，因此，从左右位置来看，面板左侧绿色的四个按钮为 L 部分，黑色的 C 为分隔线，右侧的蓝色按钮为 R 部分。<br>
例如，我们常用的 6DR，我们仅需选择面板中 123 车道，勾选双向，即可调用。<br>
![](/assets/img/wiki/example3.png) <br>

而第二排带 P 的按钮，是标准位置右移半个车道的位置。<br>
![](/assets/img/wiki/example5.png) <br>
因为护栏宽度的关系，选择带 P 的类型，能与普通类型刚好并排，而不会产生模型冲突。

实例：<br>
![](/assets/img/wiki/example6.png) <br>
当我们需要将 4R 与 2R 和 2R4P 连接时<br>
起始端：4R，选择 1234；<br>
目标端：2R，选择 12； 2R4P，选择 3P 4P。<br>
![](/assets/img/wiki/example1.png) <br>

当我们需要将 4R、1R5P 与 3R、2R5P 连接时<br>
起始端：4R，选择1234； 1R5P，选择 5P<br>
目标端：3R，选择123； 2R5P，选择 4P 5P。<br>
![](/assets/img/wiki/example2.png) <br>

### 3.6 调整面板

调整面板有三个按钮，作用是对车道面板的内容进行调整。<br>

|按钮图案|名称|作用|
|:---:|:---:|:---:|
|![](/assets/img/wiki/copy.png)|复制|将**下方**起始面板选中的按钮复制到**上方**目标面板|
|![](/assets/img/wiki/swap.png)|交换|将起始面板和目标面板选中的按钮调换，相当于反向修建|
|![](/assets/img/wiki/clear.png)|清除|将两个面板恢复初始状态，取消所有选中的按钮|

### 3.7 关闭按钮

点击关闭 UI。另外，再次点击图标也可以关闭 UI。<br>
