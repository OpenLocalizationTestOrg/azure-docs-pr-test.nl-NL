---
title: een Azure Automation-runbook met een webhook aaaStarting | Microsoft Docs
description: "Een webhook waarmee een client toostart een runbook in Azure Automation van een HTTP-aanroep.  Dit artikel wordt beschreven hoe een webhook toocreate en hoe toocall één toostart een runbook."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9b20237c-a593-4299-bbdc-35c47ee9e55d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: ca6cde66b3784ceb5d0bc5921cee87aea74cb150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="starting-an-azure-automation-runbook-with-a-webhook"></a>Een Azure Automation-runbook beginnen met een webhook
Een *webhook* kunt u een bepaald runbook toostart in Azure Automation via één HTTP-aanvraag. Hierdoor kan externe services, zoals Visual Studio Team Services, GitHub, logboekanalyse van Microsoft Operations Management Suite of aangepaste toepassingen toostart runbooks zonder het implementeren van een volledige oplossing met behulp van hello Azure Automation-API.  
![WebhooksOverview](media/automation-webhooks/webhook-overview-image.png)

U kunt vergelijken met webhooks tooother methoden van een runbook starten [een runbook starten in Azure Automation](automation-starting-a-runbook.md)

## <a name="details-of-a-webhook"></a>Details van een webhook
Hallo beschrijft volgende tabel Hallo-eigenschappen die u voor een webhook configureren moet.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Naam |U kunt opgeven dat elke gewenste naam voor een webhook aangezien dit toohello-client niet weergegeven.  Het wordt alleen gebruikt voor u tooidentify hello runbook in Azure Automation. <br>  Als een best practice moet u Hallo webhook geeft een naam gerelateerde toohello-client die wordt gebruikt. |
| URL |Hallo-URL van de webhook Hallo is Hallo uniek adres dat een client met een HTTP POST toostart hello runbook aanroept toohello webhook gekoppeld.  Bij het maken van de webhook hello wordt automatisch gegenereerd.  U kunt een aangepaste URL niet opgeven. <br> <br>  Hallo-URL bevat een beveiligingstoken waarmee Hallo runbook toobe aangeroepen door een systeem van derden met geen verdere authenticatie. Daarom moet het worden behandeld als een wachtwoord.  Uit veiligheidsoverwegingen kunt u alleen weergave Hallo-URL in hello Azure-portal op Hallo tijd Hallo webhook is gemaakt. Houd er rekening mee Hallo-URL op een veilige locatie voor toekomstig gebruik. |
| Vervaldatum |Zoals een certificaat heeft elke webhook een vervaldatum op dat moment kan niet meer worden gebruikt.  Deze vervaldatum kan worden gewijzigd nadat Hallo webhook is gemaakt. |
| Ingeschakeld |Een webhook is standaard ingeschakeld wanneer deze wordt gemaakt.  Als u deze tooDisabled hebt ingesteld, wordt geen client kunnen toouse deze.  U kunt instellen Hallo **ingeschakeld** eigenschap bij het maken van Hallo webhook of op elk gewenst moment eenmaal is gemaakt. |

### <a name="parameters"></a>Parameters
Een webhook kunt waarden voor runbookparameters die worden gebruikt als Hallo runbook wordt gestart door die webhook definiëren. Hallo webhook waarden voor de verplichte parameters van Hallo runbook moet bevatten en waarden voor de volgende optionele parameters kan bevatten. Een parameter die is geconfigureerd tooa webhook kan zelfs na het maken van Hallo webhoook worden gewijzigd. Meerdere webhooks gekoppeld tooa één runbook kunt elke andere parameterwaarden gebruiken.

Wanneer een client wordt gestart van een runbook met behulp van een webhook, kan het Hallo-parameterwaarden die is gedefinieerd in Hallo webhook niet overschrijven.  tooreceive gegevens van de client hello, Hallo runbook kan aangeroepen één parameter accepteren **$WebhookData** van het type [object] die gegevens bevat die client Hallo in Hallo POST-aanvraag bevat.

![Webhookdata-eigenschappen](media/automation-webhooks/webhook-data-properties.png)

Hallo **$WebhookData** object Hallo volgende eigenschappen hebben:

| Eigenschap | Beschrijving |
|:--- |:--- |
| WebhookName |Hallo-naam van de webhook Hallo. |
| RequestHeader |Hash-tabel met Hallo-kopteksten van Hallo binnenkomende POST-aanvraag. |
| requestBody |Hallo-hoofdtekst van Hallo binnenkomende POST-aanvraag.  Hiermee behoudt alle opmaak zoals tekenreeks, JSON, XML, of formulier gecodeerde gegevens. Hallo runbook moet worden geschreven als toowork met Hallo gegevensindeling die wordt verwacht. |

