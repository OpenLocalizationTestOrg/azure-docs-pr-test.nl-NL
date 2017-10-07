---
title: aaaStarting en stoppen virtuele machines met een Azure Automation - PowerShell Workflow | Microsoft Docs
description: Grafische versie van Azure Automation-scenario met inbegrip van runbooks toostart en stop klassieke virtuele machines.
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
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
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

Dit is Hallo PowerShell Workflow-runbook-versie van dit scenario. Het is ook beschikbaar via [grafische runbooks](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Hallo scenario ophalen
Dit scenario bestaat uit twee PowerShell Workflow-runbooks die u kunt downloaden van Hallo koppelingen te volgen.  Zie Hallo [grafische versie](automation-solution-startstopvm-graphical.md) van dit scenario voor koppelingen toohello grafische runbooks.

| Runbook | Koppeling | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| Start AzureVMs |[Klassieke Azure-machines starten](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell-werkstroom |Start alle klassieke virtuele machines in een Azure subscriptionor alle virtuele machines met de naam van een bepaalde service. |
| Stop AzureVMs |[Stoppen van Azure Classic VM 's](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell-werkstroom |Alle virtuele machines in een automation-account of alle virtuele machines met de naam van een bepaalde service stopt. |

## <a name="installing-and-configuring-hello-scenario"></a>Installeren en configureren van Hallo-scenario
### <a name="1-install-hello-runbooks"></a>1. Hallo runbooks installeren
Na het downloaden van Hallo runbooks, kunt u deze importeren met behulp van de procedure Hallo in [importeren van een Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Bekijk Hallo beschrijving en vereisten
Hallo runbooks bevatten opmerkingen help-tekst met een beschrijving en de vereiste activa.  U kunt ook ophalen Hallo dezelfde informatie uit dit artikel.

### <a name="3-configure-assets"></a>3. Activa configureren
Hallo runbooks vereisen Hallo assets die u moet maken en vullen met de juiste waarden te volgen.

| Activatype | De Assetnaam van de | Beschrijving |
|:--- |:--- |:--- |:--- |
| Referentie |AzureCredential |Bevat de referenties voor een account met autoriteit toostart stop de virtuele machines en in hello Azure-abonnement.  U kunt ook een andere referentie-element opgeven in Hallo **referentie** parameter Hallo **Add-AzureAccount** activiteit. |
| Variabele |AzureSubscriptionId |Hallo abonnements-ID van uw Azure-abonnement bevat. |

## <a name="using-hello-scenario"></a>Met behulp van Hallo scenario
### <a name="parameters"></a>Parameters
Hallo runbooks hebben Hallo parameters te volgen.  U moet waarden opgeven voor de verplichte parameters en u kunt eventueel waarden opgeven voor de andere parameters, afhankelijk van uw vereisten.

| Parameter | Type | Verplicht | Beschrijving |
|:--- |:--- |:--- |:--- |
| Servicenaam |Tekenreeks |Nee |Als een waarde is opgegeven, worden alle virtuele machines met die servicenaam de gestart of gestopt.  Als geen waarde is opgegeven, worden alle klassieke virtuele machines in Azure-abonnement Hallo de gestart of gestopt. |
| AzureSubscriptionIdAssetName |Tekenreeks |Nee |Hallo naam bevat van Hallo [variabelenactivum](#installing-and-configuring-the-scenario) die Hallo abonnements-ID van uw Azure-abonnement bevat.  Als u een waarde niet opgeeft *AzureSubscriptionId* wordt gebruikt. |
| AzureCredentialAssetName |Tekenreeks |Nee |Hallo naam bevat van Hallo [referentieasset](#installing-and-configuring-the-scenario) die Hallo referenties voor Hallo runbook toouse bevat.  Als u een waarde niet opgeeft *AzureCredential* wordt gebruikt. |

### <a name="starting-hello-runbooks"></a>Hallo runbooks starten
U kunt een van de methoden Hallo in [een runbook starten in Azure Automation](automation-starting-a-runbook.md) toostart ofwel Hallo runbooks in dit scenario.

Hallo volgende voorbeeldopdrachten maakt gebruik van Windows PowerShell toorun **StartAzureVMs** toostart alle virtuele machines met de naam van de service Hallo *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Uitvoer
Hallo runbooks wordt [uitvoer van een bericht](automation-runbook-output-and-messages.md) voor elke virtuele machine die aangeeft of start Hallo of stop-instructie is ingediend.  U kunt zoeken naar een specifieke tekenreeks in Hallo toodetermine hello uitvoerresultaat voor elk runbook.  Hallo eventuele uitvoertekenreeksen worden vermeld in de volgende tabel Hallo.

| Runbook | Voorwaarde | Bericht |
|:--- |:--- |:--- |
| Start AzureVMs |Virtuele machine wordt al uitgevoerd. |MyVM wordt al uitgevoerd. |
| Start AzureVMs |Start-aanvraag voor de virtuele machine zijn verzonden |MyVM is gestart |
| Start AzureVMs |De startaanvraag voor de virtuele machine is mislukt |MyVM toostart is mislukt |
| Stop AzureVMs |Virtuele machine is al gestopt. |MyVM is al gestopt. |
| Stop AzureVMs |Stoppen van de aanvraag voor de virtuele machine zijn verzonden |MyVM is gestopt |
| Stop AzureVMs |Aanvraag tot stoppen voor de virtuele machine is mislukt |MyVM toostop is mislukt |

Bijvoorbeeld Hallo volgende codefragment uit een runbook probeert toostart alle virtuele machines met de naam van de service Hallo *MyServiceName*.  Als een van de Hallo aanvragen mislukken start, kunnen acties worden uitgevoerd.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>In detail
Hier volgt een gedetailleerd overzicht van Hallo runbooks in dit scenario.  U kunt deze informatie gebruiken tooeither hello runbooks of alleen toolearn daarvan voor het ontwerpen van uw eigen automatiseringsscenario's aanpassen.

### <a name="parameters"></a>Parameters
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hallo werkstroom begint met het Hallo-waarden ophalen voor Hallo [invoerparameters](#using-the-scenario).  Standaardnamen worden gebruikt als Hallo elementnamen zijn niet opgegeven.

### <a name="output"></a>Uitvoer
    # Returns strings with status messages
    [OutputType([String])]

Deze regel wordt gedeclareerd Hallo-uitvoer van Hallo runbook is een tekenreeks.  Dit is niet vereist, maar wordt aanbevolen voor wanneer Hallo runbook wordt gebruikt als een [onderliggend runbook](automation-child-runbooks.md) zodat een bovenliggend runbook Hallo uitvoer weten tooexpect typt.

### <a name="authentication"></a>Authentication
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

de volgende regels Hallo Hallo ingesteld [referenties](automation-credentials.md) en Azure-abonnement dat wordt gebruikt voor de rest van de runbook Hallo Hallo.
Eerst gebruiken we **Get-AutomationPSCredential** tooget Hallo asset die heeft Hallo-referenties met toegang tot virtuele machines toostart en stop in hello Azure-abonnement. **-AzureAccount** maakt gebruik van deze asset tooset Hallo-referenties.  Hallo-uitvoer is tooa dummy-variabele toegewezen zodat deze niet is opgenomen in Hallo runbookuitvoer.  

Hallo-variabelenactivum met Hallo abonnement-ID wordt vervolgens opgehaald met **Get-AutomationVariable** en het Hallo-abonnement in te stellen **Select-AzureSubscription**.

### <a name="get-vms"></a>Virtuele machines ophalen
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** is gebruikte tooretrieve Hallo virtuele machines Hallo runbook samenwerkt.  Als een waarde is opgegeven in Hallo **ServiceName** invoer variabele vervolgens alleen Hallo virtuele machines met die servicenaam worden opgehaald.  Als **ServiceName** is leeg, en vervolgens alle virtuele machines worden opgehaald.

### <a name="startstop-virtual-machines-and-send-output"></a>Virtuele machines starten/stoppen en uitvoer te sturen
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

de volgende regels Hallo stapsgewijs door elke virtuele machine.  Eerst Hallo **PowerState** Hallo virtuele machine is ingeschakeld toosee als deze al uitgevoerd of is gestopt, afhankelijk van het Hallo-runbook is.  Als het zich al in de doelstatus hello, klikt u vervolgens een bericht verzonden toooutput en Hallo runbook eindigt.  Als dat niet het geval is, klikt u vervolgens **Start-AzureVM** of **Stop-AzureVM** gebruikte tooattempt toostart of stop Hallo virtuele machine met Hallo resultaat van Hallo aanvraag opgeslagen tooa variabele is.  Een bericht vervolgens verzonden toooutput opgeven of Hallo aanvraag toostart of stoppen is verzonden.

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over het werken met onderliggende runbooks [onderliggende runbooks in Azure Automation](automation-child-runbooks.md)
* informatie over toolearn uitvoer berichten tijdens de uitvoering van runbook en logboekregistratie toohelp oplossen, raadpleegt u [Runbook uitvoer en berichten in Azure Automation](automation-runbook-output-and-messages.md)

