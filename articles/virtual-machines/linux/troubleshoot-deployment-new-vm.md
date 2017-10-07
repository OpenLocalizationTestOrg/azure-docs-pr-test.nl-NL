---
title: Linux-VM-implementatie-RM aaaTroubleshoot | Microsoft Docs
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
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="95ee0-103">Resource Manager deployment problemen met het maken van een nieuwe virtuele Linux-machine in Azure oplossen</span><span class="sxs-lookup"><span data-stu-id="95ee0-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="95ee0-104">Meest voorkomende problemen</span><span class="sxs-lookup"><span data-stu-id="95ee0-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="95ee0-105">Zie voor andere VM-implementatieproblemen en vragen [problemen met implementatie Linux virtuele machine in Azure](troubleshoot-deploy-vm.md).</span><span class="sxs-lookup"><span data-stu-id="95ee0-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="95ee0-106">Registreert activiteit verzamelen</span><span class="sxs-lookup"><span data-stu-id="95ee0-106">Collect activity logs</span></span>
<span data-ttu-id="95ee0-107">het oplossen van problemen toostart verzamelen Hallo activiteit registreert tooidentify Hallo fout die is gekoppeld aan Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="95ee0-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="95ee0-108">Hallo bevatten volgende koppelingen gedetailleerde informatie over Hallo proces toofollow.</span><span class="sxs-lookup"><span data-stu-id="95ee0-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="95ee0-109">Implementatiebewerkingen bekijken</span><span class="sxs-lookup"><span data-stu-id="95ee0-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="95ee0-110">Weergeven van de activiteit logboeken toomanage Azure resources</span><span class="sxs-lookup"><span data-stu-id="95ee0-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="95ee0-111">**Y:** als Hallo OS Linux gegeneraliseerd, en deze wordt geüpload en/of vastgelegd Hello gegeneraliseerd instellen, wordt niet eventuele fouten.</span><span class="sxs-lookup"><span data-stu-id="95ee0-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="95ee0-112">Op dezelfde manier als Hallo OS Linux speciaal bedoeld is, en deze wordt geüpload en/of vastgelegd met gespecialiseerde Hallo instelling, en eventuele fouten niet.</span><span class="sxs-lookup"><span data-stu-id="95ee0-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="95ee0-113">**Fouten uploaden:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-113">**Upload Errors:**</span></span>

<span data-ttu-id="95ee0-114">**N<sup>1</sup>:** als Hallo OS Linux gegeneraliseerd en is geüpload als gespecialiseerde, ontvangt u een inrichting time-outfout omdat Hallo VM is vastgelopen bij Hallo fase inrichten.</span><span class="sxs-lookup"><span data-stu-id="95ee0-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="95ee0-115">**N<sup>2</sup>:** als Hallo OS is Linux gespecialiseerde en als gegeneraliseerd is geüpload, krijgt u een inrichting is mislukt omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam hello, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="95ee0-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="95ee0-116">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-116">**Resolution:**</span></span>

<span data-ttu-id="95ee0-117">tooresolve beide deze fouten uploaden Hallo oorspronkelijke VHD, beschikbare on-premises, Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke).</span><span class="sxs-lookup"><span data-stu-id="95ee0-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="95ee0-118">tooupload zoals gegeneraliseerd, houd er rekening mee toorun-inrichting eerst ervan ongedaan maakt.</span><span class="sxs-lookup"><span data-stu-id="95ee0-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="95ee0-119">**Vastleggen fouten:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-119">**Capture Errors:**</span></span>

<span data-ttu-id="95ee0-120">**N<sup>3</sup>:** als Hallo OS Linux gegeneraliseerd en deze wordt vastgelegd als gespecialiseerde, ontvangt u een inrichting time-outfout omdat Hallo oorspronkelijke VM kan niet worden gebruikt als deze is gemarkeerd als gegeneraliseerd.</span><span class="sxs-lookup"><span data-stu-id="95ee0-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="95ee0-121">**N<sup>4</sup>:** als Hallo OS is Linux gespecialiseerde en deze is vastgelegd, zoals gegeneraliseerd, krijgt u een inrichting is mislukt omdat hello nieuwe virtuele machine wordt uitgevoerd met de oorspronkelijke computernaam hello, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="95ee0-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="95ee0-122">Bovendien Hallo oorspronkelijke VM kan niet worden gebruikt omdat deze is gemarkeerd als gespecialiseerde.</span><span class="sxs-lookup"><span data-stu-id="95ee0-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="95ee0-123">**Oplossing:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-123">**Resolution:**</span></span>

<span data-ttu-id="95ee0-124">tooresolve beide deze fouten Hallo huidige installatiekopie verwijderen vanuit de portal Hallo en [opnieuw vastleggen van Hallo huidige VHD's](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Hallo met dezelfde instelling als die voor Hallo OS (gegeneraliseerd/specifieke).</span><span class="sxs-lookup"><span data-stu-id="95ee0-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="95ee0-125">Probleem: Aangepaste / galerie / marketplace-installatiekopie; Toewijzingsfout</span><span class="sxs-lookup"><span data-stu-id="95ee0-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="95ee0-126">Deze fout zich voordoet in situaties wanneer Hallo nieuwe VM-aanvraag is vastgemaakt tooa cluster Hallo aangevraagde VM-grootte kan niet worden ondersteund of heeft geen beschikbare vrije ruimte tooaccommodate Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="95ee0-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="95ee0-127">**1 oorzaak:** Hallo cluster ondersteunt geen Hallo aangevraagde VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="95ee0-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="95ee0-128">**Oplossing 1:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-128">**Resolution 1:**</span></span>

* <span data-ttu-id="95ee0-129">Probeer Hallo-aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="95ee0-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="95ee0-130">Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="95ee0-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="95ee0-131">Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="95ee0-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="95ee0-132">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="95ee0-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="95ee0-133">Nadat alle virtuele machines stoppen hello, maakt u Hallo nieuwe virtuele machine in Hallo gewenst grootte.</span><span class="sxs-lookup"><span data-stu-id="95ee0-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="95ee0-134">Start eerst Hallo van nieuwe virtuele machine en vervolgens Selecteer Hallo gestopt VM's en klik op **Start**.</span><span class="sxs-lookup"><span data-stu-id="95ee0-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="95ee0-135">**2 oorzaak:** Hallo cluster heeft geen gratis resources.</span><span class="sxs-lookup"><span data-stu-id="95ee0-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="95ee0-136">**Oplossing 2:**</span><span class="sxs-lookup"><span data-stu-id="95ee0-136">**Resolution 2:**</span></span>

* <span data-ttu-id="95ee0-137">Hallo aanvraag opnieuw proberen op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="95ee0-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="95ee0-138">Als hello nieuwe virtuele machine kan deel uitmaken van een andere beschikbaarheidsset instellen</span><span class="sxs-lookup"><span data-stu-id="95ee0-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="95ee0-139">Maak een nieuwe virtuele machine in een andere beschikbaarheidsset (in Hallo dezelfde regio).</span><span class="sxs-lookup"><span data-stu-id="95ee0-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="95ee0-140">Toevoegen van nieuwe VM-toohello Hallo hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="95ee0-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95ee0-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95ee0-141">Next steps</span></span>
<span data-ttu-id="95ee0-142">Als u problemen ondervindt wanneer u een gestopte Linux VM starten of het formaat van een bestaande Linux VM in Azure, Zie [problemen bij de implementatie met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure Resource Manager oplossen](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95ee0-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

