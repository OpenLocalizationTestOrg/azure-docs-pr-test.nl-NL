---
title: Voorbeelden van aaaAzure Monitor PowerShell snel starten. | Microsoft Docs
description: Gebruik PowerShell tooaccess Azure Monitor functies zoals automatisch schalen, waarschuwingen, webhooks en activiteitenlogboeken zoeken.
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a>Azure PowerShell Monitor snel starten-voorbeelden
In dit artikel worden steekproef van PowerShell-opdrachten toohelp u toegang tot Azure Monitor functies. Monitor voor Azure kunt u tooAutoScale Cloudservices, virtuele Machines en Web-Apps en toosend waarschuwingsmeldingen of een aanroep van web-URL's op basis van waarden van de geconfigureerde telemetrische gegevens.

> [!NOTE]
> Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016. Hallo-naamruimten en dus Hallo na opdrachten nog steeds echter bevatten Hallo 'insights'.
> 
> 

## <a name="set-up-powershell"></a>Instellen van PowerShell
Als u nog niet gedaan hebt, stelt u PowerShell toorun op uw computer. Zie voor meer informatie [hoe tooInstall en PowerShell configureren](/powershell/azure/overview).

## <a name="examples-in-this-article"></a>Voorbeelden in dit artikel
Hallo-voorbeelden in Hallo artikel ziet u hoe u Azure Monitor cmdlets kunt gebruiken. U kunt ook de volledige lijst van Azure Monitor PowerShell-cmdlets op Hallo bekijken [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).

## <a name="sign-in-and-use-subscriptions"></a>Aanmelden en abonnementen gebruiken
Meld u eerst in tooyour Azure-abonnement.

```PowerShell
Login-AzureRmAccount
```

Hiervoor moet u toosign in. Zodra u dit, uw Account doet worden TenantID en standaard abonnements-ID weergegeven. Alle Hallo Azure-cmdlets werk in de context van uw standaardabonnement Hallo. tooview hello lijst met abonnementen die u hebt toegang tot, Hallo volgende opdracht gebruiken.

```PowerShell
Get-AzureRmSubscription
```

toochange uw werkende context tooa verschillende abonnement, gebruik Hallo opdracht te volgen.

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a>Activiteitenlogboek voor een abonnement ophalen
Gebruik Hallo `Get-AzureRmLog` cmdlet.  Hallo hieronder vindt u enkele algemene voorbeelden.

Logboekvermeldingen ophalen uit deze toopresent tijd/datum:

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

Logboekvermeldingen tussen een bereik van tijd/datum ophalen:

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Logboekvermeldingen ophalen uit een specifieke resourcegroep:

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

Logboekvermeldingen ophalen van een bepaalde resourceprovider tussen een bereik van tijd/datum:

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

Alle logboekvermeldingen met een specifieke aanroeper ophalen:

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

Hallo opdracht haalt de laatste 1000 gebeurtenissen van activiteitenlogboek Hallo Hallo te volgen:

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

`Get-AzureRmLog`biedt ondersteuning voor veel andere parameters. Zie Hallo `Get-AzureRmLog` documentatie voor meer informatie.

