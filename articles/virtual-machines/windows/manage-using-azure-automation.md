---
title: aaaManage virtuele machines met Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage kan worden virtuele Azure-machines op grote schaal.
services: virtual-machines-windows, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: ce49f83a-f409-42ee-af74-a8ea2caa9ae8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2016
ms.author: timlt
ms.openlocfilehash: bfe7b3a51b6e82bd7cd5b0a83df7226476ed4f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="0c206-103">Azure Virtual Machines beheren met Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0c206-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="0c206-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze kan worden gebruikt toosimplify het beheren van uw virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="0c206-104">This guide introduces you toohello Azure Automation service and how it can be used toosimplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0c206-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="0c206-105">What is Azure Automation?</span></span>
<span data-ttu-id="0c206-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="0c206-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="0c206-107">Met behulp van Azure Automation, zijn langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en naar tijdwaarde maken voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="0c206-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="0c206-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar toomeet wanneer uw organisatie groeit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="0c206-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="0c206-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="0c206-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0c206-110">U kunt lagere operationele overhead en vrijmaken IT en DevOps personeel toofocus op werk waarmee bedrijfswaarde toegevoegd door het uitvoeren van uw cloud beheertaken automatisch met Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="0c206-110">You can lower operational overhead and free up IT and DevOps staff toofocus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="0c206-111">Hoe kan Azure Automation helpen beheren van virtuele machines in Azure?</span><span class="sxs-lookup"><span data-stu-id="0c206-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="0c206-112">Virtuele machines in Azure Automation kunnen worden beheerd met behulp van [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c206-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="0c206-113">Azure Automation bevat hello Azure PowerShell-cmdlets, zodat u al uw taken voor het beheer van virtuele machine binnen Hallo-service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0c206-113">Azure Automation includes hello Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within hello service.</span></span> <span data-ttu-id="0c206-114">U kunt ook Hallo-cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate koppelen in Azure-services en systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="0c206-114">You can also pair hello cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c206-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c206-115">Next steps</span></span>
<span data-ttu-id="0c206-116">Nu dat u hebt geleerd Hallo basisbeginselen van Azure Automation en hoe deze gebruikt toomanage kan worden virtuele machines in Azure, meer informatie:</span><span class="sxs-lookup"><span data-stu-id="0c206-116">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="0c206-117">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0c206-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="0c206-118">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="0c206-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="0c206-119">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="0c206-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

