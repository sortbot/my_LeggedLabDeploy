# LeggedLabDeploy 安装与使用指南

## 依赖项

- Python 3.8-3.10
- PyTorch
- NumPy
- SciPy
- PyYAML
- unitree_sdk2_python (Unitree 官方 SDK)

## 安装步骤

### 1. 创建 Conda 环境

```bash
conda create -n leggedlab_deploy python=3.10 -y
conda activate leggedlab_deploy
```

### 2. 克隆项目

```bash
git clone https://github.com/sortbot/my_LeggedLabDeploy.git
cd my_LeggedLabDeploy
```

### 3. 安装 unitree_sdk2_python

```bash
git clone https://github.com/unitreerobotics/unitree_sdk2_python.git
cd unitree_sdk2_python
pip install -e .
cd ..
```

### 4. 安装其他依赖

```bash
pip install -r requirements.txt
```

## 启动命令

### Sim2Sim (MuJoCo 仿真)

```bash
# 终端 1: 启动 MuJoCo
cd /path/to/unitree_mujoco/simulate/build
./unitree_mujoco

# 终端 2: 启动部署代码
conda activate leggedlab_deploy
cd /path/to/my_LeggedLabDeploy
python deploy.py --net lo --config_path configs/g1.yaml
```

### Sim2Real (真实机器人)

```bash
conda activate leggedlab_deploy
python deploy.py --net <网卡名> --config_path configs/g1.yaml
```

- `<网卡名>`: 连接机器人的网卡，如 `eno1`, `eth0`, `enp3s0`
- 用 `ip addr` 命令查看网卡名称

## 操作流程

1. 启动程序后，机器人进入零力矩状态
2. 按手柄 **Menu (≡)** 键 → 移动到默认站立位置
3. 按手柄 **A** 键 → 开始运动控制
4. 左摇杆控制移动，右摇杆控制旋转
5. 按 **View (⧉)** 键或 **Ctrl+C** 退出

## MuJoCo 键盘控制

| 按键 | 功能 |
|------|------|
| 7 | 升高弹性带 |
| 8 | 放低弹性带 |
| 9 | 关闭弹性带 |

## 支持的机器人

- Unitree G1 (`configs/g1.yaml`)
- Unitree H1 (`configs/h1.yaml`)

## 环境变量

- `AUTO_START=1`: 自动跳过手柄按键等待（用于自动化测试）

```bash
AUTO_START=1 python deploy.py --net lo --config_path configs/g1.yaml
```
