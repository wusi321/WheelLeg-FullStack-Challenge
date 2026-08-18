WheelLeg-FullStack-Challenge



«四连杆双轮腿小型机器人全栈开发综合考核»



项目类型： 机器人全栈研发能力考核

考核对象： 机械设计 / 机器人仿真 / ROS 2 / Linux / C++ / 嵌入式 / CAN / Git / GitHub 协作

推荐平台： Ubuntu 22.04 + ROS 2 Humble

核心要求： 必须形成从机械模型到仿真控制、Linux 开发环境、MCU 通信以及 Git 版本管理的完整工程闭环。



\---



一、项目背景



本项目要求参赛者/开发者完成一个四连杆双轮腿机器人的软件、硬件及仿真全栈开发。



由于实际轮腿机器人涉及机械加工、电机、驱动器、电池及安全风险，本项目原则上不要求实际制作机器人本体。



开发者应通过：



机械 CAD

&#x20;  ↓

URDF / Xacro

&#x20;  ↓

机器人动力学模型

&#x20;  ↓

Gazebo / ROS 2 仿真

&#x20;  ↓

C++ 控制器

&#x20;  ↓

Sim2Sim

&#x20;  ↓

MCU 控制程序

&#x20;  ↓

CAN 通信



建立完整的机器人研发流程。



最终应能够证明：



«开发者具备独立完成一个小型轮腿机器人从机械建模、机器人描述、仿真、控制算法、Linux 环境搭建、嵌入式通信到工程版本管理的能力。»



\---



二、总体系统架构



推荐系统架构如下：



&#x20;                       GitHub

&#x20;                         │

&#x20;                ┌────────┴────────┐

&#x20;                │                 │

&#x20;            主分支 main       开发分支 develop

&#x20;                │                 │

&#x20;      ┌─────────┼──────────┬──────┴──────┐

&#x20;      │         │          │             │

&#x20;    机械      仿真       Linux         嵌入式

&#x20;      │         │          │             │

&#x20;    CAD       URDF       Ubuntu          MCU

&#x20;      │         │          │             │

&#x20;      └─────────┴──────────┴─────────────┘

&#x20;                        │

&#x20;                       ROS 2

&#x20;                        │

&#x20;                    C++ Controller

&#x20;                        │

&#x20;             ┌──────────┴──────────┐

&#x20;             │                     │

&#x20;          Simulation             MCU

&#x20;             │                     │

&#x20;         Sim2Sim                CAN

&#x20;             │                     │

&#x20;             └──────────┬──────────┘

&#x20;                        │

&#x20;                   Wheel-Leg Robot



\---



三、考核目标



开发者最终需要完成以下六个核心部分：



1\. 机械结构设计

2\. 机器人 URDF/Xacro 建模

3\. ROS 2 + C++ 仿真控制

4\. Ubuntu/Linux 机器人开发环境

5\. MCU + CAN 嵌入式系统

6\. Git/GitHub 版本管理与团队协作



六个部分必须最终形成一个完整工程，而不是六个相互独立的小实验。



\---



四、机械设计部分



4.1 机器人结构



机器人采用：



«双轮 + 四连杆腿机构»



基本结构：



&#x20;       机身

&#x20;  ┌───────────┐

&#x20;  │           │

&#x20;  └───────────┘

&#x20;      │     │

&#x20;     四连杆 四连杆

&#x20;      │     │

&#x20;     ○       ○

&#x20;   左轮     右轮



左右两侧腿部均采用四连杆结构。



允许开发者自行确定：



\- 连杆长度

\- 轮径

\- 轮距

\- 机身尺寸

\- 电机安装方式

\- 关节位置

\- 轮轴位置

\- 关节限位



但必须满足机械结构的运动学合理性。



\---



五、CAD 建模要求



机械模型必须使用三维 CAD 软件完成。



推荐：



\- SolidWorks

\- Fusion 360

\- Creo

\- FreeCAD

\- 其他能够导出标准三维模型的软件



5.1 必须提交



至少包含：



CAD/

├── Assembly/

├── Parts/

├── Drawing/

├── STEP/

