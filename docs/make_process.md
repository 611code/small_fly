# 快速入门指南

















# 一、陀螺仪MPU6050

​	摘自[超详细陀螺仪MPU6050模块输出姿态角(有完整版源码)_陀螺仪输出角度是多少度到多少度-CSDN博客](https://blog.csdn.net/lihaotian111/article/details/117307644)

## 1、MPU6050介绍

​	MPU6050内部整合了三轴MEMS陀螺仪、三轴MEMS加速度计以及一个可扩展的数字运动处理器DMP(Digital Motion Processor)，而且还可以连接一个第三方数字传感器(如磁力计)，这样的话，就可以通过IIC接口输出一个9轴信号(链接第三方数字传感器才可以输出九轴信号，否则只有六轴信号)。更加方便的是，有了DMP，可以结合InvenSense公司提供的运动处理资料库，实现姿态解算。通过自带的DMP，可以通过IIC接口输出9轴融合演算的数据，大大降低了运动处理运算对操作系统的负荷，同时也降低了开发难度。其实，简单一句话说，陀螺仪就是测角速度的，加速度传感器就是测角加速度的，二者数据通过算法就可以得到PITCH、YAW、ROLL角了。
![image-20250309185053383](C:\Users\34125\Desktop\github_小四轴\03_make\make_process.assets\image-20250309185053383.png)



![image-20250309185127213](C:\Users\34125\Desktop\github_小四轴\03_make\make_process.assets\image-20250309185127213.png)

​	MPU6050芯片中内置了三轴加速度传感器、三轴陀螺仪和一个温度传感器。右侧INT为中断输出脚，TCS为片选脚、AD0为设置地址脚、SCL和SDA为主IIC接口、AUX_CL和AUX_DA为从IIC接口，主要用到的是AD0、SCL、SDA。

![image-20250317131258700](C:\Users\34125\Desktop\github_小四轴\03_make\make_process.assets\image-20250317131258700.png)

## 2、应用

​	通过I2C总线发送命令读取加速度计和陀螺仪的数据（详情见代码）数据手册在驱动库里。

![image-20250317131514788](C:\Users\34125\Desktop\github_小四轴\03_make\make_process.assets\image-20250317131514788.png)



# 二、