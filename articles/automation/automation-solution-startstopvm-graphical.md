---
title: aaaStarting en stoppen virtuele machines - grafiek | Microsoft Docs
description: PowerShell Workflow-versie van Azure Automation-scenario met inbegrip van runbooks toostart en stop klassieke virtuele machines.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure Automation-scenario: starten en stoppen van virtuele machines
Dit scenario Azure Automation omvat runbooks toostart en stop klassieke virtuele machines.  U kunt dit scenario voor een van de volgende hello gebruiken:  

* Hallo runbooks zonder aanpassingen gebruiken in uw eigen omgeving.
* Hallo runbooks tooperform aangepast functionaliteit wijzigen.  
* Hallo runbooks aanroepen vanuit een ander runbook als onderdeel van een algemene oplossing.
* Hallo runbooks gebruiken als zelfstudies toolearn runbook authoring concepten.

> [!div class="op_single_selector"]
> * [Grafisch](automation-solution-startstopvm-graphical.md)
> * [PowerShell-werkstroom](automation-solution-startstopvm-psworkflow.md)
>
>

Dit is Hallo grafisch runbookversie van dit scenario. Het is ook beschikbaar via [PowerShell Workflow-runbooks](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-hello-scenario"></a>Hallo scenario ophalen
Dit scenario bestaat uit twee twee grafische runbooks die u van downloaden kunt Hallo volgende koppelingen.  Zie Hallo [PowerShell Workflow-versie](automation-solution-startstopvm-psworkflow.md) van dit scenario voor koppelingen toohello PowerShell Workflow-runbooks.

| Runbook | Koppeling | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Azure Classic VM grafisch Runbook starten](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafische |Alle klassieke virtuele machines start in een Azure-abonnement of alle virtuele machines met de naam van een bepaalde service. |
| StopAzureClassicVM |[Azure Classic VM grafisch Runbook stoppen](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafische |Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt. |

## <a name="installing-and-configuring-hello-scenario"></a>Installeren en configureren van Hallo-scenario
### <a name="1-install-hello-runbooks"></a>1. Hallo runbooks installeren
Na het downloaden van Hallo runbooks, kunt u deze importeren met behulp van de procedure Hallo in [grafisch runbook procedures](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-hello-description-and-requirements"></a>2. Bekijk Hallo beschrijving en vereisten
Hallo runbooks bevatten een activiteit aangeroepen **Leesmij** die bevat een beschrijving en de vereiste activa.  U kunt deze informatie weergeven door Hallo **Leesmij** activiteit en klik vervolgens op Hallo **Werkstroomscript** parameter.  U kunt ook ophalen Hallo dezelfde informatie uit dit artikel.

### <a name="3-configure-assets"></a>3. Activa configureren
Hallo runbooks vereisen Hallo assets die u moet maken en vullen met de juiste waarden te volgen.  Hallo-namen zijn standaard.  U kunt activa met verschillende namen gebruiken als u deze namen in Hallo opgeeft [invoerparameters](#using-the-runbooks) wanneer u Hallo runbook start.

| Activatype | De naam van standaard | Beschrijving |
|:--- |:--- |:--- |:--- |
| [Referentie](automation-credentials.md) |AzureCredential |Bevat de referenties voor een account met autoriteit toostart stop de virtuele machines en in hello Azure-abonnement. |
| [Variabele](automation-variables.md) |AzureSubscriptionId |Hallo abonnements-ID van uw Azure-abonnement bevat. |

## <a name="using-hello-scenario"></a>Met behulp van Hallo scenario
### <a name="parameters"></a>Parameters
Hallo runbooks elke hebben de volgende Hallo [invoerparameters](automation-starting-a-runbook.md#runbook-parameters).  U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.

| Parameter | Type | Verplicht | Beschrijving |
|:--- |:--- |:--- |:--- |
| Servicenaam |Tekenreeks |Nee |Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.  Als geen waarde is opgegeven, worden alle klassieke virtuele machines in Azure-abonnement Hallo de gestart of gestopt. |
| AzureSubscriptionIdAssetName |Tekenreeks |Nee |Hallo naam bevat van Hallo [variabelenactivum](#installing-and-configuring-the-scenario) die Hallo abonnements-ID van uw Azure-abonnement bevat.  Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt. |
| AzureCredentialAssetName |Tekenreeks |Nee |Hallo naam bevat van Hallo [referentieasset](#installing-and-configuring-the-scenario) die Hallo referenties voor Hallo runbook toouse bevat.  Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt. |

### <a name="starting-hello-runbooks"></a>Hallo runbooks starten
U kunt een van de methoden Hallo in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) toostart ofwel Hallo runbooks in dit artikel.

Hallo volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell toorun **StartAzureClassicVM** toostart alle virtuele machines met de naam van de service Hallo *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Uitvoer
Hallo runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of start Hallo of stop-instructie is ingediend.  U kunt zoeken naar een specifieke tekenreeks in Hallo toodetermine hello uitvoerresultaat voor elk runbook.  Hallo eventuele uitvoertekenreeksen worden vermeld in de volgende tabel Hallo.

| Runbook | Voorwaarde | Bericht |
|:--- |:--- |:--- |
| StartAzureClassicVM |Virtuele machine wordt al uitgevoerd. |MyVM wordt al uitgevoerd. |
| StartAzureClassicVM |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| StartAzureClassicVM |De startaanvraag voor de virtuele machine is mislukt |MyVM toostart is mislukt |
| StopAzureClassicVM |Virtuele machine wordt al uitgevoerd. |MyVM is al gestopt. |
| StopAzureClassicVM |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| StopAzureClassicVM |De startaanvraag voor de virtuele machine is mislukt |MyVM toostart is mislukt |

Hieronder vindt u een installatiekopie van het gebruik van Hallo **StartAzureClassicVM** als een [onderliggend runbook](automation-child-runbooks.md) in een grafische voorbeeldrunbook.  Dit maakt gebruik van Hallo voorwaardelijke koppelingen in de volgende tabel Hallo.

| Koppeling | Criteria |
|:--- |:--- |
| Geslaagd-koppeling |$ActivityOutput [StartAzureClassicVM]-zoals '\* is gestart ' |
| Fout-koppeling |$ActivityOutput [StartAzureClassicVM]-notlike '\* is gestart ' |

![Voorbeeld van onderliggende runbook](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>In detail
Hier volgt een gedetailleerd overzicht van Hallo runbooks in dit scenario.  U kunt deze informatie gebruiken tooeither hello runbooks of alleen toolearn daarvan voor het ontwerpen van uw eigen automatiseringsscenario's aanpassen.

### <a name="authentication"></a>Authentication
![Authentication](media/automation-solution-startstopvm/graphical-authentication.png)

Hallo runbook start met activiteiten tooset hello [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van de runbook Hallo Hallo.

Hallo eerst twee activiteiten **abonnements-Id ophalen** en **Azure-referenties ophalen**, Hallo ophalen [activa](#installing-the-runbook) die door de volgende twee activiteiten hello worden gebruikt.  Deze activiteiten kunnen rechtstreeks Hallo activa opgeven, maar ze Hallo elementnamen nodig.  Aangezien we bieden de mogelijkheid Hallo gebruiker toospecify deze namen in Hallo [invoerparameters](#using-the-runbooks), moeten we deze activiteiten tooretrieve Hallo activa met een naam die is opgegeven door een invoerparameter.

**-AzureAccount** sets referenties die worden gebruikt voor de rest van de runbook Hallo HALLO hallo.  Hallo-referentieasset opgehaald uit **ophalen Azure referentie** toegang toostart stop de virtuele machines en moet hebben in hello Azure-abonnement.  Hallo abonnement dat wordt gebruikt is geselecteerd door **Select-AzureSubscription** waarin Hallo abonnements-Id van **abonnements-Id ophalen**.

### <a name="get-virtual-machines"></a>Virtuele machines ophalen
![Virtuele machines ophalen](media/automation-solution-startstopvm/graphical-getvms.png)

Hallo runbook moet toodetermine welke virtuele machines deze met werkt en of ze zijn al is gestart of (afhankelijk van de runbook Hallo gestopt).   Een van twee activiteiten worden Hallo VM's opgehaald.  **Ophalen van virtuele machines in de Service** wordt uitgevoerd als hello *ServiceName* invoerparameter voor Hallo runbook bevat een waarde.  **Ophalen van alle VM's** wordt uitgevoerd als hello *ServiceName* invoerparameter voor Hallo runbook bevat geen waarde.  Deze logica wordt uitgevoerd door Hallo voorwaardelijke koppelingen voorafgaand aan elke activiteit.

Beide activiteiten gebruik Hallo **Get-AzureVM** cmdlet.  **Ophalen van alle VM's** gebruikt Hallo **ListAllVMs** parameter ingesteld tooreturn alle virtuele machines.  **Ophalen van virtuele machines in de Service** gebruikt Hallo **GetVMByServiceAndVMName** parameter ingesteld en biedt Hallo **ServiceName** invoerparameter voor Hallo **ServiceName**parameter.  

### <a name="merge-vms"></a>Virtuele machines samenvoegen
![Virtuele machines samenvoegen](media/automation-solution-startstopvm/graphical-mergevms.png)

Hallo **samenvoegen VMs** activiteit is vereist tooprovide invoer te**Start-AzureVM** moeten Hallo en servicenaam van Hallo VM('s) toostart.  Dat invoer afkomstig van een zijn kan **alle VM's ophalen** of **virtuele machines ophalen in Service**, maar **Start-AzureVM** kunt slechts één activiteit voor de invoer opgeven.   

Hallo-scenario is toocreate **samenvoegen VMs** die wordt uitgevoerd Hallo **Write-Output** cmdlet.  Hallo **InputObject** parameter voor deze cmdlet is een PowerShell-expressie die Hallo invoer van de vorige twee Hallo activiteiten combineert.  Slechts één van deze activiteiten worden uitgevoerd, zodat alleen een reeks uitvoer wordt verwacht.  **Start-AzureVM** die uitvoer kunt gebruiken voor de invoerparameters.

### <a name="startstop-virtual-machines"></a>Virtuele machines starten/stoppen
![Virtuele machines starten](media/automation-solution-startstopvm/graphical-startvm.png) ![Virtuele machines stoppen](media/automation-solution-startstopvm/graphical-stopvm.png)

Afhankelijk van het Hallo-runbook Hallo volgende activiteiten toostart proberen of stoppen Hallo runbook met **Start-AzureVM** of **Stop-AzureVM**.  Aangezien Hallo activiteit voorafgegaan door een pipeline-koppeling, wordt het eenmaal uitvoeren voor elk object dat wordt geretourneerd door **samenvoegen VMs**.  Hallo koppeling is voorwaardelijke zodat Hallo activiteit wordt alleen uitgevoerd als hello *RunningState* Hallo virtuele machine is *gestopt* voor **Start-AzureVM** en  *Gestart* voor **Stop-AzureVM**. Als dit probleem niet wordt voldaan, klikt u vervolgens **gestart melden al** of **melden al gestopt** toosend voert u een bericht met **Write-Output**.

### <a name="send-output"></a>Verzenden van uitvoer
![Melding van virtuele machines starten](media/automation-solution-startstopvm/graphical-notifystart.png) ![Melding van virtuele machines stoppen](media/automation-solution-startstopvm/graphical-notifystop.png)

Hallo laatste stap bij het Hallo-runbook is toosend uitvoer Hallo of start of aanvraag tot stoppen voor elke virtuele machine is ingediend. Er is een afzonderlijke **Write-Output** activiteit voor elk, en we bepalen welke één toorun met voorwaardelijke koppelingen.  **VM gestart melden** of **melden VM gestopt** wordt uitgevoerd als *OperationStatus* is *geslaagd*.  Als *OperationStatus* is een andere waarde dan **mislukt melden tooStart** of **tooStop mislukt melden** wordt uitgevoerd.

## <a name="next-steps"></a>Volgende stappen
* [Grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* [Onderliggende runbooks in Azure Automation](automation-child-runbooks.md)
* [Runbookuitvoer en -berichten in Azure Automation](automation-runbook-output-and-messages.md)
