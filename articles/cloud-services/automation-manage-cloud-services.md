---
title: Azure Cloud Services beheren met Azure Automation | Microsoft Docs
description: Meer informatie over hoe Azure Automation-service kan worden gebruikt voor het beheren van Azure-cloud-services op grote schaal.
services: cloud-services, automation
documentationcenter: 
author: jodoglevy
manager: timlt
editor: 
ms.assetid: 3789810a-2892-4eef-bf29-c781c1b5af48
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2016
ms.author: timlt
ms.openlocfilehash: 6b5acac1b8647c324988c316cd5602b3dba98a1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="7cb66-103">Azure Cloud Services met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="7cb66-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="7cb66-104">Deze handleiding vindt u de Azure Automation-service en hoe deze kan worden gebruikt voor het vereenvoudigen van beheer van uw Azure-cloud-services.</span><span class="sxs-lookup"><span data-stu-id="7cb66-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="7cb66-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="7cb66-105">What is Azure Automation?</span></span>
<span data-ttu-id="7cb66-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="7cb66-107">Met behulp van Azure Automation, worden langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken geautomatiseerd om betrouwbaarheid, efficiëntie en tijd voor de waarde voor uw organisatie te verhogen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="7cb66-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar is om te voldoen aan de behoeften van uw wanneer uw organisatie groeit.</span><span class="sxs-lookup"><span data-stu-id="7cb66-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="7cb66-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="7cb66-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="7cb66-110">Lagere operationele overhead en vrijmaken IT / DevOps-personeel te concentreren op het werk dat zakelijke voegt waarde door uw cloud-beheertaken automatisch wordt uitgevoerd door Azure Automation te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="7cb66-111">Hoe kan Azure Automation helpen Azure-cloudservices beheren</span><span class="sxs-lookup"><span data-stu-id="7cb66-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="7cb66-112">Azure-cloud-services in Azure Automation kunnen worden beheerd met behulp van de PowerShell-cmdlets die beschikbaar zijn in de [hulpprogramma's van Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="7cb66-112">Azure cloud services can be managed in Azure Automation by using the PowerShell cmdlets that are available in the [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="7cb66-113">Azure Automation heeft deze cloud service PowerShell-cmdlets beschikbaar gebruiksklaar, zodat u al uw cloud service management-taken in de service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7cb66-113">Azure Automation has these cloud service PowerShell cmdlets available out of the box, so that you can perform all of your cloud service management tasks within the service.</span></span> <span data-ttu-id="7cb66-114">U kunt ook deze cmdlets in Azure Automation met de cmdlets voor andere Azure-services, complexe om taken te automatiseren via Azure-services en 3e systemen van derden koppelen.</span><span class="sxs-lookup"><span data-stu-id="7cb66-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="7cb66-115">Sommige voorbeeld maakt gebruik van Azure Automation voor het beheren van Azure Cloud Services omvatten:</span><span class="sxs-lookup"><span data-stu-id="7cb66-115">Some example uses of Azure Automation to manage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="7cb66-116">Continue implementatie van een Cloudservice wanneer cscfg of cspkg wordt bijgewerkt in Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="7cb66-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="7cb66-117">Cloud Service-exemplaren parallel één upgradedomein tegelijk opnieuw op te starten</span><span class="sxs-lookup"><span data-stu-id="7cb66-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="7cb66-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7cb66-118">Next Steps</span></span>
<span data-ttu-id="7cb66-119">Nu u de basisprincipes van Azure Automation en hoe deze kan worden gebruikt voor het beheren van Azure-cloudservices hebt geleerd, volgt u deze koppelingen voor meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="7cb66-119">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure cloud services, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="7cb66-120">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="7cb66-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="7cb66-121">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="7cb66-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="7cb66-122">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="7cb66-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
