---
title: analyse van aaaLog voor Azure CDN | Microsoft Docs
description: De klant kunt logboekanalyse inschakelen voor Azure CDN.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="31cc6-103">Diagnostische logboeken voor Azure CDN</span><span class="sxs-lookup"><span data-stu-id="31cc6-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="31cc6-104">Nadat de CDN is ingeschakeld voor uw toepassing, wordt u waarschijnlijk wilt toomonitor Hallo CDN gebruik, Controleer de status van uw levering Hallo en mogelijke problemen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="31cc6-105">Azure CDN biedt deze mogelijkheden met [CDN basisanalyse](cdn-analyze-usage-patterns.md) en [diagnostische logboeken](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span><span class="sxs-lookup"><span data-stu-id="31cc6-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="31cc6-106">CDN-basisanalyse</span><span class="sxs-lookup"><span data-stu-id="31cc6-106">CDN Core Analytics</span></span>
<span data-ttu-id="31cc6-107">Als een huidige Azure CDN-gebruiker met Verizon standard of premium-profiel bent u al basisanalyse kunnen tooview in Hallo aanvullende portal toegankelijk via 'Beheren' Hallo-optie van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="31cc6-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="31cc6-108">Azure diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="31cc6-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="31cc6-109">Azure met deze nieuwe functie, u kunt nu zien basisanalyse en deze opslaan in een of meer bestemmingen, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="31cc6-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="31cc6-110">Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="31cc6-110">Azure Storage account</span></span>
 - <span data-ttu-id="31cc6-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="31cc6-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="31cc6-112">De opslagplaats OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="31cc6-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="31cc6-113">Deze functie is beschikbaar voor alle CDN-eindpunten die behoren tooVerizon (Standard en Premium) en CDN-profielen van Akamai (standaard).</span><span class="sxs-lookup"><span data-stu-id="31cc6-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="31cc6-114">Logboeken met diagnostische gegevens kunnen u tooexport basisgebruik metrische gegevens van uw CDN-eindpunt tooa verschillende bronnen, zodat u ze in een aangepaste manier gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="31cc6-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="31cc6-115">Bijvoorbeeld, u kunt doen Hallo volgende soorten gegevens exporteren:</span><span class="sxs-lookup"><span data-stu-id="31cc6-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="31cc6-116">Gegevensopslag tooblob exporteren, tooCSV exporteren en grafieken genereren in excel.</span><span class="sxs-lookup"><span data-stu-id="31cc6-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="31cc6-117">Exporteer gegevens tooevent hubs en correleren met gegevens van andere azure-services.</span><span class="sxs-lookup"><span data-stu-id="31cc6-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="31cc6-118">Exporteren van gegevens toolog analytics weergave gegevens en in uw eigen OMS-werkruimte</span><span class="sxs-lookup"><span data-stu-id="31cc6-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="31cc6-119">Hallo toont volgende afbeelding een typische basisanalyse CDN-overzicht van gegevens.</span><span class="sxs-lookup"><span data-stu-id="31cc6-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="31cc6-121">*Afbeelding 1: CDN basisanalyse weergeven*</span><span class="sxs-lookup"><span data-stu-id="31cc6-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="31cc6-122">Hallo volgen stapsgewijze Kennismaking gaat door het Hallo-schema van Hallo core analytische gegevens, stappen voor het Hallo-functie inschakelen en gebruiken van deze bestemmingen leveren van toovarious bestemmingen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="31cc6-123">Inschakelen van logboekregistratie met Azure-portal</span><span class="sxs-lookup"><span data-stu-id="31cc6-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="31cc6-124">Hallo diagnostische logboeken zijn ingeschakeld **uit** standaard.</span><span class="sxs-lookup"><span data-stu-id="31cc6-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="31cc6-125">Hallo stappen hieronder tooenable logboekregistratie met CDN basisanalyse:</span><span class="sxs-lookup"><span data-stu-id="31cc6-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="31cc6-126">Meld u aan toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31cc6-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="31cc6-127">Als u nog niet ingeschakeld voor uw werkstroom CDN hebt [Azure CDN inschakelen](cdn-create-new-endpoint.md) voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="31cc6-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="31cc6-128">Navigeer te in Hallo portal**CDN-profiel**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="31cc6-129">Selecteer een CDN-profiel en vervolgens Hallo CDN-eindpunt dat u wilt dat tooenable **diagnostische logboeken**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="31cc6-131">Ga te**diagnostische logboeken** blade onder **bewaking** sectie en klik vervolgens op Hallo status te**op**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="31cc6-133">Logboekregistratie met Azure Storage inschakelen</span><span class="sxs-lookup"><span data-stu-id="31cc6-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="31cc6-134">Selecteer toouse Azure Storage toostore Hallo logboeken **archiveren tooa storage-account**, selecteer de dagen bewaren en op **CoreAnalytics** onder **logboek**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="31cc6-136">*Afbeelding 2 - logboekregistratie met Azure Storage*</span><span class="sxs-lookup"><span data-stu-id="31cc6-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="31cc6-137">Logboekregistratie met OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="31cc6-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="31cc6-138">toouse OMS Log Analytics toostore Hallo Logboeken als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="31cc6-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="31cc6-139">Van Hallo **diagnostische logboeken** blade onder **bewaking**, selecteer **tooLog Analytics verzenden** uit</span><span class="sxs-lookup"><span data-stu-id="31cc6-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="31cc6-141">Hallo logboekanalyse logboekregistratie configureren door te klikken op configureren.</span><span class="sxs-lookup"><span data-stu-id="31cc6-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="31cc6-142">Hiermee gaat u tooa dialoogvenster kunt u een vorige werkruimte selecteren of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="31cc6-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="31cc6-144">Klik op **Maak nieuwe werkruimte**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-144">Click **Create New Workspace**.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="31cc6-146">Vervolgens moet u een nieuwe naam van de werkruimte, bestaande abonnement, resourcegroep (nieuwe of bestaande), locatie en prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="31cc6-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="31cc6-147">U hebt de optie Hallo van dit configuration tooyour dashboard vastmaken.</span><span class="sxs-lookup"><span data-stu-id="31cc6-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="31cc6-148">Klik op OK toocomplete Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="31cc6-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="31cc6-149">U ziet naast uw werkruimte met uw namen OMS-werkruimte en de Resource.</span><span class="sxs-lookup"><span data-stu-id="31cc6-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="31cc6-150">Namen moeten uniek zijn en gebruiken kunnen alleen letters, cijfers en afbreekstreepjes.</span><span class="sxs-lookup"><span data-stu-id="31cc6-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="31cc6-151">Spaties en onderstrepingstekens bevatten, zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="31cc6-151">Spaces and underscores are not allowed.</span></span> 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="31cc6-153">U wordt vervolgens een kort bericht vermeld dat uw werkruimte is gemaakt en u logboekregistratie van het Configuratiescherm tooyour worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="31cc6-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="31cc6-154">U kunt bevestigen Hallo-naam van de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="31cc6-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="31cc6-156">Als u een Hallo logboekanalyse configuratie hebt ingesteld, moet dat u ook selectievakje Hallo CoreAnalytics voor CDN-logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="31cc6-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="31cc6-157">Als alles tooyour eigen smaak, klikt u op Hallo **opslaan** knop Hallo boven aan het dialoogvenster Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="31cc6-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="31cc6-159">Hallo **opslaan** knop bestaat niet meer actief is en dat Hallo in/uit-knop is nu ingeschakeld, maar blauw in plaats van paars.</span><span class="sxs-lookup"><span data-stu-id="31cc6-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="31cc6-160">Als u wilt uw nieuwe OMS-werkruimte toosee, klik Ga tooyour Azure-portal-Dashboard Hallo-naam van de werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="31cc6-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="31cc6-161">Vervolgens ziet u uw werkruimte (Zorg ervoor dat de OMS-werkruimte is geselecteerd op Hallo links).</span><span class="sxs-lookup"><span data-stu-id="31cc6-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="31cc6-162">Klik op Hallo OMS-Portal tegel toosee uw werkruimte in Hallo OMS-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="31cc6-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![Portal - logboeken met diagnostische gegevens](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="31cc6-164">De OMS-opslagplaats is nu gereed toolog gegevens.</span><span class="sxs-lookup"><span data-stu-id="31cc6-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="31cc6-165">In volgorde tooconsume die gegevens, moet u een [OMS oplossing](#consuming-oms-log-analytics-data), gedekte verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="31cc6-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="31cc6-166">Ga voor meer informatie over het logboek gegevens vertragingen [hier](#log-data-delays).</span><span class="sxs-lookup"><span data-stu-id="31cc6-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="31cc6-167">Inschakelen van logboekregistratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="31cc6-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="31cc6-168">Hieronder volgt een voorbeeld van hoe tooenable en get diagnostische logboeken via hello Azure PowerShell-Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="31cc6-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="31cc6-169">Inschakelen van diagnostische logboeken in een Opslagaccount</span><span class="sxs-lookup"><span data-stu-id="31cc6-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="31cc6-170">Meldt u zich eerst en selecteer een abonnement:</span><span class="sxs-lookup"><span data-stu-id="31cc6-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="31cc6-171">logboeken met diagnostische gegevens in een Opslagaccount tooEnable Gebruik deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="31cc6-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="31cc6-172">tooEnable diagnostische logboeken in een OMS-werkruimte, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="31cc6-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="31cc6-173">Diagnostische logboeken van Azure Storage gebruiken</span><span class="sxs-lookup"><span data-stu-id="31cc6-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="31cc6-174">Deze sectie beschrijft Hallo-schema van Hallo CDN basisanalyse, hoe deze zijn ingedeeld binnen een Azure Storage-Account en biedt voorbeeld code toodownload Hallo Logboeken in tooa CSV-bestand.</span><span class="sxs-lookup"><span data-stu-id="31cc6-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="31cc6-175">Met behulp van Microsoft Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="31cc6-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="31cc6-176">Voordat u Hallo core analytische gegevens vanaf hello Azure Storage-Account openen kunt, moet u eerst een hulpprogramma tooaccess Hallo inhoud in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="31cc6-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="31cc6-177">Er zijn verschillende hulpprogramma's beschikbaar in de markt Hallo, is Hallo dat het is raadzaam Hallo Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="31cc6-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="31cc6-178">U kunt downloaden Hallo hulpprogramma van [hier](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="31cc6-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="31cc6-179">Nadat het Hallo-software downloaden en installeren configureert Hallo toouse hetzelfde Azure-Opslagaccount die is geconfigureerd als een bestemming toohello CDN diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="31cc6-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="31cc6-180">Open **Microsoft Azure Opslagverkenner**</span><span class="sxs-lookup"><span data-stu-id="31cc6-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="31cc6-181">Zoek Hallo storage-account</span><span class="sxs-lookup"><span data-stu-id="31cc6-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="31cc6-182">Ga toohello **'Blob-Containers'** knooppunt onder deze opslag account en het Hallo-knooppunt uitvouwen</span><span class="sxs-lookup"><span data-stu-id="31cc6-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="31cc6-183">Selecteer Hallo-container met de naam **'insights-logboeken-coreanalytics'** en dubbelklik erop</span><span class="sxs-lookup"><span data-stu-id="31cc6-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="31cc6-184">Weergeven van resultaten op Hallo rechterdeelvenster beginnen met Hallo eerst niveau, ziet eruit als **' resourceId = "**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="31cc6-185">Blijf klikken alle Hallo manier totdat er Hallo bestand **PT1H.json**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="31cc6-186">Zie Hallo Opmerking voor een uitleg van Hallo pad te volgen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="31cc6-187">Elke blob **PT1H.json** vertegenwoordigt Hallo analytics logboeken gedurende één uur voor een specifieke CDN-eindpunt of het aangepaste domein.</span><span class="sxs-lookup"><span data-stu-id="31cc6-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="31cc6-188">Hallo-schema van Hallo inhoud van dit JSON-bestand wordt beschreven in Hallo sectie Schema Hallo Core Analytics Logboeken</span><span class="sxs-lookup"><span data-stu-id="31cc6-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="31cc6-189">**BLOB-padindeling**</span><span class="sxs-lookup"><span data-stu-id="31cc6-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="31cc6-190">Core Analytics logboeken worden elk uur gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="31cc6-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="31cc6-191">Alle gegevens voor een uur zijn verzameld en opgeslagen in één Azure Blob als JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="31cc6-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="31cc6-192">Hallo pad toothis Azure Blob wordt weergegeven als er een hiërarchische structuur is.</span><span class="sxs-lookup"><span data-stu-id="31cc6-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="31cc6-193">Dit is omdat Hallo Storage explorer hulpprogramma interpreteert '/' als een mapscheidingsteken en toont Hallo hiërarchie voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="31cc6-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="31cc6-194">Hallo hele pad vertegenwoordigt eigenlijk alleen Hallo blob-naam.</span><span class="sxs-lookup"><span data-stu-id="31cc6-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="31cc6-195">Deze naam van de blob Hallo volgt Hallo naamconventie volgen</span><span class="sxs-lookup"><span data-stu-id="31cc6-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="31cc6-196">**Beschrijving van velden:**</span><span class="sxs-lookup"><span data-stu-id="31cc6-196">**Description of fields:**</span></span>

|<span data-ttu-id="31cc6-197">waarde</span><span class="sxs-lookup"><span data-stu-id="31cc6-197">value</span></span>|<span data-ttu-id="31cc6-198">description</span><span class="sxs-lookup"><span data-stu-id="31cc6-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="31cc6-199">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="31cc6-199">Subscription ID</span></span>    |<span data-ttu-id="31cc6-200">ID van hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="31cc6-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="31cc6-201">Dit is in Hallo Guid-indeling.</span><span class="sxs-lookup"><span data-stu-id="31cc6-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="31cc6-202">Resource</span><span class="sxs-lookup"><span data-stu-id="31cc6-202">Resource</span></span> |<span data-ttu-id="31cc6-203">Groepsnaam van Hallo resource groep toowhich Hallo CDN resources behoren.</span><span class="sxs-lookup"><span data-stu-id="31cc6-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="31cc6-204">Profielnaam</span><span class="sxs-lookup"><span data-stu-id="31cc6-204">Profile Name</span></span> |<span data-ttu-id="31cc6-205">Naam van Hallo CDN-profiel</span><span class="sxs-lookup"><span data-stu-id="31cc6-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="31cc6-206">Naam van het eindpunt</span><span class="sxs-lookup"><span data-stu-id="31cc6-206">Endpoint Name</span></span> |<span data-ttu-id="31cc6-207">Naam van Hallo CDN-eindpunt</span><span class="sxs-lookup"><span data-stu-id="31cc6-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="31cc6-208">jaar</span><span class="sxs-lookup"><span data-stu-id="31cc6-208">Year</span></span>|  <span data-ttu-id="31cc6-209">4-cijferige representatie van Hallo jaar bijvoorbeeld 2017</span><span class="sxs-lookup"><span data-stu-id="31cc6-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="31cc6-210">Maand</span><span class="sxs-lookup"><span data-stu-id="31cc6-210">Month</span></span>| <span data-ttu-id="31cc6-211">2 cijfers weergave van Hallo nummer van de maand.</span><span class="sxs-lookup"><span data-stu-id="31cc6-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="31cc6-212">01 januari =... 12 December =</span><span class="sxs-lookup"><span data-stu-id="31cc6-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="31cc6-213">Dag</span><span class="sxs-lookup"><span data-stu-id="31cc6-213">Day</span></span>|   <span data-ttu-id="31cc6-214">weergave van de dag van de maand Hallo Hallo 2 cijfers</span><span class="sxs-lookup"><span data-stu-id="31cc6-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="31cc6-215">PT1H.JSON</span><span class="sxs-lookup"><span data-stu-id="31cc6-215">PT1H.json</span></span>| <span data-ttu-id="31cc6-216">Werkelijke JSON-bestand waarin Hallo analytische gegevens is opgeslagen</span><span class="sxs-lookup"><span data-stu-id="31cc6-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="31cc6-217">Hallo Core analytische gegevens tooa CSV-bestand exporteren</span><span class="sxs-lookup"><span data-stu-id="31cc6-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="31cc6-218">toomake it eenvoudig tooaccess Hallo basisanalyse, bieden we een voorbeeld van code voor een hulpprogramma waarmee Hallo JSON-bestanden downloaden naar een platte door komma's gescheiden bestandsindeling, wat kan gebruikte tooeasily grafieken of andere aggregaties maken.</span><span class="sxs-lookup"><span data-stu-id="31cc6-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="31cc6-219">Dit is hoe u Hallo hulpprogramma kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="31cc6-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="31cc6-220">Ga naar Hallo github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="31cc6-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="31cc6-221">Hallo code downloaden</span><span class="sxs-lookup"><span data-stu-id="31cc6-221">Download hello code</span></span>
3.  <span data-ttu-id="31cc6-222">Volg de instructies toocompile en configureren</span><span class="sxs-lookup"><span data-stu-id="31cc6-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="31cc6-223">Hallo-hulpprogramma uitvoeren</span><span class="sxs-lookup"><span data-stu-id="31cc6-223">Run hello tool</span></span>
5.  <span data-ttu-id="31cc6-224">Resulterende CSV-bestand bevat Hallo analytische gegevens in een eenvoudige platte hiërarchie.</span><span class="sxs-lookup"><span data-stu-id="31cc6-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="31cc6-225">Diagnostische logboeken van een opslagplaats OMS Log Analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="31cc6-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="31cc6-226">Log Analytics is een service in Operations Management Suite (OMS) die uw cloud en on-premises omgevingen toomaintain de beschikbaarheid en prestaties bewaakt.</span><span class="sxs-lookup"><span data-stu-id="31cc6-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="31cc6-227">Gegevens die zijn gegenereerd door de resources in uw cloud en on-premises omgevingen en van andere bewaking extra tooprovide analysis over meerdere bronnen worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="31cc6-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="31cc6-228">toouse Log Analytics, moet u [logboekregistratie inschakelen](#enable-logging-with-azure-storage) toohello Azure-logboekanalyse OMS-opslagplaats, die eerder in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="31cc6-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="31cc6-229">Met behulp van Hallo OMS-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="31cc6-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="31cc6-230">Hallo volgende diagram ziet u Hallo-architectuur van Hallo invoer en uitvoer van Hallo opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="31cc6-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![OMS Log Analytics-opslagplaats](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="31cc6-232">*Afbeelding 3 - Log Analytics-opslagplaats*</span><span class="sxs-lookup"><span data-stu-id="31cc6-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="31cc6-233">U kunt Hallo gegevens op verschillende manieren weergeven met behulp van oplossingen voor het beheer.</span><span class="sxs-lookup"><span data-stu-id="31cc6-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="31cc6-234">U kunt beheeroplossingen verkrijgen van Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span><span class="sxs-lookup"><span data-stu-id="31cc6-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="31cc6-235">U kunt beheeroplossingen vanuit Azure marketplace installeren door te klikken op Hallo **nu downloaden** koppeling onderin Hallo van elke oplossing.</span><span class="sxs-lookup"><span data-stu-id="31cc6-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="31cc6-236">Toevoegen van een oplossing voor het beheer van OMS CDN</span><span class="sxs-lookup"><span data-stu-id="31cc6-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="31cc6-237">Volg deze stappen tooadd een oplossing voor:</span><span class="sxs-lookup"><span data-stu-id="31cc6-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="31cc6-238">Als u dit nog niet hebt gedaan, toohello aanmelden met Azure portal met behulp van uw Azure-abonnement en ga tooyour Dashboard.</span><span class="sxs-lookup"><span data-stu-id="31cc6-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="31cc6-239">![Azure-Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="31cc6-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="31cc6-240">In Hallo **nieuw** blade onder **Marketplace**, selecteer **bewaking + management**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="31cc6-242">In Hallo **bewaking + management** blade, klikt u op **alle**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="31cc6-244">Zoeken naar de CDN in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="31cc6-244">Search for CDN in hello search box.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="31cc6-246">Selecteer **Azure CDN basisanalyse**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![Alles bekijken](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="31cc6-248">Wanneer u op **maken**, kunt u zich toocreate gevraagd een nieuwe OMS-werkruimte of gebruik een bestaande.</span><span class="sxs-lookup"><span data-stu-id="31cc6-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![Alles bekijken](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="31cc6-250">Hallo-werkruimte die u hebt gemaakt voordat selecteren.</span><span class="sxs-lookup"><span data-stu-id="31cc6-250">Select hello workspace you created before.</span></span> <span data-ttu-id="31cc6-251">Vervolgens moet u tooadd een automation-account.</span><span class="sxs-lookup"><span data-stu-id="31cc6-251">You then need tooadd an automation account.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="31cc6-253">Hallo ziet volgende scherm Hallo automation-accountformulier die moet invullen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![Alles bekijken](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="31cc6-255">Nadat u Hallo automation-account hebt gemaakt, u bent klaar tooadd uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="31cc6-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="31cc6-256">Klik op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="31cc6-256">Click hello **Create** button.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="31cc6-258">Uw oplossing is nu tooyour werkruimte toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="31cc6-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="31cc6-259">Ga terug tooyour Azure-portal Dashboard.</span><span class="sxs-lookup"><span data-stu-id="31cc6-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="31cc6-261">Klik op de werkruimte voor logboekanalyse Hallo u toogo tooyour werkruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="31cc6-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="31cc6-262">Klik op Hallo **OMS-Portal** tegel toosee uw nieuwe oplossing in Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="31cc6-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="31cc6-264">De OMS-portal ziet er nu als Hallo scherm te volgen:</span><span class="sxs-lookup"><span data-stu-id="31cc6-264">Your OMS portal should now look like hello following screen:</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="31cc6-266">Klik op een van de Hallo tegels toosee verschillende weergaven in uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="31cc6-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![Alles bekijken](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="31cc6-268">Kunt u zelf schuiven links of rechts toosee meer tegels die afzonderlijke weergaven in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="31cc6-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="31cc6-269">Op een Hallo tegels te klikken, kunt u meer informatie over uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="31cc6-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![Alles bekijken](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="31cc6-271">Aanbiedingen en Prijscategorieën</span><span class="sxs-lookup"><span data-stu-id="31cc6-271">Offers and pricing tiers</span></span>

<span data-ttu-id="31cc6-272">U kunt zien aanbiedingen en Prijscategorieën voor OMS-beheeroplossingen voor [hier](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span><span class="sxs-lookup"><span data-stu-id="31cc6-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="31cc6-273">Weergaven aanpassen</span><span class="sxs-lookup"><span data-stu-id="31cc6-273">Customizing views</span></span>

<span data-ttu-id="31cc6-274">U kunt Hallo weergave aanpassen in uw gegevens met behulp van Hallo **ontwerper**.</span><span class="sxs-lookup"><span data-stu-id="31cc6-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="31cc6-275">Ga tooyour OMS-werkruimte en ontwerpen beginnen door te klikken op Hallo **ontwerper** tegel.</span><span class="sxs-lookup"><span data-stu-id="31cc6-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![Designer weergeven](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="31cc6-277">U kunt slepen en neerzetten grafiektypen van Hallo links en vul in Hallo Gegevensdetails tooanalyze op Hallo van links gewenste.</span><span class="sxs-lookup"><span data-stu-id="31cc6-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![Designer weergeven](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="31cc6-279">Logboek gegevens vertragingen</span><span class="sxs-lookup"><span data-stu-id="31cc6-279">Log data delays</span></span>

<span data-ttu-id="31cc6-280">Verizon logboek gegevens vertragingen</span><span class="sxs-lookup"><span data-stu-id="31cc6-280">Verizon log data delays</span></span> | <span data-ttu-id="31cc6-281">Akamai logboek gegevens vertragingen</span><span class="sxs-lookup"><span data-stu-id="31cc6-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="31cc6-282">Logboekgegevens van Verizon is 1 uur vertraging en een too2 uren toostart verschijnen na voltooiing van de endpoint-doorgifte in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="31cc6-283">Logboekgegevens Akamai is 24 uur vertraging en too2 uren toostart verschijnen als deze meer dan 24 uur geleden is gemaakt in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="31cc6-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="31cc6-284">Als u onlangs is gemaakt, kan het Hallo logboeken toostart verschijnen too25 uur duren.</span><span class="sxs-lookup"><span data-stu-id="31cc6-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="31cc6-285">Diagnostische logboeken typen voor CDN-basisanalyse</span><span class="sxs-lookup"><span data-stu-id="31cc6-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="31cc6-286">Momenteel bieden we alleen basisanalyse logboeken met HTTP-antwoord statistieken en uitgaande gezien vanaf Hallo CDN POP's / randen metrische gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="31cc6-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="31cc6-287">Core Analytics metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="31cc6-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="31cc6-288">Hallo volgende tabel bevat een overzicht van metrische gegevens beschikbaar zijn in Hallo die basisanalyse registreert.</span><span class="sxs-lookup"><span data-stu-id="31cc6-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="31cc6-289">Niet alle metrische gegevens zijn beschikbaar in alle providers, hoewel deze verschillen minimaal zijn.</span><span class="sxs-lookup"><span data-stu-id="31cc6-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="31cc6-290">Hallo ook volgende van de tabel wordt aangegeven als een metriek beschikbaar van een provider.</span><span class="sxs-lookup"><span data-stu-id="31cc6-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="31cc6-291">Houd er rekening mee dat Hallo metrische gegevens beschikbaar zijn voor de CDN-eindpunten die verkeer op deze hebben.</span><span class="sxs-lookup"><span data-stu-id="31cc6-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="31cc6-292">Gegevens</span><span class="sxs-lookup"><span data-stu-id="31cc6-292">Metric</span></span>                     | <span data-ttu-id="31cc6-293">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="31cc6-293">Description</span></span>   | <span data-ttu-id="31cc6-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="31cc6-294">Verizon</span></span>  | <span data-ttu-id="31cc6-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="31cc6-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="31cc6-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="31cc6-296">RequestCountTotal</span></span>         |<span data-ttu-id="31cc6-297">Totaal aantal treffers aanvraag tijdens deze periode</span><span class="sxs-lookup"><span data-stu-id="31cc6-297">Total number of request hits during this period</span></span>| <span data-ttu-id="31cc6-298">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-298">Yes</span></span>  |<span data-ttu-id="31cc6-299">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-299">Yes</span></span>   |
| <span data-ttu-id="31cc6-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="31cc6-301">Telling van alle aanvragen dat heeft geresulteerd in een 2xx HTTP-code (bijvoorbeeld 200, 202)</span><span class="sxs-lookup"><span data-stu-id="31cc6-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="31cc6-302">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-302">Yes</span></span>  |<span data-ttu-id="31cc6-303">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-303">Yes</span></span>   |
| <span data-ttu-id="31cc6-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="31cc6-305">Telling van alle aanvragen dat heeft geresulteerd in een 3xx HTTP-code (bijvoorbeeld 300, 302)</span><span class="sxs-lookup"><span data-stu-id="31cc6-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="31cc6-306">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-306">Yes</span></span>  |<span data-ttu-id="31cc6-307">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-307">Yes</span></span>   |
| <span data-ttu-id="31cc6-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="31cc6-309">Telling van alle aanvragen dat heeft geresulteerd in een 4xx HTTP-code (bijvoorbeeld 400, 404)</span><span class="sxs-lookup"><span data-stu-id="31cc6-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="31cc6-310">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-310">Yes</span></span>   |<span data-ttu-id="31cc6-311">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-311">Yes</span></span>   |
| <span data-ttu-id="31cc6-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="31cc6-313">Telling van alle aanvragen dat heeft geresulteerd in een 5xx HTTP-code (bijvoorbeeld 500, 504)</span><span class="sxs-lookup"><span data-stu-id="31cc6-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="31cc6-314">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-314">Yes</span></span>  |<span data-ttu-id="31cc6-315">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-315">Yes</span></span>   |
| <span data-ttu-id="31cc6-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="31cc6-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="31cc6-317">Telling van alle andere HTTP-codes (buiten 2xx-5xx)</span><span class="sxs-lookup"><span data-stu-id="31cc6-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="31cc6-318">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-318">Yes</span></span>  |<span data-ttu-id="31cc6-319">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-319">Yes</span></span>   |
| <span data-ttu-id="31cc6-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="31cc6-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="31cc6-321">Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 200 code</span><span class="sxs-lookup"><span data-stu-id="31cc6-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="31cc6-322">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-322">No</span></span>   |<span data-ttu-id="31cc6-323">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-323">Yes</span></span>   |
| <span data-ttu-id="31cc6-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="31cc6-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="31cc6-325">Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 206 code</span><span class="sxs-lookup"><span data-stu-id="31cc6-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="31cc6-326">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-326">No</span></span>   |<span data-ttu-id="31cc6-327">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-327">Yes</span></span>   |
| <span data-ttu-id="31cc6-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="31cc6-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="31cc6-329">Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 302 code</span><span class="sxs-lookup"><span data-stu-id="31cc6-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="31cc6-330">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-330">No</span></span>   |<span data-ttu-id="31cc6-331">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-331">Yes</span></span>   |
| <span data-ttu-id="31cc6-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="31cc6-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="31cc6-333">Telling van alle aanvragen dat heeft geresulteerd in een HTTP-antwoord voor 304 code</span><span class="sxs-lookup"><span data-stu-id="31cc6-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="31cc6-334">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-334">No</span></span>   |<span data-ttu-id="31cc6-335">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-335">Yes</span></span>   |
| <span data-ttu-id="31cc6-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="31cc6-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="31cc6-337">Telling van alle aanvragen dat heeft geresulteerd in een 404 HTTP-code-antwoord</span><span class="sxs-lookup"><span data-stu-id="31cc6-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="31cc6-338">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-338">No</span></span>   |<span data-ttu-id="31cc6-339">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-339">Yes</span></span>   |
| <span data-ttu-id="31cc6-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="31cc6-340">RequestCountCacheHit</span></span> |<span data-ttu-id="31cc6-341">Telling van alle aanvragen dat heeft geresulteerd in een treffers in de Cache.</span><span class="sxs-lookup"><span data-stu-id="31cc6-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="31cc6-342">Dit betekent dat Hallo asset rechtstreeks vanuit Hallo POP toohello Client in behandeling is genomen.</span><span class="sxs-lookup"><span data-stu-id="31cc6-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="31cc6-343">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-343">Yes</span></span>  |<span data-ttu-id="31cc6-344">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-344">No</span></span>   |
| <span data-ttu-id="31cc6-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="31cc6-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="31cc6-346">Telling van alle aanvragen dat heeft geresulteerd in een Cache ontbreekt.</span><span class="sxs-lookup"><span data-stu-id="31cc6-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="31cc6-347">Dit betekent Hallo asset is niet gevonden op Hallo POP dichtstbijzijnde toohello client en daarom is opgehaald uit de Hallo oorsprong.</span><span class="sxs-lookup"><span data-stu-id="31cc6-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="31cc6-348">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-348">Yes</span></span>   | <span data-ttu-id="31cc6-349">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-349">No</span></span>  |
| <span data-ttu-id="31cc6-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="31cc6-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="31cc6-351">Telling van alle aanvragen tooan asset die niet worden opgeslagen vanwege de Gebruikersconfiguratie tooa op Hallo rand.</span><span class="sxs-lookup"><span data-stu-id="31cc6-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="31cc6-352">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-352">Yes</span></span>   | <span data-ttu-id="31cc6-353">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-353">No</span></span>  |
| <span data-ttu-id="31cc6-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="31cc6-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="31cc6-355">Telling van alle tooassets die niet worden opgeslagen door Hallo asset van Cache-Control-aanvragen en -headers die aangeven dat deze mag niet worden opgeslagen op een pop-server of door Hallo HTTP-client is verlopen</span><span class="sxs-lookup"><span data-stu-id="31cc6-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="31cc6-356">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-356">Yes</span></span>   |<span data-ttu-id="31cc6-357">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-357">No</span></span>   |
| <span data-ttu-id="31cc6-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="31cc6-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="31cc6-359">Telling van alle aanvragen met de status van de cache niet wordt gedekt door hierboven.</span><span class="sxs-lookup"><span data-stu-id="31cc6-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="31cc6-360">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-360">Yes</span></span>   | <span data-ttu-id="31cc6-361">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-361">No</span></span>  |
| <span data-ttu-id="31cc6-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="31cc6-362">EgressTotal</span></span> | <span data-ttu-id="31cc6-363">Uitgaande gegevensoverdracht in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="31cc6-364">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-364">Yes</span></span>   |<span data-ttu-id="31cc6-365">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-365">Yes</span></span>   |
| <span data-ttu-id="31cc6-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="31cc6-367">Uitgaande gegevens overdracht * voor antwoorden met 2xx HTTP-statuscodes in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="31cc6-368">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-368">Yes</span></span>   |<span data-ttu-id="31cc6-369">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-369">No</span></span>   |
| <span data-ttu-id="31cc6-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="31cc6-371">Uitgaande gegevensoverdracht voor antwoorden met 3xx HTTP-statuscodes in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="31cc6-372">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-372">Yes</span></span>   |<span data-ttu-id="31cc6-373">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-373">No</span></span>   |
| <span data-ttu-id="31cc6-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="31cc6-375">Uitgaande gegevensoverdracht voor antwoorden met 4xx HTTP-statuscodes in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="31cc6-376">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-376">Yes</span></span>   | <span data-ttu-id="31cc6-377">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-377">No</span></span>  |
| <span data-ttu-id="31cc6-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="31cc6-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="31cc6-379">Uitgaande gegevensoverdracht voor antwoorden met 5xx HTTP-statuscodes in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="31cc6-380">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-380">Yes</span></span>   |  <span data-ttu-id="31cc6-381">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-381">No</span></span> |
| <span data-ttu-id="31cc6-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="31cc6-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="31cc6-383">Uitgaande gegevensoverdracht voor antwoorden met andere HTTP-statuscodes in GB</span><span class="sxs-lookup"><span data-stu-id="31cc6-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="31cc6-384">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-384">Yes</span></span>   |<span data-ttu-id="31cc6-385">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-385">No</span></span>   |
| <span data-ttu-id="31cc6-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="31cc6-386">EgressCacheHit</span></span> |  <span data-ttu-id="31cc6-387">Uitgaande gegevensoverdracht voor antwoorden die zijn geleverd direct van Hallo CDN cache op Hallo CDN POP's / randen</span><span class="sxs-lookup"><span data-stu-id="31cc6-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="31cc6-388">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-388">Yes</span></span>   |  <span data-ttu-id="31cc6-389">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-389">No</span></span> |
| <span data-ttu-id="31cc6-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="31cc6-390">EgressCacheMiss</span></span> | <span data-ttu-id="31cc6-391">Uitgaande gegevensoverdracht voor reacties waarbij zijn niet gevonden op Hallo dichtstbijzijnde POP-server en opgehaald uit de bronserver Hallo</span><span class="sxs-lookup"><span data-stu-id="31cc6-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="31cc6-392">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-392">Yes</span></span>   |  <span data-ttu-id="31cc6-393">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-393">No</span></span> |
| <span data-ttu-id="31cc6-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="31cc6-394">EgressCacheNoCache</span></span> | <span data-ttu-id="31cc6-395">Uitgaande gegevensoverdracht voor bedrijfsmiddelen die niet worden opgeslagen vanwege de Gebruikersconfiguratie tooa op Hallo rand.</span><span class="sxs-lookup"><span data-stu-id="31cc6-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="31cc6-396">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-396">Yes</span></span>   |<span data-ttu-id="31cc6-397">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-397">No</span></span>   |
| <span data-ttu-id="31cc6-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="31cc6-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="31cc6-399">Uitgaande gegevensoverdracht voor bedrijfsmiddelen die niet worden opgeslagen door Hallo asset van Cache-Control en/of Expires-koppen die aangeven dat deze mag niet worden opgeslagen op een pop-server of door Hallo HTTP-client</span><span class="sxs-lookup"><span data-stu-id="31cc6-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="31cc6-400">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-400">Yes</span></span>   | <span data-ttu-id="31cc6-401">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-401">No</span></span>  |
| <span data-ttu-id="31cc6-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="31cc6-402">EgressCacheOthers</span></span> |  <span data-ttu-id="31cc6-403">Uitgaande gegevensoverdracht voor andere scenario's met cache.</span><span class="sxs-lookup"><span data-stu-id="31cc6-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="31cc6-404">Ja</span><span class="sxs-lookup"><span data-stu-id="31cc6-404">Yes</span></span>   | <span data-ttu-id="31cc6-405">Nee</span><span class="sxs-lookup"><span data-stu-id="31cc6-405">No</span></span>  |

<span data-ttu-id="31cc6-406">* Uitgaande gegevensoverdracht verwijst tootraffic van CDN pop-locatie servers toohello client geleverd.</span><span class="sxs-lookup"><span data-stu-id="31cc6-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="31cc6-407">Schema van Hallo Core Analytics Logboeken</span><span class="sxs-lookup"><span data-stu-id="31cc6-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="31cc6-408">Alle logboeken worden opgeslagen in de JSON-indeling en elk item heeft tekenreeksvelden Hallo hieronder schema te volgen:</span><span class="sxs-lookup"><span data-stu-id="31cc6-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="31cc6-409">Waar vertegenwoordigt tijd' Hallo' hello begintijd van Hallo uur grens waarvoor Hallo statistieken is gemeld.</span><span class="sxs-lookup"><span data-stu-id="31cc6-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="31cc6-410">Wanneer een waarde niet wordt ondersteund door een CDN-provider in plaats van een dubbel of integer-waarde, zal er een null-waarde.</span><span class="sxs-lookup"><span data-stu-id="31cc6-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="31cc6-411">Deze null-waarde duidt Hallo afwezigheid van een metriek en deze verschilt van de waarde 0.</span><span class="sxs-lookup"><span data-stu-id="31cc6-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="31cc6-412">Rekening mee dat er een set met deze metrische gegevens per domein geconfigureerd op Hallo-eindpunt worden.</span><span class="sxs-lookup"><span data-stu-id="31cc6-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="31cc6-413">Van de Voorbeeldeigenschappen van onderstaande:</span><span class="sxs-lookup"><span data-stu-id="31cc6-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="31cc6-414">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="31cc6-414">Additional resources</span></span>

* [<span data-ttu-id="31cc6-415">Azure diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="31cc6-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="31cc6-416">Basisanalyse via de aanvullende portal Azure CDN</span><span class="sxs-lookup"><span data-stu-id="31cc6-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="31cc6-417">OMS Azure Log Analytics</span><span class="sxs-lookup"><span data-stu-id="31cc6-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="31cc6-418">Azure-logboekanalyse REST-API</span><span class="sxs-lookup"><span data-stu-id="31cc6-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