Er is geen configuratie van Hallo webhook vereist toosupport hello **$WebhookData** parameter, en Hallo runbook is niet vereist tooaccept deze.  Als Hallo runbook geen Hallo parameter gedefinieerd, wordt er details van Hallo-aanvraag is verzonden vanaf de client Hallo genegeerd.

Als u een waarde voor $WebhookData opgeven bij het maken van de webhook hello, wordt die waarde worden onderdrukt wanneer Hallo webhook hello runbook met Hallo gegevens van Hallo client POST-aanvraag Start, zelfs als het Hallo-client geen gegevens in de aanvraagtekst Hallo bevatten.  Als u een runbook met een andere methode dan een webhook met $WebhookData start, kunt u een waarde opgeven voor $Webhookdata die wordt herkend door Hallo runbook.  Deze waarde moet een object met Hallo dezelfde [eigenschappen](#details-of-a-webhook) als $Webhookdata zodat dat runbook Hallo goed ermee werken kunt alsof het was in combinatie met de werkelijke WebhookData doorgegeven door een webhook.

Bijvoorbeeld, als u begint Hallo na het runbook uit hello Azure-Portal en toopass sommige WebhookData voorbeeld voor het testen, aangezien WebhookData een object is wilt, moet deze worden doorgegeven als JSON in Hallo gebruikersinterface.

![De parameter WebhookData door de gebruikersinterface](media/automation-webhooks/WebhookData-parameter-from-UI.png)

Voor Hallo hierboven runbook, als u de volgende eigenschappen voor de parameter WebhookData Hallo Hallo hebt:

1. WebhookName: *MyWebhook*
2. RequestHeader: *van de testgebruiker =*
3. RequestBody: *['VM1', 'VM2']*

U zou vervolgens Hallo volgende JSON-waarde in Hallo UI voor Hallo WebhookData parameter doorgeven:  

* {'WebhookName': 'MyWebhook', "RequestHeader": {'Van': 'Test gebruiker'}, "RequestBody": "[\"VM1\",\"VM2\"]"}

![Parameter WebhookData starten door de gebruikersinterface](media/automation-webhooks/Start-WebhookData-parameter-from-UI.png)

> [!NOTE]
> Hallo-waarden van alle invoerparameters worden geregistreerd met de runbooktaak Hallo.  Dit betekent dat een invoer zoals opgegeven door de client Hallo Hallo webhook aanvraag worden vastgelegd en beschikbaar tooanyone met toegang toohello automation-taak.  Daarom moet u voorzichtig met gevoelige informatie in de webhook aanroepen.
>

## <a name="security"></a>Beveiliging
Hallo beveiliging van een webhook is afhankelijk van Hallo privacy van de URL die bevat een beveiligingstoken waarmee dit toobe aangeroepen. Azure Automation biedt verificatie niet uitvoeren op aanvraag hello, zolang de juiste URL toohello wordt gemaakt. Om deze reden moet webhooks niet worden gebruikt voor runbooks die uiterst gevoelige functies uitvoeren zonder gebruik van een alternatieve methode Hallo-aanvraag wordt gevalideerd.

U kunt opnemen logica binnen Hallo runbook toodetermine dat deze door een webhook is aangeroepen door het controleren van Hallo **WebhookName** eigenschap van Hallo $WebhookData-parameter. Hallo-runbook kan verder validatie uitvoeren door te zoeken naar specifieke informatie in Hallo **RequestHeader** of **RequestBody** eigenschappen.

Een andere strategie die is toohave hello runbook validatie van een externe voorwaarde uitvoeren wanneer het een webhook-aanvraag ontvangen.  Neem bijvoorbeeld een runbook dat wordt aangeroepen door GitHub wanneer er een nieuwe doorvoeren tooa GitHub-opslagplaats.  Hallo runbook mogelijk verbinding tooGitHub toovalidate die eigenlijk gewoon een nieuwe doorvoer voordat u doorgaat opgetreden.

## <a name="creating-a-webhook"></a>Maken van een webhook
Hallo te volgen procedure toocreate een nieuw webhook gekoppeld tooa runbook in hello Azure-portal gebruiken.

1. Van Hallo **Runbooks blade** in hello Azure-portal, klikt u op Hallo runbook dat webhook Hallo gaat tooview de blade met details.
2. Klik op **Webhook** bovenaan Hallo Hallo blade tooopen hello **Webhook toevoegen** blade. <br>
   ![Knop webhooks.](media/automation-webhooks/webhooks-button.png)
3. Klik op **maken van nieuwe webhook** tooopen hello **webhook-blade maken**.
4. Geef een **naam**, **vervaldatum** voor Hallo webhook en Hiermee wordt aangegeven of moet worden ingeschakeld. Zie [Details van een webhook](#details-of-a-webhook) voor meer informatie deze eigenschappen.
5. Klik op de pictogram kopiëren Hallo en druk op Ctrl + C toocopy Hallo-URL van de webhook Hallo.  Noteer de op een veilige plaats.  **Als u Hallo webhook gemaakt, kan u Hallo URL opnieuw niet ophalen.** <br>
   ![Webhook-URL](media/automation-webhooks/copy-webhook-url.png)
6. Klik op **Parameters** tooprovide waarden voor de runbookparameters Hallo.  Als Hallo runbook verplichte parameters heeft, klikt u vervolgens zich u niet kunnen toocreate hello webhook tenzij waarden zijn opgegeven.
7. Klik op **maken** toocreate hello webhook.

## <a name="using-a-webhook"></a>Met behulp van een webhook
toouse een webhook nadat deze is gemaakt, de clienttoepassing moet een HTTP POST met Hallo-URL voor Hallo webhook verlenen.  Hallo syntaxis van de webhook Hallo zal Hallo na indeling zijn.

    http://<Webhook Server>/token?=<Token Value>

Hallo client ontvangt een Hallo volgende retourcodes uit Hallo POST-aanvraag.  

| Code | Tekst | Beschrijving |
|:--- |:--- |:--- |
| 202 |Geaccepteerd |Hallo-aanvraag is geaccepteerd en Hallo runbook is in de wachtrij geplaatst. |
| 400 |Onjuiste aanvraag |Hallo-aanvraag is niet geaccepteerd voor een van de volgende redenen Hallo. <ul> <li>Hallo webhook is verlopen.</li> <li>Hallo webhook is uitgeschakeld.</li> <li>Hallo-token in Hallo-URL is ongeldig.</li>  </ul> |
| 404 |Niet gevonden |Hallo-aanvraag is niet geaccepteerd voor een van de volgende redenen Hallo. <ul> <li>Hallo webhook is niet gevonden.</li> <li>Hallo runbook is niet gevonden.</li> <li>Hallo-account is niet gevonden.</li>  </ul> |
| 500 |Interne serverfout |Hallo-URL is geldig, maar er is een fout opgetreden.  Verzend Hallo-aanvraag. |

Ervan uitgaande dat Hallo-aanvraag is gelukt, bevat antwoord van de webhook Hallo Hallo taak-id in JSON-indeling als volgt. Bevat een enkele taak-id, maar Hallo JSON-indeling kunt u mogelijke toekomstige verbeteringen.

    {"JobIds":["<JobId>"]}  

Hallo-client kan niet bepalen wanneer Hallo runbooktaak is voltooid of de eindstatus van Hallo webhook.  Dit kan bepalen dat deze informatie met taak-id Hallo met een andere methode, zoals [Windows PowerShell](http://msdn.microsoft.com/library/azure/dn690263.aspx) of Hallo [Azure Automation-API](https://msdn.microsoft.com/library/azure/mt163826.aspx).

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld maakt gebruik van Windows PowerShell toostart een runbook met een webhook.  Houd er rekening mee dat elke taal die u van een HTTP-aanvraag maken kunt een webhook; kunt gebruiken Windows PowerShell wordt alleen gebruikt als voorbeeld hier.

Hallo runbook is een lijst met virtuele machines die zijn opgemaakt in JSON in Hallo hoofdtekst van Hallo-aanvraag verwacht. We zijn informatie over die wordt gestart Hallo runbook en Hallo datum en tijd wordt gestart in de header van Hallo aanvraag Hallo ook inclusief.      

    $uri = "https://s1events.azure-automation.net/webhooks?token=8ud0dSrSo%2fvHWpYbklW%3c8s0GrOKJZ9Nr7zqcS%2bIQr4c%3d"
    $headers = @{"From"="user@contoso.com";"Date"="05/28/2015 15:47:00"}

    $vms  = @(
                @{ Name="vm01";ServiceName="vm01"},
                @{ Name="vm02";ServiceName="vm02"}
            )
    $body = ConvertTo-Json -InputObject $vms

    $response = Invoke-RestMethod -Method Post -Uri $uri -Headers $headers -Body $body
    $jobid = ConvertFrom-Json $response


Hallo volgende afbeelding ziet u headerinformatie hello (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) van deze aanvraag. Dit omvat standaard een HTTP-aanvraag-headers in toevoeging toohello aangepaste datum en van de headers die we hebben toegevoegd.  Elk van deze waarden is beschikbaar toohello runbook in Hallo **RequestHeaders** eigenschap van **WebhookData**.

![Knop webhooks.](media/automation-webhooks/webhook-request-headers.png)

Hallo volgende afbeelding toont Hallo hoofdtekst van Hallo-aanvraag (met behulp van een [Fiddler](http://www.telerik.com/fiddler) trace) die beschikbaar toohello runbook in Hallo **RequestBody** eigenschap van **WebhookData**. Dit is opgemaakt als JSON omdat die was Hallo-indeling die is opgenomen in de hoofdtekst Hallo van Hallo-aanvraag.     

![Knop webhooks.](media/automation-webhooks/webhook-request-body.png)

Hallo toont volgende afbeelding worden verzonden vanaf de Windows PowerShell en de resulterende antwoord Hallo Hallo-aanvraag.  Hallo-taak-id is opgehaald uit het antwoord Hallo en geconverteerde tooa tekenreeks.

![Knop webhooks.](media/automation-webhooks/webhook-request-response.png)

Hallo volgende voorbeeldrunbook accepteert van het vorige voorbeeldaanvraag Hallo en Hallo virtuele machines is opgegeven in de aanvraagtekst hello wordt gestart.

    workflow Test-StartVirtualMachinesFromWebhook
    {
        param (
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {

            # Collect properties of WebhookData
            $WebhookName     =     $WebhookData.WebhookName
            $WebhookHeaders =     $WebhookData.RequestHeader
            $WebhookBody     =     $WebhookData.RequestBody

            # Collect individual headers. VMList converted from JSON.
            $From = $WebhookHeaders.From
            $VMList = ConvertFrom-Json -InputObject $WebhookBody
            Write-Output "Runbook started from webhook $WebhookName by $From."

            # Authenticate tooAzure resources
            $Cred = Get-AutomationPSCredential -Name 'MyAzureCredential'
            Add-AzureAccount -Credential $Cred

            # Start each virtual machine
            foreach ($VM in $VMList)
            {
                $VMName = $VM.Name
                Write-Output "Starting $VMName"
                Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName
            }
        }
        else {
            Write-Error "Runbook mean toobe started only from webhook."
        }
    }


## <a name="starting-runbooks-in-response-tooazure-alerts"></a>Starten van runbooks in antwoord tooAzure waarschuwingen
Webhook ingeschakeld runbooks kunnen worden gebruikt tooreact te[waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Bronnen in Azure worden gecontroleerd door het verzamelen van statistieken Hallo zoals prestaties, beschikbaarheid en gebruik met Hallo hulp van waarschuwingen van Azure. U kunt een waarschuwing op basis van de bewaking van metrische gegevens ontvangen of gebeurtenissen voor uw Azure-resources, momenteel Automation-Accounts ondersteunen alleen metrische gegevens. Als het Hallo-waarde van een opgegeven metriek overschrijdt Hallo drempelwaarde toegewezen of als Hallo geconfigureerd gebeurtenis wordt geactiveerd en vervolgens een melding wordt verzonden toohello service beheerder of co-beheerders tooresolve Hallo waarschuwing voor meer informatie over metrische gegevens en gebeurtenissen Raadpleeg te[ Waarschuwingen van Azure](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Naast het gebruik van waarschuwingen van Azure als een waarschuwingssysteem, kunt u ook ere van runbooks in het antwoord tooalerts. Azure Automation biedt Hallo mogelijkheid toorun webhook ingeschakeld runbooks met waarschuwingen van Azure. Wanneer een waarde groter is dan geconfigureerd Hallo drempelwaarde Hallo waarschuwingsregel actief en triggers Hallo automation-webhook die op zijn beurt Hallo runbook worden uitgevoerd.

![Webhooks.](media/automation-webhooks/webhook-alert.jpg)

### <a name="alert-context"></a>Waarschuwingscontext
Houd rekening met een Azure-resource zoals een virtuele machine, CPU-gebruik van deze machine is een van de Hallo prestatie metriek. Als Hallo CPU-gebruik is 100% of meer dan een bepaald bedrag gedurende lange tijd weergegeven, kunt u toorestart Hallo virtuele machine toofix Hallo probleem. Dit kan worden opgelost door een virtuele machine van de waarschuwingsregel toohello configureren en deze regel gaat CPU-percentage als de metriek. Hier CPU-percentage wordt alleen gemaakt als voorbeeld, maar er zijn veel andere metrische gegevens kunt u tooyour Azure configureren bronnen en opnieuw starten Hallo virtuele machine is een actie die is genomen toofix dit probleem, kunt u Hallo runbook tootake andere acties configureren.

Wanneer deze waarschuwingsregel Hallo actief en triggers Hallo runbook webhook is ingeschakeld, verzendt het Hallo waarschuwingscontext toohello runbook. [Waarschuwingscontext](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) bevat details, zoals **SubscriptionID**, **ResourceGroupName**, **ResourceName**, **ResourceType**, **ResourceId** en **tijdstempel** die zijn vereist voor Hallo runbook tooidentify Hallo resource waarop deze actie duurt. Waarschuwing context is ingesloten in het hoofddeel Hallo Hallo **WebhookData** verzonden toohello runbook object en kan worden gebruikt met **Webhook.RequestBody** eigenschap

### <a name="example"></a>Voorbeeld
Maken van een virtuele machine van Azure in uw abonnement en koppelen aan een [toomonitor CPU-percentage metriek waarschuwing](../monitoring-and-diagnostics/insights-receive-alert-notifications.md). Zorg dat u Hallo webhook veld met de Hallo-URL van Hallo webhook die is gegenereerd tijdens het maken van de webhook Hallo vullen tijdens het maken van Hallo waarschuwing.

Hallo wordt volgende voorbeeldrunbook geactiveerd wanneer de waarschuwingsregel Hallo actief en Hallo waarschuwingscontext parameters die zijn vereist voor Hallo runbook tooidentify Hallo resource waarop deze actie te worden verzameld.

    workflow Invoke-RunbookUsingAlerts
    {
        param (      
            [object]$WebhookData
        )

        # If runbook was called from Webhook, WebhookData will not be null.
        if ($WebhookData -ne $null) {   
            # Collect properties of WebhookData.
            $WebhookName    =   $WebhookData.WebhookName
            $WebhookBody    =   $WebhookData.RequestBody
            $WebhookHeaders =   $WebhookData.RequestHeader

            # Outputs information on hello webhook name that called This
            Write-Output "This runbook was started from webhook $WebhookName."


            # Obtain hello WebhookBody containing hello AlertContext
            $WebhookBody = (ConvertFrom-Json -InputObject $WebhookBody)
            Write-Output "`nWEBHOOK BODY"
            Write-Output "============="
            Write-Output $WebhookBody

            # Obtain hello AlertContext     
            $AlertContext = [object]$WebhookBody.context

            # Some selected AlertContext information
            Write-Output "`nALERT CONTEXT DATA"
            Write-Output "==================="
            Write-Output $AlertContext.name
            Write-Output $AlertContext.subscriptionId
            Write-Output $AlertContext.resourceGroupName
            Write-Output $AlertContext.resourceName
            Write-Output $AlertContext.resourceType
            Write-Output $AlertContext.resourceId
            Write-Output $AlertContext.timestamp

            # Act on hello AlertContext data, in our case restarting hello VM.
            # Authenticate tooyour Azure subscription using Organization ID toobe able toorestart that Virtual Machine.
            $cred = Get-AutomationPSCredential -Name "MyAzureCredential"
            Add-AzureAccount -Credential $cred
            Select-AzureSubscription -subscriptionName "Visual Studio Ultimate with MSDN"

            #Check hello status property of hello VM
            Write-Output "Status of VM before taking action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
            Write-Output "Restarting VM"

            # Restart hello VM by passing VM name and Service name which are same in this case
            Restart-AzureVM -ServiceName $AlertContext.resourceName -Name $AlertContext.resourceName
            Write-Output "Status of VM after alert is active and takes action"
            Get-AzureVM -Name $AlertContext.resourceName -ServiceName $AlertContext.resourceName
        }
        else  
        {
            Write-Error "This runbook is meant tooonly be started from a webhook."  
        }  
    }



## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie op verschillende manieren toostart een runbook [een Runbook starten](automation-starting-a-runbook.md).
* Voor informatie over Hallo weer te geven de Status van een Runbook-Job, Raadpleeg te[uitvoeren van Runbook in Azure Automation](automation-runbook-execution.md).
* hoe toouse Azure Automation tootake actie op Azure-waarschuwingen zien toolearn [Azure VM-waarschuwingen oplossen met Automation-Runbooks](automation-azure-vm-alert-integration.md).
