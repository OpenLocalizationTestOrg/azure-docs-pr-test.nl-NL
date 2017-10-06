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
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Hoe tooupdate Azure PowerShell-modules in Azure Automation

Hallo meest voorkomende Azure PowerShell-modules zijn standaard in elk Automation-account opgegeven.  Hallo-team van Azure updates hello Azure modules regelmatig, zodat in Hallo Automation-account wij een manier voor u tooupdate Hallo modules in Hallo-account bieden wanneer nieuwe versies beschikbaar zijn vanuit de portal Hallo.  

Omdat modules regelmatig door de productgroep hello bijgewerkt worden, worden wijzigingen kunnen optreden met Hallo opgenomen-cmdlets die mogelijk negatieve invloed hebben op uw runbooks, afhankelijk van Hallo type wijziging, zoals de naam van een parameter of een cmdlet volledig bestandstypen. tooavoid die invloed hebben op uw runbooks en Hallo processen die ze automatiseren, is het raadzaam dat u testen en te voordat u doorgaat valideren.  Als u een speciale voor dit doel bestemde Automation-account niet hebt, kunt u een maken zodat u veel verschillende scenario's en permutaties tijdens het ontwikkelen van uw runbooks, in aanvulling tooiterative wijzigingen zoals het bijwerken van Hallo Hallo kunt testen PowerShell-modules.  Nadat Hallo resultaten worden gevalideerd en u vereiste wijzigingen hebt toegepast, doorgaan met het Hallo-migratie van alle runbooks die wijziging vereist coördinatie en Hallo update uitvoeren, zoals hieronder wordt beschreven in de productieomgeving.     

## <a name="updating-azure-modules"></a>Bijwerken van de Azure-Modules

1. Hallo-Modules blade van uw Automation-account er is een optie **Azure-Modules WU**.  Het is altijd ingeschakeld.<br><br> ![De optie Azure Modules in Modules blade bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Klik op **Azure-Modules WU** en u krijgt een bevestigingsbericht weergegeven waarin u wordt gevraagd als u wilt dat toocontinue.<br><br> ![Azure-Modules updatebericht](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Klik op **Ja** en begint met het updateproces Hallo-module.  Hallo updateproces neemt ongeveer 15-20 minuten tooupdate Hallo modules te volgen:

  * Azure
  * Azure.Storage
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Als het Hallo-modules zijn al toodate, wordt in een paar seconden Hallo proces voltooid.  U ontvangt een melding wanneer Hallo update is voltooid.<br><br> ![Azure-Modules updatestatus bijwerken](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Azure Automation gebruikt de meest recente modules Hallo in uw Automation-account wanneer een nieuwe geplande taak wordt uitgevoerd.    

Als u cmdlets gebruiken van deze Azure PowerShell-modules in uw runbooks toomanage Azure-resources, dan hebt u wordt aangeraden tooperform dit updateproces elke maand of dus tooassure die u hebt de meest recente modules Hallo.

## <a name="next-steps"></a>Volgende stappen

* toolearn meer informatie over integratiemodules en hoe toocreate aangepaste modules toofurther Automation integreren met andere systemen, services of oplossingen, Zie [integratiemodules](automation-integration-modules.md).

* Overweeg het gebruik van bron besturingselement integratie [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) of [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally beheren en versies van uw Automation-runbook en configuratie portfolio bepalen.  
