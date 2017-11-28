---
title: aaaOverview van diagnostische Azure-Logboeken | Microsoft Docs
description: Informatie over wat Azure diagnostische logboeken zijn en hoe u ze kunt gebruiken toounderstand gebeurtenissen binnen een Azure-resource.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="d8bea-103">Verzamelen en gebruiken van de logboekgegevens van uw Azure-resources</span><span class="sxs-lookup"><span data-stu-id="d8bea-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="d8bea-104">Wat zijn Azure-resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="d8bea-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="d8bea-105">**Diagnostische logboeken van Azure resource niveau** logboeken die door een resource die uitgebreide, regelmatig gegevens over Hallo-bewerking van de bron.</span><span class="sxs-lookup"><span data-stu-id="d8bea-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="d8bea-106">Hallo-inhoud van deze logboeken varieert per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="d8bea-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="d8bea-107">Netwerkbeveiligingsgroep regel tellers en Sleutelkluis audits zijn bijvoorbeeld twee categorieën van Logboeken van de resource.</span><span class="sxs-lookup"><span data-stu-id="d8bea-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="d8bea-108">Diagnostische logboeken niveau resource verschillen van Hallo [activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="d8bea-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="d8bea-109">Hallo activiteitenlogboek verschaft inzicht in het Hallo-bewerkingen die zijn uitgevoerd op resources in uw abonnement met behulp van Resource Manager, bijvoorbeeld een virtuele machine maken of verwijderen van een logische app.</span><span class="sxs-lookup"><span data-stu-id="d8bea-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="d8bea-110">Hallo activiteitenlogboek is een logboek abonnement.</span><span class="sxs-lookup"><span data-stu-id="d8bea-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="d8bea-111">Niveau van de resource diagnostische logboeken bieden inzicht in bewerkingen die zijn uitgevoerd binnen die bron zelf, bijvoorbeeld een geheim ophalen uit een Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="d8bea-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="d8bea-112">Diagnostische logboeken niveau resource afwijken van de Gast OS-niveau diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="d8bea-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="d8bea-113">Gastbesturingssysteem diagnostische logboeken zijn deze die worden verzameld door een agent wordt uitgevoerd binnen een virtuele machine of andere ondersteund resourcetype.</span><span class="sxs-lookup"><span data-stu-id="d8bea-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="d8bea-114">Diagnostische logboeken niveau resource vereisen geen gegevens van de resource-specifieke agent en vastleggen van hello Azure-platform zelf, terwijl de Gast OS-niveau diagnostische logboeken vastleggen van gegevens uit het Hallo-besturingssysteem en toepassingen die worden uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="d8bea-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="d8bea-115">Niet alle resources ondersteuning Hallo nieuwe type resource diagnostische logboeken die hier wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="d8bea-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="d8bea-116">Dit artikel bevat een sectie aanbieding brontypen Hallo nieuwe niveau resource diagnostische logboeken ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="d8bea-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="d8bea-117">Resource diagnostische logboeken tegenover andere typen logboeken</span><span class="sxs-lookup"><span data-stu-id="d8bea-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="d8bea-118">Wat u kunt doen met het niveau van de resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="d8bea-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="d8bea-119">Hier volgen enkele Hallo dingen die u met resource diagnostische logboeken doen kunt:</span><span class="sxs-lookup"><span data-stu-id="d8bea-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Logische plaatsing van diagnostische logboeken van Resource](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="d8bea-121">Deze tooa opslaan [ **Opslagaccount** ](monitoring-archive-diagnostic-logs.md) voor inspectie controle of handmatig.</span><span class="sxs-lookup"><span data-stu-id="d8bea-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="d8bea-122">U kunt opgeven met behulp Hallo bewaren (in dagen) **diagnostische broninstellingen**.</span><span class="sxs-lookup"><span data-stu-id="d8bea-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="d8bea-123">[Ze te streamen**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) voor opname door een service van derden of aangepaste analytics-oplossing zoals Power BI.</span><span class="sxs-lookup"><span data-stu-id="d8bea-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="d8bea-124">Analyseer ze met [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="d8bea-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="d8bea-125">U kunt een opslagaccount of Event Hubs-naamruimte die zich niet in hetzelfde abonnement Hallo zoals Hallo een tekensetcodering Logboeken.</span><span class="sxs-lookup"><span data-stu-id="d8bea-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="d8bea-126">Hallo-gebruiker die Hallo instelling configureert, moet Hallo juiste RBAC toegang tooboth abonnementen hebben.</span><span class="sxs-lookup"><span data-stu-id="d8bea-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="d8bea-127">Diagnostische instellingen voor bronnen</span><span class="sxs-lookup"><span data-stu-id="d8bea-127">Resource diagnostic settings</span></span>
<span data-ttu-id="d8bea-128">Diagnostische logboeken van de resource voor niet-Compute bronnen worden geconfigureerd met behulp van de diagnostische instellingen resource.</span><span class="sxs-lookup"><span data-stu-id="d8bea-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="d8bea-129">**Diagnostische instellingen voor resource** voor een besturingselement resource:</span><span class="sxs-lookup"><span data-stu-id="d8bea-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="d8bea-130">Waar resource diagnostische logboeken en metrische gegevens worden verzonden (Storage-Account, Event Hubs en/of logboekanalyse OMS).</span><span class="sxs-lookup"><span data-stu-id="d8bea-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="d8bea-131">Welke categorieën logboek worden verzonden en of u metrische gegevens ook verzonden.</span><span class="sxs-lookup"><span data-stu-id="d8bea-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="d8bea-132">Hoe lang elke categorie van het logboek moet worden bewaard in een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="d8bea-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="d8bea-133">Een bewaartermijn van nul dagen betekent logboeken permanent worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="d8bea-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="d8bea-134">Hallo-waarden zijn anders wordt een willekeurig aantal dagen tussen 1 en 2147483647.</span><span class="sxs-lookup"><span data-stu-id="d8bea-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="d8bea-135">Als bewaarbeleid worden ingesteld, maar Logboeken opslaan in een Opslagaccount is uitgeschakeld (bijvoorbeeld, als er alleen Event Hubs of OMS-opties zijn geselecteerd), is het bewaarbeleid Hallo hebben geen effect.</span><span class="sxs-lookup"><span data-stu-id="d8bea-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="d8bea-136">Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d8bea-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="d8bea-137">Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d8bea-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="d8bea-138">Deze instellingen gemakkelijk worden geconfigureerd via Hallo diagnostische instellingen voor een resource in hello Azure-portal, via Azure PowerShell en CLI-opdrachten of via Hallo [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bea-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="d8bea-139">Diagnostische logboeken en metrische gegevens voor uit Hallo Gast OS laag van Compute-resources (bijvoorbeeld virtuele machines of Service Fabric) Gebruik [een afzonderlijk mechanisme voor configuratie en de selectie van uitvoer](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d8bea-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="d8bea-140">Hoe tooenable verzamelen van diagnostische logboeken van resource</span><span class="sxs-lookup"><span data-stu-id="d8bea-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="d8bea-141">Verzamelen van diagnostische logboeken resource kan worden ingeschakeld [als onderdeel van het maken van een resource in het Resource Manager-sjabloon](./monitoring-enable-diagnostic-logs-using-template.md) of nadat een bron wordt gemaakt van de pagina die resource in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="d8bea-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="d8bea-142">U kunt ook de verzameling op elk gewenst moment Azure PowerShell of CLI-opdrachten gebruikt of als Hallo Monitor REST-API van Azure inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d8bea-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="d8bea-143">Deze instructies kunnen niet van toepassing rechtstreeks tooevery resource.</span><span class="sxs-lookup"><span data-stu-id="d8bea-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="d8bea-144">Zie Hallo schema koppelingen op Hallo onder aan deze pagina toounderstand speciale stappen die mogelijk toocertain brontypen die van toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8bea-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="d8bea-145">Verzamelen van diagnostische logboeken van de resource in Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="d8bea-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="d8bea-146">U kunt verzamelen van diagnostische logboeken van de resource in hello Azure inschakelen portal nadat een resource is gemaakt door specifieke resource tooa gaat of door te navigeren tooAzure Monitor.</span><span class="sxs-lookup"><span data-stu-id="d8bea-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="d8bea-147">tooenable via Azure Monitor:</span><span class="sxs-lookup"><span data-stu-id="d8bea-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="d8bea-148">In Hallo [Azure-portal](http://portal.azure.com), gaat u tooAzure Monitor en klikt u op **diagnostische instellingen**</span><span class="sxs-lookup"><span data-stu-id="d8bea-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sectie van de Monitor Azure bewaking](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="d8bea-150">Eventueel Hallo lijst filteren op resourcegroep of brontype en klik vervolgens op Hallo resource waarvoor u een diagnostische instelling tooset wilt.</span><span class="sxs-lookup"><span data-stu-id="d8bea-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="d8bea-151">Als u geen instellingen bestaat op het Hallo-resource die u hebt geselecteerd, bent u na vragen aan gebruiker toocreate een instelling.</span><span class="sxs-lookup"><span data-stu-id="d8bea-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="d8bea-152">Klik op "Diagnostische gegevens inschakelen."</span><span class="sxs-lookup"><span data-stu-id="d8bea-152">Click "Turn on diagnostics."</span></span>

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="d8bea-154">Als er bestaande instellingen op Hallo resource, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource.</span><span class="sxs-lookup"><span data-stu-id="d8bea-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="d8bea-155">Klik op 'Diagnostische instelling toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="d8bea-155">Click "Add diagnostic setting."</span></span>

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="d8bea-157">Geef een naam van de instelling, Hallo selectievakjes voor elke doel toowhich u wilt toosend gegevens, en welke resource configureren voor elk doel wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d8bea-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="d8bea-158">Desgewenst instellen een aantal dagen tooretain deze logboeken via Hallo **bewaartermijn (dagen)** schuifregelaars (alleen van toepassing toohello storage account doel).</span><span class="sxs-lookup"><span data-stu-id="d8bea-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="d8bea-159">Een bewaartermijn van nul dagen Hallo logboeken voor onbepaalde tijd worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d8bea-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="d8bea-161">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d8bea-161">Click **Save**.</span></span>

<span data-ttu-id="d8bea-162">Na enkele ogenblikken opgegeven Hallo nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron en logboeken met diagnostische gegevens worden verzonden toohello bestemmingen zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d8bea-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="d8bea-163">Verzamelen van diagnostische logboeken van de resource via PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8bea-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="d8bea-164">tooenable verzamelen van diagnostische logboeken van de resource via Azure PowerShell, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d8bea-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="d8bea-165">tooenable opslag van diagnostische logboeken in een opslagaccount, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="d8bea-166">Hallo storage account-ID is Hallo resource-ID voor Hallo storage account toowhich gewenste toosend Hallo registreert.</span><span class="sxs-lookup"><span data-stu-id="d8bea-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="d8bea-167">tooenable streaming van diagnostische logboeken tooan event hub, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="d8bea-168">Hallo service bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="d8bea-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="d8bea-169">tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="d8bea-170">U kunt Hallo bron-ID van de werkruimte voor logboekanalyse met behulp van de volgende opdracht Hallo verkrijgen:</span><span class="sxs-lookup"><span data-stu-id="d8bea-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="d8bea-171">U kunt deze parameters tooenable meerdere uitvoeropties combineren.</span><span class="sxs-lookup"><span data-stu-id="d8bea-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="d8bea-172">Verzamelen van diagnostische logboeken van de resource via CLI</span><span class="sxs-lookup"><span data-stu-id="d8bea-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="d8bea-173">tooenable verzamelen van diagnostische logboeken van de resource via hello Azure CLI gebruiken Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d8bea-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="d8bea-174">tooenable opslag van diagnostische logboeken in een Opslagaccount, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="d8bea-175">Hallo storage account-ID is Hallo resource-ID voor Hallo storage account toowhich gewenste toosend Hallo registreert.</span><span class="sxs-lookup"><span data-stu-id="d8bea-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="d8bea-176">tooenable streaming van diagnostische logboeken tooan event hub, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="d8bea-177">Hallo service bus regel-ID is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="d8bea-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="d8bea-178">tooenable verzending van diagnostische logboeken tooa Log Analytics-werkruimte, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8bea-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="d8bea-179">U kunt deze parameters tooenable meerdere uitvoeropties combineren.</span><span class="sxs-lookup"><span data-stu-id="d8bea-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="d8bea-180">Verzamelen van diagnostische logboeken van de resource via REST-API</span><span class="sxs-lookup"><span data-stu-id="d8bea-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="d8bea-181">Diagnostische instellingen voor toochange hello Azure Monitor REST API, gebruik Zie [dit document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8bea-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="d8bea-182">Diagnostische instellingen van de resource in Hallo portal beheren</span><span class="sxs-lookup"><span data-stu-id="d8bea-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="d8bea-183">Zorg ervoor dat alle resources met diagnostische instellingen zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d8bea-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="d8bea-184">Navigeer te**Monitor** in Hallo portal en open **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="d8bea-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Diagnostische logboeken blade in Hallo-portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="d8bea-186">Mogelijk hebt u tooclick meer gedeelte ' ' toofind Hallo Monitor.</span><span class="sxs-lookup"><span data-stu-id="d8bea-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="d8bea-187">Hier kunt u bekijken en alle resources die ondersteuning bieden voor diagnostische instellingen toosee als ze ingeschakeld diagnostische gegevens hebben filteren.</span><span class="sxs-lookup"><span data-stu-id="d8bea-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="d8bea-188">U kunt ook inzoomen toosee als meerdere instellingen is ingesteld op een resource en welke storage-account, de Event Hubs-naamruimte en/of de werkruimte voor logboekanalyse die gegevens om te stromen controleren.</span><span class="sxs-lookup"><span data-stu-id="d8bea-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Diagnostische logboeken resultaten in de portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="d8bea-190">Resource toevoegen van dat een diagnostische instelling wordt Hallo diagnostische instellingen weergeven, waarin u kunt inschakelen, uitschakelen of wijzigen van de diagnostische instellingen voor Hallo worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d8bea-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="d8bea-191">Ondersteunde services, categorieën en schema's voor resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="d8bea-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="d8bea-192">[Raadpleeg dit artikel](monitoring-diagnostic-logs-schema.md) voor een volledige lijst van ondersteunde diensten en Hallo logboek categorieën en schema's die worden gebruikt door deze services.</span><span class="sxs-lookup"><span data-stu-id="d8bea-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8bea-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d8bea-193">Next steps</span></span>

* [<span data-ttu-id="d8bea-194">Resource diagnostische logboeken te streamen**Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="d8bea-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="d8bea-195">Resource diagnostische instellingen wijzigen met hello Azure Monitor REST-API</span><span class="sxs-lookup"><span data-stu-id="d8bea-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="d8bea-196">Logboeken van de Azure-opslag met logboekanalyse analyseren</span><span class="sxs-lookup"><span data-stu-id="d8bea-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
