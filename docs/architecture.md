# 系统架构与接口

```text
GitHub(main/develop)
        │
机械 CAD ─ URDF/Xacro ─ ROS 2/Gazebo
                         │
                  C++ Controller API
                    ┌────┴────┐
                 仿真后端   硬件后端
                    │         │
                 Sim2Sim   CAN ↔ MCU ↔ IMU
```

控制器只依赖机器人状态、关节目标和执行器抽象接口；Gazebo 和硬件/CAN 通过后端适配。所有长度使用米、角度使用弧度、质量使用千克，坐标系和正方向记录在 `docs/coordinate_system.md`。
