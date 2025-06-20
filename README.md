# 四轴无人机项目（hal库）

本项目基于STM32F103C8T6微控制器实现了一套完整的四轴飞行器控制系统。该系统集成了姿态解算、PID控制、无线通信等功能模块，可实现稳定的悬停、定高和遥控飞行。

本文档将详细介绍系统的硬件组成、软件架构、算法原理以及实现步骤，帮助读者理解四轴飞行器的工作原理和开发流程。

## 项目结构

本项目主要分为以下几个模块：
1. 硬件设计
2. 系统初始化
3. 传感器驱动与数据采集
4. 姿态解算
5. 飞行控制算法
6. 无线通信
7. 任务调度与实时控制

# 项目目录：

```
github_小四轴/
├── README.md                # 项目主要说明文档
├── docs/                    # 所有文档集中在这里
│   ├── README.md            # 文档说明
│   ├── guide.md             # 指南文档，详细文档
│   ├── make_process.md      # 制作流程文档,快速入门指南
│   └── make_process.assets/ # 文档图片资源
├── drivers/                 # 驱动库
│   ├── bmp280/              # 气压传感器驱动
│   ├── mpu6050/             # 六轴传感器驱动
│   └── nrf24l01/            # 无线通信模块驱动
|── pcb/                     # PCB相关文件
│   ├── gerber/              # Gerber制版文件
│   ├── source/              # 源设计文件
│   ├── bom.xlsx             # 元器件清单
│   └── schematic/           # 原理图
├── project/                 # 项目代码
│   ├── fly/                 # 飞行器控制代码
│   └── remote/              # 遥控器代码
├── reference/               # 参考项目
│   └── baiduwangpan.md      # 百度网盘分享链接
└── tools/                   # 工具类
```



## 00_前言

本项目是基于STM32F103C8T6微控制器的四轴飞行器控制系统。目标是实现稳定的飞行控制和高效的数据传输。

## 01_硬件组成

1. **MCU**: STM32F103C8T6
2. **MPU6050**: 六轴运动传感器
3. **NRF24L01**: 2.4GHz无线通信模块

### 硬件连接

1. **MCU与MPU6050**: 通过I2C总线连接，获取加速度计和陀螺仪数据。
2. **MCU与NRF24L01**: 通过SPI接口与无线模块连接，进行数据的收发。

## 02_核心模块

1. **系统初始化**: 时钟、GPIO、中断等基础配置
2. **传感器驱动**: 读取并处理MPU6050的传感器数据
3. **姿态解算**: 使用卡尔曼滤波和互补滤波算法，融合加速度计与陀螺仪数据，实现精确的姿态估算。
4. **飞行控制**: 使用级联PID控制算法，外环控制角度，内环控制角速度。
5. **通信协议**: 解析遥控器的数据，进行数据上传。
6. **任务调度**: 使用RTOS进行多任务调度，保证系统的实时性。

## 03_软件架构

1. **操作系统**: 本项目使用了匿名飞控任务调度器进行任务调度，确保系统的实时性和任务分配。

2. **传感器驱动**: 采用I2C与SPI协议进行数据采集，确保传感器的稳定工作。

3. **通信协议**: 使用NRF24L01模块与遥控器进行数据交互，通过自定义协议实现指令传递。

   ## 算法原理

   - **姿态解算**：本系统采用互补滤波算法融合加速度计与陀螺仪数据，实时估算飞行器的姿态角度。
   - **飞行控制**：采用级联PID控制结构，外环负责控制飞行器的角度，内环负责控制角速度，以实现稳定的飞行。

## 04_安装与使用

1. 将本项目的代码下载到本地。
2. 使用Keil或STM32CubeIDE进行项目编译。
3. 将编译后的固件烧录到STM32F103C8T6开发板中。
4. 连接传感器（MPU6050）与通信模块（NRF24L01），进行硬件测试。
5. 使用遥控器测试飞行器的悬停、定高与遥控控制功能。

## 05_贡献

欢迎大家为本项目贡献代码，提出问题或提供建议。你可以通过创建Issue或Pull Request来与我们进行互动。

## 06_许可

本项目采用MIT许可证，详情请查看[LICENSE](./LICENSE)文件。

## 07_参考资料

