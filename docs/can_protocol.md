# CAN 通信协议（待实现）

本文件是 MCU 与 Linux/C++ 控制器的接口契约。实际提交时必须补齐字节序、数据类型、缩放系数、单位、周期和故障处理，并与固件代码一致。

| CAN ID | 类型 | DLC | 周期 | 内容 |
| --- | --- | ---: | ---: | --- |
| `0x101` | Control | 8 | 10 ms | 左轮速度、右轮速度、左腿位置、右腿位置 |
| `0x110` | RemoteCommand | 8 | 20 ms | 遥控器模式、速度、子命令、急停和序号，详见 [`remote_control.md`](remote_control.md) |
| `0x102` | LegTarget | 8 | 10 ms | 四个腿部电机目标：左 1/2、右 1/2 |
| `0x103` | WheelTarget | 8 | 10 ms | 两个轮足电机目标：左轮、右轮 |
| `0x201` | IMU | 8 | 10 ms | 加速度与角速度（或分帧说明） |
| `0x301` | Status | 8 | 20 ms | 电机状态、关节位置、速度、故障码 |

## Control `0x101`

Byte 0~1 左轮目标速度，Byte 2~3 右轮目标速度，Byte 4~5 左腿目标位置，Byte 6~7 右腿目标位置。必须声明有符号性、端序、缩放系数和范围。

## 6 电机映射

`0x101` 可传输左右轮和左右腿高层目标，由下位机运动学展开为六路目标。若需要直接控制电机，使用以下扩展帧：

- `0x102`：Byte 0~1 `left_leg_motor_1`，Byte 2~3 `left_leg_motor_2`，Byte 4~5 `right_leg_motor_1`，Byte 6~7 `right_leg_motor_2`；均为小端 `int16`，位置单位 rad 或速度单位 rad/s，缩放系数必须在实现中固定并记录。
- `0x103`：Byte 0~1 `left_wheel_motor`，Byte 2~3 `right_wheel_motor`，Byte 4 `mode`，Byte 5 `flags`，Byte 6 `sequence`，Byte 7 保留；轮足目标单位为 rad/s，缩放系数必须记录。

三种控制部署模式可使用同一组帧：纯上位机通过 USB-CAN/GPIO 发送，联合模式由下位机转发/展开，纯下位机由本地控制器生成。必须声明 ID、周期和仲裁优先级。

## 验收

使用 `can0` 或 `vcan0` 完成收发抓包；提供正常帧、边界值、超时和故障状态的测试记录。
