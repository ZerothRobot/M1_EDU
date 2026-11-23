# M1 EDU

[English](README.md)

M1 EDU 是元点智能 M1 人形机器人学习、训练和部署强化学习策略的公开入口仓库。本仓库负责整理完整工作流，并链接持续维护的训练仓库和部署仓库。

## 从这里开始

| 目标 | 仓库 |
| --- | --- |
| 在仿真环境中训练和评估策略 | [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train) |
| 将导出的 ONNX 策略部署到机器人 | [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy) |

<div align="center">
  <img src="assets/m1-edu-lab.png" alt="M1 EDU 开发工作台" width="760">
  <br>
</div>

<div align="center">
  <img src="assets/m1-edu-xray.png" alt="M1 EDU 内部结构参考图" width="420">
  <br>
</div>

## 工作流

```text
M1 EDU 机器人
      │
      ├── 仿真与策略训练
      │       └── M1_EDU_Train
      │
      ├── 将策略导出为 ONNX
      │
      └── 机器人端策略部署
              └── M1_EDU_Deploy
```

两个代码仓库保持独立维护。训练依赖、仿真资源、检查点和实验日志归属于训练仓库。机器人连接代码、部署配置、ONNX 模型和运行示例归属于部署仓库。本仓库提供统一入口和工作流说明。

## 训练

环境配置和命令请进入 [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train) 查看。

训练仓库当前说明的技术栈包括：

- Ubuntu 20.04 或 Ubuntu 22.04
- Conda 环境中的 Python 3.8
- NVIDIA Isaac Gym Preview 4
- `rsl_rl`
- `JOYIn_gym`

当前文档中的训练入口为：

```bash
python JOYIn_gym/legged_gym/scripts/train.py --task=mini1_18dof_walk --num_envs=40
```

安装细节、任务配置、检查点和仿真故障排查以训练仓库 README 为准。

## 导出与部署

在仿真环境中验证策略后，请按照 [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy) 中的说明，将策略导出为部署运行时需要的格式并部署到机器人。

部署仓库当前包含以下内容：

- 将开发电脑与机器人连接到同一局域网
- 通过 SSH 连接机器人
- 将 ONNX 策略放入部署模型目录
- 配置观测维度、历史观测堆叠、关节参数和缩放因子
- 使用指定策略启动行走示例

示例部署命令为：

```bash
python demo_walk.py --model=model/your_model_name.onnx
```

部署时使用的策略配置必须与训练时保持一致。修改观测布局、历史长度、动作维度、关节默认值或控制参数前，请先核对部署仓库中的说明。

## 仓库职责

### 本仓库

- 提供 M1 EDU 项目入口
- 记录从仿真到机器人的工作流
- 链接持续维护的公开仓库
- 记录适用于整个工作流的项目级说明

### [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train)

- 包含 Isaac Gym 训练环境
- 包含 M1 任务配置和训练脚本
- 包含 `JOYIn_gym` 与 `rsl_rl` 源码目录
- 包含由该仓库管理的仿真资源和实验输出

### [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy)

- 包含 ROS 2 部署示例
- 包含机器人通信和控制代码
- 包含部署配置和 ONNX 策略示例
- 在 `api/` 下提供机器人 API 和环境配置参考

## 获取帮助

训练失败、任务配置或仿真行为问题，请在 [M1_EDU_Train](https://github.com/ZerothRobot/M1_EDU_Train) 中提交 Issue。机器人连接、ROS 2 运行时、策略加载或部署失败，请在 [M1_EDU_Deploy](https://github.com/ZerothRobot/M1_EDU_Deploy) 中提交 Issue。项目级文档和导航问题请在本仓库反馈。