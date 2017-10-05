---
title: PowerShell gebruiken voor het maken en configureren van een Log Analytics-werkruimte | Microsoft Docs
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="3a55e-104">Log Analytics beheren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a55e-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="3a55e-105">U kunt de [Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) diverse functies uitvoeren in logboekanalyse vanaf een opdrachtregel of als onderdeel van een script.</span><span class="sxs-lookup"><span data-stu-id="3a55e-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="3a55e-106">Voorbeelden van de taken die u met PowerShell uitvoeren kunt zijn:</span><span class="sxs-lookup"><span data-stu-id="3a55e-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="3a55e-107">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="3a55e-107">Create a workspace</span></span>
* <span data-ttu-id="3a55e-108">Toevoegen of verwijderen van een oplossing</span><span class="sxs-lookup"><span data-stu-id="3a55e-108">Add or remove a solution</span></span>
* <span data-ttu-id="3a55e-109">Importeren en exporteren van opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="3a55e-109">Import and export saved searches</span></span>
* <span data-ttu-id="3a55e-110">Maak een computergroep</span><span class="sxs-lookup"><span data-stu-id="3a55e-110">Create a computer group</span></span>
* <span data-ttu-id="3a55e-111">Verzamelen van IIS-logboeken van computers met de Windows-agent die is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="3a55e-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="3a55e-112">Verzamelen van prestatiemeteritems van Linux- en Windows-computers</span><span class="sxs-lookup"><span data-stu-id="3a55e-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="3a55e-113">Gebeurtenissen verzamelen van syslog op Linux-computers</span><span class="sxs-lookup"><span data-stu-id="3a55e-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="3a55e-114">Verzamelen van gebeurtenissen van Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="3a55e-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="3a55e-115">Aangepaste logboeken verzamelen</span><span class="sxs-lookup"><span data-stu-id="3a55e-115">Collect custom event logs</span></span>
* <span data-ttu-id="3a55e-116">Log analytics agent toevoegen aan een virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="3a55e-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="3a55e-117">Log analytics om gegevens te indexeren verzameld met behulp van Azure diagnostics configureren</span><span class="sxs-lookup"><span data-stu-id="3a55e-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="3a55e-118">Dit artikel bevat twee codevoorbeelden die illustratie van enkele van de functies die u vanuit PowerShell uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="3a55e-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="3a55e-119">U kunt verwijzen naar de [Log Analytics PowerShell-cmdlet-verwijzing](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor andere functies.</span><span class="sxs-lookup"><span data-stu-id="3a55e-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="3a55e-120">Log Analytics is eerder aangeroepen voor operationeel inzicht, dat is waarom dit de naam in de cmdlets gebruikt is.</span><span class="sxs-lookup"><span data-stu-id="3a55e-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3a55e-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a55e-121">Prerequisites</span></span>
<span data-ttu-id="3a55e-122">Deze voorbeelden werkt met versie 2.3.0 of hoger van de module AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="3a55e-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="3a55e-123">Maak en configureer een Log Analytics-werkruimte</span><span class="sxs-lookup"><span data-stu-id="3a55e-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="3a55e-124">Het volgende voorbeeldscript ziet u hoe:</span><span class="sxs-lookup"><span data-stu-id="3a55e-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="3a55e-125">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="3a55e-125">Create a workspace</span></span>
2. <span data-ttu-id="3a55e-126">Lijst van beschikbare oplossingen</span><span class="sxs-lookup"><span data-stu-id="3a55e-126">List the available solutions</span></span>
3. <span data-ttu-id="3a55e-127">Oplossingen toevoegen aan de werkruimte</span><span class="sxs-lookup"><span data-stu-id="3a55e-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="3a55e-128">Importeren opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="3a55e-128">Import saved searches</span></span>
5. <span data-ttu-id="3a55e-129">Export opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="3a55e-129">Export saved searches</span></span>
6. <span data-ttu-id="3a55e-130">Maak een computergroep</span><span class="sxs-lookup"><span data-stu-id="3a55e-130">Create a computer group</span></span>
7. <span data-ttu-id="3a55e-131">Verzamelen van IIS-logboeken van computers met de Windows-agent die is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="3a55e-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="3a55e-132">Verzamelen van prestatiemeteritems voor logische schijf van Linux-computers (% gebruikte Inodes Beschikbare Megabytes; Percentage gebruikte ruimte; Schijfoverdrachten per seconde; Schijf lezen per seconde; Schijf schrijven per seconde)</span><span class="sxs-lookup"><span data-stu-id="3a55e-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="3a55e-133">Syslog-gebeurtenissen verzamelen van Linux-computers</span><span class="sxs-lookup"><span data-stu-id="3a55e-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="3a55e-134">Fout- en waarschuwingsberichten gebeurtenissen verzamelen uit het gebeurtenislogboek van toepassing op Windows-computers</span><span class="sxs-lookup"><span data-stu-id="3a55e-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="3a55e-135">Beschikbaar geheugen in megabytes-prestatiemeteritem verzamelen van Windows-computers</span><span class="sxs-lookup"><span data-stu-id="3a55e-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="3a55e-136">Een aangepaste logboekgegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="3a55e-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="3a55e-137">Log Analytics index van Azure diagnostics configureren</span><span class="sxs-lookup"><span data-stu-id="3a55e-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="3a55e-138">Voor de bewaking zonder agents van Azure-resources, moeten de resources Azure diagnostics ingeschakeld en geconfigureerd voor het schrijven naar een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="3a55e-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="3a55e-139">Deze methode verzendt gegevens rechtstreeks naar het Log Analytics en vereist geen gegevens naar een opslagaccount worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="3a55e-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="3a55e-140">Ondersteunde resources omvatten:</span><span class="sxs-lookup"><span data-stu-id="3a55e-140">Supported resources include:</span></span>

