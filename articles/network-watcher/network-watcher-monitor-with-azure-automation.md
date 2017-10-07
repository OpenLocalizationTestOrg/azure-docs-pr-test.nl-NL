---
title: aaaMonitor VPN-gateways met Azure-netwerk-Watcher probleemoplossing | Microsoft Docs
description: Dit artikel wordt beschreven hoe sporen On-premises-connectiviteit met Azure Automation en netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>VPN-gateways bij het oplossen van netwerk-Watcher bewaken

Veel inzicht op de netwerkprestaties van uw krijgen is kritieke tooprovide betrouwbare services toocustomers. Het is daarom kritieke toodetect onderbreking netwerkomstandigheden snel en corrigerende maatregelen toomitigate Hallo onderbreking van deze voorwaarde. Azure Automation kunt u tooimplement en een taak uitvoeren op een programmatische wijze via runbooks. Met behulp van Azure Automation maakt een perfecte recept voor het uitvoeren van continue en proactieve netwerkbewaking en waarschuwingen.

## <a name="scenario"></a>Scenario

Hallo-scenario in Hallo volgende afbeelding is een toepassing met meerdere lagen met op premises-verbinding tot stand gebracht via een VPN-Gateway en de tunnel. Is de essentiële toohello toepassingsprestaties gezorgd Hallo die VPN-Gateway actief is en wordt uitgevoerd.

Een runbook met een script toocheck voor verbindingsstatus van Hallo VPN-tunnel met Hallo Resource-API voor het oplossen van problemen toocheck voor verbindingsstatus tunnel gemaakt. Als Hallo status niet in orde is, wordt een e-trigger tooadministrators verzonden.

![Voorbeeldscenario][scenario]

Dit scenario wordt:

- Maken van een runbook aanroepen Hallo `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot verbindingsstatus
- Een planning toohello runbook koppelen

## <a name="before-you-begin"></a>Voordat u begint

Voordat u dit scenario begint, hebt u Hallo volgende vereisten:

- Een Azure automation-account in Azure. Zorg ervoor dat Hallo automation-account de meest recente modules Hallo zijn en ook Hallo AzureRM.Network module heeft. Hallo AzureRM.Network module is beschikbaar in de Modulegalerie Hallo als u tooadd moet het tooyour automation-account.
- U moet een set referenties configureren in Azure Automation hebben. Meer informatie in [Azure Automation-beveiliging](../automation/automation-security-overview.md)
- Een geldig SMTP-server (Office 365, uw on-premises e-mail of andere) en de referenties die zijn gedefinieerd in Azure Automation
- Een geconfigureerde virtuele netwerkgateway in Azure.
- Een bestaand opslagaccount met een bestaande container toostore Hallo zich aanmeldt.

> [!NOTE]
> Hallo-infrastructuur in de voorgaande afbeelding Hallo is ter illustratie en zijn niet gemaakt met de Hallo stappen in dit artikel.

### <a name="create-hello-runbook"></a>Hallo-runbook maken

Hallo eerste stap tooconfiguring Hallo voorbeeld is toocreate hello runbook. In dit voorbeeld wordt een run as-account. toolearn over run as-accounts, gaat u naar [Runbooks verifiëren met Azure uitvoeren als-account](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Stap 1

Navigeer tooAzure automatisering in Hallo [Azure-portal](https://portal.azure.com) en klik op **Runbooks**

![overzicht van Automation-account][1]

### <a name="step-2"></a>Stap 2

Klik op **een runbook toevoegen** toostart Hallo proces voor het maken van Hallo runbook.

![runbooks-blade][2]

### <a name="step-3"></a>Stap 3

Onder **snelle invoer**, klikt u op **een nieuw runbook maken** toocreate hello runbook.

![toevoegen van een runbookblade][3]

### <a name="step-4"></a>Stap 4

In deze stap we Hallo runbook een naam geven, in Hallo voorbeeld aangeroepen **Get-VPNGatewayStatus**. Het is belangrijk toogive hello runbook een beschrijvende naam en hieraan een naam die standaard PowerShell naamgevingsstandaarden volgt aanbevolen. Hallo runbooktype voor dit voorbeeld is **PowerShell**, hello andere opties zijn grafisch, PowerShell workflow, en de grafische PowerShell-werkstroom.

![runbookblade][4]

### <a name="step-5"></a>Stap 5

In deze stap hello runbook is gemaakt, Hallo volgende codevoorbeeld geeft dat alle code nodig bijvoorbeeld Hallo Hallo. Hallo-items in de Hallo code die bevatten \<waarde\> toobe vervangen door waarden uit uw abonnement Hallo nodig.

Gebruik Hallo volgende code als Klik **opslaan**

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a>Stap 6

Zodra Hallo runbook is opgeslagen, een schema moet worden gekoppeld tooit tooautomate Hallo begin van het Hallo-runbook. toostart hello proces, klikt u op **planning**.

![Stap 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Een planning toohello runbook koppelen

Een nieuw schema moet worden gemaakt. Klik op **koppelen van een planning tooyour runbook**.

![Stap 7][7]

### <a name="step-1"></a>Stap 1

Op Hallo **planning** blade, klikt u op **een nieuw schema maken**

![Stap 8][8]

### <a name="step-2"></a>Stap 2

Op Hallo **nieuwe planning** blade Hallo planningsgegevens invullen. Hallo-waarden kunnen worden ingesteld zijn in Hallo lijst volgende:

- **Naam** -Hallo beschrijvende naam van het Hallo-schema.
- **Beschrijving** -een beschrijving van het Hallo-schema.
- **Start** -deze waarde is een combinatie van datum, tijd en tijdzone die gezamenlijk Hallo tijd Hallo planning triggers.
- **Terugkeerpatroon** -deze waarde bepaalt Hallo planningen herhaling.  Geldige waarden zijn **eenmaal** of **terugkerend**.
- **Herhaald elke** -terugkeerpatroon Hallo Hallo schema in uren, dagen, weken of maanden.
- **Instellen dat verlopen** -Hallo waarde bepaalt als Hallo schema of niet verlopen moet. Te kunnen worden ingesteld**Ja** of **Nee**. Een geldige datum en tijd zijn opgegeven als u Ja kiest toobe.

> [!NOTE]
> Als u toohave een runbook vaker dan elk uur uitgevoerd moet, moeten meerdere planningen worden gemaakt met een ander interval (dat wil zeggen, 15, 30, 45 minuten na Hallo uur)

![Stap 9][9]

### <a name="step-3"></a>Stap 3

Klik op Opslaan toosave Hallo planning toohello runbook.

![Stap 10][10]

## <a name="next-steps"></a>Volgende stappen

Nu dat u inzicht hebben in over het toointegrate netwerk-Watcher het oplossen van problemen met Azure Automation, informatie over hoe tootrigger pakket worden vastgelegd op de VM-waarschuwingen in via [een waarschuwing geactiveerd pakketopname maken met Azure-netwerk-Watcher](network-watcher-alert-triggered-packet-capture.md).

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
