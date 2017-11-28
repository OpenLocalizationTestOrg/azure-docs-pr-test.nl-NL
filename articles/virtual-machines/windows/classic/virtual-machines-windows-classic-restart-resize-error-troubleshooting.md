---
title: aaaVM opnieuw te starten of het formaat problemen | Microsoft Docs
description: Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande Windows virtuele Machine in Azure
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 3d00ba17d9558941a37a29034604cb15e0803e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="d218f-103">Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande Windows virtuele Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="d218f-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d218f-104">Klassiek</span><span class="sxs-lookup"><span data-stu-id="d218f-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="d218f-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d218f-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="d218f-106">Wanneer u een gestopte Azure virtuele Machine (VM) toostart probeert of vergroten of verkleinen van een bestaande virtuele machine in Azure, is Hallo veelvoorkomende fout die u tegenkomt een geheugentoewijzing is mislukt.</span><span class="sxs-lookup"><span data-stu-id="d218f-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="d218f-107">Deze fout treedt op wanneer het Hallo-cluster of de regio ofwel geen beschikbare bronnen heeft of kan niet aangevraagd ondersteuning Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="d218f-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d218f-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d218f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d218f-109">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d218f-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d218f-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d218f-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="d218f-111">De auditlogboeken verzamelen</span><span class="sxs-lookup"><span data-stu-id="d218f-111">Collect audit logs</span></span>
<span data-ttu-id="d218f-112">het oplossen van problemen toostart verzamelen Hallo audit registreert tooidentify Hallo fout Hallo probleem gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="d218f-112">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="d218f-113">Klik in hello Azure-portal, op **Bladeren** > **virtuele machines** > *uw Windows-machine*  >   **Instellingen** > **controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="d218f-113">In hello Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="d218f-114">Probleem: Fout bij het starten van een gestopte VM</span><span class="sxs-lookup"><span data-stu-id="d218f-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="d218f-115">U probeert een gestopte VM toostart maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="d218f-115">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="d218f-116">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d218f-116">Cause</span></span>
<span data-ttu-id="d218f-117">Hallo-aanvraag toostart Hallo gestopt VM heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe.</span><span class="sxs-lookup"><span data-stu-id="d218f-117">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="d218f-118">Hallo-cluster heeft echter geen vrije ruimte beschikbaar toofulfill Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d218f-118">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="d218f-119">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d218f-119">Resolution</span></span>
* <span data-ttu-id="d218f-120">Een nieuwe cloudservice maken en deze koppelen aan ofwel een regio of een virtueel netwerk met op basis van regio, maar niet in een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="d218f-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="d218f-121">Verwijder Hallo VM gestopt.</span><span class="sxs-lookup"><span data-stu-id="d218f-121">Delete hello stopped VM.</span></span>
* <span data-ttu-id="d218f-122">Maak opnieuw Hallo VM in de nieuwe cloudservice Hallo Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="d218f-122">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="d218f-123">Start Hallo VM opnieuw wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d218f-123">Start hello re-created VM.</span></span>

<span data-ttu-id="d218f-124">Als u een fout opgetreden krijgt bij een poging een nieuwe cloudservice toocreate, probeer het later opnieuw of regio voor de cloudservice Hallo Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d218f-124">If you get an error when trying toocreate a new cloud service, either retry later or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d218f-125">nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, zodat u toochange die informatie nodig voor alle Hallo afhankelijkheden die deze informatie voor een bestaande cloudservice Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d218f-125">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="d218f-126">Probleem: Fout wanneer het formaat van een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="d218f-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="d218f-127">U probeert een bestaande VM tooresize maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="d218f-127">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="d218f-128">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="d218f-128">Cause</span></span>
<span data-ttu-id="d218f-129">Hallo-aanvraag tooresize Hallo VM toobe heeft geprobeerd op het oorspronkelijke cluster Hallo hosts Hallo cloudservice.</span><span class="sxs-lookup"><span data-stu-id="d218f-129">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="d218f-130">Hallo-cluster biedt echter geen ondersteuning Hallo aangevraagde VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="d218f-130">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="d218f-131">Oplossing</span><span class="sxs-lookup"><span data-stu-id="d218f-131">Resolution</span></span>
<span data-ttu-id="d218f-132">Verminderen Hallo aangevraagde VM-grootte en probeer het opnieuw Hallo vergroten of verkleinen van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d218f-132">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="d218f-133">Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > *uw virtuele machine* > **instellingen** > **grootte**.</span><span class="sxs-lookup"><span data-stu-id="d218f-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="d218f-134">Zie voor gedetailleerde stappen [Hallo virtuele machine vergroten of verkleinen](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="d218f-134">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="d218f-135">Als dit niet mogelijk tooreduce Hallo VM-grootte is, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="d218f-135">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="d218f-136">Maak een nieuwe cloudservice, zodat het is niet gekoppeld tooan affiniteitsgroep en niet zijn gekoppeld aan een virtueel netwerk dat is gekoppeld tooan affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="d218f-136">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="d218f-137">Maak een nieuwe, groter formaat VM in het.</span><span class="sxs-lookup"><span data-stu-id="d218f-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="d218f-138">U kunt uw virtuele machines consolideren Hallo moeten dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="d218f-138">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="d218f-139">Als uw bestaande cloudservice gekoppeld aan een regio op basis van een virtueel netwerk is, kunt u Hallo nieuwe cloud service toohello bestaand virtueel netwerk verbinden.</span><span class="sxs-lookup"><span data-stu-id="d218f-139">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="d218f-140">Als de bestaande cloudservice Hallo niet gekoppeld aan een regio op basis van een virtueel netwerk is, vervolgens u hebt toodelete hello, virtuele machines in een bestaande cloudservice hello, en ze opnieuw maken in een nieuwe cloudservice Hallo van hun schijven.</span><span class="sxs-lookup"><span data-stu-id="d218f-140">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="d218f-141">Het is echter belangrijk tooremember dat nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, dus u tooupdate moet deze voor alle Hallo afhankelijkheden die momenteel gebruikmaken van deze informatie voor een bestaande cloudservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="d218f-141">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d218f-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d218f-142">Next steps</span></span>
<span data-ttu-id="d218f-143">Als u problemen ondervindt bij het maken van een virtuele Windows-machine in Azure, Zie [implementatieproblemen oplossen met het maken van een virtuele Windows-machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d218f-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