└── README.md



需要提供：



\- 完整装配体

\- 所有关键零件

\- 四连杆机构

\- 左右轮

\- 机器人主体

\- 电机安装位置

\- 关节连接关系

\- 关键尺寸图



\---



六、机械设计真实性要求



禁止仅为了仿真而随意建立一个没有工程意义的模型。



必须保证：



6.1 尺寸合理



需要明确：



\- 总长度

\- 总宽度

\- 总高度

\- 轮径

\- 轮距

\- 连杆长度

\- 关节间距

\- 最大腿展

\- 最小腿展



6.2 质量合理



每个主要刚体必须具有合理质量。



例如：



Body

├── chassis

├── left\_link\_1

├── left\_link\_2

├── left\_link\_3

├── left\_wheel

├── right\_link\_1

├── right\_link\_2

├── right\_link\_3

└── right\_wheel



不得全部使用：



mass = 1 kg



等明显不合理的统一参数。



6.3 惯量合理



必须提供：



ixx

iyy

izz

ixy

ixz

iyz



或者由 CAD 软件根据真实材料及几何模型计算。



禁止随意填写惯量参数。



\---



七、URDF / Xacro 要求



必须将机械模型转换为：



URDF



或者：



Xacro → URDF



推荐使用 Xacro。



目录示例：



robot\_description/

├── urdf/

│   ├── wheelleg.xacro

│   ├── materials.xacro

│   └── transmissions.xacro

├── meshes/

├── rviz/

└── launch/



必须正确描述：



\- link

\- joint

\- visual

\- collision

\- inertial

\- joint limit

\- joint axis

\- transmission（如使用）

\- material



\---



八、URDF 验证



必须能够通过 ROS 2 工具验证：



check\_urdf



并能够在 RViz 2 中正确显示机器人。



要求：



CAD模型

&#x20;   ↓

URDF

&#x20;   ↓

RViz



三者结构必须一致。



\---



九、仿真部分



9.1 仿真平台



推荐：



«Ubuntu 22.04 + ROS 2 Humble + Gazebo»



也允许使用其他 ROS 2 兼容仿真平台，但必须能够加载提交的 URDF/Xacro。



\---



十、机器人基本运动



必须实现：



10.1 前进



机器人能够：



↑



沿机器人自身前方运动。



10.2 后退



机器人能够：



↓



10.3 左转



↺



10.4 右转



↻



10.5 跳跃



机器人必须能够通过腿部运动产生：



压缩

&#x20;↓

蓄力

&#x20;↓

伸展

&#x20;↓

离地

&#x20;↓

空中

&#x20;↓

落地



\---



十一、仿真控制器



机器人控制程序必须使用：



«C++»



完成。



禁止使用 Python 作为最终机器人控制器。



例如：



wheelleg\_controller/

├── include/

├── src/

│   ├── controller.cpp

│   ├── kinematics.cpp

│   ├── dynamics.cpp

│   ├── balance.cpp

│   └── trajectory.cpp

├── config/

└── launch/



允许 Python 用于：



\- 数据分析

\- 绘图

\- 数据集处理

\- 自动测试

\- 辅助工具



但：



«核心机器人控制逻辑必须由 C++ 实现。»



\---



十二、控制系统最低要求



至少实现以下控制链：



用户指令

&#x20;  ↓

ROS 2 Topic

&#x20;  ↓

C++ Controller

&#x20;  ↓

运动学计算

&#x20;  ↓

关节目标

&#x20;  ↓

Gazebo

&#x20;  ↓

机器人运动



例如：



/cmd\_vel

&#x20;   ↓

WheelLegController

&#x20;   ↓

inverse kinematics

&#x20;   ↓

joint command

&#x20;   ↓

Gazebo



\---



十三、Sim2Sim 要求



由于实际机器人制造成本较高，本项目必须提供：



«Sim2Sim 非实机演示机制»



要求控制器不能与具体仿真器强耦合。



推荐架构：



&#x20;                C++ Controller

&#x20;                      │

&#x20;                Controller API

&#x20;                      │

&#x20;            ┌─────────┴─────────┐

