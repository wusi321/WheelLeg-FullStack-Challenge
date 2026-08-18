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
| Git/GitHub 协作 | [`git/`](git/) | 10 |
| 工程文档 | [`docs/`](docs/) | 5 |
| **合计** |  | **100** |

每个模块的题目、交付物和评分细则写在对应目录的 `README.md` 中。轮足外形和六电机约束见 [`docs/wheelleg_geometry.md`](docs/wheelleg_geometry.md)，机械 CNC/铨洲平台验收见 [`mechanical/CNC/README.md`](mechanical/CNC/README.md)，遥控器、订阅 Topic 和演示输入见 [`docs/remote_control.md`](docs/remote_control.md)。模块之间必须使用同一套尺寸、质量、坐标系和接口，不能提交互相独立的小实验。

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

CAD/STEP、逐零件 CNC 上传清单与铨洲预览截图、URDF/Xacro、ROS 2/Gazebo 工程、C++ 控制器、Linux 配置脚本、MCU 固件、[`docs/can_protocol.md`](docs/can_protocol.md)、[`docs/remote_control.md`](docs/remote_control.md)、测试脚本、演示视频和完整 Git 历史均为验收材料。

## 开源协议

本仓库采用 [MIT License](LICENSE) 开源。你可以在遵守许可证条款并保留版权和许可声明的前提下使用、复制、修改、合并、发布和再许可本项目。提交者应确保新增代码、模型、图片、数据和文档具有合法来源，并分别遵守第三方素材的原始许可证；MIT 协议不代表铨州平台、硬件厂商或第三方模型的授权。

## 参与测试与成品回传

欢迎参与测试、仿真、CNC 可制造性验证和真实硬件联调。建议以本仓库的目录架构、接口约定、提交规范和分支策略作为实现基础，优先复用已有文档和测试入口，并在修改时同步记录参数、环境和已知限制。

完成一个可运行的仿真或实体成品后，欢迎将成果回传到本仓库的其他分支，供后续评审和复现：

1. 从 `develop` 创建 `submission/<姓名>/<版本>` 分支；多人协作可使用 `submission/<团队>/<版本>`。
2. 保留真实 Commit 历史，不要把全部成果压缩成一次 `final` 提交，也不要直接覆盖 `main` 或 `develop`。
3. 在分支中补充成品说明、构建/烧录命令、测试日志、演示视频链接、CAD/URDF 参数一致性说明，以及铨州平台预览加工截图。
4. 推送分支并创建 Pull Request，目标分支建议为 `develop`；在 PR 中说明硬件版本、控制模式、已知问题和复现步骤。

如果没有本仓库写权限，可以先 Fork 后使用同样的分支命名和 Pull Request 流程。项目维护者会根据可复现性、文档完整性和许可证合规情况进行 Review，并将合格成果合并或保留在对应分支中。

## 严重扣分与加分

一次性使用 `git add .` + `final` 提交、未注明的他人代码、CAD 与 URDF 不一致、用 Python 替代核心 C++ 控制器、缺少 Sim2Sim 或缺少模块开发历史，会导致对应模块大幅扣分。自动部署、自动测试、Docker、CI/CD、统一仿真/实机接口各可加 2 分，Bonus 最高 10 分。
