---
title: aaaVM opnieuw te starten of het formaat problemen | Microsoft Docs
description: Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="f36ca-103">Klassieke implementatieproblemen oplossen met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure</span><span class="sxs-lookup"><span data-stu-id="f36ca-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f36ca-104">Klassiek</span><span class="sxs-lookup"><span data-stu-id="f36ca-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="f36ca-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f36ca-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="f36ca-106">Wanneer u een gestopte Azure virtuele Machine (VM) toostart probeert of vergroten of verkleinen van een bestaande virtuele machine in Azure, is Hallo veelvoorkomende fout die u tegenkomt een geheugentoewijzing is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f36ca-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="f36ca-107">Deze fout treedt op wanneer het Hallo-cluster of de regio ofwel geen beschikbare bronnen heeft of kan niet aangevraagd ondersteuning Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="f36ca-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f36ca-108">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f36ca-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f36ca-109">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="f36ca-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f36ca-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f36ca-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f36ca-111">Zie voor de Resource Manager-versie Hallo [hier](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f36ca-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="f36ca-112">De auditlogboeken verzamelen</span><span class="sxs-lookup"><span data-stu-id="f36ca-112">Collect audit logs</span></span>
<span data-ttu-id="f36ca-113">het oplossen van problemen toostart verzamelen Hallo audit registreert tooidentify Hallo fout Hallo probleem gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f36ca-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="f36ca-114">Klik in hello Azure-portal, op **Bladeren** > **virtuele machines** > *uw virtuele Linux-machine*  >   **Instellingen** > **controlelogboeken**.</span><span class="sxs-lookup"><span data-stu-id="f36ca-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="f36ca-115">Probleem: Fout bij het starten van een gestopte VM</span><span class="sxs-lookup"><span data-stu-id="f36ca-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="f36ca-116">U probeert een gestopte VM toostart maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="f36ca-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f36ca-117">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f36ca-117">Cause</span></span>
<span data-ttu-id="f36ca-118">Hallo-aanvraag toostart Hallo gestopt VM heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe.</span><span class="sxs-lookup"><span data-stu-id="f36ca-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f36ca-119">Hallo-cluster heeft echter geen vrije ruimte beschikbaar toofulfill Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f36ca-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="f36ca-120">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f36ca-120">Resolution</span></span>
* <span data-ttu-id="f36ca-121">Een nieuwe cloudservice maken en deze koppelen aan ofwel een regio of een virtueel netwerk met op basis van regio, maar niet in een affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="f36ca-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="f36ca-122">Verwijder Hallo VM gestopt.</span><span class="sxs-lookup"><span data-stu-id="f36ca-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="f36ca-123">Maak opnieuw Hallo VM in de nieuwe cloudservice Hallo Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="f36ca-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="f36ca-124">Start Hallo VM opnieuw wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f36ca-124">Start hello re-created VM.</span></span>

<span data-ttu-id="f36ca-125">Als u een fout opgetreden krijgt bij een poging een nieuwe cloudservice toocreate, probeer op een later tijdstip of regio voor de cloudservice Hallo Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f36ca-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f36ca-126">nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, zodat u toochange die informatie nodig voor alle Hallo afhankelijkheden die deze informatie voor een bestaande cloudservice Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f36ca-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="f36ca-127">Probleem: Fout wanneer het formaat van een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f36ca-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="f36ca-128">U probeert een bestaande VM tooresize maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="f36ca-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="f36ca-129">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="f36ca-129">Cause</span></span>
<span data-ttu-id="f36ca-130">Hallo-aanvraag tooresize Hallo VM toobe heeft geprobeerd op het oorspronkelijke cluster Hallo hosts Hallo cloudservice.</span><span class="sxs-lookup"><span data-stu-id="f36ca-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="f36ca-131">Hallo-cluster biedt echter geen ondersteuning Hallo aangevraagde VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="f36ca-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="f36ca-132">Oplossing</span><span class="sxs-lookup"><span data-stu-id="f36ca-132">Resolution</span></span>
<span data-ttu-id="f36ca-133">Verminderen Hallo aangevraagde VM-grootte en probeer het opnieuw Hallo vergroten of verkleinen van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="f36ca-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="f36ca-134">Klik op **door alle Bladeren** > **virtuele machines (klassiek)** > *uw virtuele machine* > **instellingen** > **grootte**.</span><span class="sxs-lookup"><span data-stu-id="f36ca-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="f36ca-135">Zie voor gedetailleerde stappen [Hallo virtuele machine vergroten of verkleinen](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="f36ca-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="f36ca-136">Als dit niet mogelijk tooreduce Hallo VM-grootte is, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="f36ca-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="f36ca-137">Maak een nieuwe cloudservice, zodat het is niet gekoppeld tooan affiniteitsgroep en niet zijn gekoppeld aan een virtueel netwerk dat is gekoppeld tooan affiniteitsgroep.</span><span class="sxs-lookup"><span data-stu-id="f36ca-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="f36ca-138">Maak een nieuwe, groter formaat VM in het.</span><span class="sxs-lookup"><span data-stu-id="f36ca-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="f36ca-139">U kunt uw virtuele machines consolideren Hallo moeten dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="f36ca-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="f36ca-140">Als uw bestaande cloudservice gekoppeld aan een regio op basis van een virtueel netwerk is, kunt u Hallo nieuwe cloud service toohello bestaand virtueel netwerk verbinden.</span><span class="sxs-lookup"><span data-stu-id="f36ca-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="f36ca-141">Als de bestaande cloudservice Hallo niet gekoppeld aan een regio op basis van een virtueel netwerk is, vervolgens u hebt toodelete hello, virtuele machines in een bestaande cloudservice hello, en ze opnieuw maken in een nieuwe cloudservice Hallo van hun schijven.</span><span class="sxs-lookup"><span data-stu-id="f36ca-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="f36ca-142">Het is echter belangrijk tooremember dat nieuwe cloudservice Hallo heeft een nieuwe naam en het VIP, dus u tooupdate moet deze voor alle Hallo afhankelijkheden die momenteel gebruikmaken van deze informatie voor een bestaande cloudservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="f36ca-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f36ca-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f36ca-143">Next steps</span></span>
<span data-ttu-id="f36ca-144">Als u problemen ondervindt bij het maken van een nieuwe Linux VM in Azure, Zie [implementatieproblemen oplossen met het maken van een nieuwe virtuele Linux-machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f36ca-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

