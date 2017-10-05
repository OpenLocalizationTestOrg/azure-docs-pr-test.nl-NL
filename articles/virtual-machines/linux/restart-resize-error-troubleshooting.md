---
title: Virtuele machine opnieuw te starten of het formaat problemen in Azure | Microsoft Docs
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
ms.openlocfilehash: e49322dbccf4ec1157bc7e3a109175869b53518d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="da5f8-103">Problemen oplossen implementatie met opnieuw te starten of het formaat van een bestaande Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="da5f8-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="da5f8-104">Wanneer u een gestopte Azure virtuele Machine (VM) start of het formaat van een bestaande virtuele machine in Azure, is de algemene fout die u tegenkomt een geheugentoewijzing is mislukt.</span><span class="sxs-lookup"><span data-stu-id="da5f8-104">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="da5f8-105">Deze fout treedt op wanneer het cluster of de regio geen bronnen beschikbaar heeft of het aangevraagde VM-grootte kan niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="da5f8-105">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="da5f8-106">Registreert activiteit verzamelen</span><span class="sxs-lookup"><span data-stu-id="da5f8-106">Collect activity logs</span></span>
<span data-ttu-id="da5f8-107">U start het oplossen van problemen door de activiteitenlogboeken om u te identificeren van de fout die is gekoppeld aan het probleem te verzamelen.</span><span class="sxs-lookup"><span data-stu-id="da5f8-107">To start troubleshooting, collect the activity logs to identify the error associated with the issue.</span></span> <span data-ttu-id="da5f8-108">De volgende koppelingen bevatten gedetailleerde informatie over het proces:</span><span class="sxs-lookup"><span data-stu-id="da5f8-108">The following links contain detailed information on the process:</span></span>

[<span data-ttu-id="da5f8-109">Implementatiebewerkingen bekijken</span><span class="sxs-lookup"><span data-stu-id="da5f8-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="da5f8-110">Activiteit-logboeken voor het beheren van Azure-resources bekijken</span><span class="sxs-lookup"><span data-stu-id="da5f8-110">View activity logs to manage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="da5f8-111">Probleem: Fout bij het starten van een gestopte VM</span><span class="sxs-lookup"><span data-stu-id="da5f8-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="da5f8-112">U probeert te starten van een gestopte VM maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="da5f8-112">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="da5f8-113">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="da5f8-113">Cause</span></span>
<span data-ttu-id="da5f8-114">De aanvraag voor het starten van de gestopte virtuele machine moet worden uitgevoerd op het oorspronkelijke cluster die als host fungeert voor de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="da5f8-114">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="da5f8-115">Het cluster heeft echter geen vrije schijfruimte om de aanvraag te voldoen.</span><span class="sxs-lookup"><span data-stu-id="da5f8-115">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="da5f8-116">Oplossing</span><span class="sxs-lookup"><span data-stu-id="da5f8-116">Resolution</span></span>
* <span data-ttu-id="da5f8-117">Alle VM's in de beschikbaarheidsset Stop en start opnieuw op elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="da5f8-117">Stop all the VMs in the availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="da5f8-118">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="da5f8-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="da5f8-119">Nadat de virtuele machines stoppen, selecteert u elk van de gestopte virtuele machines en klik op Start.</span><span class="sxs-lookup"><span data-stu-id="da5f8-119">After all the VMs stop, select each of the stopped VMs and click Start.</span></span>
* <span data-ttu-id="da5f8-120">Probeer de aanvraag opnieuw opstarten op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="da5f8-120">Retry the restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="da5f8-121">Probleem: Fout wanneer het formaat van een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="da5f8-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="da5f8-122">U probeert te vergroten of verkleinen van een bestaande virtuele machine, maar een toewijzingsfout ophalen.</span><span class="sxs-lookup"><span data-stu-id="da5f8-122">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="da5f8-123">Oorzaak</span><span class="sxs-lookup"><span data-stu-id="da5f8-123">Cause</span></span>
<span data-ttu-id="da5f8-124">De aanvraag voor het formaat van de virtuele machine moet worden uitgevoerd op het oorspronkelijke cluster die als host fungeert voor de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="da5f8-124">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="da5f8-125">Het cluster biedt echter geen ondersteuning voor de aangevraagde VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="da5f8-125">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="da5f8-126">Oplossing</span><span class="sxs-lookup"><span data-stu-id="da5f8-126">Resolution</span></span>
* <span data-ttu-id="da5f8-127">Probeer de aanvraag met een kleinere VM.</span><span class="sxs-lookup"><span data-stu-id="da5f8-127">Retry the request using a smaller VM size.</span></span>
* <span data-ttu-id="da5f8-128">Als de grootte van de aangevraagde virtuele machine kan niet worden gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="da5f8-128">If the size of the requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="da5f8-129">Stop de virtuele machines in de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="da5f8-129">Stop all the VMs in the availability set.</span></span>
     
     * <span data-ttu-id="da5f8-130">Klik op **resourcegroepen** > *uw resourcegroep* > **Resources** > *uw beschikbaarheidsset*  >  **Virtuele Machines** > *uw virtuele machine* > **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="da5f8-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="da5f8-131">Nadat de virtuele machines stoppen, de grootte van de gewenste VM in een groter formaat.</span><span class="sxs-lookup"><span data-stu-id="da5f8-131">After all the VMs stop, resize the desired VM to a larger size.</span></span>
  3. <span data-ttu-id="da5f8-132">Selecteer de VM formaat is gewijzigd en klik op **Start**, en start de gestopte virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="da5f8-132">Select the resized VM and click **Start**, and then start each of the stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da5f8-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="da5f8-133">Next steps</span></span>
<span data-ttu-id="da5f8-134">Als u problemen ondervindt bij het maken van een nieuwe Linux VM in Azure, Zie [implementatieproblemen oplossen met het maken van een nieuwe virtuele Linux-machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da5f8-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

