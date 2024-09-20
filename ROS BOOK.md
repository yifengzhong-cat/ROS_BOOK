# ROS BOOK

## 第1章 ROS概述与环境搭建

学习是一个循序渐进的过程，具体到计算机领域的软件开发层面，每当接触一个新的知识模块时，按照一般的步骤，我们会先去了解该模块的相关概念。然后再安装官方软件包，接下来再搭建其集成的开发环境...这些准备工作完毕之后，才算是叩开了新领域的大门。

学习ROS，我们也是遵循这一流程，本章作为ROS体系的开篇主要内容如下;

+ ROS的相关概念
+ 怎样安装ROS
+ 如何搭建ROS的集成开发环境

该章内容学习完毕预期达成的目标如下：

+ 了解ROS概念、设计目标以及发展历程
+ 能够独立安装并运行ROS
+ 能够使用C++或Python实现ROS版本的HelloWorld
+ 能够搭建ROS的集成开发环境
+ 了解ROS架构设计

案例演示：

1. ROS安装成功后，可以运行内置案例：该案例是通过键盘控制乌龟运动

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/01_ROS%E6%A1%88%E4%BE%8B%E6%BC%94%E7%A4%BA.gif)

2. 集成开发环境使用VSCode，可以提高开发效率

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/vscode.gif)

### 1.1 ROS简介

ROS诞生背景

> 机器人是一种高度复杂的系统性实现，机器人设计包含了机械加工、机械结构设计、硬件设计、嵌入式软件设计、上层软件设计....是各种硬件与软件的集成，甚至可以说机器人系统是当今工业体系的集大成者。
>
> ![](C:/Users/XSYT/Desktop/12_%E5%89%8D%E8%A8%80.jpg)

> 机器人体系是相当庞大的，其复杂度之高，以至于没有任何人、组织甚至公司能够独立完成系统性的机器人研发工作。
>
> 一种更合适的策略是：让机器人研发者专注于自己擅长的领域，其他模块直接复用相关领域更专业研发团队的实现，当然自身的研究也可以被他人继续复用。这种基于“复用”的分工协作，遵循了**不重复发明轮子**的原则，显然可以大大提高机器人的研发效率的，尤其是随着机器人硬件越来越丰富，软件库越来越庞大，这种复用性和模块化开发需求也愈发强烈。

在此大背景下，于2007年，一家名为柳树车库（Willow Garage）的机器人公司发布了ROS(机器人操作系统), ROS是一套机器人通用软件框架，可以提升功能模块的复用性，并且随着该系统的不断迭代与完善，如今ROS已经成为机器人领域的事实标准。

![13_前言](C:/Users/XSYT/Desktop/13_%E5%89%8D%E8%A8%80.png)

#### 1.1.1 ROS概念

**ROS全称RObot Operating System（机器人操作系统）**

+ ROS是适用于机器人的**开源**元操作系统
+ ROS集成了大量的工具，库，协议，提供类似OS所提供的功能，简化对机器人的控制
+ 还提供了用于在**多台计算机**上获取，构建，编写和运行代码的工具和库，ROS在某些方面类似于“机器人框架”
+ ROS设计者将ROS表述为"ROS = Plumbing + Tools + Capabilities + Ecosystem", 即ROS是通讯机制、工具软件包、机器人高层技能以及机器人生态系统的集合体

![05ROS简介](C:/Users/XSYT/Desktop/05ROS%E7%AE%80%E4%BB%8B.png)



#### 1.1.2 ROS设计目标

机器人开发的分工思想，实现了不同研发团队间的共享和协作，提升了机器人的研发效率，为了服务“分工”,ROS主要设计了如下目标：

