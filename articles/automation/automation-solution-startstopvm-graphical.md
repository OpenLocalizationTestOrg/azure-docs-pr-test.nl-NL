---
title: Starten en stoppen van virtuele machines - grafiek | Microsoft Docs
description: PowerShell Workflow-versie van Azure Automation-scenario met inbegrip van runbooks starten en stoppen van klassieke virtuele machines.
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
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure Automation-scenario: starten en stoppen van virtuele machines
Dit scenario Azure Automation bevat runbooks starten en stoppen van klassieke virtuele machines.  U kunt dit scenario kunt gebruiken voor het volgende:  

* Gebruik de runbooks zonder aanpassingen in uw eigen omgeving.
* Wijzig de runbooks voor het uitvoeren van aangepaste functionaliteit.  
* De runbooks aanroepen vanuit een ander runbook als onderdeel van een algemene oplossing.
* Gebruik de runbooks als zelfstudies voor meer informatie over runbook authoring concepten.

> [!div class="op_single_selector"]
> * [Grafisch](automation-solution-startstopvm-graphical.md)
> * [PowerShell-werkstroom](automation-solution-startstopvm-psworkflow.md)
>
>

Dit is de grafisch runbook-versie van dit scenario. Het is ook beschikbaar via [PowerShell Workflow-runbooks](automation-solution-startstopvm-psworkflow.md).

## <a name="getting-the-scenario"></a>Het scenario ophalen
Dit scenario bestaat uit twee twee grafische runbooks die u van de volgende koppelingen downloaden kunt.  Zie de [PowerShell Workflow-versie](automation-solution-startstopvm-psworkflow.md) van dit scenario voor koppelingen naar de PowerShell Workflow-runbooks.

