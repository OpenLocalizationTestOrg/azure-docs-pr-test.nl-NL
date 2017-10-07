---
title: aaaAzure N-reeks stuurprogramma-instellingen voor Windows | Microsoft Docs
description: Hoe tooset NVIDIA GPU-stuurprogramma's voor N-reeks virtuele machines waarop Windows wordt uitgevoerd in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>GPU-stuurprogramma's instellen voor N-serie VM's met Windows Server
tootake profiteren van Hallo GPU-mogelijkheden van Azure N-reeks virtuele machines waarop Windows Server 2016 of Windows Server 2012 R2 wordt uitgevoerd, installatie ondersteund NVIDIA grafische stuurprogramma's. Dit artikel bevat de installatiestappen stuurprogramma nadat u een VM N-serie implementeren. Stuurprogramma-installatie-informatie is ook beschikbaar voor [virtuele Linux-machines](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zie voor basic specificaties, opslagcapaciteit en details van de schijf, [GPU Windows VM-grootten](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>De installatie van stuurprogramma

1. Verbinding maken met extern bureaublad-tooeach N-serie VM.

2. Downloaden, ophalen en Hallo ondersteunde stuurprogramma voor uw Windows-besturingssysteem wordt geïnstalleerd.

Op Azure NV virtuele machines, moet worden opgestart na de installatie van het stuurprogramma. Op virtuele machines NC is niet opnieuw opstarten vereist.

## <a name="verify-driver-installation"></a>Controleer of de installatie van stuurprogramma

U kunt controleren of stuurprogramma-installatiebestand in Apparaatbeheer. Hallo volgende voorbeeld ziet geslaagde configuratie van Hallo Tesla R80 kaart op een NC Azure VM.

![Eigenschappen van de GPU-stuurprogramma](./media/n-series-driver-setup/GPU_driver_properties.png)

tooquery hello GPU Apparaatstatus, Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd.

1. Open een opdrachtprompt en wijzig toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.

2. Voer **nvidia smi**. Als Hallo-stuurprogramma is geïnstalleerd ziet u uitvoer vergelijkbare toobelow. Houd er rekening mee dat **GPU-Util** toont **0%** tenzij u de werkbelasting van een GPU die momenteel worden uitgevoerd op Hallo VM.

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>RDMA-netwerk voor NC24r VM

RDMA-netwerkverbinding kan worden ingeschakeld op NC24r VM's geïmplementeerd in Hallo dezelfde beschikbaarheidsset. Hallo HpcVmDrivers uitbreiding moet worden toegevoegd als tooinstall Windows netwerk apparaatstuurprogramma's die RDMA-verbindingen. Gebruik tooadd Hallo VM-extensie tooan NC24r VM, [Azure PowerShell](/powershell/azure/overview) cmdlets voor Azure Resource Manager.

> [!NOTE]
> Op dit moment ondersteunt alleen Windows Server 2012 R2 Hallo RDMA-netwerk op NC24r VM's.
> 

tooinstall Hallo meest recente versie 1.1 HpcVMDrivers-extensie op een bestaande virtuele machine van RDMA-compatibel is met de naam myVM in de regio VS-West Hallo:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Zie voor meer informatie [uitbreidingen van de virtuele machine en functies voor Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hallo RDMA-netwerk ondersteunt Message Passing Interface (MPI)-verkeer voor toepassingen die worden uitgevoerd met [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) of Intel MPI 5.x. 


## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over Hallo NVIDIA GPU's op Hallo N-reeks virtuele machines:
    * [NVIDIA Tesla R80](http://www.nvidia.com/object/tesla-k80.html) (voor NC Azure VM's)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (voor NV Azure VM's)

* Ontwikkelaars die toepassingen GPU-versnelde voor Hallo NVIDIA Tesla GPU's maken ook kunnen downloaden en installeren van Hallo CUDA Toolkit 8 voor [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) of [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Zie voor meer informatie, Hallo [CUDA installatiehandleiding](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


