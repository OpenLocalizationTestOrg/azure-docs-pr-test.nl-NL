---
title: aaaUse PowerShell tooCreate en configureren van een Log Analytics-werkruimte | Microsoft Docs
description: Log Analytics maakt gebruik van gegevens van servers in uw on-premises of cloud-infrastructuur. U kunt gegevens van de machine van Azure storage wanneer gegenereerd door Azure diagnostics verzamelen.
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a>Log Analytics beheren met PowerShell
U kunt Hallo [Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform diverse functies in logboekanalyse vanaf een opdrachtregel of als onderdeel van een script.  Voorbeelden van Hallo kunt u taken met PowerShell uitvoeren zijn:

* Een werkruimte maken
* Toevoegen of verwijderen van een oplossing
* Importeren en exporteren van opgeslagen zoekopdrachten
* Maak een computergroep
* Verzamelen van IIS-logboeken van computers met Hallo Windows-agent is geïnstalleerd
* Verzamelen van prestatiemeteritems van Linux- en Windows-computers
* Gebeurtenissen verzamelen van syslog op Linux-computers 
* Verzamelen van gebeurtenissen van Windows-gebeurtenislogboeken
* Aangepaste logboeken verzamelen
* Hallo log analytics agent tooan Azure virtuele machine toevoegen
* Log analytics-tooindex gegevens verzameld met behulp van Azure diagnostics configureren

Dit artikel bevat twee codevoorbeelden die illustratie van enkele Hallo-functies die u vanuit PowerShell uitvoeren kunt.  U kunt verwijzen toohello [Log Analytics PowerShell-cmdlet-verwijzing](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor andere functies.

> [!NOTE]
> Log Analytics is eerder aangeroepen voor operationeel inzicht, die daarom is het Hallo-naam die wordt gebruikt in Hallo-cmdlets.
> 
> 

## <a name="prerequisites"></a>Vereisten
Deze voorbeelden werkt met versie 2.3.0 of hoger van Hallo AzureRm.OperationalInsights module.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Maak en configureer een Log Analytics-werkruimte
Hallo volgende voorbeeldscript ziet u hoe:

1. Een werkruimte maken
2. Lijst Hallo beschikbare oplossingen
3. Oplossingen toohello werkruimte toevoegen
4. Importeren opgeslagen zoekopdrachten
5. Export opgeslagen zoekopdrachten
6. Maak een computergroep
7. Verzamelen van IIS-logboeken van computers met Hallo Windows-agent is geïnstalleerd
8. Verzamelen van prestatiemeteritems voor logische schijf van Linux-computers (% gebruikte Inodes Beschikbare Megabytes; Percentage gebruikte ruimte; Schijfoverdrachten per seconde; Schijf lezen per seconde; Schijf schrijven per seconde)
9. Syslog-gebeurtenissen verzamelen van Linux-computers
10. Fout- en waarschuwingsberichten gebeurtenissen verzamelen van Hallo gebeurtenislogboek van toepassing op Windows-computers
11. Beschikbaar geheugen in megabytes-prestatiemeteritem verzamelen van Windows-computers
12. Een aangepaste logboekgegevens verzamelen 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Log Analytics tooindex Azure diagnostics configureren
Hallo resources moeten voor bewaking zonder agents van Azure-resources, toohave Azure diagnostics is ingeschakeld en geconfigureerd toowrite tooa Log Analytics-werkruimte. Deze methode verzendt gegevens rechtstreeks tooLog Analytics en vereist geen gegevens toobe tooa storage-account geschreven. Ondersteunde resources omvatten:

| Resourcetype | Logboeken | Metrische gegevens |
| --- | --- | --- |
| Toepassingsgateways    | Ja | Ja |
| Automation-accounts     | Ja | |
| Batch-accounts          | Ja | Ja |
| Data Lake analytics     | Ja | | 
| Data Lake store         | Ja | |
| Elastische SQL-groep        |     | Ja |
| Event Hub-naamruimte     |     | Ja |
| IoT-Hubs                |     | Ja |
| Key Vault               | Ja | |
| Taakverdelers          | Ja | |
| Logic Apps              | Ja | Ja |
| Netwerkbeveiligingsgroepen | Ja | |
| Redis Cache             |     | Ja |
| Services zoeken         | Ja | Ja |
| Service Bus-naamruimte   |     | Ja |
| SQL (v12)               |     | Ja |
| Web Sites               |     | Ja |
| Webserver-farms        |     | Ja |

Raadpleeg te voor details van de beschikbare metrische gegevens Hallo Hallo[ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Raadpleeg te voor details van de beschikbare logboeken Hallo Hallo[ondersteund services en het schema voor diagnostische logboeken](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

U kunt ook Hallo voorafgaand aan de cmdlet toocollect logboeken van de resources die tot verschillende abonnementen behoren. Hallo-cmdlet is kunnen toowork voor abonnementen, omdat u biedt Hallo-id van beide Hallo-resource maken van Logboeken en Hallo werkruimte Hallo logboeken worden verzonden naar.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Log Analytics tooindex Azure diagnostische gegevens van opslag configureren
toocollect logboekgegevens vanuit een actief exemplaar van een klassieke cloudservice of een service fabric-cluster, moet u toofirst schrijven Hallo-gegevensopslag tooAzure. Log Analytics wordt vervolgens geconfigureerd toocollect Hallo logboeken van Hallo storage-account. Ondersteunde resources omvatten:

* Klassieke cloudservices (web- en werkrollen rollen)
* Service fabric-clusters

Hallo volgende voorbeeld ziet u hoe aan:

1. Hallo bestaande opslagaccounts en de locaties die logboekanalyse indexeert gegevens uit lijst
2. Een tooread configuratie van een opslagaccount maken
3. Hallo nieuw gemaakte tooindex configuratiegegevens van extra locaties bijwerken
4. Hallo nieuw gemaakte configuratie verwijderen

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

U kunt ook Hallo vóór het script toocollect logboeken van de storage-accounts in verschillende abonnementen behoren. Hallo-script is kunnen toowork voor abonnementen, omdat u Hallo storage account resource-id en een bijbehorende toegangssleutel opgeeft. Wanneer u de toegangssleutel Hallo wijzigt, moet u tooupdate Hallo opslag inzicht toohave Hallo nieuwe sleutel.


## <a name="next-steps"></a>Volgende stappen
* [Bekijk Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor meer informatie over het gebruik van PowerShell voor de configuratie van logboekanalyse.