| Runbook | Koppeling | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[Azure Classic VM grafisch Runbook starten](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |Grafische |Alle klassieke virtuele machines start in een Azure-abonnement of alle virtuele machines met de naam van een bepaalde service. |
| StopAzureClassicVM |[Azure Classic VM grafisch Runbook stoppen](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |Grafische |Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt. |

## <a name="installing-and-configuring-the-scenario"></a>Installeren en configureren van het scenario
### <a name="1-install-the-runbooks"></a>1. De runbooks installeren
Na het downloaden van de runbooks, kunt u ze met behulp van de procedure in importeren [grafisch runbook procedures](automation-graphical-authoring-intro.md#graphical-runbook-procedures).

### <a name="2-review-the-description-and-requirements"></a>2. Lees de beschrijving en de vereisten
De runbooks bevatten een activiteit aangeroepen **Leesmij** die bevat een beschrijving en de vereiste activa.  U kunt deze informatie weergeven door de **Leesmij** activiteit en vervolgens de **Werkstroomscript** parameter.  U kunt ook dezelfde informatie opvragen uit dit artikel.

### <a name="3-configure-assets"></a>3. Activa configureren
De runbooks vereisen de volgende elementen die u moet maken en vullen met de juiste waarden.  De namen zijn standaard.  U kunt activa met verschillende namen gebruiken als u deze namen in de [invoerparameters](#using-the-runbooks) wanneer u het runbook wordt gestart.

| Activatype | De naam van standaard | Beschrijving |
|:--- |:--- |:--- |:--- |
| [Referentie](automation-credentials.md) |AzureCredential |Bevat de referenties voor een account dat gemachtigd is om te starten en stoppen van virtuele machines in het Azure-abonnement. |
| [Variabele](automation-variables.md) |AzureSubscriptionId |Bevat de abonnement-ID van uw Azure-abonnement. |

## <a name="using-the-scenario"></a>Met behulp van het scenario
### <a name="parameters"></a>Parameters
De runbooks hebt de volgende [invoerparameters](automation-starting-a-runbook.md#runbook-parameters).  U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.

| Parameter | Type | Verplicht | Beschrijving |
|:--- |:--- |:--- |:--- |
| Servicenaam |Tekenreeks |Nee |Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.  Als geen waarde is opgegeven, worden alle klassieke virtuele machines in het Azure-abonnement de gestart of gestopt. |
| AzureSubscriptionIdAssetName |Tekenreeks |Nee |Bevat de naam van de [variabelenactivum](#installing-and-configuring-the-scenario) die de abonnement-ID van uw Azure-abonnement bevat.  Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt. |
| AzureCredentialAssetName |Tekenreeks |Nee |Bevat de naam van de [referentieasset](#installing-and-configuring-the-scenario) die de referenties voor het runbook bevat.  Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt. |

### <a name="starting-the-runbooks"></a>Starten van de runbooks
U kunt een van de methoden in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) een van de runbooks te starten in dit artikel.

De volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell om uit te voeren **StartAzureClassicVM** alle virtuele machines starten met de naam van de *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>Uitvoer
De runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of de instructie starten of stoppen met succes is ingediend.  U kunt zoeken naar een specifieke tekenreeks in de uitvoer van het resultaat voor elk runbook te bepalen.  De uitvoer-tekenreeksen worden in de volgende tabel vermeld.

| Runbook | Voorwaarde | Bericht |
|:--- |:--- |:--- |
| StartAzureClassicVM |Virtuele machine wordt al uitgevoerd. |MyVM wordt al uitgevoerd. |
| StartAzureClassicVM |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| StartAzureClassicVM |De startaanvraag voor de virtuele machine is mislukt |MyVM kan niet worden gestart |
| StopAzureClassicVM |Virtuele machine wordt al uitgevoerd. |MyVM is al gestopt. |
| StopAzureClassicVM |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| StopAzureClassicVM |De startaanvraag voor de virtuele machine is mislukt |MyVM kan niet worden gestart |

Hieronder vindt u een installatiekopie van het gebruik van de **StartAzureClassicVM** als een [onderliggend runbook](automation-child-runbooks.md) in een grafische voorbeeldrunbook.  Dit maakt gebruik van de voorwaardelijke koppelingen in de volgende tabel.

| Koppeling | Criteria |
|:--- |:--- |
| Geslaagd-koppeling |$ActivityOutput [StartAzureClassicVM]-zoals '\* is gestart ' |
| Fout-koppeling |$ActivityOutput [StartAzureClassicVM]-notlike '\* is gestart ' |

![Voorbeeld van onderliggende runbook](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>In detail
Hier volgt een gedetailleerd overzicht van de runbooks in dit scenario.  Deze informatie kunt u alleen wilt leren van deze voor het ontwerpen van uw eigen automatiseringsscenario's of aanpassen van de runbooks.

### <a name="authentication"></a>Authentication
![Authentication](media/automation-solution-startstopvm/graphical-authentication.png)

Het runbook begint met activiteiten in te stellen de [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van het runbook.

De eerste twee activiteiten **abonnements-Id ophalen** en **ophalen Azure referentie**, halen de [activa](#installing-the-runbook) die worden gebruikt door de volgende twee activiteiten.  Deze activiteiten kunnen rechtstreeks opgeven voor de activa, maar moeten de namen van de asset.  Aangezien we staat de gebruiker om op te geven die namen in de [invoerparameters](#using-the-runbooks), moeten we deze activiteiten voor het ophalen van de activa met een naam die is opgegeven door een invoerparameter.

**-AzureAccount** stelt de referenties die worden gebruikt voor de rest van het runbook.  De referentie-element het ophalen van **ophalen Azure referentie** moet toegang hebben tot het starten en stoppen van virtuele machines in het Azure-abonnement.  Het abonnement dat wordt gebruikt, wordt geselecteerd door **Select-AzureSubscription** waarin de abonnements-Id van **abonnements-Id ophalen**.

### <a name="get-virtual-machines"></a>Virtuele machines ophalen
![Virtuele machines ophalen](media/automation-solution-startstopvm/graphical-getvms.png)

Het runbook moet om te bepalen welke virtuele machines met werkt en of ze zijn al is gestart of (afhankelijk van het runbook gestopt).   Een van twee activiteiten van worden de virtuele machines opgehaald.  **Ophalen van virtuele machines in de Service** wordt uitgevoerd als de *ServiceName* invoerparameter voor het runbook bevat een waarde.  **Ophalen van alle VM's** wordt uitgevoerd als de *ServiceName* invoerparameter voor het runbook bevat geen waarde.  Deze logica wordt uitgevoerd door de voorwaardelijke koppelingen voorafgaand aan elke activiteit.

Beide activiteiten maken gebruik van de **Get-AzureVM** cmdlet.  **Ophalen van alle VM's** maakt gebruik van de **ListAllVMs** parameter ingesteld op het retourneren van alle virtuele machines.  **Ophalen van virtuele machines in de Service** maakt gebruik van de **GetVMByServiceAndVMName** parameter ingesteld en biedt de **ServiceName** invoerparameter voor de **ServiceName** parameter.  

### <a name="merge-vms"></a>Virtuele machines samenvoegen
![Virtuele machines samenvoegen](media/automation-solution-startstopvm/graphical-mergevms.png)

De **samenvoegen VMs** activiteit is vereist voor invoer van **Start-AzureVM** moeten de naam en de servicenaam van de VM('s) te starten.  Dat invoer afkomstig van een zijn kan **alle VM's ophalen** of **virtuele machines ophalen in Service**, maar **Start-AzureVM** kunt slechts één activiteit voor de invoer opgeven.   

Het scenario is het maken van **samenvoegen VMs** waaronder wordt uitgevoerd de **Write-Output** cmdlet.  De **InputObject** parameter voor deze cmdlet is een PowerShell-expressie die de invoer van de vorige twee activiteiten combineert.  Slechts één van deze activiteiten worden uitgevoerd, zodat alleen een reeks uitvoer wordt verwacht.  **Start-AzureVM** die uitvoer kunt gebruiken voor de invoerparameters.

### <a name="startstop-virtual-machines"></a>Virtuele machines starten/stoppen
![Virtuele machines starten](media/automation-solution-startstopvm/graphical-startvm.png) ![Virtuele machines stoppen](media/automation-solution-startstopvm/graphical-stopvm.png)

Afhankelijk van het runbook de volgende activiteiten proberen te starten of stoppen van het runbook met behulp van **Start-AzureVM** of **Stop-AzureVM**.  Omdat de activiteit wordt voorafgegaan door een pipeline-koppeling, wordt het eenmaal uitvoeren voor elk object dat wordt geretourneerd door **samenvoegen VMs**.  De koppeling is voorwaardelijke zodat de activiteit wordt alleen uitgevoerd als de *RunningState* van de virtuele machine is *gestopt* voor **Start-AzureVM** en *gestart*  voor **Stop-AzureVM**. Als dit probleem niet wordt voldaan, klikt u vervolgens **gestart melden al** of **melden al gestopt** wordt uitgevoerd om een bericht te verzenden met behulp van **Write-Output**.

### <a name="send-output"></a>Verzenden van uitvoer
![Melding van virtuele machines starten](media/automation-solution-startstopvm/graphical-notifystart.png) ![Melding van virtuele machines stoppen](media/automation-solution-startstopvm/graphical-notifystop.png)

De laatste stap in het runbook is voor het verzenden van uitvoer of voor elke virtuele machine starten of stoppen verzoek is ingediend. Er is een afzonderlijke **Write-Output** activiteit voor elk, en we bepalen welke uit te voeren met voorwaardelijke koppelingen.  **VM gestart melden** of **melden VM gestopt** wordt uitgevoerd als *OperationStatus* is *geslaagd*.  Als *OperationStatus* is een andere waarde dan **melding is mislukt om te beginnen** of **mislukt melden in stoppen** wordt uitgevoerd.

## <a name="next-steps"></a>Volgende stappen
* [Grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md)
* [Onderliggende runbooks in Azure Automation](automation-child-runbooks.md)
* [Runbookuitvoer en -berichten in Azure Automation](automation-runbook-output-and-messages.md)
