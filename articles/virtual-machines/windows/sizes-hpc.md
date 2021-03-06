---
title: Azure Windows VM 大小 - HPC | Microsoft Docs
description: 列出 Azure 中适用于 Windows 高性能计算虚拟机的各种大小。 针对此系列中的大小列出了 vCPU、数据磁盘和 NIC 的数量，以及存储吞吐量和网络带宽。
services: virtual-machines-windows
documentationcenter: ''
author: jonbeck7
manager: jeconnoc
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/15/2018
ms.author: jonbeck
ms.openlocfilehash: e402fd3ac95cac4816b9442f7c08aeaf7c108886
ms.sourcegitcommit: 5b2ac9e6d8539c11ab0891b686b8afa12441a8f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="high-performance-compute-vm-sizes"></a>高性能计算 VM 大小

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]


* **操作系统** - Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

* **MPI**：Microsoft MPI (MS-MPI) 2012 R2 或更高版本、Intel MPI Library 5.x

  支持的 MPI 实现使用 Microsoft Network Direct 接口在实例之间通信。 

* **RDMA 网络地址空间** - Azure 中的 RDMA 网络保留地址空间 172.16.0.0/16。 若要在 Azure 虚拟网络中部署的实例上运行 MPI 应用程序，请确保虚拟网络地址空间不与 RDMA 网络重叠。

* **HpcVmDrivers VM 扩展** - 在支持 RDMA 的 VM 上，添加 HpcVmDrivers 扩展以安装 RDMA 连接所需的 Windows 网络设备驱动程序。 （在某些 A8 和 A9 实例的部署中，会自动添加 HpcVmDrivers 扩展。）若要将 VM 扩展添加到 VM，可以使用 [Azure PowerShell](/powershell/azure/overview) cmdlet。 

  
  以下命令在 *West US* 区域的 *myResourceGroup* 资源组中部署的、支持 RDMA 的现有 VM *myVM* 上安装最新的 HpcVMDrivers 扩展版本 1.1：

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  有关详细信息，请参阅[虚拟机扩展和功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 还可使用[经典部署模型](classic/manage-extensions.md)中部署的 VM 扩展。


## <a name="using-hpc-pack"></a>使用 HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx)：Microsoft 的免费 HPC 群集和作业管理解决方案，它是一个方便在 Azure 中创建计算群集来运行基于 Windows 的 MPI 应用程序和其他 HPC 工作负荷的选项。 HPC Pack 2012 R2 和更高版本包括用于 MS-MPI 的、在支持 RDMA 的 VM 上部署时使用 Azure RDMA 网络的运行时环境。



## <a name="other-sizes"></a>其他大小
- [常规用途](sizes-general.md)
- [计算优化](sizes-compute.md)
- [内存优化](../virtual-machines-windows-sizes-memory.md)
- [存储优化](../virtual-machines-windows-sizes-storage.md)
- [GPU 优化](sizes-gpu.md)

## <a name="next-steps"></a>后续步骤

- 有关在 Windows Server 上配合使用计算密集型实例和 HPC Pack 的清单，请参阅[使用 HPC Pack 设置一个用于运行 MPI 应用程序的 Windows RDMA 群集](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

- 若要在 Azure Batch 中运行 MPI 应用程序时使用计算密集型实例，请参阅[在 Azure Batch 中使用多实例任务来运行消息传递接口 (MPI) 应用程序](../../batch/batch-mpi.md)。

- 了解有关 [Azure 计算单元 (ACU)](acu.md) 如何帮助你跨 Azure SKU 比较计算性能的详细信息。




