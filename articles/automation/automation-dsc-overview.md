---
title: Overzicht van Azure Automation DSC | Microsoft Docs
description: Een overzicht van Azure Automation Desired State Configuration (DSC), de termen en bekende problemen
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell dsc, de configuratie van de gewenste status, de powershell dsc-azure
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 468321fa6863d78bc0d179fbe5c2ed6195040d50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="5e6d8-104">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="5e6d8-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="5e6d8-105">Azure Automation DSC is een Azure-service waarmee u kunt schrijven, beheren en PowerShell Desired State Configuration (DSC) worden gecompileerd [configuraties](https://msdn.microsoft.com/powershell/dsc/configurations), importeren [DSC-Resources](https://msdn.microsoft.com/powershell/dsc/resources), en configuraties toewijzen aan de doelknooppunten allemaal in de cloud.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-105">Azure Automation DSC is an Azure service that allows you to write, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations to target nodes, all in the cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="5e6d8-106">Waarom Azure Automation DSC gebruiken</span><span class="sxs-lookup"><span data-stu-id="5e6d8-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="5e6d8-107">Azure Automation DSC biedt verschillende voordelen ten opzichte van DSC buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="5e6d8-108">Ingebouwde pull-server</span><span class="sxs-lookup"><span data-stu-id="5e6d8-108">Built-in pull server</span></span>

<span data-ttu-id="5e6d8-109">Azure Automation biedt een [DSC-pull-server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) zodat doelknooppunten automatisch configuraties ontvangen, voldoen aan de gewenste status en rapporteren over hun compliance.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform to the desired state, and report back on their compliance.</span></span>
<span data-ttu-id="5e6d8-110">De ingebouwde pull-server in Azure Automation hoeven instellen en onderhouden van uw eigen pull-server.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-110">The built-in pull server in Azure Automation eliminates the need to set up and maintain your own pull server.</span></span>
<span data-ttu-id="5e6d8-111">Azure Automation kunt richten virtuele of fysieke Windows of Linux machines, in de cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-111">Azure Automation can target virtual or physical Windows or Linux machines, in the cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="5e6d8-112">Beheer van alle DSC-artefacten</span><span class="sxs-lookup"><span data-stu-id="5e6d8-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="5e6d8-113">Azure Automation DSC biedt dezelfde management laag bij [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) zoals Azure Automation voor het PowerShell-scripts biedt.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-113">Azure Automation DSC brings the same management layer to [PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="5e6d8-114">De Azure-portal, of PowerShell, kunt u alle uw DSC-configuraties, bronnen en doelknooppunten kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-114">From the Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Schermopname van het Azure Automation-blade](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="5e6d8-116">Reporting gegevens importeren in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="5e6d8-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="5e6d8-117">Gedetailleerde status rapportagegegevens verzenden knooppunten die worden beheerd met Azure Automation DSC naar de ingebouwde pull-server.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data to the built-in pull server.</span></span>
<span data-ttu-id="5e6d8-118">U kunt Azure Automation DSC voor het verzenden van deze gegevens naar de werkruimte voor logboekanalyse voor Microsoft Operations Management Suite (OMS) configureren.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-118">You can configure Azure Automation DSC to send this data to your Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="5e6d8-119">Zie voor meer informatie over DSC statusgegevens verzenden naar de werkruimte voor logboekanalyse, [doorsturen Azure Automation-DSC rapportagegegevens met OMS Log Analytics](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5e6d8-119">To learn how to send DSC status data to your Log Analytics workspace, see [Forward Azure Automation DSC reporting data to OMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="5e6d8-120">Introductievideo</span><span class="sxs-lookup"><span data-stu-id="5e6d8-120">Introduction video</span></span>

<span data-ttu-id="5e6d8-121">Wilt u liever kijken dan lezen?</span><span class="sxs-lookup"><span data-stu-id="5e6d8-121">Prefer watching to reading?</span></span> <span data-ttu-id="5e6d8-122">Bekijk de volgende video van mei 2015, wanneer Azure Automation DSC voor het eerst is aangekondigd hebben.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-122">Have a look at the following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="5e6d8-123">Terwijl de concepten en de levenscyclus van de in deze video worden besproken correct zijn, is Azure Automation DSC veel gevorderd sinds deze video is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-123">While the concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="5e6d8-124">Het is nu algemeen beschikbaar, heeft een veel uitgebreidere gebruikersinterface in de Azure-portal en biedt ondersteuning voor veel meer mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5e6d8-124">It is now generally available, has a much more extensive UI in the Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="5e6d8-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e6d8-125">Next steps</span></span>

* <span data-ttu-id="5e6d8-126">Voor meer informatie over hoe voor vrijgeven knooppunten moeten worden beheerd met Azure Automation DSC zien [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-126">To learn how to onboard nodes to be managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="5e6d8-127">Om aan de slag met Azure Automation DSC, Zie [aan de slag met Azure Automation DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-127">To get started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="5e6d8-128">Zie voor meer informatie over het compileren van DSC-configuraties, zodat u deze aan de doelknooppunten toewijzen kunt, [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-128">To learn about compiling DSC configurations so that you can assign them to target nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="5e6d8-129">Zie voor referentiemateriaal voor PowerShell-cmdlet voor Azure Automation DSC, [Azure Automation DSC-cmdlets](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="5e6d8-130">Zie voor informatie over prijzen, [prijzen van Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="5e6d8-131">Zie voor een voorbeeld van het gebruik van Azure Automation DSC in een pijplijn continue implementatie [continue implementatie voor IaaS VM's met behulp van Azure Automation DSC en Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="5e6d8-131">To see an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment to IaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>