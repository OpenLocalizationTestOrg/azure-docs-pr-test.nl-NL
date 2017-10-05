---
title: Beheren van virtuele machines met Azure Automation | Microsoft Docs
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van virtuele machines op de gewenste schaal in Azure.
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
ms.openlocfilehash: 15653c5d653ae538bdb66eaf0daee12c35858b45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-virtual-machines-using-azure-automation"></a><span data-ttu-id="b2d79-103">Azure Virtual Machines beheren met Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b2d79-103">Managing Azure Virtual Machines using Azure Automation</span></span>
<span data-ttu-id="b2d79-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van het beheren van uw virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2d79-104">This guide introduces you to the Azure Automation service and how it can be used to simplify managing your Azure virtual machines.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b2d79-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="b2d79-105">What is Azure Automation?</span></span>
<span data-ttu-id="b2d79-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="b2d79-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b2d79-107">Met behulp van Azure Automation, worden langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken voor een verhoging van betrouwbaarheid, efficiëntie en een time-to-value voor uw organisatie geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="b2d79-107">By using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time-to-value for your organization.</span></span>

<span data-ttu-id="b2d79-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar is om te voldoen aan de behoeften van uw wanneer uw organisatie groeit.</span><span class="sxs-lookup"><span data-stu-id="b2d79-108">Azure Automation provides a highly reliable and highly available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="b2d79-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="b2d79-109">In Azure Automation, processes can be kicked off manually, by third-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b2d79-110">U kunt lagere operationele overhead en vrijmaken IT en DevOps-personeel te concentreren op het werk dat bedrijfswaarde toegevoegd door het uitvoeren van uw cloud beheertaken automatisch met Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b2d79-110">You can lower operational overhead and free up IT and DevOps staff to focus on work that adds business value by running your cloud management tasks automatically with Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-virtual-machines"></a><span data-ttu-id="b2d79-111">Hoe kan Azure Automation helpen beheren van virtuele machines in Azure?</span><span class="sxs-lookup"><span data-stu-id="b2d79-111">How can Azure Automation help manage Azure virtual machines?</span></span>
<span data-ttu-id="b2d79-112">Virtuele machines in Azure Automation kunnen worden beheerd met behulp van [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2d79-112">Virtual machines can be managed in Azure Automation by using [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="b2d79-113">Azure Automation bevat de Azure PowerShell-cmdlets waarmee u al uw taken voor het beheer van virtuele machine in de service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b2d79-113">Azure Automation includes the Azure PowerShell cmdlets, so you can perform all of your virtual machine management tasks within the service.</span></span> <span data-ttu-id="b2d79-114">U kunt ook de cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="b2d79-114">You can also pair the cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and third-party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2d79-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2d79-115">Next steps</span></span>
<span data-ttu-id="b2d79-116">Nu dat u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van virtuele machines in Azure hebt geleerd, meer informatie:</span><span class="sxs-lookup"><span data-stu-id="b2d79-116">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure virtual machines, learn more:</span></span>

* [<span data-ttu-id="b2d79-117">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b2d79-117">Azure Automation Overview</span></span>](../../automation/automation-intro.md)
* [<span data-ttu-id="b2d79-118">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="b2d79-118">My first runbook</span></span>](../../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b2d79-119">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="b2d79-119">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)

