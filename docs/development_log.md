# 开发记录与 Git 证据

## 分支建议

`main`、`develop` 以及 `feature/mechanical`、`feature/urdf`、`feature/simulation`、`feature/controller`、`feature/linux`、`feature/embedded`、`feature/can`。多人协作时使用 `feature/<姓名>/<模块>`。

## Commit 规范

使用能描述实际工作的 Conventional Commit，例如 `feat: add wheelleg urdf`、`fix: correct inertial parameters`、`test: validate can frame parser`。禁止 `update`、`aaa`、`111`、`final` 等无法说明内容的提交。

## 里程碑 Tag

| Tag | 里程碑 |
| --- | --- |
| v0.1.0 | CAD 基础模型 |
| v0.2.0 | URDF/Xacro |
| v0.3.0 | ROS 2 仿真 |
| v0.4.0 | C++ 控制器 |
| v0.5.0 | Linux 环境 |
| v0.6.0 | MCU |
| v0.7.0 | CAN 通信 |
| v0.8.0 | Sim2Sim |
| v1.0.0 | 最终验收 |

## 贡献证明

每位成员使用自己的 Git 身份、独立分支和 Commit，通过 Pull Request 合并并保留 Review 记录。模块只有一次 `Add everything` 提交时，不能充分证明个人开发贡献。
