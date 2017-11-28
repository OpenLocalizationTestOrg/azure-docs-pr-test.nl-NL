---
title: aaaManage Azure Cloud Services met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure-cloud-services op grote schaal kan worden.
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
ms.openlocfilehash: 8e920fb94955466bfec71cc332444f5f0ee497a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-cloud-services-using-azure-automation"></a><span data-ttu-id="b31f0-103">Azure Cloud Services met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="b31f0-103">Managing Azure Cloud Services using Azure Automation</span></span>
<span data-ttu-id="b31f0-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikte toosimplify beheer van uw Azure-cloud-services kan zijn.</span><span class="sxs-lookup"><span data-stu-id="b31f0-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure cloud services.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b31f0-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="b31f0-105">What is Azure Automation?</span></span>
<span data-ttu-id="b31f0-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="b31f0-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b31f0-107">Met behulp van Azure Automation, kunnen langlopende, handmatige, foutgevoelige en regelmatig herhaalde taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="b31f0-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b31f0-108">Azure Automation biedt een engine voor het uitvoeren van maximaal betrouwbaar en maximaal beschikbare werkstroom die schaalbaar toomeet wanneer uw organisatie groeit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="b31f0-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b31f0-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="b31f0-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b31f0-110">Lagere operationele overhead en vrijmaken IT / DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b31f0-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-cloud-services"></a><span data-ttu-id="b31f0-111">Hoe kan Azure Automation helpen Azure-cloudservices beheren</span><span class="sxs-lookup"><span data-stu-id="b31f0-111">How can Azure Automation help manage Azure cloud services?</span></span>
<span data-ttu-id="b31f0-112">Azure-cloud-services kunnen worden beheerd in Azure Automation met Hallo PowerShell-cmdlets die beschikbaar in Hallo zijn [hulpprogramma's van Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="b31f0-112">Azure cloud services can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="b31f0-113">Azure Automation heeft deze cloud service PowerShell-cmdlets beschikbaar out of box hello, zodat u al uw cloud service management-taken in Hallo service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b31f0-113">Azure Automation has these cloud service PowerShell cmdlets available out of hello box, so that you can perform all of your cloud service management tasks within hello service.</span></span> <span data-ttu-id="b31f0-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="b31f0-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b31f0-115">Maakt gebruik van een aantal voorbeelden van Azure Automation toomanage die Azure Cloud Services omvatten:</span><span class="sxs-lookup"><span data-stu-id="b31f0-115">Some example uses of Azure Automation toomanage Azure Cloud Services include:</span></span>

* [<span data-ttu-id="b31f0-116">Continue implementatie van een Cloudservice wanneer cscfg of cspkg wordt bijgewerkt in Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="b31f0-116">Continous deployment of a Cloud Service whenever cscfg or cspkg is updated in Azure Blob storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Continuous-Deployment-of-A-eeebf3a6)
* [<span data-ttu-id="b31f0-117">Cloud Service-exemplaren parallel één upgradedomein tegelijk opnieuw op te starten</span><span class="sxs-lookup"><span data-stu-id="b31f0-117">Rebooting Cloud Service instances in parallel, one upgrade domain at a time</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Reboot-Cloud-Service-PaaS-b337a06d)

## <a name="next-steps"></a><span data-ttu-id="b31f0-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b31f0-118">Next Steps</span></span>
<span data-ttu-id="b31f0-119">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure cloudservices hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b31f0-119">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure cloud services, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="b31f0-120">Overzicht van Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b31f0-120">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="b31f0-121">Mijn eerste runbook</span><span class="sxs-lookup"><span data-stu-id="b31f0-121">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b31f0-122">Azure Automation-leeroverzicht</span><span class="sxs-lookup"><span data-stu-id="b31f0-122">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
