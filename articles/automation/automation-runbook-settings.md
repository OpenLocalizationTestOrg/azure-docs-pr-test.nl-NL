---
title: aaaRunbook instellingen | Microsoft Docs
description: Beschrijft Hallo configuratie-instellingen voor een runbook in Azure Automation en hoe ze met zowel Azure-beheerportal en Windows PowerShell Hallo toochange.
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Runbook-instellingen
Elk runbook in Azure Automation heeft meerdere instellingen waarmee het toobe geïdentificeerd en toochange de logboekregistratie kan. Elk van deze instellingen wordt hieronder beschreven en gevolgd door procedures voor het toomodify ze.

## <a name="settings"></a>Instellingen
### <a name="name-and-description"></a>Naam en beschrijving
U kunt Hallo-naam van een runbook niet wijzigen nadat deze is gemaakt. Hallo beschrijving is optioneel en kan up too512 tekens.

### <a name="tags"></a>Tags
Labels kunt dat u tooassign verschillende woorden en woordgroepen toohelp identificatie van een runbook. Bijvoorbeeld, wanneer het indienen van een runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), u bepaalde labels tooidentify welke categorieën Hallo runbook zou moeten worden vermeld opgeven. U kunt meerdere labels voor een runbook opgeven door deze te scheiden met komma's.

### <a name="logging"></a>Logboekregistratie
Standaard worden uitgebreid en voortgang van de records niet toojob geschiedenis geschreven. U kunt instellingen voor een bepaald runbook toolog Hallo deze records te wijzigen. Zie voor meer informatie over deze records [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md).

## <a name="changing-runbook-settings"></a>Runbookinstellingen

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>Runbookinstellingen met hello Azure-portal
U kunt instellingen voor een runbook in hello Azure-portal wijzigen via Hallo **instellingen** blade voor Hallo runbook.

1. Selecteer in de Azure-portal hello, **Automation** en klik vervolgens op Hallo-naam van een automation-account.
2. Selecteer Hallo **Runbooks** tabblad.
3. Klik op de naam van een runbook hello en u de instellingenblade gerichte toohello voor Hallo runbook. Hier kunt u opgeven of labels wijzigen, Hallo runbook beschrijving, logboekregistratie en tracering instellingen configureren en toegang tot support tools toohelp oplossen van problemen.     

### <a name="changing-runbook-settings-with-windows-powershell"></a>Runbookinstellingen met Windows PowerShell
U kunt Hallo [Set AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange Hallo-instellingen voor een runbook. Als u meerdere labels toospecify wilt, kunt u ofwel een matrix of een tekenreeks met door komma's gescheiden waarden toohello labels parameter opgeven. Kun je huidige labels Hallo Hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).

Hallo volgende voorbeeldopdrachten laten zien hoe tooset Hallo eigenschappen voor een runbook. Dit voorbeeld voegt drie tags toohello bestaande tags en geeft aan dat uitgebreide records moeten worden vastgelegd.

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>Volgende stappen
* hoe toocreate en ophalen uitvoer en foutberichten van runbooks, Zie toolearn [Runbookuitvoer en -berichten](automation-runbook-output-and-messages.md) 
* hoe een runbook dat is al ontwikkeld door Hallo community of andere bron- of toocreate uw eigen runbook tooadd zien toounderstand [een Runbook maken of importeren](automation-creating-importing-runbook.md) 

