---
title: Linux-VM-implementatie-RM oplossen | Microsoft Docs
description: Resource Manager implementatieproblemen bij het maken van een nieuwe virtuele Linux-machine in Azure oplossen
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: aea5db05843b0175b8ef8b713944e12262e33010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="69566-103">Resource Manager deployment problemen met het maken van een nieuwe virtuele Linux-machine in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="69566-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="69566-104">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="69566-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="69566-105">Zie voor andere VM-implementatieproblemen en vragen [problemen met implementatie Linux virtuele machine in Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="69566-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="69566-106">Registreert activiteit verzamelen</span><span class="sxs-lookup"><span data-stu-id="69566-106">Collect activity logs</span></span>
<span data-ttu-id="69566-107">U start het oplossen van problemen door de activiteitenlogboeken om u te identificeren van de fout die is gekoppeld aan het probleem te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="69566-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="69566-108">De volgende koppelingen bevatten gedetailleerde informatie over het proces te volgen.</span><span class="sxs-lookup"><span data-stu-id="69566-108">The following links contain detailed information on the process to follow.</span></span>

[<span data-ttu-id="69566-109">Implementatiebewerkingen bekijken</span><span class="sxs-lookup"><span data-stu-id="69566-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="69566-110">Activiteit-logboeken voor het beheren van Azure-resources bekijken</span><span class="sxs-lookup"><span data-stu-id="69566-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="69566-111">**Y:** als het besturingssysteem Linux gegeneraliseerd, en deze wordt geüpload en/of met de algemene instelling vastgelegd, wordt niet eventuele fouten.</span><span class="sxs-lookup"><span data-stu-id="69566-111">**Y:** If the OS is Linux generalized, and it is uploaded and/or captured with the generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="69566-112">Op dezelfde manier als het besturingssysteem zich Linux gespecialiseerde, en deze wordt geüpload en/of met de instelling voor gespecialiseerde vastgelegd en vervolgens niet eventuele fouten.</span><span class="sxs-lookup"><span data-stu-id="69566-112">Similarly, if the OS is Linux specialized, and it is uploaded and/or captured with the specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="69566-113">**Fouten uploaden:**</span><span class="sxs-lookup"><span data-stu-id="69566-113">**Upload Errors:**</span></span>

<span data-ttu-id="69566-114">**N<sup>1</sup>:** als het besturingssysteem is gegeneraliseerd Linux, en is geüpload als gespecialiseerde, ontvangt u een inrichting time-outfout omdat de virtuele machine in de inrichting stadium is vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="69566-114">**N<sup>1</sup>:** If the OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because the VM is stuck at the provisioning stage.</span></span>

<span data-ttu-id="69566-115">**N<sup>2</sup>:** als het besturingssysteem is Linux gespecialiseerde en als gegeneraliseerd is geüpload, krijgt u een inrichting is mislukt omdat de nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="69566-115">**N<sup>2</sup>:** If the OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span>

<span data-ttu-id="69566-116">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="69566-116">**Resolution:**</span></span>

<span data-ttu-id="69566-117">Als u wilt zowel deze fouten oplossen, de oorspronkelijke schijf geüpload, beschikbare on-premises, met dezelfde instelling als die voor het besturingssysteem (gegeneraliseerd/specifieke).</span><span class="sxs-lookup"><span data-stu-id="69566-117">To resolve both these errors, upload the original VHD, available on-prem, with the same setting as that for the OS (generalized/specialized).</span></span> <span data-ttu-id="69566-118">Als u wilt uploaden als gegeneraliseerd, vergeet niet om uit te voeren - inrichting eerst ervan ongedaan maakt.</span><span class="sxs-lookup"><span data-stu-id="69566-118">To upload as generalized, remember to run -deprovision first.</span></span>

<span data-ttu-id="69566-119">**Vastleggen fouten:**</span><span class="sxs-lookup"><span data-stu-id="69566-119">**Capture Errors:**</span></span>

<span data-ttu-id="69566-120">**N<sup>3</sup>:** als het besturingssysteem gegeneraliseerd Linux is, en deze wordt vastgelegd als gespecialiseerde, ontvangt u een inrichting time-outfout omdat de oorspronkelijke virtuele machine kan niet worden gebruikt als deze is gemarkeerd als gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="69566-120">**N<sup>3</sup>:** If the OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because the original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="69566-121">**N<sup>4</sup>:** als het besturingssysteem is Linux gespecialiseerde en deze is vastgelegd, zoals gegeneraliseerd, krijgt u een inrichting is mislukt omdat de nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="69566-121">**N<sup>4</sup>:** If the OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because the new VM is running with the original computer name, username and password.</span></span> <span data-ttu-id="69566-122">Ook de oorspronkelijke virtuele machine kan niet worden gebruikt omdat deze is gemarkeerd als gespecialiseerde.</span><span class="sxs-lookup"><span data-stu-id="69566-122">Also, the original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="69566-123">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="69566-123">**Resolution:**</span></span>

<span data-ttu-id="69566-124">Beide deze fouten oplossen, de huidige installatiekopie verwijderen vanuit de portal en [opnieuw vanaf het huidige VHD's vastleggen](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) met dezelfde instelling als die voor het besturingssysteem (gegeneraliseerd/specifieke).</span><span class="sxs-lookup"><span data-stu-id="69566-124">To resolve both these errors, delete the current image from the portal, and [recapture it from the current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with the same setting as that for the OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="69566-125">Probleem: Aangepaste / galerie / marketplace-installatiekopie; Toewijzingsfout</span><span class="sxs-lookup"><span data-stu-id="69566-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="69566-126">Deze fout zich voordoet in situaties wanneer de nieuwe VM-aanvraag is vastgemaakt aan een cluster dat de aangevraagde VM-grootte kan niet worden ondersteund of heeft geen beschikbare vrije ruimte voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="69566-126">This error arises in situations when the new VM request is pinned to a cluster that either cannot support the VM size being requested, or does not have available free space to accommodate the request.</span></span>

<span data-ttu-id="69566-127">**1 oorzaak:** het cluster kan het aangevraagde VM-grootte niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="69566-127">**Cause 1:** The cluster cannot support the requested VM size.</span></span>

<span data-ttu-id="69566-128">**Oplossing 1:**</span><span class="sxs-lookup"><span data-stu-id="69566-128">**Resolution 1:**</span></span>

* <span data-ttu-id="69566-129">Probeer de aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="69566-129">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="69566-130">Als de grootte van de aangevraagde virtuele machine kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="69566-130">If the size of the requested VM cannot be changed:</span></span>
  * <span data-ttu-id="69566-131">Stop de virtuele machines in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="69566-131">Stop all the VMs in the availability set.</span></span>
    <span data-ttu-id="69566-132">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="69566-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="69566-133">Nadat de virtuele machines stoppen, moet u de nieuwe virtuele machine maken in de gewenste grootte.</span><span class="sxs-lookup"><span data-stu-id="69566-133">After all the VMs stop, create the new VM in the desired size.</span></span>
  * <span data-ttu-id="69566-134">De nieuwe virtuele machine eerst te starten en vervolgens selecteert u elk van de gestopte virtuele machines en klik op **Start**.</span><span class="sxs-lookup"><span data-stu-id="69566-134">Start the new VM first, and then select each of the stopped VMs and click **Start**.</span></span>

<span data-ttu-id="69566-135">**2 oorzaak:** het cluster heeft geen gratis resources.</span><span class="sxs-lookup"><span data-stu-id="69566-135">**Cause 2:** The cluster does not have free resources.</span></span>

<span data-ttu-id="69566-136">**Oplossing 2:**</span><span class="sxs-lookup"><span data-stu-id="69566-136">**Resolution 2:**</span></span>

* <span data-ttu-id="69566-137">De aanvraag op een later tijdstip opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="69566-137">Retry the request at a later time.</span></span>
* <span data-ttu-id="69566-138">Als de nieuwe virtuele machine deel van een andere beschikbaarheidsset uitmaken kan</span><span class="sxs-lookup"><span data-stu-id="69566-138">If the new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="69566-139">Maak een nieuwe virtuele machine in een andere beschikbaarheidsset (in dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="69566-139">Create a new VM in a different availability set (in the same region).</span></span>
  * <span data-ttu-id="69566-140">De nieuwe virtuele machine toevoegen aan hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="69566-140">Add the new VM to the same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69566-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69566-141">Next steps</span></span>
<span data-ttu-id="69566-142">Als u problemen ondervindt wanneer u een gestopte Linux VM starten of het formaat van een bestaande Linux VM in Azure, Zie [problemen bij de implementatie met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure Resource Manager oplossen](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="69566-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