&#x20;            │                   │

&#x20;       Simulation A        Simulation B

&#x20;            │                   │

&#x20;         Gazebo            其他仿真器



同一套控制逻辑至少能够在不同仿真环境中运行，或者能够在：



仿真模型

&#x20;     ↓

机器人状态

&#x20;     ↓

控制器

&#x20;     ↓

模拟执行器



之间进行完整闭环。



\---



十四、仿真评分



总分建议设置为：



25 分



项目| 分值

URDF 正确加载| 3

关节运动正确| 3

前进| 3

后退| 3

左转| 3

右转| 3

跳跃| 5

Sim2Sim| 2



\---



十五、Linux 开发环境



要求开发者在：



«Ubuntu 22.04»



环境完成开发。



允许：



\- VMware 虚拟机

\- 实体 PC

\- ARM 开发板

\- x86 上位机

\- 其他 Ubuntu 22.04 环境



\---



十六、Linux 用户与权限配置



必须创建：



用户：

wheelleg



用户组：

wheelleg



要求：



useradd

groupadd

usermod



完成账户配置。



\---



十七、用户权限要求



"wheelleg" 用户必须具有机器人开发所需权限。



至少包括：



USB



能够访问：



/dev/ttyUSB\*

/dev/ttyACM\*



串口



能够进行：



USB → UART



开发。



GPIO



能够访问 Linux GPIO 接口。



摄像头



能够访问：



/dev/video\*



例如：



v4l2-ctl



能够识别摄像头。



CAN



能够使用：



can0



或者虚拟 CAN：



vcan0



\---



十八、Linux 权限验收



必须提供测试脚本：



linux/

├── setup\_user.sh

├── setup\_permissions.sh

├── check\_usb.sh

├── check\_camera.sh

├── check\_gpio.sh

├── check\_can.sh

└── README.md



执行：



./check\_environment.sh



能够自动检查开发环境。



\---



十九、ROS 2 环境



必须正确配置：



ROS 2 Humble



并保证：



ros2 --version



以及：



ros2 topic list

ros2 node list

ros2 run

ros2 launch



可以正常工作。



\---



二十、嵌入式系统部分



开发者自行选择 MCU。



允许：



\- STM32

\- MSPM0

\- ESP32

\- GD32

\- NXP

\- Renesas

\- 其他具有 CAN 能力的 MCU



但必须说明：



MCU型号

CPU架构

主频

Flash

RAM

CAN外设

开发环境



\---



二十一、MCU 基础功能



必须完成：



MCU

&#x20;│

&#x20;├── IMU

&#x20;│

&#x20;├── UART

&#x20;│

&#x20;├── CAN

&#x20;│

&#x20;└── 控制接口



至少实现：



IMU



能够读取：



加速度

角速度



建议进一步提供：



姿态角

四元数



\---



二十二、CAN 通信



MCU 必须能够：



接收



上位机

&#x20;  ↓

CAN

&#x20;  ↓

MCU



接收控制数据。



例如：



ID: 0x101



Byte0\~1: 左轮目标速度

Byte2\~3: 右轮目标速度

Byte4\~5: 左腿目标位置

Byte6\~7: 右腿目标位置



发送



MCU 必须能够：



MCU

&#x20;↓

CAN

&#x20;↓

上位机



发送：



IMU

电机状态

关节位置

速度

故障状态



\---



二十三、CAN 协议文档



必须在仓库中提供：



docs/can\_protocol.md



至少说明：



CAN ID

数据长度

Byte定义

数据类型

缩放系数

单位

发送周期



例如：



ID| 类型| 周期| 内容

0x101| Control| 10ms| 机器人控制

0x201| IMU| 10ms| IMU数据

0x301| Status| 20ms| MCU状态



\---



二十四、嵌入式测试



至少完成：



MCU启动

&#x20;↓

读取IMU

&#x20;↓

解析控制命令

&#x20;↓

生成CAN帧

&#x20;↓

发送CAN



建议使用：



Linux SocketCAN



与 MCU 进行联调。



\---



二十五、Linux ↔ MCU 联调



