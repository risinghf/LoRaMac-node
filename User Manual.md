### User Manual

---

- 瑞兴恒方的各个型号模块的demo程序位于分支：rxhf中，该分支以semtech源码为基础，可以直接进行快速合并；

- pro文件夹中是KEIL的工程文件，包含了三个瑞兴恒方三个模块型号，分别是RHF76-052DM/RHF0M010/RHF0M003，使用时，分别对应不同的瑞兴恒方硬件模块；

- src文件夹中，包含了各个瑞兴恒方型号模块的特定底层驱动文件以及应用文件。其中应用app文件中，只有用于LoRaWAN通信的demo文件，位于src/apps/LoRaMac中

- lorawan的mac层协议栈文件、radio的驱动文件、系统的驱动文件等都复用semtech提供的源码

- 当使用任一瑞兴恒方型号模块的demo程序时，打开Keil工程后，需要根据需求配置好频率计划，如使用CN470，应该在工程的‘Options’中的‘C/C++’中的'Define'中定义`REGION_CN470`，并且在main.c文件中34行附近的位置，定义ACTIVE_REGION为LORAMAC_REGION_CN470：

  ```c
  #define ACTIVE_REGION LORAMAC_REGION_CN470
  ```

- 如果需要配置所选择的频率计划下初始的信道，则到工程文件中src/mac/region文件夹中，找到对应的region文件，进入后，找到类似`RegionCN470InitDefaults`函数即可修改

- 模块硬件上连接好对应的串口，波特率为115200，运行程序，则可以看到串口上开始打印如下图所示的log信息，具体信息会不一样，但总体格式如下：

  ###### ===== ClassA demo application v1.0.RC1 ==== ######
  
  DevEui      : 34-38-37-32-5B-37-68-0B
  AppEui      : 00-00-00-00-00-00-00-00
  AppKey      : 2B 7E 15 16 28 AE D2 A6 AB F7 15 88 09 CF 4F 3C
  
  ###### ===== JOINED ==== ######
  
  ABP
  
  DevAddr     : 014B85D5
  NwkSKey     : 2B 7E 15 16 28 AE D2 A6 AB F7 15 88 09 CF 4F 3C
  AppSKey     : 2B 7E 15 16 28 AE D2 A6 AB F7 15 88 09 CF 4F 3C
  
  
  ###### ===== MCPS-Request ==== ######
  STATUS      : OK
  
  ###### ===== MCPS-Confirm ==== ######
  STATUS      : OK
  
  ###### ===== UPLINK FRAME 1 ==== ######
  
  CLASS       : A
  
  TX PORT     : 2
  TX DATA     : UNCONFIRMED
  00 
  
  DATA RATE   : DR_0
  U/L FREQ    : 471300000
  TX POWER    : 0
  CHANNEL MASK: 00FF 0000 0000 0000 0000 