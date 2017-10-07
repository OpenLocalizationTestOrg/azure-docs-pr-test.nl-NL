---
title: aaaManage Azure Web-App met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure-Web-App kan zijn.
services: app-service\web, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: c960a44f-f941-401d-afba-a4bc0f0394eb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte
ms.openlocfilehash: 6d80351a2927f26753cfbaead6e1c0c3c94e86e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-web-app-using-azure-automation"></a><span data-ttu-id="edd14-103">Azure Web-App met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="edd14-103">Managing Azure Web App using Azure Automation</span></span>
<span data-ttu-id="edd14-104">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van Azure-Web-App kan zijn.</span><span class="sxs-lookup"><span data-stu-id="edd14-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure Web App.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="edd14-105">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="edd14-105">What is Azure Automation?</span></span>
<span data-ttu-id="edd14-106">[Azure Automation](../automation/automation-intro.md) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="edd14-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="edd14-107">Met behulp van Azure Automation, kunnen handmatige, herhaalde langlopende en foutgevoelige-taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="edd14-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="edd14-108">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="edd14-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="edd14-109">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="edd14-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="edd14-110">Operationele overhead verminderen en vrijmaken IT en DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="edd14-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-web-app"></a><span data-ttu-id="edd14-111">Hoe kan Azure Automation helpen Azure-Web-App beheren?</span><span class="sxs-lookup"><span data-stu-id="edd14-111">How can Azure Automation help manage Azure Web App?</span></span>
<span data-ttu-id="edd14-112">Web-App in Azure Automation kan worden beheerd met Hallo PowerShell-cmdlets die beschikbaar in Hallo zijn [Azure PowerShell-modules](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="edd14-112">Web App can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell modules](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="edd14-113">U kunt [deze Web-App PowerShell-cmdlets installeren in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), zodat u al uw Web-App management-taken in Hallo service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="edd14-113">You can [install these Web App PowerShell cmdlets in Azure Automation](https://azure.microsoft.com/blog/announcing-azure-resource-manager-support-azure-automation-runbooks/), so that you can perform all of your Web App management tasks within hello service.</span></span> <span data-ttu-id="edd14-114">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services tooautomate complexe taken ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="edd14-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="edd14-115">Hier volgen enkele voorbeelden van het beheer van App-Services met Automation:</span><span class="sxs-lookup"><span data-stu-id="edd14-115">Here are some examples of managing App Services with Automation:</span></span>

* [<span data-ttu-id="edd14-116">Scripts voor het beheren van Web-Apps</span><span class="sxs-lookup"><span data-stu-id="edd14-116">Scripts for managing Web Apps</span></span>](https://azure.microsoft.com/documentation/scripts/)

## <a name="next-steps"></a><span data-ttu-id="edd14-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="edd14-117">Next steps</span></span>
<span data-ttu-id="edd14-118">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure-Web-App hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="edd14-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Web App, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="edd14-119">Zie hello Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="edd14-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