最终要求实现：



ROS 2

&#x20;↓

C++ Controller

&#x20;↓

CAN

&#x20;↓

MCU

&#x20;↓

IMU

&#x20;↓

CAN

&#x20;↓

Linux



即形成一个基本闭环。



在没有实际机器人执行器的情况下，可以使用：



MCU

&#x20;↓

CAN

&#x20;↓

Linux

&#x20;↓

虚拟执行器



模拟完整系统。



\---



二十六、Git / GitHub 版本管理



本项目强制使用 Git。



必须建立 GitHub 仓库。



不得最后一次性上传整个项目。



必须保留开发历史。



\---



二十七、推荐 Git 分支结构



main

│

├── develop

│

├── feature/mechanical

├── feature/urdf

├── feature/simulation

├── feature/controller

├── feature/linux

├── feature/embedded

└── feature/can



如果多人协作：



feature/<name>/<module>



例如：



feature/zhangsan/controller

feature/lisi/urdf

feature/wangwu/embedded



\---



二十八、Commit 要求



Commit 必须能够体现真实开发过程。



推荐：



feat: add four bar linkage model



feat: add wheelleg urdf



feat: implement forward controller



feat: add jump trajectory



fix: correct wheel joint axis



fix: correct inertial parameters



feat: add CAN protocol



feat: add Linux permission script



禁止：



update

test

aaa

111

final

final\_final

final\_final2



等无法描述实际工作的提交信息。



\---



二十九、Tag 版本管理



必须建立正式版本：



v0.1.0

v0.2.0

v0.3.0

v1.0.0



推荐：



v0.1.0

机械模型完成



v0.2.0

URDF完成



v0.3.0

ROS 2仿真完成



v0.4.0

C++控制器完成



v0.5.0

Linux环境完成



v0.6.0

MCU + CAN完成



v1.0.0

最终验收版本



\---



三十、版本里程碑



建议至少存在以下 Tag：



Tag| 要求

v0.1.0| CAD基础模型

v0.2.0| URDF

v0.3.0| ROS 2仿真

v0.4.0| C++控制器

v0.5.0| Linux环境

v0.6.0| MCU

v0.7.0| CAN通信

v0.8.0| Sim2Sim

v1.0.0| 最终版本



\---



三十一、GitHub 协作



多人开发时，每个人必须：



1\. 使用自己的 Git 身份

2\. 使用自己的分支

3\. 独立提交 Commit

4\. 通过 Pull Request 合并

5\. 在 PR 中说明修改内容

6\. 保留 Review 记录



禁止：



«一个人完成所有内容，其他人最后直接复制代码并提交。»



\---



三十二、贡献证明机制



本项目采用：



«Git History + Commit + Branch + Tag + Pull Request»



作为开发贡献证明。



如果某个模块只有最终一次提交：



Add everything



而没有对应开发历史，则该模块的个人贡献无法得到充分证明。



\---



三十三、多人协作示例



例如三人团队：



张三

机械 + URDF



李四

ROS2 + C++



王五

MCU + CAN



GitHub：



main

&#x20;│

&#x20;└── develop

&#x20;     │

&#x20;     ├── feature/zhangsan/mechanical

&#x20;     ├── feature/zhangsan/urdf

&#x20;     │

&#x20;     ├── feature/lisi/ros2

&#x20;     ├── feature/lisi/controller

&#x20;     │

&#x20;     ├── feature/wangwu/mcu

&#x20;     └── feature/wangwu/can



每个人必须能够通过 Git 历史证明自己的开发过程。



\---



三十四、最终仓库结构



推荐最终仓库：



WheelLeg-FullStack-Challenge/

│

├── README.md

├── LICENSE

├── .gitignore

│

├── docs/

│   ├── requirements.md

│   ├── architecture.md

│   ├── can\_protocol.md

│   ├── coordinate\_system.md

│   └── development\_log.md

│

├── mechanical/

│   ├── CAD/

│   ├── STEP/

│   ├── Drawing/

│   └── README.md

│

├── robot\_description/

│   ├── urdf/

│   ├── xacro/