+ **代码复用：** ROS的目标不是成为具有最多功能的框架，ROS的主要目标是支持机器人技术研发中的代码重用。
+ **分布式：** ROS是进程（也称为Node）的分布式框架，ROS中的进程分布于不同的主机，不同主机之间协同工作，从而分散计算压力。
+ **松耦合：** ROS中功能模块封装于独立的功能包或元功能包，便于分享，功能包内的模块以节点为单位运行，以ROS标准的IO作为接口，开发者不需要关注模块内部实现，只要了解接口规则就能实现复用，实现了模块点对点之间的松耦合连接。
+ **精简：** ROS被设计为尽可能精简，以便于为ROS编写代码可以与其他机器人软件框架一起使用。ROS易于与其他机器人软件框架集成：ROS已与OpenRAVE，Orocos和Player集成。
+ **语言独立性：** 包括Java,C++,Python等。为了支持更多应用开发，ROS设计为一种语言弱相关的框架结构，使用简介，中立的定义语言描述模块之间的消息接口，在编译中再产生所使用语言的目标文件，为消息交互提供支持，同时允许消息接口的嵌套使用。
+ **易于测试：** ROS具有称为[rostest](http://wiki.ros.org/rostest)的内置单元/集成测试框架，可轻松安装和拆卸测试工具。
+ **大型应用：** ROS适用于大型运行时系统和大型开发流程。
+ **丰富的组件化工具包：** ROS采用组件化方式集成一些工具和软件到系统中并作为一个组件直接使用，如RVIZ（3D可视化工具）,开发者根据ROS定义的接口在其中显示机器人模型等，组件还包括仿真环境和消息查看工具等。
+ **免费且开源：** 开发者众多，功能包多多。

#### 1.1.3 ROS发展历程

+ ROS是一个由来已久、贡献者众多的大型软件项目。在ROS诞生之前，很多学者认为，机器人研究需要一个开放式的协作框架，并且已经有不少类似的项目致力于实现这样的框架。在这些工作中，斯坦福大学在2000年中开展了一系列相关的研究项目，如斯坦福人工智能机器人（Standford AI  Robot, STAIR ） 项目、个人机器人（Personal Robots,PR）项目等，在上述项目中，在研究具有代表性、集成式人工智能系统的过程中，创立了用于室内场景的高灵活性、动态软件系统，其可以用于机器人学研究。

+ 2007年，柳树车库（Willow Garage） 提供了大量资源，用于斯坦福大学机器人项目中的软件系统进行扩展与完善，同时，在无数研究人员的共同努力之下，ROS的核心思想和基本软件包以及逐渐得到完善。

+ ROS的发行版本（ROS distribution）指ROS软件包的版本，其与Linux的发行版本（如Ubuntu）的概念类似。推出ROS发行版本的目的在于使开发人员可以使用相对稳定的代码库，直到其准备好将所有内容进行版本升级为止。因此，每个发行版本推出后，ROS开发者通常仅对这一版本的bug进行修复，同时提供少量针对核心软件包的改进。

+ 版本特点：按照英文字母顺序命名，ROS目前已经发布了ROS1的终极版本：noetic，并建议后期过渡至ROS2版本。noetic版本之前默认使用的是Python2，noetic支持Python3。

  版本建议： noetic 或 melodic 或 kinetic

  ![版本](%E7%89%88%E6%9C%AC.png)

**另请参考：**

[关于ROS](https://www.ros.org/about-ros/)

[ROS介绍](https://wiki.ros.org/ROS/Introduction)

[ROS版本](https://wiki.ros.org/Distributions)



### 1.2 ROS安装

我们使用ROS的版本是Noetic，那么可以在ubuntu20.04、Mac或windows10系统上安装，虽然一般用户平时使用操作系统以windows居多，但是ROS之前的版本都基本上不支持windows，所以当前我们选用的操作系统是ubuntu，以方便历史版本过渡。ubuntu安装常用的方式有两种：

+ 实体机安ubuntu（较为常用的双系统，windows和Ubuntu并存）；

+ 虚拟机安装ubuntu.

两种方式比较，各有优缺点：

+ 方案1可以保证性能，且不需要考虑硬件兼容性问题，但是和windows系统交互不方便；
+ 方案2可以方便的实现Windows与Ubuntu交互，不过性能稍差，且与硬件交互不便。

在ROS中，一些仿真操作时比较耗资源的，且经常需要一些硬件（雷达、摄像头、imu、STM32、arduino...）交互，因此，原则上建议采用方案1，不过只是出于学习目的，那么方案2基本够用，且方案2在windows与ubuntu的交互上更为方便，对于学习者更为友好，因此本教程在此选用的是方案2.当然，具体采用哪种实现方案，请按需选择。

如果采用虚拟机安装ubuntu，再安装ROS的话，大致流程如下:

1. 安装虚拟机软件（比如：virtualbox 或 VMware）；
2. 使用虚拟机软件虚拟一台主机；
3. 再虚拟主机上安装ubuntu20..04；
4. 再ubuntu上安装ROS；
5. 测试ROS环境是否可以正常运行。

虚拟机软件选择上，对于我们学习而言virtualbox和VMware都可以满足需求，二者比较前者免费，后者收费，所以本教程选用virtualbox。

#### 1.2.1 安装虚拟机软件

##### 1.2.1.1 下载virtualbox

安装virtualbox需要访问官网，官网下载地址：https://www.virtualbox.org/wiki/Downloads

![14_virtualbox下载](ROS_asserts/14_virtualbox%E4%B8%8B%E8%BD%BD.png)

##### 1.2.1.2 安装virtualbox

virtualbox安装比较简单，如果没有特殊需求，双击安装文件，一直“下一步”即可。

![15_VB安装1](ROS_asserts/15_VB%E5%AE%89%E8%A3%851.png)

![16_VB安装2](ROS_asserts/16_VB%E5%AE%89%E8%A3%852.png)

![17_VB安装3](ROS_asserts/17_VB%E5%AE%89%E8%A3%853.png)

![18_VB安装4](ROS_asserts/18_VB%E5%AE%89%E8%A3%854.png)

![19_VB安装5](ROS_asserts/19_VB%E5%AE%89%E8%A3%855.png)

![20_VB安装6](ROS_asserts/20_VB%E5%AE%89%E8%A3%856.png)

![21_VB安装7](ROS_asserts/21_VB%E5%AE%89%E8%A3%857.png)

![22_VB安装8](ROS_asserts/22_VB%E5%AE%89%E8%A3%858.png)

![23_VB安装9](ROS_asserts/23_VB%E5%AE%89%E8%A3%859.png)

安装完毕之后，虚拟机已经可以正常启动了，接下来需要使用其虚拟出一台计算机



#### 1.2.2 虚拟出一台主机

使用virtual虚拟计算机的过程也不算复杂，只需要按照提示配置其相关参数即可

![24_虚拟主机01](ROS_asserts/24_%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA01.png)

![25_虚拟主机02](ROS_asserts/25_%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA02.png)

![26_虚拟主机03](ROS_asserts/26_%E8%99%9A%E6%8B%9F%E4%B8%BB%E6%9C%BA03.png)



#### 1.2.3 安装ubuntu

##### 1.2.3.1 ubuntu安装

首先下载Ubuntu镜像文件，链接如下：http://mirrors.aliyun.com/ubuntu-releases/20.04/；

然后，配置虚拟主机，关联Ubuntu镜像文件：

![28_Ubuntu安装02](ROS_asserts/28_Ubuntu%E5%AE%89%E8%A3%8502.png)

![29_Ubuntu安装03](ROS_asserts/29_Ubuntu%E5%AE%89%E8%A3%8503.png)

启动后，开始配置ubuntu操作系统：

![30_Ubuntu安装04](ROS_asserts/30_Ubuntu%E5%AE%89%E8%A3%8504.png)

![31_Ubuntu安装05](ROS_asserts/31_Ubuntu%E5%AE%89%E8%A3%8505.png)

安装过程中，断开网络连接，可以提升安装速度：

![32_Ubuntu安装06](ROS_asserts/32_Ubuntu%E5%AE%89%E8%A3%8506.png)

![33_Ubuntu安装07](ROS_asserts/33_Ubuntu%E5%AE%89%E8%A3%8507.png)

![34_Ubuntu安装08](ROS_asserts/34_Ubuntu%E5%AE%89%E8%A3%8508.png)

![35_Ubuntu安装09](ROS_asserts/35_Ubuntu%E5%AE%89%E8%A3%8509.png)

![36_Ubuntu安装10](ROS_asserts/36_Ubuntu%E5%AE%89%E8%A3%8510.png)

![37_Ubuntu安装11](ROS_asserts/37_Ubuntu%E5%AE%89%E8%A3%8511.png)

![38_Ubuntu安装12](ROS_asserts/38_Ubuntu%E5%AE%89%E8%A3%8512.png)

到目前为止 VirtualBox 已经正常安装了 Ubuntu, 并启动成功。

##### 1.2.3.2 使用优化

为了优化ubuntu操作的用户体验，方便虚拟机与宿主机的文件交换以及USB设备的正常使用，还需做如下操作

###### 1.2.3.2.1 安装虚拟机工具

![40_Ubuntu优化02](ROS_asserts/40_Ubuntu%E4%BC%98%E5%8C%9602.png)

![41_Ubuntu优化03](ROS_asserts/41_Ubuntu%E4%BC%98%E5%8C%9603.png)

重启使之生效，选择菜单栏 `自动调整窗口大小`，然后ubuntu桌面会自动使用窗口大小: `右ctrl+F`全屏。



###### 1.2.3.2.2 启动文件交换模式

![39_Ubuntu优化01](ROS_asserts/39_Ubuntu%E4%BC%98%E5%8C%9601.png)

###### 1.2.3.2.3 安装扩展插件

先去 virtualbox 官网下载扩展包

![14_virtualbox下载](ROS_asserts/14_virtualbox%E4%B8%8B%E8%BD%BD.png)

在virtual box中添加扩展工具

![42_Ubuntu优化04](ROS_asserts/42_Ubuntu%E4%BC%98%E5%8C%9604.png)

在虚拟机中添加USB设备

![43_Ubuntu优化05](ROS_asserts/43_Ubuntu%E4%BC%98%E5%8C%9605.png)

重启后，使用  `ll /dev/ttyUSB*` 或`ll /dev/ttyACM* `即可查看新接入的双设备。

###### 1.2.3.2.4 其他

其他设置，比如输入法可以根据喜好自行下载安装。

ubuntu20.04鼠标右击没有创建文件选项，如果想要设置此选项，可以进入`主目录`下的`模版`目录，使用gedit创建一个空文本文档，以后，鼠标右击就可以添加新建文档选项，并且创建的文档与当前自定义的文档名称一致。



#### 1.2.4 安装ROS

Ubuntu安装完毕之后，就可以安装ROS操作系统了，大致步骤如下：

1. 配置ubuntu的软件和更新；
2. 设置安装源；
3. 设置key
4. 安装；
5. 配置环境变量。

##### 1.2.4.1 配置ubuntu的软件和更新

配置ubuntu的软件和更新，允许安装不经认证的软件。

首先打开“软件和更新”对话框，具体可以在Ubuntu搜索按钮中搜索。

打开后按照下图进行配置（确保勾选了“restricted”,“universe”，“multiverse”）

![00ROS安装之ubuntu准备](http://www.autolabor.com.cn/book/ROSTutorials/assets/00ROS%E5%AE%89%E8%A3%85%E4%B9%8Bubuntu%E5%87%86%E5%A4%87.png)

##### 1.2.4.2 设置安装源

官方默认安装源：

```shell
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

或来自国内清华的安装源

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

或来自国内中科大的安装源

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

PS

1. 回车后，可能需要输入管理员密码
2. 建议使用国内资源，安装速度快

##### 1.2.4.3 设置Key

```shell
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

##### 1.2.4.4 安装

首先需要更新`apt`（以前是`apt-get`，官方建议使用`apt`而不是`apt-get`），`apt`是用于从互联网仓库搜索、安装、升级、卸载软件或操作系统的工具。

```shell
sudo apt update
```

等待...

然后，再安装所需类型的ROS:ROS多个类型，**Desktop-FUll**、**Desktop**、**ROS-Base**。这里介绍较为常用的Desktop-Full（官方推荐）安装： ROS，rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception

```shell
sudo apt install ros-noetic-desktop-full
```

等待...... (比较耗时)

友情提示：由于网络原因，导致连接超时，可能会安装失败，如下所示：

![09\_安装异常](http://www.autolabor.com.cn/book/ROSTutorials/assets/09_%E5%AE%89%E8%A3%85%E5%BC%82%E5%B8%B8.PNG)

可以多次重复调用 更新 和 安装命令， 直至成功。

##### 1.2.4.5 配置环境变量

配置环境变量，方便在任意终端中使用ROS

```shell
echo "source /opt/ros/noetic/srtup.bash" >> ~/.bashrc source ~/.bashrc
```

##### 卸载

如果需要卸载ROS可以调用如下命令：

```shell
sudo apt remove ros-noetic-*
```

注意：在ROS版本noetic中无需构建软件包的依赖关系，没有 `rosdep`的相关安装与配置。

另请参考: https://wiki.ros.org/noetic/Installation/Ubuntu

----------------------------------------

----------------------------------------

----------------------------------------

#### 后记

##### 1.2.4.6 安装构建依赖

在noetic最初发布时，和其他历史版本稍有差异的是：没有安装构建依赖这一步骤。随着noetic不断完善，官方补齐了这一操作。

首先安装构建依赖的相关工具

```shell
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

ROS中使用许多工具前，要求需要初始化rosdep（可以安装系统依赖）-- 上一步实现已经安装过了。

```shell
sudo apt install python3-rosdep
```

初始化rosdep

```shell
sudo rosdep  init
rosdep update
```

如果一切顺利的话，rosdep初始化与更新对的打印结果如下：

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/rosdep%E6%AD%A3%E5%B8%B8%E5%88%9D%E5%A7%8B%E5%8C%96.PNG)

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/rosdep%E6%AD%A3%E5%B8%B8%E6%9B%B4%E6%96%B0.PNG)

----------------------------------------------------------------------------------

但是，在rosdep初始化时，多半会抛出异常。

**问题：**

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/noetic%E5%BC%82%E5%B8%B8%E6%8F%90%E7%A4%BA.PNG)

**原因：**

境外资源被屏蔽

**解决：**

百度或者google搜索，解决方式有多种（https://github.com/ros/rosdistro/issues/9721）,可惜在ubuntu20.04下，集体失效。

新思路：将相关资源备份到gitee,修改rosdep源码，重新定位资源。

**实现：**

1. 先打开资源备份路径：https://gitee.com/zhongyifeng/rosdistro，打开rosdistro/rosdep/sources.list.d/20-default.list文件留作备用（主要是复用URL的部分内容：gitee.com/zhongyifeng/rosistro/raw/master）

   ![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/gitee%E8%B5%84%E6%BA%90.PNG)

2. 进入“/usr/lib/python3/dist-packages/"查找rosdep中和raw.githubusercontent.com相关的内容，调用命令：

   ```shell
   find . -type f | xargs grep "raw.githubusercontent"
   ```

   

   ![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/noetic_%E6%9F%A5%E6%89%BE%E5%8C%85%E5%90%ABgithubusercontent%E7%9A%84%E6%96%87%E4%BB%B6.PNG)

3. 修改相关文件，主要有：

   ```shell
   ./rosdistro/__init__.py \ ./rosdep2/gbpdistro_support.py \ ./rosdep2/sources_list.py \ ./rosdep2/rep3.py。 可以使用 sudo gedit 命令修改文件
   ```

   文件中涉及的URL内容，如果

   是：`raw.githubusercontent.com/ros/rosddistro/master`都替换成步骤1中准备的

   `gitee.com/zhongyifeng/rosdistro/raw/master`即可。

   修改完毕，再重新执行命令：

   ```shell
   sudo rosdep init
   rosdep update
   ```

   就可以正常实现rosdep的初始化和更新了。

   #### 1.2.5 测试ROS

   ROS内置了一些小程序，可以通过运行这些小程序以检测ROS环境是否可以正常运行

   1. 首先启动三个命令行（ctrl + alt +  T）
   2. 命令行1键入： roscore
   3. 命令行2键入： rosrun turtlesim turtlesim_node（此时会弹出图形化界面）
   4. 命令行3键入： rosrun turtlesim turtle_teleop_key（在3中可以通过上下左右控制2中的乌龟的运动）

   最终结果如下所示：

   ![01ROS环境测试](http://www.autolabor.com.cn/book/ROSTutorials/assets/01ROS%E7%8E%AF%E5%A2%83%E6%B5%8B%E8%AF%95.png)

​		注意： 光标必须聚焦在键盘控制窗口，否则无法控制乌龟运动。

#### 1.2.6 资料：其他ROS版本安装

我们的教程采用的是ROS的最新版本noetic，不过noetic较于之前的ROS版本变动较大且部分功能包还未更新，因此如果有需要（比如到后期实践阶段，由于部分重要的功能包还未更新，需要降级），也会安装ROS，在此，建议选用的版本数melodic和kinetic。

接下来，就以melodic为例演示ROS历史版本安装（当然先要准备与melodic对应的Ubuntu18.04）

##### 1.2.6.1 配置ubuntu的软件和更新

首先打开“软件和更新”的对话框，打开后按照下图进行配置 (确保你的“restricted”,“universe”,和“multiverse”前是打上勾的)

##### 1.2.6.2 安装源

官方默认安装源：

```shell
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

或来自国内中科大的安装源

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.ustc.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

或来自国内清华的安装源

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

PS:回车后，可能需要输入管理员密码

##### 1.2.6.3 设置key

```shell
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

##### 1.2.6.4 安装

首先需要更新`apt`(以前是`apt-get`,官方建议使用`apt`而非`apt-get`)，`apt`是用于从互联网仓库搜索、安装、升级、卸载软件或操作系统的工具。

```shell
sudo apt update
```

等待...

然后，再安装所需要类型的ROS:ROS多个类型：**Desktop-full**、**Desktop**、**ROS-Base**。这里介绍较为常用的Desktop-Full（官方推荐）安装：ROS、rqt、robot-generic libraries、2D/3D simulators、navigation and  2D/3D perception

```shell
sudo apt install ros-melodic-desktop-full
```

等待...

##### 1.2.6.5 环境配置

配置环境变量，方便在任意终端中使用ROS。

```shell
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc source ~/.bashrc
```

##### 1.2.6.6 安装构建依赖

首先安装构建依赖的相关工具

```shell
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```

然后安装rosdep（可以安装系统依赖）

```shell
sudo apt install python-rosdep
```

初始化rosdep

```shell
sudo rosdep init
rosdep update
```

**注意：**

当执行到最后 `sudo rosdep init`时，可能会抛出异常；

**错误提示:**

ERROR: cannot download default sources list from:

https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/sources.list.d/20-default.list

Website may be down.

**原因：**

境外资源被屏蔽

**解决思路：**

查询错误提示中域名的IP地址，然后修改 `/etc/hosts`文件，添加域名与IP映射

**实现：**

1. 访问域名查询网址: https://site.ip138.com/

2. 查询域名ip，搜索框中输入：raw.githubusercontent.com，自由复制一个查询到的IP

   

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/%E5%9F%9F%E5%90%8Dip%E6%9F%A5%E8%AF%A2.PNG)

3. 修改`/etc/hosts`文件，命令:

   ```shell
   sudo gedit /etc/hosts
   ```

​	 添加内容：151.101.76.133 raw.githubusercontent.com (查询到的ip与域名)，保存并退出。

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/hosts%E6%96%87%E4%BB%B6%E4%BF%AE%E6%94%B9.PNG)

​	或者，也可以直接使用`vi`或`vim`修改

4. 重新执行 `rosdep`初始化与更新命令，如果`rosdep update`抛出异常，基本都是网络原因导致的（建议使用手机热点）, 多尝试几次即可。

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/rosdep%E5%88%9D%E5%A7%8B%E5%8C%96%E6%88%90%E5%8A%9F.PNG)

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/rosdepupdate%E6%88%90%E5%8A%9F.PNG)

-----------------------------------------------------------------------------

综上，历史版本的安装与noetic流程类似，只是多了“构建功能包依赖关系”的步骤

另请参考：http://wiki.ros.org/melodic/Installation/Ubuntu

### 1.3 ROS快速体验

#### 1.3.1 HelloWorld实现简介

ROS中涉及的编程语言以C++和Python为主，ROS中的大多数程序两者都可以实现，在本系列教程中，每一个案例都会分别使用C++和Python两种方案演示，大家可以根据自身情况选择合适的实现方案。

ROS中的程序即便使用不同的编程语言，实现流程也大致类似，以当前HelloWorld程序为例，实现流程大致如下：

1. 先创建一个工作空间；
2. 再创建一个功能包；
3. 编辑源文件；
4. 编辑配置文件；
5. 编译并执行。

上述流程中，C++和Python只是在步骤3和步骤4的实现细节上面存在差异，其他流程基本一致。本节先实现C++和Python程序编写的通用部分步骤1和步骤2，1.3.2节和1.3.3节分别使用C++和Python编写HelloWorld

##### 1.3.1.1 创建工作空间并初始化

```shell
mkdir -p demo1/src  // 递归创建文件夹
cd demo1 
catkin_make
```

上述命令，首先会创建一个工作空间以及一个src子目录，然后再进入工作空间调用catkin_make命令编译

##### 1.3.1.2 进入src创建ros包并添加依赖

```shell
cd src
catkin_create_pkg 自定义ROS包名 roscpp rospy std_msgs
```

上述命令，会在工作空间下生成一个功能包，该功能包依赖于roscpp、rospy与std_msgs，其中roscpp是使用C++实现的库，而rospy则是python实现的库，std_msgs是标准消息库，创建ROS功能包时，一般都会依赖这个三个库实现

-------------------------------------------------------------------------------------------------------

**注意：**在ROS中，虽然实现同一功能时，C++和Python可以互换，但是具体选择哪种语言，需要视需求而定，因为两种语言相比较而言：C++运行效率高但是编码效率低， 而Python则反之，基于二者互补的特点，ROS设计者分别设计了roscpp与rospy库，前者旨在成为ROS的高性能库，而后者则一般用于对性能无需求的场景，旨在提高开发效率。

#### 1.3.2 HelloWorld（C++版本）

本节内容基于1.3.1，假设你已经创建了ROS的工作空间，并且创建了ROS的功能包，那么就可以进入核心步骤了，使用C++编写程序实现：

##### 1.3.2.1 进入ros包的src目录编辑源文件

```shell
cd 自定义的包
```

C++源码实现（文件名自定义）

```c++
#include "ros/ros.h"

int main(int argc,char **argv)
{
	// 执行ros节点初始化
	ros::init(argc,argv,"hello");
	// 创建ros节点句柄 （非必须）
	ros::NodeHandle n;
	// 控制台输出 "hello world"
	ROS_INFO("hello world!");
	
	return 0;
}
```

##### 1.3.2.2  编辑ros包下面的CMakeLists.txt 文件

```cmake
add_excutable(步骤3的源文件名 src/步骤3的源文件名.cpp)
target_link_libraries(步骤3的源文件名 ${catkin_LIBRARIES})
```

##### 1.3.2.3 进入工作空间目录并编译

```shell
cd 自定义工作空间名称
catkin_make
```

生成build devel ...

##### 1.3.2.4 执行

先启动命令行1：

```shell
roscore
```

再启动命令行2:

```shell
cd 自定义工作空间名称
source ./devel/setup.bash
rosrun 包名 C++节点(也就是步骤3的源文件名)
```

命令行输出： hello world！

**PS:**`source ~/工作空间/devel/setup.bash`可以添加进`.bashrc`文件，使用上更方便

添加方式1：直接使用`gedit`或`vi`编辑`.bashrc`文件，最后添加该内容

添加方式2: `echo "source ~/工作空间/devel/setup.bash" >> ~/.bashrc` 别忘记 `source ~/.bashrc`哦

#### 1.3.3 HelloWorld (Python版)

本节内容基于1.3.1，假设你已经创建了ROS的工作空间，并且创建了ROS的功能包，那么就可以进入核心步骤了，使用Python编写程序实现：

##### 1.3.3.1 进入ros包添加script目录并编辑python文件

```shell
cd ros包
mkdir scripts
cd scripts
touch 自定义文件名.py
```

新建python文件：(文件名自定义)

```python
#! /usr/bin/env python

'''
	Python版的 HelloWorld
'''
import rospy

if __name__ == "__main__":
	
	rospy.init_node("Hello")
	rospy.loginfo("Hello World!!!!")
```

##### 1.3.3.2 为python文件添加可执行权限

```shell
chmod +x 自定义文件名.py
```

##### 1.3.3.3 编辑ros包下的CMakeLists.txt文件

````shell
catkin_install_python(PROGRAMS scripts/自定义文件名.py DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
````

##### 1.3.3.4 进入工作空间目录并解释

```shell
cd 自定义空间名称
catkin_make
```

##### 1.3.3.5 进入工作空间目录并执行

先启动命令行1:

```shell
roscore
```

再启动命令行2：

```shell
cd 自定义工作空间名称
source ./devel/setup.bash
rosrun 包名 自定义文件名.py
```

输出结果：Hello World!!!!

#### 1.4 ROS集成开发环境搭建

和大多数开发环境一样，理论上，在ROS中，只需要记事本就可以编写基本的ROS程序，但是工欲善其事必先利其器，为了提高开发效率，可以先安装集成开放工具和使用方便的工具: 终端、IDE...

#### 1.4.1 安装终端

在ROS中，需要频繁的使用到终端，且可能需要同时开启多个窗口，推荐一款较为好用的终端**Terminator**。效果如下：

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/terminator%E6%95%88%E6%9E%9C.PNG)

##### 1.4.1.1 安装

```shell
sudo apt install terminator
```

##### 1.4.1.2 添加到收藏夹

显示应用程序 ---> 搜索terminator ---> 右击 选择 添加到收藏夹

##### 1.4.1.3 Terminator 常用快捷键

第一部分: 关于在同一个标签内的操作

```
Alt+Up                          //移动到上面的终端
Alt+Down                        //移动到下面的终端
Alt+Left                        //移动到左边的终端
Alt+Right                       //移动到右边的终端
Ctrl+Shift+O                    //水平分割终端
Ctrl+Shift+E                    //垂直分割终端
Ctrl+Shift+Right                //在垂直分割的终端中将分割条向右移动
Ctrl+Shift+Left                 //在垂直分割的终端中将分割条向左移动
Ctrl+Shift+Up                   //在水平分割的终端中将分割条向上移动
Ctrl+Shift+Down                 //在水平分割的终端中将分割条向下移动
Ctrl+Shift+S                    //隐藏/显示滚动条
Ctrl+Shift+F                    //搜索
Ctrl+Shift+C                    //复制选中的内容到剪贴板
Ctrl+Shift+V                    //粘贴剪贴板的内容到此处
Ctrl+Shift+W                    //关闭当前终端
Ctrl+Shift+Q                    //退出当前窗口，当前窗口的所有终端都将被关闭
Ctrl+Shift+X                    //最大化显示当前终端
Ctrl+Shift+Z                    //最大化显示当前终端并使字体放大
Ctrl+Shift+N or Ctrl+Tab        //移动到下一个终端
Ctrl+Shift+P or Ctrl+Shift+Tab  //Crtl+Shift+Tab 移动到之前的一个终端
```

第二部分:有关各个标签之间的操作

```
F11                             //全屏开关
Ctrl+Shift+T                    //打开一个新的标签
Ctrl+PageDown                   //移动到下一个标签
Ctrl+PageUp                     //移动到上一个标签
Ctrl+Shift+PageDown             //将当前标签与其后一个标签交换位置
Ctrl+Shift+PageUp               //将当前标签与其前一个标签交换位置
Ctrl+Plus (+)                   //增大字体
Ctrl+Minus (-)                  //减小字体
Ctrl+Zero (0)                   //恢复字体到原始大小
Ctrl+Shift+R                    //重置终端状态
Ctrl+Shift+G                    //重置终端状态并clear屏幕
Super+g                         //绑定所有的终端，以便向一个输入能够输入到所有的终端
Super+Shift+G                   //解除绑定
Super+t                         //绑定当前标签的所有终端，向一个终端输入的内容会自动输入到其他终端
Super+Shift+T                   //解除绑定
Ctrl+Shift+I                    //打开一个窗口，新窗口与原来的窗口使用同一个进程
Super+i                         //打开一个新窗口，新窗口与原来的窗口使用不同的进程
```

#### 1.4.2 安装VSCode

VSCode全称Visual Studio Code，是微软推出的一款轻量级的代码编辑器，免费、开源而且功能强大。它支持几乎所有的主流的编程语言的语法高亮、智能代码补全、自定义热键、括号匹配、代码片段、代码比对Diff、Git等特性，支持插件扩展，并针对网页开发和云端应用开发做了优化。软件跨平台支持Win、Mac以及Linux。

#####  1.4.2.1 下载

vscode下载:https://code.visualstudio.com/docs?start=true

历史版本下载链接:  https://code.visualstudio.com/updates

##### 1.4.2.2 vscode安装与卸载

###### 1.4.2.2.1 安装

方式1：双击安装即可(或右击选择安装)

方式2：`sudo dpkg -i xxx.deb`

###### 1.4.2.2.2 卸载

```shell
sudo dpkg --purge code
```

##### 1.4.2.3 vscode集成ROS插件

使用VSCode开发ROS程序，需要先安装一些插件，常用插件如下:

![Snipaste_2024-09-19_14-47-47](Snipaste_2024-09-19_14-47-47.png)

![Snipaste_2024-09-19_14-48-03](Snipaste_2024-09-19_14-48-03.png)

![Snipaste_2024-09-19_14-48-15](Snipaste_2024-09-19_14-48-15.png)

![Snipaste_2024-09-19_14-48-32](Snipaste_2024-09-19_14-48-32.png)

##### 1.4.2.4 vscode 使用基本配置

###### 1.4.2.4.1 创建ROS工作空间

```shell
mkdir -p xxx_ws/src (必须得有 src)
cd xxx_ws
catkin_make  
```

###### 1.4.2.4.2 启动vscode

进入xxx_ws 启动 vscode

```shell
cd xxx_ws
code .
```

###### 1.4.2.4.3 vscode 中编译 ros

快捷键 `Ctrl + Shift +B` 调用编译，选择`catkin_make:build`

可以点击配置设置为默认，修改.vscode/tasks.json文件

```json
{
	// 有关 tasks.json 格式的文档，请参见
	   // https://go.microsoft.com/fwlink/?LinkId=73358
	"version":"2.0.0",
	"tasks":[
		{
			"label":"catkin_make:debug", // 代表提示的描述性信息
			"type":"shell",  // 可以选择shell或者process,如果是shell代码是在shell里面运行命令，如果是process代表作为一个进程来运行
			"command":"catkin_make", // 这个是我们需要运行的命令
			"args":[],  // 如果需要再命令后面添加一些后缀，可以写在这里，比如-DCATKIN_WHITELIST_PACKAGES="pac1;pac2"
			"groups":{"kind":"build","isDefault":true},
			"presentation":{
				"reveal":"always" // 可选always或者silence，代表是否输出信息
			}，
			"problemMatcher":"$msCompile"
		}
	]
}
```

###### 1.4.2.4.4 创建ROS功能包

选定src右击  ---> create catkin package

设置包名 添加依赖

###### 1.4.2.4.5 C++实现

在功能包的src下新建cpp文件

```C++
/*
	控制台输出 HelloVSCode !!!

*/
#include "ros/ros.h"

int main(int argc,char **argv)
{
	setlocale(LC_ALL,"");
	// 执行节点初始化
	ros::init(argc,argv,"HelloVSCode");
	// 输出日志
    ROS_INFO("Hello VSCode!!! 哈哈哈哈哈哈哈");
    return 0;
}
```

**PS1: 如果没有代码提示**

修改.vscode/c_cpp_properities.json

设置 "cppStandard":"c++17"

**PS2：main函数的参数不可以被const修饰**

**PS3：当ROS_INFO终端输出中有中文时，会出现乱码**

INFO: ??????????????????????????????????

解决办法：在函数开头加入下面代码的任意一句

```
setlocale(LC_CTYPE,"zh_CN.utf8");
setlocale(LC_ALL,"");
```

###### 1.4.2.4.6 Python实现

在功能包下新建scripts文件夹，添加python文件，**并添加可执行权限**

```python
#! /usr/bin/env python 
"""
	Python 版本的 HelloVSCode，执行在控制台输出HelloVSCode 
	实现
	1.导包
	2.初始化 ROS 节点
	3.日志输出 HelloWorld
"""

import rospy

if __name__ == "__main__":
	
	rospy.init_node("Hello_VSCode_o") # 2.初始化 ROS 节点
	rospy.loginfo("Hello VSCode，我是Python ........") # 3. 日志输出HelloWorld
```

###### 1.4.2.4.7 配置CMakeLists.txt

C++配置

```cmake
add_excutable(节点名称 src/c++源文件.cpp)
target_link_libraries(节点名称 ${catkin_LIBRARIES})
```

Python配置

```cmake 
catkin_install_python(PROGRAMS scripts/自定义文件名.py DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
```

###### 1.4.2.4.8 编译执行

编译: `Ctrl  + Shift + B`

执行：和之前一致，只是可以在VSCode中添加终端，首先执行：`source ./devel/setup.bash`

PS

如果不编译直接执行python文件，会抛出异常

1. 第一行解释器声明，可以使用绝对路径定位到python3的安装路径 #！/usr/bin/python3，但是不建议
2. 建议使用#! /usr/bin/env python但是会抛出异常： /usr/bin/env: "python": 没有那个文件或目录
3. 解决1： #!/usr/bin/env python3 直接使用python3 但是存在问题：不兼容之前的ROS相关的 python实现
4. 解决2：创建一个链接符号 python 命令：`sudo ln -s /usr/bin/python3 /usr/bin/python`

##### 1.4.2.5 其他IDE

ROS开发可以使用的IDE还是比较多的，除了上述的VSCode，还有Eclipse、QT、PyCharm、Robware ..... 详情可以参考官网介绍 :http://wiki.ros.org/IDEs

QT Creator Plugin for ROS，参考教程：https://ros-qtc-plugin.readthedocs.io/en/latest/

Roboware 参考: http://www.roboware.me/#/ (PS: Roboware 已经停止更新了)

#### 1.4.3 launch文件演示

1. 需求

   >一个程序中可能需要启动多个节点，比如：ROS内置的小乌龟案例，如果要控制乌龟运动，要启动多个窗口，分别启动roscore、乌龟界面节点、键盘控制节点。如果每次都调用rosrun逐一启动，显然效率低下，如何优化？

​			官方给出的优化策略是使用launch文件，可以一次性启动多个ROS节点

2. 实现

   1. 选定功能包右击---> 添加launch文件夹

   2. 选定launch文件夹右击 ---> 添加launch文件

   3. 编辑launch文件内容

      ```xml
      <launch>
      	<node pkg="hellworld" type="haha" name="hello" output="screen" />
          <node pkg="turtlesim" type="turtlesim_node" name="t1"/>
          <node pkg="turtlesim" type="turtle_teleop_key" name="key1"/>
      </launch>
      
      ```

      * node ---> 包含的某个节点
      * pkg ---> 功能包
      * type ---> 被运行的节点文件
      * name ---> 为节点命名
      * output ---> 设置日志的输出目标

   4. 运行launch文件

      `roslaunch 包名 launch文件名`

   5. 运行结果：一次性启动了多个节点

   ### 1.5 ROS架构

   到目前为止，我们已经安装了ROS，运行了ROS中内置的小乌龟案例，并且也编写了ROS小程序，对ROS也有了大概得认识，当然这个认知肯呢个还是比较模糊并不清晰的，接下来，我们要从宏观上来介绍一下ROS的架构设计。

   立足不同的角度，对ROS架构的描述也是不同的，一般我们可以从设计者、维护者、系统结构与自身结构4个角度来描述ROS结构：

   #### 1 设计者

   ROS**设计者**将ROS表述为“ROS = Plumbing + Tools + Capabilities + Ecosystem”

   + Plumbing: **通讯机制（实现ROS不同节点之间的交互）**
   + Tools:**工具软件包（ROS中的开发和调试工具）**
   + Capabilites: 机器人高层技能（ROS中某些功能的集合，比如：导航）
   + Ecosystem: 机器人生态系统（跨地域、跨软件与硬件的ROS联盟）

   #### 2 维护者

   立足**维护者**的角度：ROS架构可划分为两大部分

   + main：核心部分，主要由Willow Garage 和 一些开发者设计、提供以及维护。它提供了一些分布式计算的基本工具，以及整个ROS的核心部分的程序编写。
   + universe：全球范围的代码，有不同国家的ROS社区组织开发和维护。一种是库的代码，如OpenCV、PCL等；库的上一层是从功能角度提供的代码，如人脸识别，他们调用下层的库；最上层的代码是应用级的代码，让机器人完成某一确定的功能。

   #### 3 系统架构

   立足系统架构：ROS可以划分为三层

   + OS层，也即经典意义的操作系统

     ROS只是元操作系统，需要依托真正意义的操作系统，目前兼容性最好的是Linux的Ubuntu，Mac、Windows也支持ROS的较新的版本

   + 中间层

     是ROS封装的关于机器人的开发的中间件，比如：

     + 基于TCP/UDP继续封装 TCPROS/UDPROS通信系统
     + 用于进程间通信Nodelet，为数据的实时性传输提供支持
     + 另外，还提供了大量的机器人开发实现库，如：数据类型定义、坐标变换、运动控制 ... 

   + 应用层

       功能包，以及功能包内的节点，比如: master、turtlesim的控制与运动节点...

   #### 4 自身结构

   就ROS自身实现而言：也可以划分为三层

   + 文件系统

     ROS文件系统指的是在硬盘上面查看ROS源代码的组织形式

   + 计算图

     ROS分布式系统中不同进程需要进行数据交互，计算图可以以点对点的网络形式表现数据交互过程，计算图中的概念：节点（Node）、消息（message）、通讯机制__主题（topic）、通讯机制__服务（service）

   + 开源社区

     ROS的社区级概念是ROS网络上进行代码发布的一种表现形式

     + 发行版（Distribution） ROS发行版是可以独立安装、带有版本号的一些列综合功能包。ROS发行版像Linux发行版一样发挥类似的作用。这使得ROS软件安装更加容易，而且能够通过一个软件集合维持一致的版本。
     + 软件库（Repository）ROS依赖于共享开源代码与软件库的网站或主机服务，在这里不同的机构能够发布和分享各自的机器人软件与程序。
     + ROS维基（ROS Wiki） ROS Wiki是用于记录有关ROS系统信息的主要论坛。任何人都可以注册账户、贡献自己的文件、提供更正或更新、编写教程以及其他行为。网址是http://wiki.ros.org/
     + Bug提交系统（Bug Ticket System） 如果你发现问题或者想提出一个新功能，ROS提供这个资源去做这些
     + 邮箱列表（Mailing list）ROS用户邮箱列表是关于ROS的主要交流渠道，能够像论坛一样交流从ROS软件更新到ROS软件使用中的各种疑问或信息。网址是http://lists.ros.org/
     + ROS问答 (ROS Answer) 用户可以使用这个资源去提问。网址是https://answers.ros.org/questions/
     + 博客（Blog）你可以看到定期更新、照片和新闻。网址是https://www.ros.org/news/,不过博客系统已经退休，取而代之的是ROS社区，网址是https://discourse.ros.org/

   现在处于学习的初级阶段，只是运行了ROS的内置案例，编写了简单的ROS实现，因此，受限制于当前进度，不会详细介绍所有设计架构中的所有模块，当前只介绍系统与计算图，下一章会介绍ROS的通信机制，这也是ROS的核心实现之一。

   

#### 1.5.1 ROS文件系统

ROS文件系统指的是在硬盘上ROS源代码的组织形式，其结构大致可以如下图所示：

![img](http://www.autolabor.com.cn/book/ROSTutorials/assets/%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F.jpg)

```markdown
WorkSpace --- 自定义的工作空间
	|--- build:编译空间，用于存放CMake和catkin的缓存信息、配置信息和其他中间文件。
	|--- devel:开发空间，用于存放编译后生成的目标文件，包括头文件、动态&静态链接库、可执行文件等
	|--- src：源码
		|--- package：功能包（ROS基本单元）包含多个节点、库与配置文件，包名所有字母小写，只能有字母、数字与下划线组成
			|--- CMakeLists.txt 配置编译规则，比如源文件、依赖项、目标文件
			|--- package.xml 包信息，比如：包名、版本、作者、依赖项... (以前版本是manifest.xml)
			|--- scripts 存储python、shell文件
			|--- src 存储C++文件
			|--- include 头文件
			|--- msg 消息通信格式文件
			|--- srv 服务通信格式文件
			|--- action 动作格式文件
			|--- launch 可一次性运行多个节点
			|--- config 配置信息
		|--- CMakeLists.txt: 编译的基本配置
```

ROS文件系统中部分目录和文件前面编程中已经有所涉及，比如功能包的创建、src目录下cpp文件的编写、scripts目录下python文件的编写、launch目录下launch文件的编写，并且也配置了package.xml与CMakeLists.txt文件。其他目录下的内容后面教程会再行介绍，当前我们主要介绍：package.xml与CMakeLists.txt这两个配置文件。

##### 1 package.xml

 该文件定义有关软件包的属性，例如软件包名称，版本号，作者，维护者以及对其他catkin软件包的依赖性。请注意，该概念类似于旧版rosbuild构建系统中使用的manifest.xml文件。

```xml
<?xml version="1.0"?>
<!-- 格式：以前是 1,推荐使用格式 2 -->
<package format="2">
	<!-- 包名 -->
    <name>demo01_hello_vscode</name>
    <!-- 版本 -->
    <version>0.0.0</version>
    <!-- 描述信息 -->
    <description>The demo01_hello_vscode package</description>
</package>

```



