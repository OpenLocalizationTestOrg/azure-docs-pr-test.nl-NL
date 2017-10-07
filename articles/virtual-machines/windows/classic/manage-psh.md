---
title: aaaManage uw virtuele machines met behulp van Azure PowerShell | Microsoft Docs
description: Meer informatie over opdrachten waarmee u tooautomate taken kunt bij het beheren van uw virtuele machines.
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a><span data-ttu-id="3c0d4-103">Virtuele machines beheren met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c0d4-103">Manage your virtual machines by using Azure PowerShell</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3c0d4-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3c0d4-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3c0d4-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3c0d4-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3c0d4-107">Raadpleeg voor algemene PowerShell-opdrachten met Resource Manager-model hello, [hier](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c0d4-107">For common PowerShell commands using hello Resource Manager model, see [here](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="3c0d4-108">Veel taken die u elke dag toomanage uw virtuele machines kunnen worden geautomatiseerd met behulp van Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-108">Many tasks you do each day toomanage your VMs can be automated by using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3c0d4-109">In dit artikel krijgt u Voorbeeldopdrachten voor eenvoudigere taken en koppelingen tooarticles die Hallo-opdrachten voor complexere taken weergeven.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-109">This article gives you example commands for simpler tasks, and links tooarticles that show hello commands for more complex tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="3c0d4-110">Als u dit nog niet hebt geïnstalleerd en geconfigureerd Azure PowerShell nog, kunt u de instructies op Hallo artikel opvragen [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3c0d4-110">If you haven't installed and configured Azure PowerShell yet, you can get instructions in hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
> 
> 

## <a name="how-toouse-hello-example-commands"></a><span data-ttu-id="3c0d4-111">Hoe toouse Voorbeeldopdrachten Hallo</span><span class="sxs-lookup"><span data-stu-id="3c0d4-111">How toouse hello example commands</span></span>
<span data-ttu-id="3c0d4-112">U moet tooreplace deel van de tekst hello in Hallo opdrachten met de tekst die geschikt is voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-112">You'll need tooreplace some of hello text in hello commands with text that's appropriate for your environment.</span></span> <span data-ttu-id="3c0d4-113">Hallo < en > symbolen geven aan de tekst die u moet tooreplace.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-113">hello < and > symbols indicate text you need tooreplace.</span></span> <span data-ttu-id="3c0d4-114">Wanneer u de tekst hello vervangt, Hallo symbolen verwijderen, maar blijft de Hallo aanhalingstekens in.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-114">When you replace hello text, remove hello symbols but leave hello quote marks in place.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="3c0d4-115">Een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="3c0d4-115">Get a VM</span></span>
<span data-ttu-id="3c0d4-116">Dit is een eenvoudige taak die u vaak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-116">This is a basic task you'll use often.</span></span> <span data-ttu-id="3c0d4-117">Gebruik deze tooget informatie over een virtuele machine, taken uitvoeren op een virtuele machine of uitvoer toostore ophalen in een variabele.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-117">Use it tooget information about a VM, perform tasks on a VM, or get output toostore in a variable.</span></span>

<span data-ttu-id="3c0d4-118">tooget informatie over Hallo VM, deze opdracht, vervangt alles in Hallo aanhalingstekens, inclusief Hallo < en > tekens uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-118">tooget information about hello VM, run this command, replacing everything in hello quotes, including hello < and > characters:</span></span>

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

<span data-ttu-id="3c0d4-119">toostore hello uitvoer in een variabele $vm uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-119">toostore hello output in a $vm variable, run:</span></span>

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a><span data-ttu-id="3c0d4-120">Meld u aan tooa VM op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="3c0d4-120">Log on tooa Windows-based VM</span></span>
<span data-ttu-id="3c0d4-121">Deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-121">Run these commands:</span></span>

> [!NOTE]
> <span data-ttu-id="3c0d4-122">U krijgt Hallo virtuele machine en cloudservicenaam uit Hallo-weergave van Hallo **Get-AzureVM** opdracht.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-122">You can get hello virtual machine and cloud service name from hello display of hello **Get-AzureVM** command.</span></span>
> 
> <span data-ttu-id="3c0d4-123">$svcName = "<cloud service name>" $vmName = '<virtual machine name>' $localPath = "< station en de map locatie toostore Hallo gedownload RDP-bestand, bijvoorbeeld: c:\temp > ' $localFile $localPath = +"\" $vmname + ".rdp' Get-AzureRemoteDesktopFile - ServiceName $svcName-naam $vmName - LocalPath $localFile-starten</span><span class="sxs-lookup"><span data-stu-id="3c0d4-123">$svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "<drive and folder location toostore hello downloaded RDP file, example: c:\temp >" $localFile = $localPath + "\" + $vmname + ".rdp" Get-AzureRemoteDesktopFile -ServiceName $svcName -Name $vmName -LocalPath $localFile -Launch</span></span>
> 
> 

## <a name="stop-a-vm"></a><span data-ttu-id="3c0d4-124">Een VM stoppen</span><span class="sxs-lookup"><span data-stu-id="3c0d4-124">Stop a VM</span></span>
<span data-ttu-id="3c0d4-125">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-125">Run this command:</span></span>

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> <span data-ttu-id="3c0d4-126">Gebruik deze parameter tookeep Hallo virtuele IP-adres (VIP) van Hallo cloud service mocht dat Hallo laatste VM in deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-126">Use this parameter tookeep hello virtual IP (VIP) of hello cloud service in case it's hello last VM in that cloud service.</span></span> <br><br> <span data-ttu-id="3c0d4-127">Als u Hallo StayProvisioned parameter gebruikt, hebt u nog steeds worden gefactureerd voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-127">If you use hello StayProvisioned parameter, you'll still be billed for hello VM.</span></span>
> 
> 

## <a name="start-a-vm"></a><span data-ttu-id="3c0d4-128">Een VM starten</span><span class="sxs-lookup"><span data-stu-id="3c0d4-128">Start a VM</span></span>
<span data-ttu-id="3c0d4-129">Voer deze opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-129">Run this command:</span></span>

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a><span data-ttu-id="3c0d4-130">Een gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="3c0d4-130">Attach a data disk</span></span>
<span data-ttu-id="3c0d4-131">Deze taak zijn een paar stappen vereist.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-131">This task requires a few steps.</span></span> <span data-ttu-id="3c0d4-132">Gebruik eerst Hallo *** toevoegen-AzureDataDisk *** cmdlet tooadd hello toohello $vm schijfobject.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-132">First, you use hello ****Add-AzureDataDisk**** cmdlet tooadd hello disk toohello $vm object.</span></span> <span data-ttu-id="3c0d4-133">Vervolgens gebruikt u **Update-AzureVM** cmdlet tooupdate Hallo configuratie van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-133">Then, you use **Update-AzureVM** cmdlet tooupdate hello configuration of hello VM.</span></span>

<span data-ttu-id="3c0d4-134">U moet ook toodecide of tooattach een nieuwe schijf of een die bevat gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-134">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="3c0d4-135">Voor een nieuwe schijf Hallo opdracht Hallo .vhd-bestand gemaakt en gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-135">For a new disk, hello command creates hello .vhd file and attaches it.</span></span>

<span data-ttu-id="3c0d4-136">een nieuwe schijf tooattach deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-136">tooattach a new disk, run this command:</span></span>

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

<span data-ttu-id="3c0d4-137">een bestaande gegevensschijf tooattach deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-137">tooattach an existing data disk, run this command:</span></span>

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

<span data-ttu-id="3c0d4-138">de gegevensschijven tooattach van een bestaande VHD-bestand in blob storage, wordt deze opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-138">tooattach data disks from an existing .vhd file in blob storage, run this command:</span></span>

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a><span data-ttu-id="3c0d4-139">Maak een VM op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="3c0d4-139">Create a Windows-based VM</span></span>
<span data-ttu-id="3c0d4-140">een nieuwe Windows gebaseerde virtuele machine in Azure, gebruik Hallo instructies in toocreate [Azure PowerShell gebruiken toocreate en vooraf configureren van virtuele machines op basis van Windows](create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3c0d4-140">toocreate a new Windows-based virtual machine in Azure, use hello instructions in [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](create-powershell.md).</span></span> <span data-ttu-id="3c0d4-141">De stappen van dit onderwerp maakt u via Hallo maken van een Azure PowerShell opdracht ingesteld die een VM op basis van Windows die vooraf kan worden geconfigureerd:</span><span class="sxs-lookup"><span data-stu-id="3c0d4-141">This topic steps you through hello creation of an Azure PowerShell command set that creates a Windows-based VM that can be preconfigured:</span></span>

* <span data-ttu-id="3c0d4-142">Met het lidmaatschap van de Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-142">With Active Directory domain membership.</span></span>
* <span data-ttu-id="3c0d4-143">Met andere schijven.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-143">With additional disks.</span></span>
* <span data-ttu-id="3c0d4-144">Als een lid van een bestaande Netwerktaakverdeling instellen.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-144">As a member of an existing load-balanced set.</span></span>
* <span data-ttu-id="3c0d4-145">Met een statisch IP-adres.</span><span class="sxs-lookup"><span data-stu-id="3c0d4-145">With a static IP address.</span></span>

