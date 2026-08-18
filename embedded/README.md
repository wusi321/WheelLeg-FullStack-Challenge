# MCU 与 IMU 嵌入式题目（10 分）

## 题目说明

自行选择具备 CAN 能力的 MCU（如 STM32、MSPM0、ESP32、GD32、NXP、Renesas）。必须说明型号、CPU 架构、主频、Flash、RAM、CAN 外设和开发环境。建立 MCU 工程，接入 IMU、UART、CAN 和控制接口，至少读取加速度与角速度，建议提供姿态角/四元数。

## 交付物

`firmware/`、`drivers/`、`imu/`、启动和构建说明、硬件连接图、IMU 读取测试、异常/超时处理，以及与 Linux 联调的日志。CAN 帧格式见 [`../docs/can_protocol.md`](../docs/can_protocol.md)。

## 评分

| 项目 | 分值 |
| --- | ---: |
| MCU 工程、启动和构建 | 3 |
| IMU 读取、标定和数据输出 | 4 |
| Linux-MCU 联调闭环 | 3 |

CAN 收发另按 [`can/README.md`](can/README.md) 的 10 分评分，嵌入式与 CAN 合计 20 分。
