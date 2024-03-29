# 简介

## 概述
  NVMe接口允许host软件与非易失行内存子系统（non-volatile memory subsystem）进行通信。这一接口针对企业和客户端固态驱动器进行了优化，通常作为寄存器级接口连接到PCI Express接口。

  参阅<http://nvmexpress.org/changes>以获得描述新功能的文档
  
### NVMe over Pcie & NVMe over fabric

  NVM Express基本规范修订版1.4和以前的修订版为主机软件定义了一个寄存器级接口，以便通过PCI Express与非易失性存储器子系统通信（NVME over PCIe）
  
  NVMe over Fabrics规范定义了协议接口和NVMe接口的相关扩展，支持通过其他互连（例如以太网、InfiniBand™、光纤通道）进行操作,NVMe over Fabrics规范为每个NVMe传输（在该规范内或通过引用）提供了一个NVMe传输绑定。在本规范中，需求/特性可以被记录为特定于NVMe over Fabric实现或特定的NVMe传输绑定。 此外，NVMe over PCIe和NVMe over Fabric实现对特性和功能的支持要求可能不同。
  
### Scope 范围

  规范定义了用于与NVM子系统中的控制器通信的寄存器接口及controller（控制器）支持的标准命令集。其中，有三种不同的controller：
  
    - IO controllers 
    - Discovery controllers 
    - Administrative controllers

### Outside of scope
  
  寄存器接口和命令集仅定义与NVM子系统的通信接口，与NVM的使用模型无关，即本协议不关心NVM系统是否用作为固态驱动器、主存储器、高速缓冲存储器、备份存储器、冗余存储器，使用模型在本协议规定之外，可选但不被许可。
  
  这些接口定义在NVM管理上层，如用于闪存增寿的磨损均衡（wear leveling）。对擦除及其它NVM技术的管理任务（如NAND）进行了抽象。
  
  不包含任何关于缓存算法或技术。
  
  本协议中提及的其他已发布协议的实现或使用，即使为了符合本协议而需要，也在本协议的范围之外， 例如PCI、PCIE、PCI-X。
  
### Theory of Operation 工作原理

  NVM Express可扩展接口旨在满足使用基于PCI Express的固态驱动器或Fabric连接设备的企业和客户端系统的需求。该接口提供了优化的命令提交和完成路径。
    
  支持并行操作，**最多支持65,535个I/O队列**，每个I/O队列最多支持64Ki-1在途命令（outstanding commands）， 此外，还增加了对许多企业功能的支持，如端到端数据保护(与SCSI保护信息兼容，通常称为T10 DIF和SNIA DIX标准)、加强的错误报告和虚拟化。
    
  接口的关键属性如下：
  
    - 在命令提交或完成路径中不需要读不可缓存的/MMIO(Memory mapping I/O）寄存器；
    - 命令提交路径中最多需要一次MMIO寄存器写入；
    - 支持多达65,535个I/O队列，每个I/O队列支持多达65,535个在途命令；
    - 优先级关联了每一个I/O队列并具有良好的仲裁机制；
    - 完成一个4KB读取请求的所有信息都包含在64B命令本身中，确保了高效的小型I/O操作；
    - 高效精简的命令集；
    - 支持MSI/MSI-X和中断聚合；
    - 支持多个命令空间（namespace）;
    - 高效支持I/O虚拟化架构，如SR-IOV；
    - 支持多路径I/O和namespace共享；
    
  协议定义了一组简化的寄存器，功能包括：
  
    - controller功能指示；
    - controller失败状态（命令状态直接通过CQ处理）；
    - 管理队列配置（I/O队列配置通过Admin命令处理）；
    - 用于可扩展的提交和完成队列的Doorbell寄存器
    
  一个NVMe controller和单个PCI功能（PCI Function）关联。适用于整个控制器的功能和设置在控制器能力（CAP）寄存器和识别控制器数据结构中显示。
  
  namespace是可以格式化为逻辑块的非易失性内存的数量。一个NVMe控制器可以支持多个命名空间，这些命名空间可以使用一个命名空间ID来引用。   
    
    

