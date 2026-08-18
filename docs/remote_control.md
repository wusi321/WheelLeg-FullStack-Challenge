# 遥控器、订阅接口与演示控制

## 1. 控制输入来源

键盘、模拟 Web 页面、实体遥控器和上位机程序都必须转换为同一套 `RemoteCommand` 语义。这样更换输入设备不会修改核心 C++ 控制器。

推荐的 ROS 2 接口如下：

| 节点 | 方向 | Topic | 消息/用途 |
| --- | --- | --- | --- |
| keyboard/web/joystick | 发布 | `/wheelleg/remote_cmd` | `wheelleg_msgs/msg/RemoteCommand`；无自定义消息时可用 `sensor_msgs/Joy` |
| controller | 订阅 | `/wheelleg/remote_cmd` | 速度、模式、跳跃和急停 |
| controller | 订阅 | `/joint_states` | 关节位置、速度和力矩 |
| controller | 订阅 | `/imu/data` | 姿态、加速度和角速度 |
| controller | 发布 | `/wheelleg/joint_targets` | 六电机目标位置/速度/力矩 |
| controller | 发布 | `/wheelleg/mode` | 当前模式和故障状态 |
| controller | 发布 | `/wheelleg/status` | 控制器心跳、限位和错误码 |

文档和代码中使用“订阅（subscribe/subs）”时，应明确写出 Topic、消息类型、QoS、频率和超时行为。遥控输入超过 200 ms 未更新时必须进入安全停止或阻尼模式。

## 2. RemoteCommand 字段

逻辑字段建议为：`mode`（停止/行走/姿态/跳跃）、`linear_x`（m/s）、`angular_z`（rad/s）、`leg_height`（m）、`flags`（急停、使能、回中）、`sequence` 和 `timestamp`。

## 3. CAN 遥控帧 `0x110`

当遥控器经 USB-CAN 或 MCU 网关发送时，使用标准 CAN、DLC=8、小端、有符号整数：

| Byte | 字段 | 类型/缩放 | 说明 |
| --- | --- | --- | --- |
| 0 | `mode` | `uint8` | 0 停止，1 行走，2 姿态，3 跳跃 |
| 1 | `flags` | `uint8` | bit0 使能，bit1 急停，bit2 回中，bit3 清故障 |
| 2~3 | `linear_x` | `int16 * 0.001` | m/s |
| 4~5 | `angular_z` | `int16 * 0.001` | rad/s |
| 6 | `sub_cmd` | `uint8` | 0 无，1 起跳，2 落地，3 增高，4 降低 |
| 7 | `sequence` | `uint8` | 递增序号，丢帧检测 |

推荐范围为线速度 -1.5~1.5 m/s、角速度 -3.0~3.0 rad/s。实际范围可以调整，但必须同步协议文档、控制器和测试工具。

## 4. 键盘与 Web 演示

键盘建议映射：`W/S` 前进/后退，`A/D` 左转/右转，`Q/E` 降低/升高腿部，`Space` 跳跃，`X` 急停，`R` 回中。模拟 Web 页面可通过 ROS 2 WebSocket、HTTP→Topic 网关或 WebSocket→CAN 网关发布同样字段；页面必须显示当前模式、序号、急停和连接状态。