│   ├── meshes/

│   ├── rviz/

│   └── launch/

│

├── simulation/

│   ├── worlds/

│   ├── models/

│   ├── plugins/

│   ├── config/

│   └── launch/

│

├── controller/

│   ├── include/

│   ├── src/

│   ├── config/

│   ├── launch/

│   └── CMakeLists.txt

│

├── linux/

│   ├── setup/

│   ├── scripts/

│   ├── permissions/

│   └── README.md

│

├── embedded/

│   ├── firmware/

│   ├── drivers/

│   ├── imu/

│   ├── can/

│   └── README.md

│

├── tools/

│   ├── can\_tools/

│   ├── simulation\_tools/

│   └── data\_analysis/

│

├── tests/

│   ├── mechanical/

│   ├── urdf/

│   ├── simulation/

│   ├── controller/

│   ├── linux/

│   └── can/

│

└── .github/

&#x20;   ├── workflows/

&#x20;   ├── ISSUE\_TEMPLATE/

&#x20;   └── pull\_request\_template.md



\---



三十五、自动化测试



建议最终加入 CI。



例如：



Push

&#x20;↓

GitHub Actions

&#x20;↓

Ubuntu

&#x20;↓

安装 ROS 2

&#x20;↓

编译

&#x20;↓

运行测试

&#x20;↓

检查 URDF

&#x20;↓

检查 C++

&#x20;↓

输出结果



至少自动检查：



colcon build



以及：



check\_urdf



\---



三十六、最终演示要求



最终不要求实体机器人。



必须提供：



Demo 1：机械



展示：



CAD

&#x20;↓

装配体

&#x20;↓

四连杆运动



Demo 2：URDF



展示：



URDF

&#x20;↓

RViz



Demo 3：仿真



展示：



前进

后退

左转

右转

跳跃



Demo 4：Linux



展示：



wheelleg用户

ROS2

USB

Camera

GPIO

CAN



Demo 5：MCU



展示：



IMU

&#x20;↓

MCU

&#x20;↓

CAN

&#x20;↓

Linux



Demo 6：GitHub



展示：



Commit

Branch

PR

Tag

Release



\---



三十七、最终评分标准



总分：



100 分



模块| 分值

机械设计| 15

URDF / 机器人描述| 10

ROS 2 + 仿真| 20

C++ 控制器| 10

Linux 开发环境| 10

MCU + IMU| 10

CAN 通信| 10

Git / GitHub| 10

工程文档| 5

总分| 100



\---



三十八、机械设计：15分



项目| 分值

四连杆机构设计| 4

CAD完整性| 3

尺寸合理性| 2

质量参数| 2

惯量参数| 2

工程图/设计说明| 2



\---



三十九、URDF：10分



项目| 分值

Link / Joint正确| 3

Visual / Collision| 2

Inertial| 2

Joint Axis / Limit| 2

RViz正确显示| 1



\---



四十、ROS 2 + 仿真：20分



项目| 分值

ROS 2工程| 3

Gazebo加载| 3

前进| 2

后退| 2

左转| 2

右转| 2

跳跃| 4

Sim2Sim| 2



\---



四十一、C++控制器：10分



项目| 分值

C++ ROS 2 Node| 2

控制架构| 2

运动学| 2

轨迹规划| 2

控制稳定性| 2



\---



四十二、Linux：10分



项目| 分值

wheelleg用户/组| 2

USB/串口权限| 2

Camera权限| 1

GPIO权限| 1

CAN权限| 2

ROS 2环境| 2



\---



四十三、嵌入式：20分



项目| 分值

MCU工程| 3

IMU读取| 4

CAN接收| 4

CAN发送| 4

Linux-MCU联调| 3

协议文档| 2



\---



四十四、Git / GitHub：10分



项目| 分值

Git仓库| 1

Branch| 2

Commit历史| 2

Tag| 2

Pull Request| 1

多人协作| 2



\---



四十五、严重扣分项



以下行为可以直接扣除对应模块的大量分数：



1\. 最后一次性上传



git add .

git commit -m "final"



无法证明开发过程。



