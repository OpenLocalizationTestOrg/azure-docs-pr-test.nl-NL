---
title: aaa"Azure VM waarschuwingen met Automation-Runbooks oplossen | Microsoft Docs'
description: In dit artikel laat zien hoe toointegrate virtuele Machine van Azure met Azure Automation-runbooks waarschuwingen en automatisch oplossen van problemen
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a>Azure Automation-scenario: waarschuwingen van de virtuele machine in Azure oplossen
Azure Automation en Azure Virtual Machines hebben een nieuwe functie waarmee u tooconfigure virtuele Machine (VM) waarschuwingen toorun Automation-runbooks uitgebracht. Deze nieuwe mogelijkheid kunt u tooautomatically uit te voeren standaard in het antwoord tooVM waarschuwingen, zoals opnieuw te starten of stoppen Hallo VM.

Voorheen tijdens het maken van de waarschuwingsregel VM kon u te[opgeven van een Automation-webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in de volgorde toorun hello runbook wanneer Hallo waarschuwing geactiveerd. Maar vereist dit dat u toodo Hallo werk van Hallo runbook maken, Hallo webhook voor Hallo-runbook maken en vervolgens te kopiëren en plakken Hallo webhook tijdens het maken van de waarschuwingsregel. Met deze nieuwe versie is Hallo-proces is veel eenvoudiger omdat u een runbook rechtstreeks uit een lijst tijdens het maken van de waarschuwingsregel kiezen kunt en kunt u een automatiseringsaccount dat wordt Hallo runbook uitvoeren of een account gemakkelijk te maken.

In dit artikel wordt ziet u hoe eenvoudig het is tooset van een virtuele machine van Azure-waarschuwing en een Automation-runbook-toorun configureren wanneer Hallo waarschuwing wordt geactiveerd. Voorbeeldscenario's bevatten een virtuele machine opnieuw te starten wanneer het geheugengebruik Hallo sommige vanwege tooan toepassing op Hallo VM met een geheugenlek overschrijdt of een virtuele machine stoppen wanneer Hallo CPU Gebruikerstijd minder dan 1% voor het afgelopen uur is en niet gebruikt wordt. Ook wordt uitgelegd hoe Hallo automatisch maken van een service-principal in uw Automation-account vereenvoudigt Hallo gebruik van runbooks in Azure waarschuwing herbemiddeling.

## <a name="create-an-alert-on-a-vm"></a>Een waarschuwing op een virtuele machine maken
Voer Hallo volgende stappen tooconfigure een waarschuwing toolaunch een runbook wanneer de drempel is voldaan.

> [!NOTE]
> Met deze release alleen wordt ondersteund V2 virtuele machines en ondersteuning voor klassieke die virtuele machines wordt binnenkort toegevoegd.  
> 
> 

1. Meld u bij toohello Azure-portal en klikt u op **virtuele Machines**.  
2. Selecteer een van uw virtuele machines.  Hallo virtuele machine dashboard blade worden weergegeven en Hallo **instellingen** blade tooits rechts.  
3. Van Hallo **instellingen** blade onder Hallo bewaking sectie Selecteer **waarschuwing regels**.
4. Op Hallo **waarschuwing regels** blade, klikt u op **waarschuwing toevoegen**.

Hiermee opent u up Hallo **een waarschuwingsregel toevoegen** blade kunt u voorwaarden voor de waarschuwing Hallo Hallo configureren en kiezen uit een of meer van deze opties: toosomeone e-mailbericht verzenden, gebruikt u een systeem webhook tooforward Hallo waarschuwing tooanother en/of een Automation-runbook worden uitgevoerd in reactie poging tooremediate Hallo probleem.

## <a name="configure-a-runbook"></a>Een runbook configureren
tooconfigure een runbook toorun als Hallo VM waarschuwingsdrempel wordt voldaan, selecteer **Automation-Runbook**. In Hallo **runbook configureren** blade kunt u Hallo runbook toorun en Hallo Automation-account toorun hello runbook in.

![Configureer een Automation-runbook en een nieuw Automation-Account maken](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> Voor deze release kunt u kiezen uit drie runbooks waarmee Hallo service – VM starten, stoppen VM of VM verwijderen (verwijderen).  Hallo mogelijkheid tooselect andere runbooks of een van uw eigen runbooks in een toekomstige release beschikbaar zijn.
> 
> 

![Toochoose van Runbooks](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

Nadat u een Hallo drie beschikbare runbooks selecteert, Hallo **Automation-account** vervolgkeuzelijst wordt weergegeven en kunt u een automation account Hallo runbook wordt uitgevoerd. Runbooks moeten toorun in Hallo context van een [Automation-account](automation-security-overview.md) die zich in uw Azure-abonnement. U kunt een Automation-account dat u al hebt gemaakt, of u kunt een nieuw Automation-account voor u gemaakt.

Hallo runbooks die worden geleverd verifiëren met een service-principal tooAzure. Als u toorun hello runbook in een van uw bestaande Automation-accounts kiest, wordt automatisch gemaakt Hallo service principal voor u. Als u toocreate een nieuw automatiseringsaccount kiest, wordt klikt u vervolgens we automatisch gemaakt Hallo-account en Hallo service-principal. In beide gevallen twee activa ook worden gemaakt in Hallo Automation-account de activa van een certificaat met de naam **AzureRunAsCertificate** en de activa van een verbinding met de naam **AzureRunAsConnection**. Hallo runbooks gebruikt **AzureRunAsConnection** tooauthenticate met Azure in volgorde tooperform Hallo management actie tegen Hallo VM.

> [!NOTE]
> Hallo service-principal in Hallo abonnementsbereik wordt gemaakt en rol van Inzender Hallo is toegewezen. Deze rol is vereist om Hallo account toohave machtiging toorun Automation-runbooks toomanage virtuele Azure-machines.  Hallo maken van een account Automaton en/of de service-principal is een eenmalige gebeurtenis. Zodra ze zijn gemaakt, kunt u dat account toorun runbooks voor andere virtuele machine van Azure-waarschuwingen.
> 
> 

Wanneer u klikt op **OK** Hallo waarschuwing is geconfigureerd en als u Hallo optie toocreate een nieuw automatiseringsaccount hebt geselecteerd, samen met de service-principal hello wordt gemaakt.  Dit kan enkele seconden duren toocomplete.  

![Runbook wordt geconfigureerd](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

Nadat Hallo-configuratie is voltooid, ziet u Hallo de naam van Hallo runbook weergeven in Hallo **een waarschuwingsregel toevoegen** blade.

![Runbook is geconfigureerd](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

Klik op **OK** in Hallo **een waarschuwingsregel toevoegen** blade en Hallo waarschuwingsregel wordt gemaakt en wordt geactiveerd als Hallo virtuele machine actief is.

### <a name="enable-or-disable-a-runbook"></a>In- of uitschakelen van een runbook
Als u een runbook dat is geconfigureerd voor een waarschuwing hebt, kunt u deze uitschakelen zonder te verwijderen van de runbookconfiguratie Hallo. Dit kunt u tookeep Hallo waarschuwing uitgevoerd en sommige Hallo waarschuwingsregels mogelijk te testen en later opnieuw inschakelen Hallo runbook.

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a>Een runbook maken dat met een Azure-waarschuwing werkt
Wanneer u een runbook als onderdeel van een Azure waarschuwingsregel kiest, moet Hallo runbook toohave logica in het toomanage Hallo waarschuwingsgegevens die tooit wordt doorgegeven.  Wanneer een runbook is geconfigureerd in een waarschuwingsregel, is een webhook gemaakt voor runbook Hallo; Deze webhook is en gebruikte toostart Hallo runbook elke waarschuwing tijd Hallo-triggers.  Hallo werkelijke aanroep toostart hello runbook is een HTTP POST-aanvraag toohello webhook-URL. Hallo-hoofdtekst van Hallo POST-aanvraag bevat een JSON-indeling object dat nuttige eigenschappen gerelateerde toohello waarschuwing bevat.  Zoals u hieronder zien kunt, bevat de waarschuwingsgegevens Hallo-gegevens, zoals de abonnements-id, resourceGroupName resourceName en resourceType.

### <a name="example-of-alert-data"></a>Voorbeeld van waarschuwingsgegevens
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

Wanneer Hallo Automation-webhook-service Hallo HTTP POST ontvangt Hallo waarschuwingsgegevens extraheert en geeft deze door toohello runbook in runbookinvoerparameter WebhookData Hallo.  Hieronder vindt u een voorbeeldrunbook dat toont hoe toouse Hallo WebhookData-parameter en waarschuwingsgegevens Hallo uitpakken en toomanage hello Azure-resource die Hallo waarschuwing heeft geactiveerd worden gebruikt.

### <a name="example-runbook"></a>Voorbeeldrunbook
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a>Samenvatting
Wanneer u een waarschuwing op een virtuele machine in Azure configureert, hebt u nu Hallo mogelijkheid tooeasily configureren van een Automation runbook tooautomatically herstelactie uitvoeren wanneer het Hallo-waarschuwing wordt geactiveerd. Voor deze release kunt u kiezen uit runbooks toorestart, stoppen of verwijderen van een virtuele machine, afhankelijk van uw waarschuwing scenario. Dit is alleen Hallo begin van het inschakelen van scenario's waarbij u Hallo acties (melding, het oplossen van problemen herstel) die automatisch worden uitgevoerd wanneer een waarschuwing activeert beheren.

## <a name="next-steps"></a>Volgende stappen
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)
* tooget gestart met PowerShell workflow-runbooks, Zie [Mijn eerste PowerShell workflow-runbook](automation-first-runbook-textual.md)
* toolearn meer informatie over runbooktypen, hun voordelen en beperkingen, Zie [Azure Automation-runbooktypen](automation-runbook-types.md)

