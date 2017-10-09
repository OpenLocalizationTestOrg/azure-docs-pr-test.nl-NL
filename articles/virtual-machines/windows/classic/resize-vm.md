---
title: een virtuele machine van Windows hello klassieke implementatiemodel - Azure aaaResize | Microsoft Docs
description: Het formaat van een virtuele Windows-machine in Hallo klassieke implementatiemodel, met Azure Powershell hebt gemaakt.
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="18712-103">Een Windows-VM gemaakt in het klassieke implementatiemodel Hallo vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="18712-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="18712-104">Dit artikel laat zien hoe tooresize een Windows-VM gemaakt in het klassieke implementatiemodel Hallo met Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="18712-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="18712-105">Als u overweegt Hallo mogelijkheid tooresize een virtuele machine, zijn er twee concepten waarmee de Hallo bereik van grootten beschikbaar tooresize Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="18712-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="18712-106">Hallo eerste concept is Hallo-regio waarin uw virtuele machine wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="18712-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="18712-107">Hallo-lijst met VM-grootten die beschikbaar zijn in de regio is Hallo Services tabblad van hello Azure-gebieden webpagina.</span><span class="sxs-lookup"><span data-stu-id="18712-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="18712-108">tweede concept Hallo is Hallo fysieke hardware momenteel als host optreedt van de VM.</span><span class="sxs-lookup"><span data-stu-id="18712-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="18712-109">Hallo fysieke servers die als host fungeert voor VM's zijn gegroepeerd in clusters van algemene fysieke hardware.</span><span class="sxs-lookup"><span data-stu-id="18712-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="18712-110">Hallo-methode van het wijzigen van een VM-grootte verschilt afhankelijk van of hello wordt gewenste nieuwe VM-grootte ondersteund door Hallo hardware cluster momenteel host Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="18712-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="18712-111">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="18712-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="18712-112">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="18712-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="18712-113">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="18712-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="18712-114">U kunt ook [vergroten of verkleinen van een virtuele machine gemaakt in Hallo Resource Manager-implementatiemodel](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18712-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="18712-115">Uw account toevoegen</span><span class="sxs-lookup"><span data-stu-id="18712-115">Add your account</span></span>
<span data-ttu-id="18712-116">U moet Azure PowerShell toowork configureren met de klassieke Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="18712-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="18712-117">Hallo stappen hieronder tooconfigure Azure PowerShell toomanage klassieke resources.</span><span class="sxs-lookup"><span data-stu-id="18712-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="18712-118">Typ achter de PowerShell-prompt Hallo `Add-AzureAccount` en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="18712-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="18712-119">Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="18712-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="18712-120">Typ in het Hallo-wachtwoord voor je account.</span><span class="sxs-lookup"><span data-stu-id="18712-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="18712-121">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="18712-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="18712-122">Vergroten of verkleinen in Hallo dezelfde hardware-cluster</span><span class="sxs-lookup"><span data-stu-id="18712-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="18712-123">tooresize grootte van de VM-tooa beschikbaar in Hallo hardware cluster die als host fungeert voor Hallo VM, uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="18712-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="18712-124">Hallo volgende PowerShell-opdracht is beschikbaar in Hallo hardware cluster hostingservice Hallo cloud waarin toolist Hallo VM-grootten Hallo VM worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18712-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="18712-125">Hallo na opdrachten tooresize Hallo VM worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18712-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="18712-126">Op een nieuwe hardware cluster vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="18712-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="18712-127">grootte van de VM-tooa niet beschikbaar in het Hallo hardware cluster host tooresize Hallo VM, hello cloudservice en alle virtuele machines in de cloudservice Hallo moeten opnieuw worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18712-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="18712-128">Elke cloudservice wordt gehost op een cluster met één hardware, zodat alle VM's in de cloudservice Hallo moet een grootte die wordt ondersteund op een hardware-cluster.</span><span class="sxs-lookup"><span data-stu-id="18712-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="18712-129">Hallo volgende stappen wordt beschreven hoe een virtuele machine verwijderd en vervolgens opnieuw te maken van tooresize Hallo cloud service.</span><span class="sxs-lookup"><span data-stu-id="18712-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="18712-130">Hallo volgende PowerShell-opdracht toolist Hallo VM-grootten beschikbaar in Hallo regio worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="18712-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="18712-131">Noteer alle configuratie-instellingen voor elke virtuele machine in Hallo cloudservice waarin Hallo VM toobe is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="18712-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="18712-132">Verwijder alle VM's in de cloudservice Hallo Hallo optie tooretain Hallo schijven selecteren voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="18712-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="18712-133">Maak deze opnieuw Hallo VM toobe gewijzigd met behulp van Hallo gewenste VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="18712-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="18712-134">Alle andere virtuele machines die zich in de Hallo cloudservice met behulp van een VM-grootte beschikbaar zijn in Hallo hardware cluster service in de cloud Hallo nu de host opnieuw.</span><span class="sxs-lookup"><span data-stu-id="18712-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="18712-135">Een voorbeeld van een script voor het verwijderen en opnieuw maken van een cloudservice met behulp van een nieuwe VM-grootte vindt [hier](https://github.com/Azure/azure-vm-scripts).</span><span class="sxs-lookup"><span data-stu-id="18712-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="18712-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18712-136">Next steps</span></span>
* <span data-ttu-id="18712-137">[Formaat van een virtuele machine gemaakt in Hallo Resource Manager-implementatiemodel](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18712-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

