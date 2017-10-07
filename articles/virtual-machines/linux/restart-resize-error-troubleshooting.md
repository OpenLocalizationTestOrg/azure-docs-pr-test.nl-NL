---
title: aaaVM opnieuw te starten of het formaat problemen in Azure | Microsoft Docs
description: Oplossen van problemen bij de implementatie met opnieuw te starten of het formaat van een bestaande virtuele Linux-Machine in Azure Resource Manager
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="cd179-103">Problemen oplossen implementatie met opnieuw te starten of het formaat van een bestaande Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="cd179-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="cd179-104">Wanneer u een gestopte Azure virtuele Machine (VM) toostart probeert of vergroten of verkleinen van een bestaande virtuele machine in Azure, is Hallo veelvoorkomende fout die u tegenkomt een geheugentoewijzing is mislukt.</span><span class="sxs-lookup"><span data-stu-id="cd179-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="cd179-105">Deze fout treedt op wanneer het Hallo-cluster of de regio ofwel geen beschikbare bronnen heeft of kan niet aangevraagd ondersteuning Hallo VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="cd179-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="cd179-106">Registreert activiteit verzamelen</span><span class="sxs-lookup"><span data-stu-id="cd179-106">Collect activity logs</span></span>
<span data-ttu-id="cd179-107">het oplossen van problemen toostart verzamelen Hallo activiteit registreert tooidentify Hallo fout die is gekoppeld aan Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="cd179-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="cd179-108">Hallo koppelingen volgen bevatten gedetailleerde informatie over het Hallo-proces:</span><span class="sxs-lookup"><span data-stu-id="cd179-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="cd179-109">Implementatiebewerkingen bekijken</span><span class="sxs-lookup"><span data-stu-id="cd179-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="cd179-110">Weergeven van de activiteit logboeken toomanage Azure resources</span><span class="sxs-lookup"><span data-stu-id="cd179-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="cd179-111">Probleem: Fout bij het starten van een gestopte VM</span><span class="sxs-lookup"><span data-stu-id="cd179-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="cd179-112">U probeert een gestopte VM toostart maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="cd179-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="cd179-113">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="cd179-113">Cause</span></span>
<span data-ttu-id="cd179-114">Hallo-aanvraag toostart Hallo gestopt VM heeft geprobeerd op Hallo oorspronkelijke cluster die als host fungeert voor de cloudservice hello toobe.</span><span class="sxs-lookup"><span data-stu-id="cd179-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="cd179-115">Hallo-cluster heeft echter geen vrije ruimte beschikbaar toofulfill Hallo aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cd179-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="cd179-116">Oplossing</span><span class="sxs-lookup"><span data-stu-id="cd179-116">Resolution</span></span>
* <span data-ttu-id="cd179-117">Stop alle Hallo VM's in Hallo beschikbaarheid ingesteld en elke VM start opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="cd179-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="cd179-118">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="cd179-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="cd179-119">Nadat alle Hallo van virtuele machines stoppen, selecteert u elk Hallo gestopt VM's en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="cd179-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="cd179-120">Hallo herstart aanvraag opnieuw proberen op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="cd179-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="cd179-121">Probleem: Fout wanneer het formaat van een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cd179-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="cd179-122">U probeert een bestaande VM tooresize maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="cd179-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="cd179-123">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="cd179-123">Cause</span></span>
<span data-ttu-id="cd179-124">Hallo-aanvraag tooresize Hallo VM toobe heeft geprobeerd op het oorspronkelijke cluster Hallo hosts Hallo cloudservice.</span><span class="sxs-lookup"><span data-stu-id="cd179-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="cd179-125">Hallo-cluster biedt echter geen ondersteuning Hallo aangevraagde VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="cd179-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="cd179-126">Oplossing</span><span class="sxs-lookup"><span data-stu-id="cd179-126">Resolution</span></span>
* <span data-ttu-id="cd179-127">Probeer Hallo-aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="cd179-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="cd179-128">Als hello aangevraagde grootte van Hallo dat VM kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="cd179-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="cd179-129">Stop alle Hallo-VM's in de beschikbaarheidsset Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd179-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="cd179-130">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="cd179-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="cd179-131">Nadat alle virtuele machines stoppen hello, Hallo gewenst VM tooa groter formaat.</span><span class="sxs-lookup"><span data-stu-id="cd179-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="cd179-132">Selecteer Hallo gewijzigd VM en klikt u op **Start**, en vervolgens start Hallo VM's gestopt.</span><span class="sxs-lookup"><span data-stu-id="cd179-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd179-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd179-133">Next steps</span></span>
<span data-ttu-id="cd179-134">Als u problemen ondervindt bij het maken van een nieuwe Linux VM in Azure, Zie [implementatieproblemen oplossen met het maken van een nieuwe virtuele Linux-machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd179-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

