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
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="c7597-104">Log Analytics beheren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7597-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="c7597-105">U kunt Hallo [Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform diverse functies in logboekanalyse vanaf een opdrachtregel of als onderdeel van een script.</span><span class="sxs-lookup"><span data-stu-id="c7597-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="c7597-106">Voorbeelden van Hallo kunt u taken met PowerShell uitvoeren zijn:</span><span class="sxs-lookup"><span data-stu-id="c7597-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="c7597-107">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="c7597-107">Create a workspace</span></span>
* <span data-ttu-id="c7597-108">Toevoegen of verwijderen van een oplossing</span><span class="sxs-lookup"><span data-stu-id="c7597-108">Add or remove a solution</span></span>
* <span data-ttu-id="c7597-109">Importeren en exporteren van opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="c7597-109">Import and export saved searches</span></span>
* <span data-ttu-id="c7597-110">Maak een computergroep</span><span class="sxs-lookup"><span data-stu-id="c7597-110">Create a computer group</span></span>
* <span data-ttu-id="c7597-111">Verzamelen van IIS-logboeken van computers met Hallo Windows-agent is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="c7597-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="c7597-112">Verzamelen van prestatiemeteritems van Linux- en Windows-computers</span><span class="sxs-lookup"><span data-stu-id="c7597-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="c7597-113">Gebeurtenissen verzamelen van syslog op Linux-computers</span><span class="sxs-lookup"><span data-stu-id="c7597-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="c7597-114">Verzamelen van gebeurtenissen van Windows-gebeurtenislogboeken</span><span class="sxs-lookup"><span data-stu-id="c7597-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="c7597-115">Aangepaste logboeken verzamelen</span><span class="sxs-lookup"><span data-stu-id="c7597-115">Collect custom event logs</span></span>
* <span data-ttu-id="c7597-116">Hallo log analytics agent tooan Azure virtuele machine toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7597-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="c7597-117">Log analytics-tooindex gegevens verzameld met behulp van Azure diagnostics configureren</span><span class="sxs-lookup"><span data-stu-id="c7597-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="c7597-118">Dit artikel bevat twee codevoorbeelden die illustratie van enkele Hallo-functies die u vanuit PowerShell uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="c7597-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="c7597-119">U kunt verwijzen toohello [Log Analytics PowerShell-cmdlet-verwijzing](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor andere functies.</span><span class="sxs-lookup"><span data-stu-id="c7597-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="c7597-120">Log Analytics is eerder aangeroepen voor operationeel inzicht, die daarom is het Hallo-naam die wordt gebruikt in Hallo-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="c7597-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c7597-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c7597-121">Prerequisites</span></span>
<span data-ttu-id="c7597-122">Deze voorbeelden werkt met versie 2.3.0 of hoger van Hallo AzureRm.OperationalInsights module.</span><span class="sxs-lookup"><span data-stu-id="c7597-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="c7597-123">Maak en configureer een Log Analytics-werkruimte</span><span class="sxs-lookup"><span data-stu-id="c7597-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="c7597-124">Hallo volgende voorbeeldscript ziet u hoe:</span><span class="sxs-lookup"><span data-stu-id="c7597-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="c7597-125">Een werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="c7597-125">Create a workspace</span></span>
2. <span data-ttu-id="c7597-126">Lijst Hallo beschikbare oplossingen</span><span class="sxs-lookup"><span data-stu-id="c7597-126">List hello available solutions</span></span>
3. <span data-ttu-id="c7597-127">Oplossingen toohello werkruimte toevoegen</span><span class="sxs-lookup"><span data-stu-id="c7597-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="c7597-128">Importeren opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="c7597-128">Import saved searches</span></span>
5. <span data-ttu-id="c7597-129">Export opgeslagen zoekopdrachten</span><span class="sxs-lookup"><span data-stu-id="c7597-129">Export saved searches</span></span>
6. <span data-ttu-id="c7597-130">Maak een computergroep</span><span class="sxs-lookup"><span data-stu-id="c7597-130">Create a computer group</span></span>
7. <span data-ttu-id="c7597-131">Verzamelen van IIS-logboeken van computers met Hallo Windows-agent is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="c7597-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="c7597-132">Verzamelen van prestatiemeteritems voor logische schijf van Linux-computers (% gebruikte Inodes Beschikbare Megabytes; Percentage gebruikte ruimte; Schijfoverdrachten per seconde; Schijf lezen per seconde; Schijf schrijven per seconde)</span><span class="sxs-lookup"><span data-stu-id="c7597-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="c7597-133">Syslog-gebeurtenissen verzamelen van Linux-computers</span><span class="sxs-lookup"><span data-stu-id="c7597-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="c7597-134">Fout- en waarschuwingsberichten gebeurtenissen verzamelen van Hallo gebeurtenislogboek van toepassing op Windows-computers</span><span class="sxs-lookup"><span data-stu-id="c7597-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="c7597-135">Beschikbaar geheugen in megabytes-prestatiemeteritem verzamelen van Windows-computers</span><span class="sxs-lookup"><span data-stu-id="c7597-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="c7597-136">Een aangepaste logboekgegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="c7597-136">Collect a custom log</span></span> 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="c7597-137">Log Analytics tooindex Azure diagnostics configureren</span><span class="sxs-lookup"><span data-stu-id="c7597-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="c7597-138">Hallo resources moeten voor bewaking zonder agents van Azure-resources, toohave Azure diagnostics is ingeschakeld en geconfigureerd toowrite tooa Log Analytics-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c7597-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="c7597-139">Deze methode verzendt gegevens rechtstreeks tooLog Analytics en vereist geen gegevens toobe tooa storage-account geschreven.</span><span class="sxs-lookup"><span data-stu-id="c7597-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="c7597-140">Ondersteunde resources omvatten:</span><span class="sxs-lookup"><span data-stu-id="c7597-140">Supported resources include:</span></span>

| <span data-ttu-id="c7597-141">Resourcetype</span><span class="sxs-lookup"><span data-stu-id="c7597-141">Resource Type</span></span> | <span data-ttu-id="c7597-142">Logboeken</span><span class="sxs-lookup"><span data-stu-id="c7597-142">Logs</span></span> | <span data-ttu-id="c7597-143">Metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="c7597-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c7597-144">Toepassingsgateways</span><span class="sxs-lookup"><span data-stu-id="c7597-144">Application Gateways</span></span>    | <span data-ttu-id="c7597-145">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-145">Yes</span></span> | <span data-ttu-id="c7597-146">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-146">Yes</span></span> |
| <span data-ttu-id="c7597-147">Automation-accounts</span><span class="sxs-lookup"><span data-stu-id="c7597-147">Automation accounts</span></span>     | <span data-ttu-id="c7597-148">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-148">Yes</span></span> | |
| <span data-ttu-id="c7597-149">Batch-accounts</span><span class="sxs-lookup"><span data-stu-id="c7597-149">Batch accounts</span></span>          | <span data-ttu-id="c7597-150">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-150">Yes</span></span> | <span data-ttu-id="c7597-151">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-151">Yes</span></span> |
| <span data-ttu-id="c7597-152">Data Lake analytics</span><span class="sxs-lookup"><span data-stu-id="c7597-152">Data Lake analytics</span></span>     | <span data-ttu-id="c7597-153">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-153">Yes</span></span> | | 
| <span data-ttu-id="c7597-154">Data Lake store</span><span class="sxs-lookup"><span data-stu-id="c7597-154">Data Lake store</span></span>         | <span data-ttu-id="c7597-155">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-155">Yes</span></span> | |
| <span data-ttu-id="c7597-156">Elastische SQL-groep</span><span class="sxs-lookup"><span data-stu-id="c7597-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="c7597-157">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-157">Yes</span></span> |
| <span data-ttu-id="c7597-158">Event Hub-naamruimte</span><span class="sxs-lookup"><span data-stu-id="c7597-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="c7597-159">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-159">Yes</span></span> |
| <span data-ttu-id="c7597-160">IoT-Hubs</span><span class="sxs-lookup"><span data-stu-id="c7597-160">IoT Hubs</span></span>                |     | <span data-ttu-id="c7597-161">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-161">Yes</span></span> |
| <span data-ttu-id="c7597-162">Key Vault</span><span class="sxs-lookup"><span data-stu-id="c7597-162">Key Vault</span></span>               | <span data-ttu-id="c7597-163">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-163">Yes</span></span> | |
| <span data-ttu-id="c7597-164">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="c7597-164">Load Balancers</span></span>          | <span data-ttu-id="c7597-165">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-165">Yes</span></span> | |
| <span data-ttu-id="c7597-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="c7597-166">Logic Apps</span></span>              | <span data-ttu-id="c7597-167">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-167">Yes</span></span> | <span data-ttu-id="c7597-168">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-168">Yes</span></span> |
| <span data-ttu-id="c7597-169">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="c7597-169">Network Security Groups</span></span> | <span data-ttu-id="c7597-170">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-170">Yes</span></span> | |
| <span data-ttu-id="c7597-171">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="c7597-171">Redis Cache</span></span>             |     | <span data-ttu-id="c7597-172">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-172">Yes</span></span> |
| <span data-ttu-id="c7597-173">Services zoeken</span><span class="sxs-lookup"><span data-stu-id="c7597-173">Search services</span></span>         | <span data-ttu-id="c7597-174">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-174">Yes</span></span> | <span data-ttu-id="c7597-175">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-175">Yes</span></span> |
| <span data-ttu-id="c7597-176">Service Bus-naamruimte</span><span class="sxs-lookup"><span data-stu-id="c7597-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="c7597-177">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-177">Yes</span></span> |
| <span data-ttu-id="c7597-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="c7597-178">SQL (v12)</span></span>               |     | <span data-ttu-id="c7597-179">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-179">Yes</span></span> |
| <span data-ttu-id="c7597-180">Web Sites</span><span class="sxs-lookup"><span data-stu-id="c7597-180">Web Sites</span></span>               |     | <span data-ttu-id="c7597-181">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-181">Yes</span></span> |
| <span data-ttu-id="c7597-182">Webserver-farms</span><span class="sxs-lookup"><span data-stu-id="c7597-182">Web Server farms</span></span>        |     | <span data-ttu-id="c7597-183">Ja</span><span class="sxs-lookup"><span data-stu-id="c7597-183">Yes</span></span> |

<span data-ttu-id="c7597-184">Raadpleeg te voor details van de beschikbare metrische gegevens Hallo Hallo[ondersteund met een Azure-Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c7597-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="c7597-185">Raadpleeg te voor details van de beschikbare logboeken Hallo Hallo[ondersteund services en het schema voor diagnostische logboeken](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="c7597-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="c7597-186">U kunt ook Hallo voorafgaand aan de cmdlet toocollect logboeken van de resources die tot verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="c7597-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="c7597-187">Hallo-cmdlet is kunnen toowork voor abonnementen, omdat u biedt Hallo-id van beide Hallo-resource maken van Logboeken en Hallo werkruimte Hallo logboeken worden verzonden naar.</span><span class="sxs-lookup"><span data-stu-id="c7597-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="c7597-188">Log Analytics tooindex Azure diagnostische gegevens van opslag configureren</span><span class="sxs-lookup"><span data-stu-id="c7597-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="c7597-189">toocollect logboekgegevens vanuit een actief exemplaar van een klassieke cloudservice of een service fabric-cluster, moet u toofirst schrijven Hallo-gegevensopslag tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c7597-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="c7597-190">Log Analytics wordt vervolgens geconfigureerd toocollect Hallo logboeken van Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="c7597-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="c7597-191">Ondersteunde resources omvatten:</span><span class="sxs-lookup"><span data-stu-id="c7597-191">Supported resources include:</span></span>

* <span data-ttu-id="c7597-192">Klassieke cloudservices (web- en werkrollen rollen)</span><span class="sxs-lookup"><span data-stu-id="c7597-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="c7597-193">Service fabric-clusters</span><span class="sxs-lookup"><span data-stu-id="c7597-193">Service fabric clusters</span></span>

<span data-ttu-id="c7597-194">Hallo volgende voorbeeld ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="c7597-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="c7597-195">Hallo bestaande opslagaccounts en de locaties die logboekanalyse indexeert gegevens uit lijst</span><span class="sxs-lookup"><span data-stu-id="c7597-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="c7597-196">Een tooread configuratie van een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="c7597-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="c7597-197">Hallo nieuw gemaakte tooindex configuratiegegevens van extra locaties bijwerken</span><span class="sxs-lookup"><span data-stu-id="c7597-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="c7597-198">Hallo nieuw gemaakte configuratie verwijderen</span><span class="sxs-lookup"><span data-stu-id="c7597-198">Delete hello newly created configuration</span></span>

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

<span data-ttu-id="c7597-199">U kunt ook Hallo vóór het script toocollect logboeken van de storage-accounts in verschillende abonnementen behoren.</span><span class="sxs-lookup"><span data-stu-id="c7597-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="c7597-200">Hallo-script is kunnen toowork voor abonnementen, omdat u Hallo storage account resource-id en een bijbehorende toegangssleutel opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c7597-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="c7597-201">Wanneer u de toegangssleutel Hallo wijzigt, moet u tooupdate Hallo opslag inzicht toohave Hallo nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="c7597-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7597-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c7597-202">Next steps</span></span>
* <span data-ttu-id="c7597-203">[Bekijk Log Analytics PowerShell-cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) voor meer informatie over het gebruik van PowerShell voor de configuratie van logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="c7597-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