| <span data-ttu-id="3a55e-141">Resourcetype</span><span class="sxs-lookup"><span data-stu-id="3a55e-141">Resource Type</span></span> | <span data-ttu-id="3a55e-142">Logboeken</span><span class="sxs-lookup"><span data-stu-id="3a55e-142">Logs</span></span> | <span data-ttu-id="3a55e-143">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="3a55e-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a55e-144">Toepassingsgateways</span><span class="sxs-lookup"><span data-stu-id="3a55e-144">Application Gateways</span></span>    | <span data-ttu-id="3a55e-145">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-145">Yes</span></span> | <span data-ttu-id="3a55e-146">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-146">Yes</span></span> |
| <span data-ttu-id="3a55e-147">Automation-accounts</span><span class="sxs-lookup"><span data-stu-id="3a55e-147">Automation accounts</span></span>     | <span data-ttu-id="3a55e-148">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-148">Yes</span></span> | |
| <span data-ttu-id="3a55e-149">Batch-accounts</span><span class="sxs-lookup"><span data-stu-id="3a55e-149">Batch accounts</span></span>          | <span data-ttu-id="3a55e-150">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-150">Yes</span></span> | <span data-ttu-id="3a55e-151">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-151">Yes</span></span> |
| <span data-ttu-id="3a55e-152">Data Lake analytics</span><span class="sxs-lookup"><span data-stu-id="3a55e-152">Data Lake analytics</span></span>     | <span data-ttu-id="3a55e-153">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-153">Yes</span></span> | | 
| <span data-ttu-id="3a55e-154">Data Lake store</span><span class="sxs-lookup"><span data-stu-id="3a55e-154">Data Lake store</span></span>         | <span data-ttu-id="3a55e-155">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-155">Yes</span></span> | |
| <span data-ttu-id="3a55e-156">Elastische SQL-groep</span><span class="sxs-lookup"><span data-stu-id="3a55e-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="3a55e-157">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-157">Yes</span></span> |
| <span data-ttu-id="3a55e-158">Event Hub-naamruimte</span><span class="sxs-lookup"><span data-stu-id="3a55e-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="3a55e-159">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-159">Yes</span></span> |
| <span data-ttu-id="3a55e-160">IoT-Hubs</span><span class="sxs-lookup"><span data-stu-id="3a55e-160">IoT Hubs</span></span>                |     | <span data-ttu-id="3a55e-161">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-161">Yes</span></span> |
| <span data-ttu-id="3a55e-162">Key Vault</span><span class="sxs-lookup"><span data-stu-id="3a55e-162">Key Vault</span></span>               | <span data-ttu-id="3a55e-163">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-163">Yes</span></span> | |
| <span data-ttu-id="3a55e-164">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="3a55e-164">Load Balancers</span></span>          | <span data-ttu-id="3a55e-165">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-165">Yes</span></span> | |
| <span data-ttu-id="3a55e-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3a55e-166">Logic Apps</span></span>              | <span data-ttu-id="3a55e-167">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-167">Yes</span></span> | <span data-ttu-id="3a55e-168">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-168">Yes</span></span> |
| <span data-ttu-id="3a55e-169">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="3a55e-169">Network Security Groups</span></span> | <span data-ttu-id="3a55e-170">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-170">Yes</span></span> | |
| <span data-ttu-id="3a55e-171">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="3a55e-171">Redis Cache</span></span>             |     | <span data-ttu-id="3a55e-172">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-172">Yes</span></span> |
| <span data-ttu-id="3a55e-173">Services zoeken</span><span class="sxs-lookup"><span data-stu-id="3a55e-173">Search services</span></span>         | <span data-ttu-id="3a55e-174">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-174">Yes</span></span> | <span data-ttu-id="3a55e-175">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-175">Yes</span></span> |
| <span data-ttu-id="3a55e-176">Service Bus-naamruimte</span><span class="sxs-lookup"><span data-stu-id="3a55e-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="3a55e-177">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-177">Yes</span></span> |
| <span data-ttu-id="3a55e-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="3a55e-178">SQL (v12)</span></span>               |     | <span data-ttu-id="3a55e-179">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-179">Yes</span></span> |
| <span data-ttu-id="3a55e-180">Web Sites</span><span class="sxs-lookup"><span data-stu-id="3a55e-180">Web Sites</span></span>               |     | <span data-ttu-id="3a55e-181">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-181">Yes</span></span> |
| <span data-ttu-id="3a55e-182">Webserver-farms</span><span class="sxs-lookup"><span data-stu-id="3a55e-182">Web Server farms</span></span>        |     | <span data-ttu-id="3a55e-183">Ja</span><span class="sxs-lookup"><span data-stu-id="3a55e-183">Yes</span></span> |

