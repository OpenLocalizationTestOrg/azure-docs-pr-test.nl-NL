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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="b29f3-103">GPU-stuurprogramma's instellen voor N-serie VM's met Windows Server</span><span class="sxs-lookup"><span data-stu-id="b29f3-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="b29f3-104">tootake profiteren van Hallo GPU-mogelijkheden van Azure N-reeks virtuele machines waarop Windows Server 2016 of Windows Server 2012 R2 wordt uitgevoerd, installatie ondersteund NVIDIA grafische stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b29f3-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="b29f3-105">Dit artikel bevat de installatiestappen stuurprogramma nadat u een VM N-serie implementeren.</span><span class="sxs-lookup"><span data-stu-id="b29f3-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="b29f3-106">Stuurprogramma-installatie-informatie is ook beschikbaar voor [virtuele Linux-machines](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b29f3-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b29f3-107">Zie voor basic specificaties, opslagcapaciteit en details van de schijf, [GPU Windows VM-grootten](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b29f3-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="b29f3-108">De installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="b29f3-108">Driver installation</span></span>

1. <span data-ttu-id="b29f3-109">Verbinding maken met extern bureaublad-tooeach N-serie VM.</span><span class="sxs-lookup"><span data-stu-id="b29f3-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="b29f3-110">Downloaden, ophalen en Hallo ondersteunde stuurprogramma voor uw Windows-besturingssysteem wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b29f3-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="b29f3-111">Op Azure NV virtuele machines, moet worden opgestart na de installatie van het stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="b29f3-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="b29f3-112">Op virtuele machines NC is niet opnieuw opstarten vereist.</span><span class="sxs-lookup"><span data-stu-id="b29f3-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="b29f3-113">Controleer of de installatie van stuurprogramma</span><span class="sxs-lookup"><span data-stu-id="b29f3-113">Verify driver installation</span></span>

<span data-ttu-id="b29f3-114">U kunt controleren of stuurprogramma-installatiebestand in Apparaatbeheer.</span><span class="sxs-lookup"><span data-stu-id="b29f3-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="b29f3-115">Hallo volgende voorbeeld ziet geslaagde configuratie van Hallo Tesla R80 kaart op een NC Azure VM.</span><span class="sxs-lookup"><span data-stu-id="b29f3-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Eigenschappen van de GPU-stuurprogramma](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="b29f3-117">tooquery hello GPU Apparaatstatus, Voer Hallo [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) opdrachtregelprogramma met Hallo stuurprogramma geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b29f3-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="b29f3-118">Open een opdrachtprompt en wijzig toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span><span class="sxs-lookup"><span data-stu-id="b29f3-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="b29f3-119">Voer **nvidia smi**.</span><span class="sxs-lookup"><span data-stu-id="b29f3-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="b29f3-120">Als Hallo-stuurprogramma is geïnstalleerd ziet u uitvoer vergelijkbare toobelow.</span><span class="sxs-lookup"><span data-stu-id="b29f3-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="b29f3-121">Houd er rekening mee dat **GPU-Util** toont **0%** tenzij u de werkbelasting van een GPU die momenteel worden uitgevoerd op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="b29f3-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![De apparaatstatus NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="b29f3-123">RDMA-netwerk voor NC24r VM</span><span class="sxs-lookup"><span data-stu-id="b29f3-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="b29f3-124">RDMA-netwerkverbinding kan worden ingeschakeld op NC24r VM's geïmplementeerd in Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="b29f3-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="b29f3-125">Hallo HpcVmDrivers uitbreiding moet worden toegevoegd als tooinstall Windows netwerk apparaatstuurprogramma's die RDMA-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b29f3-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="b29f3-126">Gebruik tooadd Hallo VM-extensie tooan NC24r VM, [Azure PowerShell](/powershell/azure/overview) cmdlets voor Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b29f3-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="b29f3-127">Op dit moment ondersteunt alleen Windows Server 2012 R2 Hallo RDMA-netwerk op NC24r VM's.</span><span class="sxs-lookup"><span data-stu-id="b29f3-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="b29f3-128">tooinstall Hallo meest recente versie 1.1 HpcVMDrivers-extensie op een bestaande virtuele machine van RDMA-compatibel is met de naam myVM in de regio VS-West Hallo:</span><span class="sxs-lookup"><span data-stu-id="b29f3-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="b29f3-129">Zie voor meer informatie [uitbreidingen van de virtuele machine en functies voor Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b29f3-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b29f3-130">Hallo RDMA-netwerk ondersteunt Message Passing Interface (MPI)-verkeer voor toepassingen die worden uitgevoerd met [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) of Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="b29f3-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="b29f3-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b29f3-131">Next steps</span></span>

* <span data-ttu-id="b29f3-132">Zie voor meer informatie over Hallo NVIDIA GPU's op Hallo N-reeks virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="b29f3-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="b29f3-133">[NVIDIA Tesla R80](http://www.nvidia.com/object/tesla-k80.html) (voor NC Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="b29f3-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="b29f3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (voor NV Azure VM's)</span><span class="sxs-lookup"><span data-stu-id="b29f3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="b29f3-135">Ontwikkelaars die toepassingen GPU-versnelde voor Hallo NVIDIA Tesla GPU's maken ook kunnen downloaden en installeren van Hallo CUDA Toolkit 8 voor [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) of [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="b29f3-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="b29f3-136">Zie voor meer informatie, Hallo [CUDA installatiehandleiding](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="b29f3-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


