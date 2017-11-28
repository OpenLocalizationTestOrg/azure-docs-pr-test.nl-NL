---
title: aaaUpdate Azure modules in Azure Automation | Microsoft Docs
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
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="16bf0-103">Hoe tooupdate Azure PowerShell-modules in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="16bf0-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="16bf0-104">Hallo meest voorkomende Azure PowerShell-modules zijn standaard in elk Automation-account opgegeven.</span><span class="sxs-lookup"><span data-stu-id="16bf0-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="16bf0-105">Hallo-team van Azure updates hello Azure modules regelmatig, zodat in Hallo Automation-account wij een manier voor u tooupdate Hallo modules in Hallo-account bieden wanneer nieuwe versies beschikbaar zijn vanuit de portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="16bf0-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="16bf0-106">Omdat modules regelmatig door de productgroep hello bijgewerkt worden, worden wijzigingen kunnen optreden met Hallo opgenomen-cmdlets die mogelijk negatieve invloed hebben op uw runbooks, afhankelijk van Hallo type wijziging, zoals de naam van een parameter of een cmdlet volledig bestandstypen.</span><span class="sxs-lookup"><span data-stu-id="16bf0-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="16bf0-107">tooavoid die invloed hebben op uw runbooks en Hallo processen die ze automatiseren, is het raadzaam dat u testen en te voordat u doorgaat valideren.</span><span class="sxs-lookup"><span data-stu-id="16bf0-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="16bf0-108">Als u een speciale voor dit doel bestemde Automation-account niet hebt, kunt u een maken zodat u veel verschillende scenario's en permutaties tijdens het ontwikkelen van uw runbooks, in aanvulling tooiterative wijzigingen zoals het bijwerken van Hallo Hallo kunt testen PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="16bf0-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="16bf0-109">Nadat Hallo resultaten worden gevalideerd en u vereiste wijzigingen hebt toegepast, doorgaan met het Hallo-migratie van alle runbooks die wijziging vereist coördinatie en Hallo update uitvoeren, zoals hieronder wordt beschreven in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="16bf0-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="16bf0-110">Bijwerken van de Azure-Modules</span><span class="sxs-lookup"><span data-stu-id="16bf0-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="16bf0-111">Hallo-Modules blade van uw Automation-account er is een optie **Azure-Modules WU**.</span><span class="sxs-lookup"><span data-stu-id="16bf0-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="16bf0-112">Het is altijd ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="16bf0-112">It is always enabled.</span></span><br><br> <span data-ttu-id="16bf0-113">![De optie Azure Modules in Modules blade bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="16bf0-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="16bf0-114">Klik op **Azure-Modules WU** en u krijgt een bevestigingsbericht weergegeven waarin u wordt gevraagd als u wilt dat toocontinue.</span><span class="sxs-lookup"><span data-stu-id="16bf0-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="16bf0-115">![Azure-Modules updatebericht](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="16bf0-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="16bf0-116">Klik op **Ja** en begint met het updateproces Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="16bf0-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="16bf0-117">Hallo updateproces neemt ongeveer 15-20 minuten tooupdate Hallo modules te volgen:</span><span class="sxs-lookup"><span data-stu-id="16bf0-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="16bf0-118">Azure</span><span class="sxs-lookup"><span data-stu-id="16bf0-118">Azure</span></span>
  * <span data-ttu-id="16bf0-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="16bf0-119">Azure.Storage</span></span>
  * <span data-ttu-id="16bf0-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="16bf0-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="16bf0-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="16bf0-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="16bf0-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="16bf0-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="16bf0-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="16bf0-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="16bf0-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="16bf0-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="16bf0-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="16bf0-125">AzureRm.Storage</span></span>

    <span data-ttu-id="16bf0-126">Als het Hallo-modules zijn al toodate, wordt in een paar seconden Hallo proces voltooid.</span><span class="sxs-lookup"><span data-stu-id="16bf0-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="16bf0-127">U ontvangt een melding wanneer Hallo update is voltooid.</span><span class="sxs-lookup"><span data-stu-id="16bf0-127">When hello update process completes you will be notified.</span></span><br><br> ![Azure-Modules updatestatus bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="16bf0-129">Azure Automation gebruikt de meest recente modules Hallo in uw Automation-account wanneer een nieuwe geplande taak wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16bf0-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="16bf0-130">Als u cmdlets gebruiken van deze Azure PowerShell-modules in uw runbooks toomanage Azure-resources, dan hebt u wordt aangeraden tooperform dit updateproces elke maand of dus tooassure die u hebt de meest recente modules Hallo.</span><span class="sxs-lookup"><span data-stu-id="16bf0-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16bf0-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16bf0-131">Next steps</span></span>

* <span data-ttu-id="16bf0-132">toolearn meer informatie over integratiemodules en hoe toocreate aangepaste modules toofurther Automation integreren met andere systemen, services of oplossingen, Zie [integratiemodules](automation-integration-modules.md).</span><span class="sxs-lookup"><span data-stu-id="16bf0-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="16bf0-133">Overweeg het gebruik van bron besturingselement integratie [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) of [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally beheren en versies van uw Automation-runbook en configuratie portfolio bepalen.</span><span class="sxs-lookup"><span data-stu-id="16bf0-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
