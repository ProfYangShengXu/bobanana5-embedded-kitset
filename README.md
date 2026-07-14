# ⚙️ Bobanana 5.0 — 嵌入式系统开发 Adaption Kitset

嵌入式系统开发的 [Bobanana 5.0](https://github.com/ProfYangShengXu/BoBanana5) Adaption Kitset。  
17 张专业角色卡 + 8 个工具接口 + 嵌入式状态机模板。

> **前身**: [nuedc-skills](https://github.com/ProfYangShengXu/nuedc-skills.git) — 全国大学生电子设计竞赛 AI 驱动工具链  
> **母公司**: [BoBanana5](https://github.com/ProfYangShengXu/BoBanana5)

---

## 📋 角色卡（17 张）

| 方向 | 角色 | 说明 |
|------|------|------|
| 👑 **架构** | `embedded-architect` 🎗️OP | 系统架构设计、技术栈选型、工具链编排 |
| 🔵 **固件** | `stm32-firmware-engineer` | STM32 HAL/LL 库开发、外设驱动、RTOS 移植 |
| | `mcu-firmware-engineer` | 通用 MCU 裸机/RTOS 开发、Bootloader |
| | `motor-control-engineer` | FOC/PID 电机控制、伺服驱动 |
| 🟢 **Linux** | `linux-app-dev` | 嵌入式 Linux 应用层、Qt/C++ |
| | `linux-driver-engineer` | 内核模块、设备树、字符驱动 |
| | `bsp-engineer` | U-Boot、内核适配、Yocto/Buildroot |
| | `qt-developer` | Qt/QML 嵌入式 GUI、HMI |
| 🟡 **行业** | `bms-software-engineer` | 电池管理、SOX 算法、CAN 通信 |
| | `domain-controller-engineer` | AUTOSAR、DDS、多核 SoC |
| 🔴 **AI/边缘** | `edge-computing-engineer` | Edge AI 推理、TFLite Micro |
| | `model-quantization-engineer` | 模型量化/剪枝、NPU 优化 |
| 🟣 **FPGA** | `fpga-engineer` | Verilog/VHDL、Quartus/Vivado |
| 🟠 **硬件** | `embedded-hardware-engineer` | 原理图、PCB、信号完整性 |
| | `rf-engineer` | 天线设计、射频链路、EMC |
| | `power-engineer` | DC-DC/LDO、Buck/Boost、热管理 |
| ⚪ **安全** | `functional-safety-engineer` | ISO 26262、FMEA/FTA |

## 🧰 工具集

工具自动检测安装路径（常见目录 + PATH + 注册表），未安装时输出下载指引。

| 工具 | 命令 | 功能 |
|------|------|------|
| STM32CubeMX | `tools\cubemx\cubemx.bat` | MCU 引脚/时钟/外设配置代码生成 |
| Keil MDK | `tools\keil5\keil5.bat` | ARM 编译/烧录/调试 |
| SEGGER J-Link | `tools\jlink\jlink.bat` | 烧录/RTT/GDB Server |
| 统一入口 | `python tools\tools.py` | 跨平台 CLI 接口 |

### 使用示例

```bash
# CubeMX — 打开 GUI
tools\cubemx\cubemx.bat -g

# CubeMX — 从 .ioc 生成代码
tools\cubemx\cubemx.bat -s project.ioc

# Keil — 编译工程
tools\keil5\keil5.bat -b project.uvprojx

# JLink — 烧录固件
tools\jlink\jlink.bat -flash STM32F103C8 firmware.hex

# JLink — 启动 GDB Server
tools\jlink\jlink.bat -gdb STM32F407VG

# Python 统一入口
python tools\tools.py cubemx --gui
```

## 📊 状态机模板

`state-machine-embedded.yaml` — 适用于嵌入式开发项目的完整管线：

```
embedded-architect(OP)
  ├── 固件链: STM32固件 → MCU固件 → 电机控制
  ├── Linux链: 应用开发 → 驱动开发 → BSP → QT
  ├── 行业链: BMS软件 → 域控制器 → 边缘计算 → 模型量化
  ├── FPGA链: FPGA工程师
  ├── 硬件链: 硬件设计 → 射频 → 电源
  └── 安全链: 功能安全 → 架构师终验 → CL终审
```

## 🚀 接入 Bobanana 5.0

```bash
# 克隆到 BoBanana5 的 kitsets/ 目录下
cd path/to/BoBanana5/kitsets
git clone https://github.com/ProfYangShengXu/bobanana5-embedded-kitset.git embedded
```

Bobanana 的 Boss 角色启动时自动扫描 `kitsets/` 目录，通过 `kitsets/kitset_discovery.py` 匹配用户目标关键词。命中 ≥2 个领域标签时自动切换控制权给 `embedded-architect`。

### 匹配关键词

`embedded`, `firmware`, `stm32`, `mcu`, `fpga`, `linux-embedded`, `hardware`, `rtos`, `motor`, `bsp`, `yocto`, `functional-safety`, `edge-ai`

## 📁 目录结构

```
kitsets/embedded/
├── README.md
├── reasonix-plugin.json         ← Kitset 元数据（kitset_name, kitset_domains, entry_role）
├── state-machine-embedded.yaml  ← 嵌入式状态机模板
│
├── roles/                       ← 17 张角色卡
│   ├── .registry.yaml
│   ├── stm32-firmware-engineer/  (role-card.yaml + SKILL.md + standards-brief.yaml)
│   ├── mcu-firmware-engineer/
│   ├── ... (全部 17 角色)
│   └── embedded-architect/
│
└── tools/                       ← 可执行工具脚本
    ├── cubemx/cubemx.bat
    ├── keil5/keil5.bat
    ├── jlink/jlink.bat
    └── tools.py                 ← Python 统一入口
```

## 🔧 环境要求

- Python 3.12+
- 对应 MCU 的 IDE/工具链（Keil / IAR / STM32CubeIDE）— 自动检测
- JLink / ST-Link 调试探针 — 自动检测
- Git + Git LFS（固件二进制管理）

## 🔗 链接

- **母公司**: [BoBanana5](https://github.com/ProfYangShengXu/BoBanana5) — 可编程状态机 + 59 张通用角色卡
- **前身**: [nuedc-skills](https://github.com/ProfYangShengXu/nuedc-skills.git) — 电赛七件套

## 📜 许可证

MIT
