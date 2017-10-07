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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="4ac13-103">VPN-gateways bij het oplossen van netwerk-Watcher bewaken</span><span class="sxs-lookup"><span data-stu-id="4ac13-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="4ac13-104">Veel inzicht op de netwerkprestaties van uw krijgen is kritieke tooprovide betrouwbare services toocustomers.</span><span class="sxs-lookup"><span data-stu-id="4ac13-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="4ac13-105">Het is daarom kritieke toodetect onderbreking netwerkomstandigheden snel en corrigerende maatregelen toomitigate Hallo onderbreking van deze voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="4ac13-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="4ac13-106">Azure Automation kunt u tooimplement en een taak uitvoeren op een programmatische wijze via runbooks.</span><span class="sxs-lookup"><span data-stu-id="4ac13-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="4ac13-107">Met behulp van Azure Automation maakt een perfecte recept voor het uitvoeren van continue en proactieve netwerkbewaking en waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="4ac13-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ac13-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="4ac13-108">Scenario</span></span>

<span data-ttu-id="4ac13-109">Hallo-scenario in Hallo volgende afbeelding is een toepassing met meerdere lagen met op premises-verbinding tot stand gebracht via een VPN-Gateway en de tunnel.</span><span class="sxs-lookup"><span data-stu-id="4ac13-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="4ac13-110">Is de essentiële toohello toepassingsprestaties gezorgd Hallo die VPN-Gateway actief is en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ac13-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="4ac13-111">Een runbook met een script toocheck voor verbindingsstatus van Hallo VPN-tunnel met Hallo Resource-API voor het oplossen van problemen toocheck voor verbindingsstatus tunnel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ac13-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="4ac13-112">Als Hallo status niet in orde is, wordt een e-trigger tooadministrators verzonden.</span><span class="sxs-lookup"><span data-stu-id="4ac13-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Voorbeeldscenario][scenario]

<span data-ttu-id="4ac13-114">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="4ac13-114">This scenario will:</span></span>

