---
title: Overzicht van Automation DSC aaaAzure | Microsoft Docs
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
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a><span data-ttu-id="f96fd-104">Overzicht van Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="f96fd-104">Azure Automation DSC Overview</span></span>

<span data-ttu-id="f96fd-105">Azure Automation DSC is een Azure-service waarmee u toowrite, beheren en PowerShell Desired State Configuration (DSC) worden gecompileerd [configuraties](https://msdn.microsoft.com/powershell/dsc/configurations), importeren [DSC-Resources](https://msdn.microsoft.com/powershell/dsc/resources), en toewijzen configuraties tootarget knooppunten, die allemaal in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="f96fd-105">Azure Automation DSC is an Azure service that allows you toowrite, manage, and compile PowerShell Desired State Configuration (DSC) [configurations](https://msdn.microsoft.com/powershell/dsc/configurations), import [DSC Resources](https://msdn.microsoft.com/powershell/dsc/resources), and assign configurations tootarget nodes, all in hello cloud.</span></span>

## <a name="why-use-azure-automation-dsc"></a><span data-ttu-id="f96fd-106">Waarom Azure Automation DSC gebruiken</span><span class="sxs-lookup"><span data-stu-id="f96fd-106">Why use Azure Automation DSC</span></span>

<span data-ttu-id="f96fd-107">Azure Automation DSC biedt verschillende voordelen ten opzichte van DSC buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="f96fd-107">Azure Automation DSC provides several advantages over using DSC outside of Azure.</span></span>

### <a name="built-in-pull-server"></a><span data-ttu-id="f96fd-108">Ingebouwde pull-server</span><span class="sxs-lookup"><span data-stu-id="f96fd-108">Built-in pull server</span></span>

<span data-ttu-id="f96fd-109">Azure Automation biedt een [DSC-pull-server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) zodat doelknooppunten automatisch configuraties ontvangen, conform toohello gewenst staat, en rapporteren over hun compliance.</span><span class="sxs-lookup"><span data-stu-id="f96fd-109">Azure Automation provides a [DSC pull server](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) so that target nodes automatically receive configurations, conform toohello desired state, and report back on their compliance.</span></span>
<span data-ttu-id="f96fd-110">Hallo ingebouwde pull-server in Azure Automation Hallo nodig tooset up elimineert en onderhouden van uw eigen pull-server.</span><span class="sxs-lookup"><span data-stu-id="f96fd-110">hello built-in pull server in Azure Automation eliminates hello need tooset up and maintain your own pull server.</span></span>
<span data-ttu-id="f96fd-111">Azure Automation kunt richten virtuele of fysieke Windows of Linux machines, in Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="f96fd-111">Azure Automation can target virtual or physical Windows or Linux machines, in hello cloud or on-premises.</span></span>

### <a name="management-of-all-your-dsc-artifacts"></a><span data-ttu-id="f96fd-112">Beheer van alle DSC-artefacten</span><span class="sxs-lookup"><span data-stu-id="f96fd-112">Management of all your DSC artifacts</span></span>

<span data-ttu-id="f96fd-113">Azure Automation DSC biedt dezelfde beheerlaag te Hallo[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) zoals Azure Automation voor het PowerShell-scripts biedt.</span><span class="sxs-lookup"><span data-stu-id="f96fd-113">Azure Automation DSC brings hello same management layer too[PowerShell Desired State Configuration](https://msdn.microsoft.com/powershell/dsc/overview) as Azure Automation offers for PowerShell scripting.</span></span>

<span data-ttu-id="f96fd-114">Hello Azure-portal, of PowerShell, kunt u alle uw DSC-configuraties, bronnen en doelknooppunten kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="f96fd-114">From hello Azure portal, or from PowerShell, you can manage all your DSC configurations, resources, and target nodes.</span></span>

![Schermopname van hello Azure Automation-blade](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a><span data-ttu-id="f96fd-116">Reporting gegevens importeren in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f96fd-116">Import reporting data into Log Analytics</span></span>

<span data-ttu-id="f96fd-117">Gedetailleerde status gegevens toohello ingebouwde pull rapportserver wordt verzonden door de knooppunten die worden beheerd met Azure Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="f96fd-117">Nodes that are managed with Azure Automation DSC send detailed reporting status data toohello built-in pull server.</span></span>
<span data-ttu-id="f96fd-118">Deze gegevens tooyour Microsoft Operations Management Suite (OMS) Log Analytics-werkruimte kunt u Azure Automation DSC toosend configureren.</span><span class="sxs-lookup"><span data-stu-id="f96fd-118">You can configure Azure Automation DSC toosend this data tooyour Microsoft Operations Management Suite (OMS) Log Analytics workspace.</span></span>
<span data-ttu-id="f96fd-119">hoe toosend DSC status gegevens tooyour werkruimte voor logboekanalyse zien toolearn [doorsturen Azure Automation-DSC reporting gegevens tooOMS logboekanalyse](automation-dsc-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f96fd-119">toolearn how toosend DSC status data tooyour Log Analytics workspace, see [Forward Azure Automation DSC reporting data tooOMS Log Analytics](automation-dsc-diagnostics.md).</span></span>

## <a name="introduction-video"></a><span data-ttu-id="f96fd-120">Introductievideo</span><span class="sxs-lookup"><span data-stu-id="f96fd-120">Introduction video</span></span>

<span data-ttu-id="f96fd-121">Voorkeur tooreading bekijken?</span><span class="sxs-lookup"><span data-stu-id="f96fd-121">Prefer watching tooreading?</span></span> <span data-ttu-id="f96fd-122">Hebben bekijkt hello volgende video van mei 2015, wanneer Azure Automation DSC voor het eerst is aangekondigd.</span><span class="sxs-lookup"><span data-stu-id="f96fd-122">Have a look at hello following video from May 2015, when Azure Automation DSC was first announced.</span></span>

>[!NOTE]
><span data-ttu-id="f96fd-123">Tijdens het Hallo-concepten en levenscyclus in deze video worden besproken correct zijn, is Azure Automation DSC veel gevorderd sinds deze video is opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f96fd-123">While hello concepts and life cycle discussed in this video are correct, Azure Automation DSC has progressed a lot since this video was recorded.</span></span>
><span data-ttu-id="f96fd-124">Het is nu algemeen beschikbaar, heeft een veel uitgebreidere gebruikersinterface in hello Azure-portal en biedt ondersteuning voor veel meer mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="f96fd-124">It is now generally available, has a much more extensive UI in hello Azure portal, and supports many additional capabilities.</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a><span data-ttu-id="f96fd-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f96fd-125">Next steps</span></span>

* <span data-ttu-id="f96fd-126">toolearn hoe tooonboard knooppunten toobe beheerd met Azure Automation DSC raadpleegt [machines voorbereiden voor beheer door Azure Automation DSC](automation-dsc-onboarding.md)</span><span class="sxs-lookup"><span data-stu-id="f96fd-126">toolearn how tooonboard nodes toobe managed with Azure Automation DSC, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md)</span></span>
* <span data-ttu-id="f96fd-127">Zie tooget gestart met behulp van Azure Automation DSC [aan de slag met Azure Automation DSC](automation-dsc-getting-started.md)</span><span class="sxs-lookup"><span data-stu-id="f96fd-127">tooget started using Azure Automation DSC, see [Getting started with Azure Automation DSC](automation-dsc-getting-started.md)</span></span>
* <span data-ttu-id="f96fd-128">toolearn over het compileren van DSC-configuraties, zodat u deze, kunt u knooppunten tootarget toewijzen kunt, Zie [compileren van configuraties in Azure Automation DSC](automation-dsc-compile.md)</span><span class="sxs-lookup"><span data-stu-id="f96fd-128">toolearn about compiling DSC configurations so that you can assign them tootarget nodes, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md)</span></span>
* <span data-ttu-id="f96fd-129">Zie voor referentiemateriaal voor PowerShell-cmdlet voor Azure Automation DSC, [Azure Automation DSC-cmdlets](/powershell/module/azurerm.automation/#automation)</span><span class="sxs-lookup"><span data-stu-id="f96fd-129">For PowerShell cmdlet reference for Azure Automation DSC, see [Azure Automation DSC cmdlets](/powershell/module/azurerm.automation/#automation)</span></span>
* <span data-ttu-id="f96fd-130">Zie voor informatie over prijzen, [prijzen van Azure Automation DSC](https://azure.microsoft.com/pricing/details/automation/)</span><span class="sxs-lookup"><span data-stu-id="f96fd-130">For pricing information, see [Azure Automation DSC pricing](https://azure.microsoft.com/pricing/details/automation/)</span></span>
* <span data-ttu-id="f96fd-131">Zie voor een voorbeeld van het gebruik van Azure Automation DSC in een pijplijn continue implementatie toosee [continue implementatie tooIaaS virtuele machines met behulp van Azure Automation DSC en Chocolatey](automation-dsc-cd-chocolatey.md)</span><span class="sxs-lookup"><span data-stu-id="f96fd-131">toosee an example of using Azure Automation DSC in a continuous deployment pipeline, see  [Continuous Deployment tooIaaS VMs Using Azure Automation DSC and Chocolatey](automation-dsc-cd-chocolatey.md)</span></span>