> [!NOTE]
> `Get-AzureRmLog`biedt alleen 15 dagen van de geschiedenis. Met behulp van Hallo **- MaxEvents** parameter kunt u tooquery Hallo laatste N gebeurtenissen, afgezien van 15 dagen. tooaccess gebeurtenissen die ouder zijn dan 15 dagen Hallo REST-API of de SDK (C# voorbeeld met Hallo SDK) gebruiken. Als u geen **StartTime**, dan is de standaardwaarde Hallo **EndTime** min één uur. Als u geen **EndTime**, dan is de standaardwaarde Hallo huidige tijd. Alle tijden zijn in UTC.
> 
> 

## <a name="retrieve-alerts-history"></a>Ophalen van de geschiedenis van waarschuwingen
alle waarschuwingen gebeurtenissen, u kunt een query tooview Hallo Hallo volgen voorbeelden met Azure Resource Manager-Logboeken.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

tooview hello geschiedenis voor een specifieke waarschuwing sluiten, kunt u Hallo `Get-AzureRmAlertHistory` doorgeven in een resource-ID van de waarschuwingsregel Hallo Hallo-cmdlet.

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

Hallo `Get-AzureRmAlertHistory` cmdlet ondersteunt verschillende parameters. Meer informatie Zie [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).

## <a name="retrieve-information-on-alert-rules"></a>Ophalen van informatie over de regels voor waarschuwingen
Alle volgende opdrachten Hallo fungeren voor een resourcegroep met de naam 'montest'.

Alle Hallo-eigenschappen van de waarschuwingsregel Hallo weergeven:

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

Alle waarschuwingen voor een resourcegroep ophalen:

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

Alle regels voor waarschuwingen instellen voor een doelresource worden opgehaald. Bijvoorbeeld instellen alle regels voor waarschuwingen op een virtuele machine.

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

`Get-AzureRmAlertRule`biedt ondersteuning voor andere parameters. Zie [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) voor meer informatie.

## <a name="create-metric-alerts"></a>Metrische waarschuwingen maken
U kunt Hallo `Add-AlertRule` cmdlet toocreate, bijwerken of een waarschuwingsregel uitschakelen.

Kunt u e-mail en -webhook eigenschappen met behulp van `New-AzureRmAlertRuleEmail` en `New-AzureRmAlertRuleWebhook`respectievelijk. Wijs in Hallo waarschuwingsregel cmdlet, deze poorten als acties toohello **acties** eigenschap Hallo waarschuwingsregel.

Hallo volgende tabel beschrijft Hallo parameters en waarden gebruikte toocreate een waarschuwing met behulp van een metriek.

| Parameter | waarde |
| --- | --- |
| Naam |simpletestdiskwrite |
| Locatie van deze waarschuwingsregel |VS - oost |
| ResourceGroup |montest |
| TargetResourceId |/Subscriptions/S1/resourceGroups/montest/providers/Microsoft.COMPUTE/virtualMachines/testconfig |
| MetricName van Hallo waarschuwing die wordt gemaakt |\Disk \PhysicalDisk (_Totaal) per seconde. Zie Hallo `Get-MetricDefinitions` cmdlet over hoe tooretrieve Hallo exacte metrische namen |
| Operator |GreaterThan |
| Drempelwaarde (aantal per seconde in voor deze metrische gegevens) |1 |
| Venstergrootte (indeling: mm: SS) |00:05:00 |
| aggregator (statistiek van Hallo metrische gegevens, die in dit geval gemiddeld aantal gebruikt) |Gemiddelde |
| aangepaste e-mailberichten (string array) |'foo@example.com','bar@example.com' |
| e-mailadres tooowners, bijdragers en lezers verzenden |-SendToServiceOwners |

Een e-actie maken

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

Maken van een Webhook-actie

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

Hallo waarschuwingsregel maken op Hallo CPU % metriek op een klassieke virtuele machine

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

De waarschuwingsregel Hallo ophalen

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

Hallo regel Hallo toevoegen waarschuwing cmdlet ook bijgewerkt als er al een waarschuwingsregel voor Hallo eigenschappen bestaat. een waarschuwingsregel toodisable Hallo-parameter opnemen **- DisableRule**.

## <a name="get-a-list-of-available-metrics-for-alerts"></a>Een lijst met beschikbare metrische gegevens ophalen voor waarschuwingen
U kunt Hallo `Get-AzureRmMetricDefinition` cmdlet tooview Hallo lijst met alle metrische gegevens voor een specifieke bron.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

Hallo volgende voorbeeld genereert een tabel met Hallo metriek naam en het Hallo eenheid voor.

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Een volledige lijst met beschikbare opties voor `Get-AzureRmMetricDefinition` is beschikbaar op [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).

## <a name="create-and-manage-autoscale-settings"></a>Maken en beheren van instellingen voor automatisch schalen
Een resource, zoals een Web-app, VM, Cloudservice of virtuele-Machineschaalset kan slechts één instelling voor automatisch schalen geconfigureerd hebben.
Elke instelling voor automatisch schalen kunt echter meerdere profielen hebben. Bijvoorbeeld, een voor een profiel schalen op basis van prestaties en een tweede voor een profiel op basis van een planning. Elk profiel kan meerdere regels die zijn geconfigureerd op deze hebben. Zie voor meer informatie over automatisch schalen, [hoe een toepassing tooAutoscale](../cloud-services/cloud-services-how-to-scale.md).

Hier volgen Hallo stappen die zullen worden gebruikt:

1. Regel (s) maken.
2. Maken van profielen toewijzing Hallo regels die u eerder toohello profielen gemaakt.
3. Optioneel: Maak meldingen voor automatisch schalen door webhook en e-eigenschappen te configureren.
4. Een instelling voor automatisch schalen met een naam voor de doelbron Hallo maken via het Hallo-profielen en meldingen die u hebt gemaakt in de vorige stappen Hallo toewijzen.

Hallo volgende voorbeelden ziet u hoe u een instelling voor automatisch schalen voor een virtuele-Machineschaalset voor een Windows-besturingssysteem op basis van met behulp van Hallo CPU-gebruik metrische gegevens kunt maken.

Maak eerst een regel tooscale-out, met een verhoging van het aantal exemplaar.

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

Maak vervolgens een regel tooscale in, met een aantal exemplaar verlagen.

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

Vervolgens maakt u een profiel voor Hallo regels.

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

Maak een webhook-eigenschap.

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

Maak Hallo melding eigenschap voor de instelling voor Hallo automatisch schalen, zoals e-mail en Hallo webhook die u eerder hebt gemaakt.

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

Maak ten slotte Hallo automatisch schalen instellen tooadd Hallo van het profiel dat u hierboven hebt gemaakt.

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

Zie voor meer informatie over het beheren van instellingen voor automatisch schalen [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).

## <a name="autoscale-history"></a>Geschiedenis van automatisch schalen
Hallo volgende voorbeeld ziet u hoe u recente gebeurtenissen voor automatisch schalen en waarschuwing kunt bekijken. Hallo activiteit zoeken tooview Hallo automatisch schalen Logboekgeschiedenis gebruiken.

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

U kunt Hallo `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve historie van automatisch schalen.

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

Zie voor meer informatie [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).

### <a name="view-details-for-an-autoscale-setting"></a>Details weergeven voor een instelling voor automatisch schalen
U kunt Hallo `Get-Autoscalesetting` cmdlet tooretrieve meer informatie over het Hallo-instelling voor automatisch schalen.

Hallo volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in myrg1' hello resource group'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

Hallo volgende voorbeeld worden details weergegeven over alle instellingen voor automatisch schalen in myrg1' hello resource groep' en specifiek Hallo instelling voor automatisch schalen met de naam 'MyScaleVMSSSetting'.

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a>Verwijderen van een instelling voor automatisch schalen
U kunt Hallo `Remove-Autoscalesetting` cmdlet toodelete een instelling voor automatisch schalen.

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a>Logboek profielen beheert voor activiteitenlogboek
Kunt u een *Meld profiel* en het exporteren van gegevens van uw opslagaccount activiteit logboek tooa en u kunt bewaren van gegevens voor het configureren. U kunt eventueel ook Hallo gegevens tooyour Event Hub streamen. Let op: deze functie momenteel in Preview en u is kunt slechts één log-profiel per abonnement maken. U kunt gebruiken Hallo cmdlets met uw huidige abonnement toocreate te volgen en log-profielen te beheren. U kunt ook een bepaald abonnement. Hoewel PowerShell standaard toohello huidige abonnement, kunt u altijd wijzigen die met `Set-AzureRmContext`. U kunt een activiteit logboek tooroute gegevens tooany storage-account of Event Hub configureren binnen dat abonnement. Gegevens worden geschreven als blob-bestanden in de JSON-indeling.

### <a name="get-a-log-profile"></a>Een profiel voor een logboek ophalen
toofetch uw bestaande logboek-profielen maken gebruik van Hallo `Get-AzureRmLogProfile` cmdlet.

### <a name="add-a-log-profile-without-data-retention"></a>Een profiel logboek zonder bewaren van gegevens toevoegen
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Een logboek-profiel verwijderen
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a>Een profiel van het logboek met bewaren van gegevens toevoegen
U kunt opgeven dat Hallo **- RetentionInDays** eigenschap met de Hallo aantal dagen, als een positief geheel getal, waarbij Hallo gegevens moeten worden bewaard.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a>Logboek-profiel met bewaren en EventHub toevoegen
In aanvulling toorouting uw gegevens toostorage-account, u kunt ook streamen deze tooan Event Hub. Houd er rekening mee dat in deze preview release en Hallo account opslagconfiguratie verplicht is maar Event Hub-configuratie optioneel is.

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a>Logboeken met diagnostische gegevens configureren
Veel Azure-services bieden extra logboeken en telemetrie die geconfigureerd toosave gegevens in uw Azure Storage-account worden kan, sturen tooEvent Hubs en/of tooan logboekanalyse OMS-werkruimte verzonden. Deze bewerking kan alleen worden uitgevoerd op het niveau van een resource en Hallo storage-account of event hub moet aanwezig zijn in Hallo dezelfde regio bevinden als de doelbron Hallo waarop Hallo diagnostische instelling is geconfigureerd.

### <a name="get-diagnostic-setting"></a>De diagnostische instelling niet ophalen
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

Diagnostische instelling uitschakelen

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

Schakel diagnostische instelling zonder bewaren

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

Schakel diagnostische instelling met bewaren

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Schakel diagnostische instelling met de bewaarperiode voor een specifieke logboek-categorie

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

Schakel diagnostische instelling voor Event Hubs

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

Diagnostische instelling voor OMS inschakelen

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
