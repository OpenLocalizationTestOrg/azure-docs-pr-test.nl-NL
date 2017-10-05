---
title: Bijwerken van de Azure-modules in Azure Automation | Microsoft Docs
description: Dit artikel wordt beschreven hoe u kunt algemene Azure PowerShell-modules standaard meegeleverd in Azure Automation nu bijwerken.
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="0e6af-103">Het bijwerken van Azure PowerShell-modules in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="0e6af-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="0e6af-104">De meest voorkomende Azure PowerShell-modules zijn standaard in elk Automation-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0e6af-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="0e6af-105">Het team van Azure de Azure-modules worden regelmatig updates, zodat het Automation-account we een manier bieden om de modules in het account bijwerken wanneer er nieuwe versies beschikbaar via de portal zijn.</span><span class="sxs-lookup"><span data-stu-id="0e6af-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="0e6af-106">Omdat modules regelmatig door de productgroep bijgewerkt worden, worden wijzigingen kunnen optreden met de cmdlets opgenomen die mogelijk negatieve invloed hebben op uw runbooks afhankelijk van het type wijziging, zoals de naam van een parameter of een cmdlet volledig bestandstypen.</span><span class="sxs-lookup"><span data-stu-id="0e6af-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="0e6af-107">Om te voorkomen die invloed hebben op uw runbooks en de processen die ze automatiseren, is het raadzaam dat u testen en te voordat u doorgaat valideren.</span><span class="sxs-lookup"><span data-stu-id="0e6af-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="0e6af-108">Als u een speciale voor dit doel bestemde Automation-account niet hebt, kunt u een maken zodat u testen veel verschillende scenario's en permutaties tijdens de ontwikkeling van uw runbooks bovendien iteratieve wijzigingen zoals het bijwerken van kunt de PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="0e6af-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="0e6af-109">Nadat de resultaten worden gevalideerd en u vereiste wijzigingen hebt toegepast, doorgaan met de coördinatie van de migratie van alle runbooks die wijziging vereist en de update uitvoeren, zoals hieronder wordt beschreven in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="0e6af-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="0e6af-110">Bijwerken van de Azure-Modules</span><span class="sxs-lookup"><span data-stu-id="0e6af-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="0e6af-111">In de Modules blade van uw Automation-account er is een optie **Azure-Modules WU**.</span><span class="sxs-lookup"><span data-stu-id="0e6af-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="0e6af-112">Het is altijd ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0e6af-112">It is always enabled.</span></span><br><br> <span data-ttu-id="0e6af-113">![De optie Azure Modules in Modules blade bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="0e6af-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="0e6af-114">Klik op **Azure-Modules WU** en u krijgt een bevestigingsbericht weergegeven waarin u wordt gevraagd of u wilt doorgaan.</span><span class="sxs-lookup"><span data-stu-id="0e6af-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="0e6af-115">![Azure-Modules updatebericht](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="0e6af-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="0e6af-116">Klik op **Ja** en begint met het updateproces van de module.</span><span class="sxs-lookup"><span data-stu-id="0e6af-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="0e6af-117">Het updateproces duurt ongeveer 15-20 minuten om bij te werken van de volgende modules:</span><span class="sxs-lookup"><span data-stu-id="0e6af-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="0e6af-118">Azure</span><span class="sxs-lookup"><span data-stu-id="0e6af-118">Azure</span></span>
  * <span data-ttu-id="0e6af-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="0e6af-119">Azure.Storage</span></span>
  * <span data-ttu-id="0e6af-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="0e6af-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="0e6af-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="0e6af-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="0e6af-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="0e6af-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="0e6af-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="0e6af-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="0e6af-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="0e6af-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="0e6af-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="0e6af-125">AzureRm.Storage</span></span>

    <span data-ttu-id="0e6af-126">Als de modules al up-to-date te houden, wordt het proces voltooid binnen een paar seconden.</span><span class="sxs-lookup"><span data-stu-id="0e6af-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="0e6af-127">U ontvangt een melding wanneer de update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0e6af-127">When the update process completes you will be notified.</span></span><br><br> ![Azure-Modules updatestatus bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="0e6af-129">Azure Automation gebruikt de meest recente modules in uw Automation-account wanneer een nieuwe geplande taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e6af-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="0e6af-130">Als u cmdlets uit deze Azure PowerShell-modules in uw runbooks gebruikt om Azure-resources te beheren, wordt vervolgens u voor dit updateproces elke maand of dus voor zorgen dat u de meest recente modules hebben.</span><span class="sxs-lookup"><span data-stu-id="0e6af-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e6af-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e6af-131">Next steps</span></span>

* <span data-ttu-id="0e6af-132">Zie voor meer informatie over integratiemodules en het maken van aangepaste modules voor het Automation verder te integreren met andere systemen, services of oplossingen, [integratiemodules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="0e6af-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="0e6af-133">Overweeg het gebruik van bron besturingselement integratie [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) of [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) centraal beheren en versies van uw Automation-runbook en configuratie portfolio beheren.</span><span class="sxs-lookup"><span data-stu-id="0e6af-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  