2\. 使用他人代码但不注明



视为工程诚信问题。



3\. 机械模型与 URDF 不一致



例如：



CAD轮径 ≠ URDF轮径

CAD质量 ≠ URDF质量

CAD关节位置 ≠ URDF



按照实际误差扣分。



4\. Python 替代 C++ 控制器



核心控制程序使用 Python：



«C++ 控制器部分原则上不得分。»



5\. 没有 Sim2Sim



无法完成非实机演示：



«仿真部分最高分受限。»



6\. Git 历史缺失



如果某模块要求个人独立完成，但 Git 中不存在对应开发历史：



«该部分只能根据能够证明的实际贡献评分。»



\---



四十六、建议增加的“隐藏加分项”



为了让这个考核真正具备区分度，可以增加最高 10 分 Bonus。



+2：自动化部署



实现：



./install.sh



自动完成：



ROS 2环境检查

依赖安装

workspace创建

colcon build



+2：自动化测试



例如：



./test.sh



自动测试 URDF、ROS 2、CAN 等。



+2：Docker



提供：



Dockerfile

docker-compose.yml



实现开发环境复现。



+2：CI/CD



GitHub Actions 自动：



Build

Test

URDF Check



+2：仿真与实机接口统一



实现：



Simulation Backend

&#x20;       │

&#x20;       ├── Gazebo

&#x20;       │

&#x20;       └── Hardware



两者使用统一控制接口。



\---



四十七、最终交付物



最终提交必须包含：



1\. GitHub仓库

2\. CAD模型

3\. STEP模型

4\. URDF/Xacro

5\. ROS 2工程

6\. Gazebo仿真

7\. C++控制器

8\. Linux环境配置

9\. MCU固件

10\. CAN协议

11\. 测试脚本

12\. 项目文档

13\. Demo视频

14\. Git提交历史

15\. Branch

16\. Tag

17\. Release



\---



四十八、最终验收标准



项目最终必须能够回答以下问题：



你设计的机器人是什么？

&#x20;       ↓

机械结构为什么这样设计？

&#x20;       ↓

CAD模型是否真实？

&#x20;       ↓

质量和惯量从哪里来？

&#x20;       ↓

如何转换成URDF？

&#x20;       ↓

URDF是否正确？

&#x20;       ↓

ROS 2如何控制？

&#x20;       ↓

控制器为什么使用C++？

&#x20;       ↓

机器人能否前进？

&#x20;       ↓

能否后退？

&#x20;       ↓

能否转向？

&#x20;       ↓

能否跳跃？

&#x20;       ↓

能否Sim2Sim？

&#x20;       ↓

Linux环境是否独立配置？

&#x20;       ↓

MCU如何读取IMU？

&#x20;       ↓

MCU如何发送CAN？

&#x20;       ↓

上位机如何接收CAN？

&#x20;       ↓

Git如何管理？

&#x20;       ↓

谁完成了什么？

&#x20;       ↓

Git历史能否证明？



\---



四十九、项目核心思想



本考核不是要求开发者：



«“把一个机器人做出来”。»



而是要求开发者证明：



«“我能够按照现代机器人研发流程，从零建立一个可复现、可验证、可协作、可维护的机器人软件系统。”»



因此：



机械

&#x20;↓

模型

&#x20;↓

URDF

&#x20;↓

仿真

&#x20;↓

控制

&#x20;↓

Linux

&#x20;↓

MCU

&#x20;↓

CAN

&#x20;↓

Git

&#x20;↓

CI

&#x20;↓

Release



应当被视为一个完整系统。



\---



五十、推荐仓库名称



最终推荐：



WheelLeg-FullStack-Challenge



GitHub 仓库简介可以写成：



«A full-stack engineering challenge for a four-bar linkage dual-wheel-leg robot, covering mechanical design, URDF, ROS 2, simulation, C++ control, embedded systems, CAN communication, Linux and GitHub collaboration.»



建议仓库 Topics：



wheel-leg

robotics

ros2

gazebo

cpp

embedded

can-bus

linux

urdf

simulation

sim2sim

git

robot-control

four-bar-linkage

