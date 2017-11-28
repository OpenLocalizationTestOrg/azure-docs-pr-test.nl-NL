---
title: aaaManage Azure RemoteApp met behulp van Azure Automation | Microsoft Docs
description: Meer informatie over hoe hello Azure Automation-service gebruikte toomanage Azure RemoteApp kan worden.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: a4cb23e292c797256e971acb3b363b025f140f16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a><span data-ttu-id="ed5bf-103">Azure RemoteApp met behulp van Azure Automation beheren</span><span class="sxs-lookup"><span data-stu-id="ed5bf-103">Managing Azure RemoteApp using Azure Automation</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ed5bf-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ed5bf-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ed5bf-106">Deze handleiding vindt u toohello Azure Automation-service en hoe deze gebruikt toosimplify beheer van Azure RemoteApp kan zijn.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-106">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of Azure RemoteApp.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="ed5bf-107">Wat is Azure Automation?</span><span class="sxs-lookup"><span data-stu-id="ed5bf-107">What is Azure Automation?</span></span>
<span data-ttu-id="ed5bf-108">[Azure Automation](../automation/automation-intro.md) is een Azure-service voor het cloudbeheer via procesautomatisering vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-108">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="ed5bf-109">Met behulp van Azure Automation, kunnen handmatige, vaak herhaald, langlopende en foutgevoelige-taken worden geautomatiseerd tooincrease betrouwbaarheid, efficiëntie en een tijd toovalue voor uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-109">Using Azure Automation, manual, frequently-repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="ed5bf-110">Azure Automation biedt een engine voor het uitvoeren van uiterst betrouwbare, maximaal beschikbare workflow die schaalbaar toomeet uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-110">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="ed5bf-111">In Azure Automation kunnen processen worden gestarte handmatig, door systemen van derden 3rd of met regelmatige tussenpozen zodat taken gebeuren precies wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-111">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="ed5bf-112">Operationele overhead verminderen en vrijmaken IT en DevOps personeel toofocus op het werk dat bedrijfswaarde door te verplaatsen van uw cloud management taken toobe voegt automatisch uitgevoerd door Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-112">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a><span data-ttu-id="ed5bf-113">Hoe kan Azure Automation helpen beheren van Azure RemoteApp?</span><span class="sxs-lookup"><span data-stu-id="ed5bf-113">How can Azure Automation help manage Azure RemoteApp?</span></span>
<span data-ttu-id="ed5bf-114">RemoteApp in Azure Automation kan worden beheerd met Hallo PowerShell-cmdlets die beschikbaar in Hallo zijn [hulpprogramma's van Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed5bf-114">RemoteApp can be managed in Azure Automation by using hello PowerShell cmdlets that are available in hello [Azure PowerShell tools](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="ed5bf-115">Azure Automation heeft deze RemoteApp-PowerShell-cmdlets beschikbaar out of box hello, zodat u al uw RemoteApp-beheertaken binnen Hallo service kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-115">Azure Automation has these RemoteApp PowerShell cmdlets available out of hello box, so that you can perform all of your RemoteApp management tasks within hello service.</span></span> <span data-ttu-id="ed5bf-116">U kunt deze cmdlets in Azure Automation met Hallo-cmdlets voor andere Azure-services, complexe taken tooautomate ook koppelen in Azure-services en 3e systemen van derden.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-116">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed5bf-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed5bf-117">Next steps</span></span>
<span data-ttu-id="ed5bf-118">Nu u Hallo basisbeginselen van Azure Automation en hoe deze kan worden gebruikt toomanage Azure RemoteApp hebt geleerd, volgt u deze koppelingen toolearn meer informatie over Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="ed5bf-118">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure RemoteApp, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="ed5bf-119">Zie hello Azure Automation [zelfstudie aan de slag](../automation/automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="ed5bf-119">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md)</span></span>

