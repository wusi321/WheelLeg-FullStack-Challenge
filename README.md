# WheelLeg-FullStack-Challenge

四连杆双轮腿小型机器人的全栈开发综合考核。项目覆盖机械设计、机器人描述、ROS 2 仿真、C++ 控制、Linux 开发环境、MCU/CAN 通信以及 GitHub 协作。

## 考核目标

参赛者需要建立从 CAD 到 URDF/Xacro、Gazebo/ROS 2、C++ 控制器、Sim2Sim、MCU、CAN，再到 Git 版本管理的可复现工程闭环。不要求制造实体机器人，但必须提供可验证的仿真和通信演示。

## 模块入口

| 模块 | 目录 | 满分 |
| --- | --- | ---: |
| 机械结构与 CAD | [`mechanical/`](mechanical/) | 15 |
| URDF/Xacro 机器人描述 | [`robot_description/`](robot_description/) | 10 |
| ROS 2 与 Gazebo 仿真 | [`simulation/`](simulation/) | 20 |
| C++ 控制器 | [`controller/`](controller/) | 10 |
| Ubuntu/Linux 开发环境 | [`linux/`](linux/) | 10 |
| MCU 与 IMU | [`embedded/`](embedded/) | 10 |
| CAN 通信 | [`embedded/can/`](embedded/can/) | 10 |
| Git/GitHub 协作 | [`docs/development_log.md`](docs/development_log.md) | 10 |
| 工程文档 | [`docs/`](docs/) | 5 |
| **合计** |  | **100** |

每个模块的题目、交付物和评分细则写在对应目录的 `README.md` 中。模块之间必须使用同一套尺寸、质量、坐标系和接口，不能提交互相独立的小实验。

## 推荐环境

- Ubuntu 22.04（实体机、虚拟机、x86 上位机或 ARM 开发板均可）
- ROS 2 Humble
- Gazebo 或其他可加载 ROS 2 URDF/Xacro 的仿真器
- C++17 及以上、CMake、`colcon`
- 具备 CAN 外设的 MCU，或 `vcan0` 虚拟 CAN

## 推荐工作流

1. 阅读 [`docs/requirements.md`](docs/requirements.md) 和各模块说明。
2. 先完成 CAD 与参数表，再生成 URDF/Xacro，确保两者一致。
3. 在 Gazebo/RViz 中验证模型，随后接入 C++ 控制器并完成前进、后退、转向和跳跃。
4. 通过抽象控制接口完成 Sim2Sim，再接入 MCU、IMU 和 CAN 闭环。
5. 使用功能分支、描述性 Commit、Tag 和 Pull Request 保留真实开发历史。

## 最终交付

CAD/STEP、URDF/Xacro、ROS 2/Gazebo 工程、C++ 控制器、Linux 配置脚本、MCU 固件、[`docs/can_protocol.md`](docs/can_protocol.md)、测试脚本、演示视频和完整 Git 历史均为验收材料。

## 严重扣分与加分

一次性使用 `git add .` + `final` 提交、未注明的他人代码、CAD 与 URDF 不一致、用 Python 替代核心 C++ 控制器、缺少 Sim2Sim 或缺少模块开发历史，会导致对应模块大幅扣分。自动部署、自动测试、Docker、CI/CD、统一仿真/实机接口各可加 2 分，Bonus 最高 10 分。
