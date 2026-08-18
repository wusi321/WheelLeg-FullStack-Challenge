# URDF/Xacro 机器人描述题目（10 分）

## 题目说明

将机械模型转换为 URDF，推荐使用 Xacro。至少包含 `link`、`joint`、`visual`、`collision`、`inertial`、joint axis、joint limit、material，必要时提供 transmission。网格、RViz 配置和 launch 文件应能被 ROS 2 工具直接加载。

## 交付物

`urdf/`、`xacro/`、`meshes/`、`rviz/`、`launch/`，以及从 CAD 参数到 URDF 参数的映射说明。运行 `check_urdf`（或 ROS 2 等效检查）无错误，并在 RViz 2 正确显示。

## 评分

| 项目 | 分值 |
| --- | ---: |
| Link/Joint 拓扑和连接关系正确 | 3 |
| Visual/Collision 几何正确 | 2 |
| 质量与惯量 Inertial 正确 | 2 |
| Joint Axis/Limit 正确 | 2 |
| RViz 2 正确显示 | 1 |

## 验收

对比 CAD、URDF 和 RViz 的轮径、关节位置、质量、惯量和运动范围；任何明显不一致按实际误差扣分。
