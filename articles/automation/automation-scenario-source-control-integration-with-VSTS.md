---
title: Azure Automation aaaIntegrate met broncodebeheer Visual Stuido Team Services | Microsoft Docs
description: Scenario begeleidt u bij het instellen van integratie met een Azure Automation-account en de bronbeheer Visual Stuido Team Services.
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: Azure powershell, VSTS, bronbeheer, automation
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a>Azure Automation-scenario - integratie van broncodebeheer automatisering met Visual Studio Team Services

In dit scenario hebt u een Visual Studio Team Services-project dat u van Azure Automation-runbooks toomanage of DSC-configuraties onder bronbeheer gebruikmaakt.
Dit artikel wordt beschreven hoe toointegrate VSTS met uw Azure Automation-omgeving zodanig dat continue integratie gebeurt voor elke controle in.

## <a name="getting-hello-scenario"></a>Hallo scenario ophalen

Dit scenario bestaat uit twee PowerShell-runbooks die u rechtstreeks vanuit Hallo importeren kunt [Runbookgalerie](automation-runbook-gallery.md) in hello Azure-portal of downloaden van Hallo [PowerShell Gallery](https://www.powershellgallery.com).

### <a name="runbooks"></a>Runbooks

Runbook | Beschrijving| 
--------|------------|
Synchronisatie-VSTS | Importeren runbooks of configuraties van broncodebeheer VSTS als een check-in is voltooid. Als u handmatig uitvoert, wordt de importeren en publiceren van alle runbooks of -configuraties in Hallo Automation-account.| 
Synchronisatie VSTSGit | Runbooks of configuraties uit importeren VSTS onder bronbeheer Git als een check-in is voltooid. Als u handmatig uitvoert, wordt de importeren en publiceren van alle runbooks of -configuraties in Hallo Automation-account.|

### <a name="variables"></a>Variabelen

Variabele | Beschrijving|
-----------|------------|
VSToken | Beveiligde variabelenactivum maakt u met de Hallo VSTS persoonlijke toegangstoken. U leert hoe toocreate een VSTS persoonlijke toegang krijgen tot token op Hallo [VSTS verificatiepagina](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview). 
## <a name="installing-and-configuring-this-scenario"></a>Dit scenario installeren en configureren

Maak een [persoonlijke toegangstoken](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS die u toosync hello runbooks of -configuraties in uw automation-account gebruikt.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

Maak een [beveiligde variabele](automation-variables.md) in uw automation-account toohold Hallo personal access token zodat Hallo runbook tooVSTS en sync Hallo runbooks of -configuraties in Hallo Automation-account kan worden geverifieerd. U kunt deze VSToken naam. 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

Runbook importeren Hallo uw runbooks of -configuraties in Hallo automation-account moeten worden gesynchroniseerd. Kunt u Hallo [VSTS voorbeeldrunbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) of Hallo [VSTS met Git voorbeeldrunbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) vanuit Hallo PowerShellGallery.com afhankelijk van of u VSTS gebruiken Source control of VSTS met Git en implementeren van tooyour automation-account.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

U kunt nu [publiceren](automation-creating-importing-runbook.md#publishing-a-runbook) dit runbook zodat u kunt een webhook maken. 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

Maak een [webhook](automation-webhooks.md) voor deze runbook-synchronisatie VSTS en vul Hallo parameters zoals hieronder wordt weergegeven. Zorg ervoor dat u Hallo webhook-url kopiëren als u deze nodig voor een service haakje in VSTS. Hallo VSAccessTokenVariableName is Hallo-naam (VSToken) van beveiligde Hallo-variabele die u eerder toohold Hallo persoonlijke toegangstoken gemaakt. 

Integratie met VSTS (Sync-VSTS.ps1), duurt Hallo parameters te volgen.
### <a name="sync-vsts-parameters"></a>Synchronisatie-VSTS Parameters

Parameter | Beschrijving| 
--------|------------|
WebhookData | Dit bevat Hallo inchecken informatie verzonden van Hallo VSTS service haakje. U moet deze parameter leeg laten.| 
ResourceGroup | Dit is de naam Hallo van resourcegroep Hallo die Hallo automation-account in.|
AutomationAccountName | Hallo-naam van Hallo automation-account met VSTS moeten worden gesynchroniseerd.|
VSFolder | De naam van de map Hallo in VSTS waar Hallo runbooks en configuraties bestaan.|
VSAccount | de naam van de Hallo Hallo Visual Studio Team Services-account.| 
VSAccessTokenVariableName | Hallo naam van Hallo beveiligde variabele (VSToken) die Hallo VSTS persoonlijke toegangstoken bevat.| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

Als u van VSTS met GIT (Sync-VSTSGit.ps1 gebruikmaakt) wordt uitgevoerd, Hallo parameters te volgen.

Parameter | Beschrijving|
--------|------------|
WebhookData | Dit bevat Hallo inchecken informatie verzonden van Hallo VSTS service haakje. U moet deze parameter leeg laten.| ResourceGroup | Deze naam Hallo van resourcegroep Hallo die Hallo automation-account in.|
AutomationAccountName | Hallo-naam van Hallo automation-account met VSTS moeten worden gesynchroniseerd.|
VSAccount | de naam van de Hallo Hallo Visual Studio Team Services-account.|
VSProject | Hallo-naam van Hallo-project in VSTS waar Hallo runbooks en configuraties bestaan.|
GitRepo | Hallo-naam van Hallo Git-opslagplaats.|
GitBranch | Hallo-naam van de vertakking Hallo in VSTS Git-opslagplaats.|
Map | Hallo-naam van Hallo-map in VSTS Git vertakking.|
VSAccessTokenVariableName | Hallo naam van Hallo beveiligde variabele (VSToken) die Hallo VSTS persoonlijke toegangstoken bevat.|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

Maak een haakje service in VSTS voor controle-modules toohello map waarmee deze webhook bij code controle wordt geactiveerd. Selecteer Web Hiermee als Hallo service toointegrate met wanneer u een nieuw abonnement maakt. Voor meer informatie over service hooks op [VSTS Service Hooks documentatie](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

U zou nu kunnen toodo alle controle-modules van uw runbooks en de configuraties in VSTS zijn en deze automatisch gesynchroniseerd was in uw automation-account.

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

Als u dit runbook handmatig uitvoert zonder wordt geactiveerd door VSTS, kunt u Hallo webhookdata parameter leeg laten en doet een volledige synchronisatie van Hallo VSTS map die is opgegeven.

Als u wenst toouninstall Hallo scenario, Hallo service haakje verwijderen uit VSTS, Hallo runbook en Hallo VSToken variabele verwijderen.
