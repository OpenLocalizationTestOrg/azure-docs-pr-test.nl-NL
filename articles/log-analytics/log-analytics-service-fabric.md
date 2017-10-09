---
title: aaaAssess Service Fabric-toepassingen met Azure Log Analytics met behulp van PowerShell | Microsoft Docs
description: Hallo Service Fabric-oplossing kunt u in met behulp van PowerShell tooassess Hallo risico en status van uw Service Fabric-toepassingen, micro-services, knooppunten en clusters logboekanalyse.
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="f8382-103">Evalueer Azure Service Fabric-toepassingen en micro-services met PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8382-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8382-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f8382-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="f8382-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8382-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Service Fabric symbool](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="f8382-107">Dit artikel wordt beschreven hoe toouse Hallo Service Fabric-oplossing in logboekanalyse toohelp identificeren en oplossen van problemen in uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8382-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="f8382-108">Kunt u zien hoe uw Service Fabric-knooppunten uitvoert en hoe uw toepassingen en micro-services worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f8382-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="f8382-109">Hallo Service Fabric-oplossing gebruikt Azure Diagnostics-gegevens van uw virtuele machines van Service Fabric door het verzamelen van deze gegevens uit uw af van de Azure-tabellen.</span><span class="sxs-lookup"><span data-stu-id="f8382-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="f8382-110">Log Analytics leest vervolgens Hallo Service Fabric framework gebeurtenissen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8382-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="f8382-111">**Gebeurtenissen van betrouwbare Service**</span><span class="sxs-lookup"><span data-stu-id="f8382-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="f8382-112">**Actor-gebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="f8382-112">**Actor Events**</span></span>
- <span data-ttu-id="f8382-113">**Operationele gebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="f8382-113">**Operational Events**</span></span>
- <span data-ttu-id="f8382-114">**Aangepaste ETW-gebeurtenissen**</span><span class="sxs-lookup"><span data-stu-id="f8382-114">**Custom ETW events**</span></span>

