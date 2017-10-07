---
title: aaaManage Azure API Management met behulp van Azure Automation
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure API Management kan worden.
services: api-management, automation
documentationcenter: 
author: csand-msft
manager: eamono
editor: 
ms.assetid: 2e53c9af-f738-47f8-b1b6-593050a7c51b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 05b8e3cad786fa701feb88f7b6d9629f16686d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-api-management-using-azure-automation"></a><span data-ttu-id="3ba64-103">Azure API Management met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="3ba64-103">Managing Azure API Management using Azure Automation</span></span>
<span data-ttu-id="3ba64-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van Azure API Management kan zijn.</span><span class="sxs-lookup"><span data-stu-id="3ba64-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure API Management.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="3ba64-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="3ba64-105">What is Azure Automation?</span></span>
<span data-ttu-id="3ba64-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="3ba64-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="3ba64-107">Met behulp van Azure Automation, kunnen handmatige, herhaalde langlopende en foutgevoelige-taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="3ba64-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="3ba64-108">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="3ba64-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="3ba64-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="3ba64-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="3ba64-110">Operationele overhead verminderen en vrijmaken IT en DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3ba64-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-api-management"></a><span data-ttu-id="3ba64-111">Hoe kan Azure Automation helpen beheren van Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="3ba64-111">How can Azure Automation help manage Azure API Management?</span></span>
<span data-ttu-id="3ba64-112">API Management in Azure Automation kunnen worden beheerd met behulp van Hallo [Windows PowerShell-cmdlets voor Azure API Management-API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span><span class="sxs-lookup"><span data-stu-id="3ba64-112">API Management can be managed in Azure Automation by using hello [Windows PowerShell cmdlets for Azure API Management API](https://azure.microsoft.com/updates/full-set-of-windows-powershell-cmdlets-for-azure-api-management-api/).</span></span> <span data-ttu-id="3ba64-113">In Azure Automation kunt u veel van uw API Management-taken met behulp van cmdlets Hallo PowerShell workflow-scripts tooperform schrijven.</span><span class="sxs-lookup"><span data-stu-id="3ba64-113">Within Azure Automation you can write PowerShell workflow scripts tooperform many of your API Management tasks using hello cmdlets.</span></span> <span data-ttu-id="3ba64-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="3ba64-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="3ba64-115">Hier volgen enkele voorbeelden van het gebruik van API Management met Automation:</span><span class="sxs-lookup"><span data-stu-id="3ba64-115">Here are some examples of using API Management with Automation:</span></span>

* [<span data-ttu-id="3ba64-116">Azure API Management-PowerShell gebruiken voor back-up en herstel</span><span class="sxs-lookup"><span data-stu-id="3ba64-116">Azure API Management – Using PowerShell for backup and restore</span></span>](https://blogs.msdn.microsoft.com/katriend/2015/10/02/azure-api-management-using-powershell-for-backup-and-restore/)

## <a name="next-steps"></a><span data-ttu-id="3ba64-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3ba64-117">Next Steps</span></span>
<span data-ttu-id="3ba64-118">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure API Management hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="3ba64-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure API Management, follow these links toolearn more.</span></span>

* <span data-ttu-id="3ba64-119">Zie hello Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="3ba64-119">See hello Azure Automation [getting started tutorial](../automation/automation-first-runbook-graphical.md).</span></span>

