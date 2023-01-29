# 简介

## 概述
  NVMe接口允许host软件与非易失行内存子系统（non-volatile memory subsystem）进行通信。这一接口针对企业和客户端固态驱动器进行了优化，通常作为寄存器级接口连接到PCI Express接口。

  参阅<http://nvmexpress.org/changes>以获得描述新功能的文档
  
### NVMe over Pcie & NVMe over fabric

  NVM Express基本规范修订版1.4和以前的修订版为主机软件定义了一个寄存器级接口，以便通过PCI Express与非易失性存储器子系统通信（NVME over PCIe）
  
  NVMe over Fabrics规范定义了协议接口和NVMe接口的相关扩展，支持通过其他互连（例如以太网、InfiniBand™、光纤通道）进行操作,NVMe over Fabrics规范为每个NVMe传输（在该规范内或通过引用）提供了一个NVMe传输绑定。在本规范中，需求/特性可以被记录为特定于NVMe over Fabric实现或特定的NVMe传输绑定。 此外，NVMe over PCIe和NVMe over Fabric实现对特性和功能的支持要求可能不同。
  
### scope 范围

  规范定义了用于与NVM子系统中的控制器通信的寄存器接口及controller（控制器）支持的标准命令集。其中，有三种不同的controller：
    - IO controllers 
    - Discovery controllers 
    - Administrative controllers