<span data-ttu-id="3a55e-184">Raadpleeg voor de details van de beschikbare metrische gegevens, [ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3a55e-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="3a55e-185">Raadpleeg voor de details van de beschikbare logboeken [ondersteund services en het schema voor diagnostische logboeken](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="3a55e-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="3a55e-186">U kunt ook de voorgaande cmdlet gebruiken voor het verzamelen van Logboeken van de resources die tot verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="3a55e-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="3a55e-187">De cmdlet kan werken voor abonnementen, omdat u de id van zowel de bron voor het maken van Logboeken en de werkruimte die de logboeken worden verzonden naar opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3a55e-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="3a55e-188">Log Analytics index van Azure diagnostics uit de opslag configureren</span><span class="sxs-lookup"><span data-stu-id="3a55e-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="3a55e-189">Voor het verzamelen van logboekgegevens van binnen een actief exemplaar van een klassieke cloudservice of een service fabric-cluster, moet u eerst de gegevens te schrijven naar Azure storage.</span><span class="sxs-lookup"><span data-stu-id="3a55e-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="3a55e-190">Log Analytics wordt vervolgens geconfigureerd voor het verzamelen van de logboeken van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a55e-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="3a55e-191">Ondersteunde resources omvatten:</span><span class="sxs-lookup"><span data-stu-id="3a55e-191">Supported resources include:</span></span>

* <span data-ttu-id="3a55e-192">Klassieke cloudservices (web- en werkrollen rollen)</span><span class="sxs-lookup"><span data-stu-id="3a55e-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="3a55e-193">Service fabric-clusters</span><span class="sxs-lookup"><span data-stu-id="3a55e-193">Service fabric clusters</span></span>

<span data-ttu-id="3a55e-194">Het volgende voorbeeld wordt getoond hoe:</span><span class="sxs-lookup"><span data-stu-id="3a55e-194">The following example shows how to:</span></span>

1. <span data-ttu-id="3a55e-195">Weergeven van de bestaande opslagaccounts en de locaties die logboekanalyse indexeert gegevens uit</span><span class="sxs-lookup"><span data-stu-id="3a55e-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="3a55e-196">Een configuratie lezen van een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="3a55e-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="3a55e-197">De zojuist gemaakte configuratie bijwerken om gegevens te indexeren van extra locaties</span><span class="sxs-lookup"><span data-stu-id="3a55e-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="3a55e-198">De zojuist gemaakte configuratie verwijderen</span><span class="sxs-lookup"><span data-stu-id="3a55e-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="3a55e-199">U kunt dit script ook gebruiken voor het verzamelen van Logboeken van opslagaccounts met verschillende abonnementen.</span><span class="sxs-lookup"><span data-stu-id="3a55e-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="3a55e-200">Het script is kunnen werken voor abonnementen, omdat u de resource-id van de storage-account en een bijbehorende toegangssleutel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3a55e-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="3a55e-201">Wanneer u de toegangssleutel wijzigt, moet u het inzicht opslag als u de nieuwe sleutel wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="3a55e-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3a55e-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a55e-202">Next steps</span></span>
* <span data-ttu-id="3a55e-203">[Bekijk Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor meer informatie over het gebruik van PowerShell voor de configuratie van logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="3a55e-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

