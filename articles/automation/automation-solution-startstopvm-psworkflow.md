---
title: Starten en stoppen van virtuele machines met een Azure Automation - PowerShell Workflow | Microsoft Docs
description: Grafische versie van Azure Automation-scenario met inbegrip van runbooks starten en stoppen van klassieke virtuele machines.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: FALSE
ms.openlocfilehash: 95a7b02b0d11bf18c398daea48d16e0ead30b543
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

Dit is de PowerShell Workflow-runbook-versie van dit scenario. Het is ook beschikbaar via [grafische runbooks](automation-solution-startstopvm-graphical.md).

## <a name="getting-the-scenario"></a>Het scenario ophalen
Dit scenario bestaat uit twee PowerShell Workflow-runbooks die u van de volgende koppelingen downloaden kunt.  Zie de [grafische versie](automation-solution-startstopvm-graphical.md) van dit scenario voor koppelingen naar grafische runbooks.

| Runbook | Koppeling | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Start AzureVMs |[Klassieke Azure-machines starten](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell-werkstroom |Start alle klassieke virtuele machines in een Azure subscriptionor alle virtuele machines met de naam van een bepaalde service. |
| Stop AzureVMs |[Stoppen van Azure Classic VM 's](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell-werkstroom |Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt. |

## <a name="installing-and-configuring-the-scenario"></a>Installeren en configureren van het scenario
### <a name="1-install-the-runbooks"></a>1. De runbooks installeren
Na het downloaden van de runbooks, kunt u ze met behulp van de procedure in importeren [importeren van een Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-the-description-and-requirements"></a>2. Lees de beschrijving en de vereisten
De runbooks bevatten opmerkingen help-tekst met een beschrijving en de vereiste activa.  U kunt ook dezelfde informatie opvragen uit dit artikel.

### <a name="3-configure-assets"></a>3. Activa configureren
De runbooks vereisen de volgende elementen die u moet maken en vullen met de juiste waarden.

| Activatype | De Assetnaam van de | Beschrijving |
|:--- |:--- |:--- |:--- |
| Referentie |AzureCredential |Bevat de referenties voor een account dat gemachtigd is om te starten en stoppen van virtuele machines in het Azure-abonnement.  U kunt ook kunt u een andere referentie-element in de **referentie** parameter van de **Add-AzureAccount** activiteit. |
| Variabele |AzureSubscriptionId |Bevat de abonnement-ID van uw Azure-abonnement. |

## <a name="using-the-scenario"></a>Met behulp van het scenario
### <a name="parameters"></a>Parameters
De runbooks hebben de volgende parameters.  U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.

| Parameter | Type | Verplicht | Beschrijving |
|:--- |:--- |:--- |:--- |
| Servicenaam |Tekenreeks |Nee |Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.  Als geen waarde is opgegeven, worden alle klassieke virtuele machines in het Azure-abonnement de gestart of gestopt. |
| AzureSubscriptionIdAssetName |Tekenreeks |Nee |Bevat de naam van de [variabelenactivum](#installing-and-configuring-the-scenario) die de abonnement-ID van uw Azure-abonnement bevat.  Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt. |
| AzureCredentialAssetName |Tekenreeks |Nee |Bevat de naam van de [referentieasset](#installing-and-configuring-the-scenario) die de referenties voor het runbook bevat.  Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt. |

### <a name="starting-the-runbooks"></a>Starten van de runbooks
U kunt een van de methoden in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) een van de runbooks in dit scenario te starten.

De volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell om uit te voeren **StartAzureVMs** alle virtuele machines starten met de naam van de *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Uitvoer
De runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of de instructie starten of stoppen met succes is ingediend.  U kunt zoeken naar een specifieke tekenreeks in de uitvoer van het resultaat voor elk runbook te bepalen.  De uitvoer-tekenreeksen worden in de volgende tabel vermeld.

| Runbook | Voorwaarde | Bericht |
|:--- |:--- |:--- |
| Start AzureVMs |Virtuele machine wordt al uitgevoerd. |MyVM wordt al uitgevoerd. |
| Start AzureVMs |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| Start AzureVMs |De startaanvraag voor de virtuele machine is mislukt |MyVM kan niet worden gestart |
| Stop AzureVMs |Virtuele machine is al gestopt. |MyVM is al gestopt. |
| Stop AzureVMs |Stoppen van de aanvraag voor de virtuele machine zijn verzonden |MyVM is gestopt |
| Stop AzureVMs |Aanvraag tot stoppen voor de virtuele machine is mislukt |MyVM kan niet stoppen |

Bijvoorbeeld het volgende codefragment vanuit een runbook wordt gestart van alle virtuele machines met de naam van de service *MyServiceName*.  Als een van de start-aanvragen mislukken, kunnen acties worden uitgevoerd.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action to take in case of success.
        }
        else {
            # Action to take in case of error.
        }
    }


## <a name="detailed-breakdown"></a>In detail
Hier volgt een gedetailleerd overzicht van de runbooks in dit scenario.  Deze informatie kunt u alleen wilt leren van deze voor het ontwerpen van uw eigen automatiseringsscenario's of aanpassen van de runbooks.

### <a name="parameters"></a>Parameters
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

De werkstroom wordt gestart met het ophalen van de waarden voor de [invoerparameters](#using-the-scenario).  Standaardnamen worden gebruikt als de namen van de asset niet wordt opgegeven.

### <a name="output"></a>Uitvoer
    # Returns strings with status messages
    [OutputType([String])]

Deze regel wordt aangegeven dat de uitvoer van het runbook zal een tekenreeks.  Dit is niet vereist, maar wordt aanbevolen voor wanneer het runbook wordt gebruikt als een [onderliggend runbook](automation-child-runbooks.md) zodat een bovenliggend runbook het uitvoertype weten kunnen verwachten.

### <a name="authentication"></a>Authentication
    # Connect to Azure and select the subscription to work against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

De volgende set regels de [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van het runbook.
Eerst gebruiken we **Get-AutomationPSCredential** ophalen van de activa die de referenties die toegang heeft tot het starten en stoppen van virtuele machines in het Azure-abonnement bevat. **-AzureAccount** vervolgens dit activum gebruikt de referenties in te stellen.  De uitvoer is toegewezen aan een dummy-variabele, zodat deze niet is opgenomen in de runbookuitvoer.  

De variabele asset met het abonnement-ID wordt vervolgens opgehaald met **Get-AutomationVariable** en het abonnement in te stellen **Select-AzureSubscription**.

### <a name="get-vms"></a>Virtuele machines ophalen
    # If there is a specific cloud service, then get all VMs in the service,
    # otherwise get all VMs in the subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** wordt gebruikt voor het ophalen van de virtuele machines die is voor het runbook geschikt.  Als een waarde is opgegeven de **ServiceName** variabele, invoer en vervolgens alleen de virtuele machines met die servicenaam worden opgehaald.  Als **ServiceName** is leeg, en vervolgens alle virtuele machines worden opgehaald.

### <a name="startstop-virtual-machines-and-send-output"></a>Virtuele machines starten/stoppen en uitvoer te sturen
    # Start each of the stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # The VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # The VM needs to be started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # The VM failed to start, so send notice
                Write-Output ($VM.InstanceName + " failed to start")
            }
            else
            {
                # The VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

De volgende regels stap via elke virtuele machine.  Eerste de **PowerState** van de virtuele machine wordt gecontroleerd om te zien of deze al uitgevoerd of is gestopt, afhankelijk van het runbook is.  Als het zich al in de doelstatus, is een bericht verzonden naar uitvoer en de runbook-ends.  Als dat niet het geval is, klikt u vervolgens **Start-AzureVM** of **Stop-AzureVM** wordt gebruikt om te starten of stoppen van de virtuele machine met het resultaat van de aanvraag aan een variabele opgeslagen.  Een bericht wordt dan gezonden naar uitvoer die aangeeft of de aanvraag om te starten of stoppen is verzonden.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het werken met onderliggende runbooks, [onderliggende runbooks in Azure Automation](automation-child-runbooks.md)
* Zie voor meer informatie over Uitvoerberichten tijdens de uitvoering van runbook en logboekregistratie om op te lossen, [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md)

