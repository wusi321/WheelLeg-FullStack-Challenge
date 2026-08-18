# Ubuntu/Linux 开发环境题目（10 分）

## 题目说明

在 Ubuntu 22.04 配置独立机器人开发环境，创建 `wheelleg` 用户和同名用户组，使用 `useradd`、`groupadd`、`usermod` 完成配置。该用户应能访问 `/dev/ttyUSB*`、`/dev/ttyACM*`、`/dev/video*`、Linux GPIO 以及 `can0`/`vcan0`，并能运行 ROS 2 Humble。纯上位机方案还需验证 GPIO 或 USB-CAN；上下位机联合方案需验证 USB-TTL/串口到下位机；纯下位机方案需说明为何不依赖上位机。

## 交付物

提供 `setup/`、`scripts/`、`permissions/` 和可重复执行的脚本：用户/权限初始化、USB/串口、摄像头（可用 `v4l2-ctl`）、GPIO、CAN、ROS 2 检查。脚本应处理设备不存在、权限不足和虚拟 CAN 等情况。

## 评分

| 项目 | 分值 |
| --- | ---: |
| `wheelleg` 用户与用户组 | 2 |
| USB/串口权限 | 2 |
| 摄像头权限与检测 | 1 |
| GPIO 权限与检测 | 1 |
| CAN 权限与 `can0`/`vcan0` 检测 | 2 |
| ROS 2 Humble 环境与上位机控制链路 | 2 |

## 验收

以普通 `wheelleg` 用户执行环境检查，并展示 `ros2 --version`、`ros2 topic list`、`ros2 node list`、`ros2 run` 和 `ros2 launch` 的结果。纯下位机方案若无 ROS 2/上位机，可凭完整下位机控制、仿真部署、权限说明和日志，获得本项最多 1/2 分；纯上位机或上下位机联合方案按完整控制链路验收。
