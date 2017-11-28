---
title: aaaScheduler referentiemateriaal voor PowerShell-Cmdlets
description: Scheduler-referentiemateriaal voor PowerShell-Cmdlets
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="aabc9-103">Scheduler-referentiemateriaal voor PowerShell-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="aabc9-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="aabc9-104">Hallo volgende tabel worden beschreven en koppelingen toohello-verwijzingspagina van elk van de belangrijkste Hallo-cmdlets in Azure Scheduler.</span><span class="sxs-lookup"><span data-stu-id="aabc9-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="aabc9-105">tooinstall Azure PowerShell en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aabc9-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="aabc9-106">Voor meer informatie over [Azure Resource Manager-cmdlets](/powershell/azure/overview), Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="aabc9-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="aabc9-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="aabc9-107">Cmdlet</span></span> | <span data-ttu-id="aabc9-108">Beschrijving van de cmdlet</span><span class="sxs-lookup"><span data-stu-id="aabc9-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="aabc9-109">Schakel AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-110">Hiermee schakelt u een taakverzameling bevat.</span><span class="sxs-lookup"><span data-stu-id="aabc9-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="aabc9-111">Schakel AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-112">Een jobverzameling kunt.</span><span class="sxs-lookup"><span data-stu-id="aabc9-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="aabc9-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="aabc9-114">Scheduler-taken opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aabc9-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="aabc9-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-116">Taakverzamelingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aabc9-116">Gets job collections.</span></span> |
| [<span data-ttu-id="aabc9-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="aabc9-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="aabc9-118">Taakgeschiedenis opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aabc9-118">Gets job history.</span></span> |
| [<span data-ttu-id="aabc9-119">Nieuwe AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="aabc9-120">Maakt een HTTP-taak.</span><span class="sxs-lookup"><span data-stu-id="aabc9-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="aabc9-121">Nieuwe AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-122">Een jobverzameling maakt.</span><span class="sxs-lookup"><span data-stu-id="aabc9-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="aabc9-123">Nieuwe AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="aabc9-124">Een service bus-wachtrijtaak maakt.</span><span class="sxs-lookup"><span data-stu-id="aabc9-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="aabc9-125">Nieuwe AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="aabc9-126">Maakt een taak van service bus-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="aabc9-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="aabc9-127">Nieuwe AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="aabc9-128">Maakt een taak van de wachtrij opslag.</span><span class="sxs-lookup"><span data-stu-id="aabc9-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="aabc9-129">Verwijder AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="aabc9-130">Hiermee verwijdert u een geplande taak.</span><span class="sxs-lookup"><span data-stu-id="aabc9-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="aabc9-131">Verwijder AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-132">Hiermee verwijdert u een taakverzameling bevat.</span><span class="sxs-lookup"><span data-stu-id="aabc9-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="aabc9-133">Set-AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="aabc9-134">Hiermee wijzigt u een HTTP-Scheduler-taak.</span><span class="sxs-lookup"><span data-stu-id="aabc9-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="aabc9-135">Set-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="aabc9-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="aabc9-136">Een jobverzameling wijzigt.</span><span class="sxs-lookup"><span data-stu-id="aabc9-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="aabc9-137">Set-AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="aabc9-138">Hiermee wijzigt u een service bus-wachtrijtaak.</span><span class="sxs-lookup"><span data-stu-id="aabc9-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="aabc9-139">Set-AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="aabc9-140">Hiermee wijzigt u een service bus-onderwerp taak.</span><span class="sxs-lookup"><span data-stu-id="aabc9-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="aabc9-141">Set-AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="aabc9-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="aabc9-142">Hiermee wijzigt u een taak van de wachtrij opslag.</span><span class="sxs-lookup"><span data-stu-id="aabc9-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="aabc9-143">Voor meer gedetailleerde informatie kunt u een van de volgende cmdlets Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="aabc9-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="aabc9-144">Zie ook</span><span class="sxs-lookup"><span data-stu-id="aabc9-144">See Also</span></span>
 [<span data-ttu-id="aabc9-145">Wat is Scheduler?</span><span class="sxs-lookup"><span data-stu-id="aabc9-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="aabc9-146">Azure Scheduler-concepten, -terminologie en -entiteitenhiërarchie</span><span class="sxs-lookup"><span data-stu-id="aabc9-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="aabc9-147">Aan de slag met behulp van Scheduler in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="aabc9-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="aabc9-148">Plannen en facturering in Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="aabc9-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="aabc9-149">Naslaginformatie over REST API van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="aabc9-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="aabc9-150">Hoge beschikbaarheid en betrouwbaarheid van Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="aabc9-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="aabc9-151">Azure Scheduler-limieten, standaardwaarden en foutcodes</span><span class="sxs-lookup"><span data-stu-id="aabc9-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="aabc9-152">Azure Scheduler uitgaande verificatie</span><span class="sxs-lookup"><span data-stu-id="aabc9-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