<span data-ttu-id="f8382-115">Hallo Service Fabric-oplossing dashboard ziet u problemen die aandacht vereisen en relevante gebeurtenissen in uw omgeving Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f8382-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="f8382-116">Installeren en configureren van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="f8382-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="f8382-117">Volg deze drie eenvoudige stappen tooinstall en Hallo oplossing configureren:</span><span class="sxs-lookup"><span data-stu-id="f8382-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="f8382-118">Hello Azure-abonnement dat u toocreate alle clusterbronnen gebruikt, met inbegrip van storage-accounts met uw werkruimte koppelen.</span><span class="sxs-lookup"><span data-stu-id="f8382-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="f8382-119">Zie [aan de slag met logboekanalyse](log-analytics-get-started.md) voor informatie over het maken van een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="f8382-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="f8382-120">Log Analytics toocollect configureren en weergeven van Service Fabric-Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f8382-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="f8382-121">Hallo Service Fabric-oplossing in uw werkruimte inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f8382-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="f8382-122">Log Analytics toocollect configureren en weergeven van Service Fabric-Logboeken</span><span class="sxs-lookup"><span data-stu-id="f8382-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="f8382-123">In deze sectie leert u hoe tooconfigure logboekanalyse tooretrieve Service Fabric registreert.</span><span class="sxs-lookup"><span data-stu-id="f8382-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="f8382-124">Hallo-logboeken kunnen u tooview, analyseren en oplossen van problemen in uw cluster of in het Hallo-toepassingen en services die worden uitgevoerd in het cluster, met behulp van Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="f8382-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f8382-125">Hello Azure Diagnostics extensie tooupload Hallo logboeken voor storage-tabellen configureren.</span><span class="sxs-lookup"><span data-stu-id="f8382-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="f8382-126">Hallo tabellen moeten overeenkomen met wat logboekanalyse zoekt.</span><span class="sxs-lookup"><span data-stu-id="f8382-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="f8382-127">Zie voor meer informatie [hoe toocollect registreert met Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="f8382-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="f8382-128">Voorbeelden van Hallo configuratie-instellingen in dit artikel u welke namen Hallo Hallo opslag tabellen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f8382-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="f8382-129">Zodra de diagnostische gegevens is ingesteld op Hallo-cluster en logboeken tooa storage-account is geüpload, de volgende stap Hallo tooconfigure logboekanalyse toocollect is deze logboeken.</span><span class="sxs-lookup"><span data-stu-id="f8382-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="f8382-130">Zorg ervoor dat u Hallo bijwerken **EtwEventSourceProviderConfiguration** sectie in Hallo **template.json** tooadd vermeldingen voor nieuwe EventSources voordat u Hallo configuratie toepassen bij te werken Hallo bestand met **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="f8382-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="f8382-131">Hallo-tabel voor het uploaden is Hallo dezelfde als (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="f8382-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="f8382-132">Hallo-momenteel logboekanalyse kunnen alleen lezen toepassing ETW-gebeurtenissen van Hallo *WADETWEventTable* tabel.</span><span class="sxs-lookup"><span data-stu-id="f8382-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="f8382-133">Hallo volgende hulpprogramma's zijn gebruikte tooperform aantal Hallo-bewerkingen in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="f8382-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="f8382-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8382-134">Azure PowerShell</span></span>
* [<span data-ttu-id="f8382-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f8382-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="f8382-136">Een Log Analytics werkruimte tooshow Hallo cluster logboeken configureren</span><span class="sxs-lookup"><span data-stu-id="f8382-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="f8382-137">Nadat u een werkruimte voor logboekanalyse maakt, configureert u Hallo werkruimte toopull logboeken van hello Azure storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="f8382-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="f8382-138">Voer vervolgens de volgende PowerShell-script Hallo:</span><span class="sxs-lookup"><span data-stu-id="f8382-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="f8382-139">Nadat u hebt geconfigureerd Hallo logboekanalyse werkruimte tooread van hello Azure tabellen in uw opslagaccount toohello Azure-portal aanmelden.</span><span class="sxs-lookup"><span data-stu-id="f8382-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="f8382-140">Selecteer Hallo werkruimte voor logboekanalyse van **alle Resources**.</span><span class="sxs-lookup"><span data-stu-id="f8382-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="f8382-141">Hallo aantal storage account logboeken verbonden toohello werkruimte wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f8382-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="f8382-142">Selecteer Hallo **Storage account logboeken** tegel.</span><span class="sxs-lookup"><span data-stu-id="f8382-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="f8382-143">Bekijk de lijst Hallo met storage-account logboeken tooverify dat uw storage-account de juiste werkruimte verbonden toohello is.</span><span class="sxs-lookup"><span data-stu-id="f8382-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Storage-account Logboeken](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="f8382-145">Hallo Service Fabric-oplossing inschakelen</span><span class="sxs-lookup"><span data-stu-id="f8382-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="f8382-146">Gebruik Hallo script tooadd Hallo oplossing tooyour Log Analytics-werkruimte te volgen.</span><span class="sxs-lookup"><span data-stu-id="f8382-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="f8382-147">Hallo-script uitvoeren in met behulp van hello Azure-abonnement dat is gekoppeld aan de werkruimte voor logboekanalyse Hallo die u wilt tooenable Hallo Service Fabric-oplossing in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8382-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="f8382-148">Nadat u Hallo oplossing hebt ingeschakeld, Hallo Service Fabric-tegel tooyour logboekanalyse is toegevoegd *overzicht* pagina.</span><span class="sxs-lookup"><span data-stu-id="f8382-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="f8382-149">Hallo pagina bevat een overzicht van problemen die aandacht vereisen zoals runAsync fouten en annuleringen dat is opgetreden in Hallo afgelopen 24 uur.</span><span class="sxs-lookup"><span data-stu-id="f8382-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Service Fabric-tegel](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="f8382-151">Service Fabric-gebeurtenissen weergeven</span><span class="sxs-lookup"><span data-stu-id="f8382-151">View Service Fabric events</span></span>
<span data-ttu-id="f8382-152">Klik op Hallo **Service Fabric** tegel tooopen Hallo Service Fabric dashboard.</span><span class="sxs-lookup"><span data-stu-id="f8382-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="f8382-153">Hallo dashboard bevat Hallo kolommen in de onderstaande tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8382-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="f8382-154">Elke kolom bevat Hallo bovenste 10 gebeurtenissen door het aantal die overeenkomt met dat van de kolom criteria voor Hallo tijdbereik opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f8382-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="f8382-155">U kunt een zoekopdracht logboek waarmee de volledige lijst Hallo door te klikken op uitvoeren **alle** onderin Hallo rechts van elke kolom, of door te klikken op de kolomkop Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8382-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="f8382-156">**Service Fabric-gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="f8382-156">**Service Fabric event**</span></span> | <span data-ttu-id="f8382-157">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="f8382-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="f8382-158">Problemen die aandacht vereisen</span><span class="sxs-lookup"><span data-stu-id="f8382-158">Notable Issues</span></span> | <span data-ttu-id="f8382-159">Hiermee problemen, inclusief RunAsyncFailures RunAsynCancellations en keuzelijsten knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f8382-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="f8382-160">Operationele gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f8382-160">Operational Events</span></span> | <span data-ttu-id="f8382-161">Bevat opmerkelijke operationele gebeurtenissen, met inbegrip van de upgrade van de toepassing en implementaties.</span><span class="sxs-lookup"><span data-stu-id="f8382-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="f8382-162">Gebeurtenissen van betrouwbare Service</span><span class="sxs-lookup"><span data-stu-id="f8382-162">Reliable Service Events</span></span> | <span data-ttu-id="f8382-163">Bevat opmerkelijke betrouwbare servicegebeurtenissen, met inbegrip van Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="f8382-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="f8382-164">Actor-gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f8382-164">Actor Events</span></span> | <span data-ttu-id="f8382-165">Bevat belangrijke actor-gebeurtenissen die worden gegenereerd door uw micro-services.</span><span class="sxs-lookup"><span data-stu-id="f8382-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="f8382-166">Gebeurtenissen zijn uitzonderingen worden veroorzaakt door een actormethode, actor-activeringen en deactivations, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="f8382-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="f8382-167">Toepassingsgebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f8382-167">Application Events</span></span> | <span data-ttu-id="f8382-168">Bevat alle aangepaste ETW-gebeurtenissen die worden gegenereerd door uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f8382-168">Displays all custom ETW events generated by your applications.</span></span> |

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric-dashboard](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="f8382-171">Hallo volgende tabel bevat de methoden van de collectie en andere informatie over hoe gegevens worden verzameld voor Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="f8382-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="f8382-172">Platform</span><span class="sxs-lookup"><span data-stu-id="f8382-172">platform</span></span> | <span data-ttu-id="f8382-173">Directe Agent</span><span class="sxs-lookup"><span data-stu-id="f8382-173">Direct Agent</span></span> | <span data-ttu-id="f8382-174">Operations Manager-agent</span><span class="sxs-lookup"><span data-stu-id="f8382-174">Operations Manager agent</span></span> | <span data-ttu-id="f8382-175">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f8382-175">Azure Storage</span></span> | <span data-ttu-id="f8382-176">Operations Manager is vereist?</span><span class="sxs-lookup"><span data-stu-id="f8382-176">Operations Manager required?</span></span> | <span data-ttu-id="f8382-177">Operations Manager-agent gegevens verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="f8382-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="f8382-178">Frequentie van de verzameling</span><span class="sxs-lookup"><span data-stu-id="f8382-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f8382-179">Windows</span><span class="sxs-lookup"><span data-stu-id="f8382-179">Windows</span></span> |  |  | <span data-ttu-id="f8382-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="f8382-180">&#8226;</span></span> |  |  |<span data-ttu-id="f8382-181">10 minuten</span><span class="sxs-lookup"><span data-stu-id="f8382-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="f8382-182">Hallo-bereik van gebeurtenissen met de wijzigen **gegevens op basis van de afgelopen zeven dagen** Hallo boven aan het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f8382-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="f8382-183">U kunt ook gebeurtenissen gegenereerd binnen Hallo afgelopen zeven dagen een dag of zes uur weergeven.</span><span class="sxs-lookup"><span data-stu-id="f8382-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="f8382-184">U kunt ook selecteren **aangepaste** toospecify een aangepast datumbereik.</span><span class="sxs-lookup"><span data-stu-id="f8382-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="f8382-185">Problemen met configuratie van de Service Fabric en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f8382-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="f8382-186">Als u tooverify uw Log Analytics-configuratie moet omdat u de gebeurtenisgegevens kan geen tooview in Log Analytics, gebruikt u Hallo script te volgen.</span><span class="sxs-lookup"><span data-stu-id="f8382-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="f8382-187">Hallo van de volgende activiteiten worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f8382-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="f8382-188">De configuratie van uw Service Fabric-diagnostische leest</span><span class="sxs-lookup"><span data-stu-id="f8382-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="f8382-189">Controleert op gegevens die zijn geschreven in Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="f8382-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="f8382-190">Verifieert of Log Analytics geconfigureerde tooread uit Hallo tabellen</span><span class="sxs-lookup"><span data-stu-id="f8382-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="f8382-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8382-191">Next steps</span></span>
* <span data-ttu-id="f8382-192">Gebruik [logboek van zoekopdrachten in logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor Service Fabric-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f8382-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