- <span data-ttu-id="4ac13-115">Maken van een runbook aanroepen Hallo `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot verbindingsstatus</span><span class="sxs-lookup"><span data-stu-id="4ac13-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="4ac13-116">Een planning toohello runbook koppelen</span><span class="sxs-lookup"><span data-stu-id="4ac13-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ac13-117">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="4ac13-117">Before you begin</span></span>

<span data-ttu-id="4ac13-118">Voordat u dit scenario begint, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="4ac13-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="4ac13-119">Een Azure automation-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac13-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="4ac13-120">Zorg ervoor dat Hallo automation-account de meest recente modules Hallo zijn en ook Hallo AzureRM.Network module heeft.</span><span class="sxs-lookup"><span data-stu-id="4ac13-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="4ac13-121">Hallo AzureRM.Network module is beschikbaar in de Modulegalerie Hallo als u tooadd moet het tooyour automation-account.</span><span class="sxs-lookup"><span data-stu-id="4ac13-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="4ac13-122">U moet een set referenties configureren in Azure Automation hebben.</span><span class="sxs-lookup"><span data-stu-id="4ac13-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="4ac13-123">Meer informatie in [Azure Automation-beveiliging](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4ac13-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="4ac13-124">Een geldig SMTP-server (Office 365, uw on-premises e-mail of andere) en de referenties die zijn gedefinieerd in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4ac13-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="4ac13-125">Een geconfigureerde virtuele netwerkgateway in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac13-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="4ac13-126">Een bestaand opslagaccount met een bestaande container toostore Hallo zich aanmeldt.</span><span class="sxs-lookup"><span data-stu-id="4ac13-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="4ac13-127">Hallo-infrastructuur in de voorgaande afbeelding Hallo is ter illustratie en zijn niet gemaakt met de Hallo stappen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4ac13-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="4ac13-128">Hallo-runbook maken</span><span class="sxs-lookup"><span data-stu-id="4ac13-128">Create hello runbook</span></span>

<span data-ttu-id="4ac13-129">Hallo eerste stap tooconfiguring Hallo voorbeeld is toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="4ac13-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="4ac13-130">In dit voorbeeld wordt een run as-account.</span><span class="sxs-lookup"><span data-stu-id="4ac13-130">This example uses a run-as account.</span></span> <span data-ttu-id="4ac13-131">toolearn over run as-accounts, gaat u naar [Runbooks verifiëren met Azure uitvoeren als-account](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="4ac13-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="4ac13-132">Stap 1</span><span class="sxs-lookup"><span data-stu-id="4ac13-132">Step 1</span></span>

<span data-ttu-id="4ac13-133">Navigeer tooAzure automatisering in Hallo [Azure-portal](https://portal.azure.com) en klik op **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="4ac13-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![overzicht van Automation-account][1]

### <a name="step-2"></a><span data-ttu-id="4ac13-135">Stap 2</span><span class="sxs-lookup"><span data-stu-id="4ac13-135">Step 2</span></span>

<span data-ttu-id="4ac13-136">Klik op **een runbook toevoegen** toostart Hallo proces voor het maken van Hallo runbook.</span><span class="sxs-lookup"><span data-stu-id="4ac13-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![runbooks-blade][2]

### <a name="step-3"></a><span data-ttu-id="4ac13-138">Stap 3</span><span class="sxs-lookup"><span data-stu-id="4ac13-138">Step 3</span></span>

<span data-ttu-id="4ac13-139">Onder **snelle invoer**, klikt u op **een nieuw runbook maken** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="4ac13-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![toevoegen van een runbookblade][3]

### <a name="step-4"></a><span data-ttu-id="4ac13-141">Stap 4</span><span class="sxs-lookup"><span data-stu-id="4ac13-141">Step 4</span></span>

<span data-ttu-id="4ac13-142">In deze stap we Hallo runbook een naam geven, in Hallo voorbeeld aangeroepen **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="4ac13-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="4ac13-143">Het is belangrijk toogive hello runbook een beschrijvende naam en hieraan een naam die standaard PowerShell naamgevingsstandaarden volgt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="4ac13-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="4ac13-144">Hallo runbooktype voor dit voorbeeld is **PowerShell**, hello andere opties zijn grafisch, PowerShell workflow, en de grafische PowerShell-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="4ac13-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![runbookblade][4]

### <a name="step-5"></a><span data-ttu-id="4ac13-146">Stap 5</span><span class="sxs-lookup"><span data-stu-id="4ac13-146">Step 5</span></span>

<span data-ttu-id="4ac13-147">In deze stap hello runbook is gemaakt, Hallo volgende codevoorbeeld geeft dat alle code nodig bijvoorbeeld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ac13-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="4ac13-148">Hallo-items in de Hallo code die bevatten \<waarde\> toobe vervangen door waarden uit uw abonnement Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="4ac13-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="4ac13-149">Gebruik Hallo volgende code als Klik **opslaan**</span><span class="sxs-lookup"><span data-stu-id="4ac13-149">Use hello following code as click **Save**</span></span>

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

### <a name="step-6"></a><span data-ttu-id="4ac13-150">Stap 6</span><span class="sxs-lookup"><span data-stu-id="4ac13-150">Step 6</span></span>

<span data-ttu-id="4ac13-151">Zodra Hallo runbook is opgeslagen, een schema moet worden gekoppeld tooit tooautomate Hallo begin van het Hallo-runbook.</span><span class="sxs-lookup"><span data-stu-id="4ac13-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="4ac13-152">toostart hello proces, klikt u op **planning**.</span><span class="sxs-lookup"><span data-stu-id="4ac13-152">toostart hello process, click **Schedule**.</span></span>

![Stap 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="4ac13-154">Een planning toohello runbook koppelen</span><span class="sxs-lookup"><span data-stu-id="4ac13-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="4ac13-155">Een nieuw schema moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ac13-155">A new schedule must be created.</span></span> <span data-ttu-id="4ac13-156">Klik op **koppelen van een planning tooyour runbook**.</span><span class="sxs-lookup"><span data-stu-id="4ac13-156">Click **Link a schedule tooyour runbook**.</span></span>

![Stap 7][7]

### <a name="step-1"></a><span data-ttu-id="4ac13-158">Stap 1</span><span class="sxs-lookup"><span data-stu-id="4ac13-158">Step 1</span></span>

<span data-ttu-id="4ac13-159">Op Hallo **planning** blade, klikt u op **een nieuw schema maken**</span><span class="sxs-lookup"><span data-stu-id="4ac13-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Stap 8][8]

### <a name="step-2"></a><span data-ttu-id="4ac13-161">Stap 2</span><span class="sxs-lookup"><span data-stu-id="4ac13-161">Step 2</span></span>

<span data-ttu-id="4ac13-162">Op Hallo **nieuwe planning** blade Hallo planningsgegevens invullen.</span><span class="sxs-lookup"><span data-stu-id="4ac13-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="4ac13-163">Hallo-waarden kunnen worden ingesteld zijn in Hallo lijst volgende:</span><span class="sxs-lookup"><span data-stu-id="4ac13-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="4ac13-164">**Naam** -Hallo beschrijvende naam van het Hallo-schema.</span><span class="sxs-lookup"><span data-stu-id="4ac13-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="4ac13-165">**Beschrijving** -een beschrijving van het Hallo-schema.</span><span class="sxs-lookup"><span data-stu-id="4ac13-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="4ac13-166">**Start** -deze waarde is een combinatie van datum, tijd en tijdzone die gezamenlijk Hallo tijd Hallo planning triggers.</span><span class="sxs-lookup"><span data-stu-id="4ac13-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="4ac13-167">**Terugkeerpatroon** -deze waarde bepaalt Hallo planningen herhaling.</span><span class="sxs-lookup"><span data-stu-id="4ac13-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="4ac13-168">Geldige waarden zijn **eenmaal** of **terugkerend**.</span><span class="sxs-lookup"><span data-stu-id="4ac13-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="4ac13-169">**Herhaald elke** -terugkeerpatroon Hallo Hallo schema in uren, dagen, weken of maanden.</span><span class="sxs-lookup"><span data-stu-id="4ac13-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="4ac13-170">**Instellen dat verlopen** -Hallo waarde bepaalt als Hallo schema of niet verlopen moet.</span><span class="sxs-lookup"><span data-stu-id="4ac13-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="4ac13-171">Te kunnen worden ingesteld**Ja** of **Nee**.</span><span class="sxs-lookup"><span data-stu-id="4ac13-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="4ac13-172">Een geldige datum en tijd zijn opgegeven als u Ja kiest toobe.</span><span class="sxs-lookup"><span data-stu-id="4ac13-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="4ac13-173">Als u toohave een runbook vaker dan elk uur uitgevoerd moet, moeten meerdere planningen worden gemaakt met een ander interval (dat wil zeggen, 15, 30, 45 minuten na Hallo uur)</span><span class="sxs-lookup"><span data-stu-id="4ac13-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Stap 9][9]

### <a name="step-3"></a><span data-ttu-id="4ac13-175">Stap 3</span><span class="sxs-lookup"><span data-stu-id="4ac13-175">Step 3</span></span>

<span data-ttu-id="4ac13-176">Klik op Opslaan toosave Hallo planning toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="4ac13-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Stap 10][10]

## <a name="next-steps"></a><span data-ttu-id="4ac13-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ac13-178">Next steps</span></span>

<span data-ttu-id="4ac13-179">Nu dat u inzicht hebben in over het toointegrate netwerk-Watcher het oplossen van problemen met Azure Automation, informatie over hoe tootrigger pakket worden vastgelegd op de VM-waarschuwingen in via [een waarschuwing geactiveerd pakketopname maken met Azure-netwerk-Watcher](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="4ac13-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
