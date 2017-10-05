---
title: Overzicht van Azure diagnostische logboeken | Microsoft Docs
description: Informatie over wat Azure diagnostische logboeken zijn en hoe u ze kunt gebruiken om te begrijpen van gebeurtenissen die plaatsvinden binnen een Azure-resource.
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
ms.openlocfilehash: d59abde29fc7b73a799e5bf3659b02f824b693de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="5363c-103">Verzamelen en gebruiken van de logboekgegevens van uw Azure-resources</span><span class="sxs-lookup"><span data-stu-id="5363c-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="5363c-104">Wat zijn Azure-resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="5363c-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="5363c-105">**Diagnostische logboeken van Azure resource niveau** logboeken die door een resource die uitgebreide, regelmatig gegevens over de werking van die bron leveren.</span><span class="sxs-lookup"><span data-stu-id="5363c-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="5363c-106">De inhoud van deze logboeken varieert per resourcetype.</span><span class="sxs-lookup"><span data-stu-id="5363c-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="5363c-107">Netwerkbeveiligingsgroep regel tellers en Sleutelkluis audits zijn bijvoorbeeld twee categorieën van Logboeken van de resource.</span><span class="sxs-lookup"><span data-stu-id="5363c-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="5363c-108">Diagnostische logboeken niveau resource afwijken van de [activiteitenlogboek](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5363c-108">Resource-level diagnostic logs differ from the [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="5363c-109">Het activiteitenlogboek verschaft inzicht in de bewerkingen die zijn uitgevoerd op resources in uw abonnement met behulp van Resource Manager, bijvoorbeeld een virtuele machine maken of verwijderen van een logische app.</span><span class="sxs-lookup"><span data-stu-id="5363c-109">The Activity Log provides insight into the operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="5363c-110">Het activiteitenlogboek is een logboek abonnement.</span><span class="sxs-lookup"><span data-stu-id="5363c-110">The Activity Log is a subscription-level log.</span></span> <span data-ttu-id="5363c-111">Niveau van de resource diagnostische logboeken bieden inzicht in bewerkingen die zijn uitgevoerd binnen die bron zelf, bijvoorbeeld een geheim ophalen uit een Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="5363c-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="5363c-112">Diagnostische logboeken niveau resource afwijken van de Gast OS-niveau diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="5363c-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="5363c-113">Gastbesturingssysteem diagnostische logboeken zijn deze die worden verzameld door een agent wordt uitgevoerd binnen een virtuele machine of andere ondersteund resourcetype.</span><span class="sxs-lookup"><span data-stu-id="5363c-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="5363c-114">Diagnostische logboeken niveau resource vereisen geen gegevens van de resource-specifieke agent en vastleggen van de Azure-platform zelf, terwijl de Gast OS-niveau diagnostische logboeken vastleggen van gegevens van het besturingssysteem en toepassingen die worden uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5363c-114">Resource-level diagnostic logs require no agent and capture resource-specific data from the Azure platform itself, while guest OS-level diagnostic logs capture data from the operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="5363c-115">Niet alle resources ondersteuning voor het nieuwe type resource diagnostische logboeken die hier wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="5363c-115">Not all resources support the new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="5363c-116">In dit artikel bevat een sectie vermelden welke resourcetypen ondersteuning voor de nieuwe resource niveau diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="5363c-116">This article contains a section listing which resource types support the new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="5363c-117">Resource diagnostische logboeken tegenover andere typen logboeken</span><span class="sxs-lookup"><span data-stu-id="5363c-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="5363c-118">Wat u kunt doen met het niveau van de resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="5363c-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="5363c-119">Hier volgen enkele dingen die u met resource diagnostische logboeken doen kunt:</span><span class="sxs-lookup"><span data-stu-id="5363c-119">Here are some of the things you can do with resource diagnostic logs:</span></span>

![Logische plaatsing van diagnostische logboeken van Resource](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="5363c-121">Bewaar ze op een [ **Opslagaccount** ](monitoring-archive-diagnostic-logs.md) voor inspectie controle of handmatig.</span><span class="sxs-lookup"><span data-stu-id="5363c-121">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="5363c-122">Kunt u de bewaarperiode (in dagen) met behulp van **diagnostische broninstellingen**.</span><span class="sxs-lookup"><span data-stu-id="5363c-122">You can specify the retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="5363c-123">[Ze streamt **Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) voor opname door een service van derden of aangepaste analytics-oplossing zoals Power BI.</span><span class="sxs-lookup"><span data-stu-id="5363c-123">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="5363c-124">Analyseer ze met [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="5363c-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="5363c-125">U kunt een opslagaccount of de Event Hubs-naamruimte die zich niet in hetzelfde abonnement als de tekensetcodering Logboeken gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5363c-125">You can use a storage account or Event Hubs namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="5363c-126">De gebruiker die de instelling configureert, moet de juiste RBAC-toegang tot beide abonnementen hebben.</span><span class="sxs-lookup"><span data-stu-id="5363c-126">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="5363c-127">Diagnostische instellingen voor bronnen</span><span class="sxs-lookup"><span data-stu-id="5363c-127">Resource diagnostic settings</span></span>
<span data-ttu-id="5363c-128">Diagnostische logboeken van de resource voor niet-Compute bronnen worden geconfigureerd met behulp van de diagnostische instellingen resource.</span><span class="sxs-lookup"><span data-stu-id="5363c-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="5363c-129">**Diagnostische instellingen voor resource** voor een besturingselement resource:</span><span class="sxs-lookup"><span data-stu-id="5363c-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="5363c-130">Waar resource diagnostische logboeken en metrische gegevens worden verzonden (Storage-Account, Event Hubs en/of logboekanalyse OMS).</span><span class="sxs-lookup"><span data-stu-id="5363c-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="5363c-131">Welke categorieën logboek worden verzonden en of u metrische gegevens ook verzonden.</span><span class="sxs-lookup"><span data-stu-id="5363c-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="5363c-132">Hoe lang elke categorie van het logboek moet worden bewaard in een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="5363c-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="5363c-133">Een bewaartermijn van nul dagen betekent logboeken permanent worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="5363c-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="5363c-134">Anders wordt mag de waarde een onbeperkt aantal dagen tussen 1 en 2147483647.</span><span class="sxs-lookup"><span data-stu-id="5363c-134">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="5363c-135">Als bewaarbeleid worden ingesteld, maar Logboeken opslaan in een Opslagaccount is uitgeschakeld (bijvoorbeeld, als er alleen Event Hubs of OMS-opties zijn geselecteerd), is het bewaarbeleid hebben geen effect.</span><span class="sxs-lookup"><span data-stu-id="5363c-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="5363c-136">Bewaarbeleid zijn toegepaste per dag, dus aan het einde van een dag (UTC), logboeken van de dag dat nu is buiten de bewaarperiode beleid worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5363c-136">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="5363c-137">Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan het begin van vandaag de dag de logboeken van de dag voordat gisteren worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5363c-137">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="5363c-138">Deze instellingen gemakkelijk worden geconfigureerd via de diagnostische instellingen voor een resource in de Azure portal, via Azure PowerShell en CLI-opdrachten of via de [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="5363c-138">These settings are easily configured via the diagnostic settings for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="5363c-139">Diagnostische logboeken en metrische gegevens voor uit de Gast OS-laag van Compute-resources (bijvoorbeeld virtuele machines of Service Fabric) Gebruik [een afzonderlijk mechanisme voor configuratie en de selectie van uitvoer](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5363c-139">Diagnostic logs and metrics for from the guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="5363c-140">Het inschakelen van verzamelen van diagnostische logboeken van resource</span><span class="sxs-lookup"><span data-stu-id="5363c-140">How to enable collection of resource diagnostic logs</span></span>
<span data-ttu-id="5363c-141">Verzamelen van diagnostische logboeken resource kan worden ingeschakeld [als onderdeel van het maken van een resource in het Resource Manager-sjabloon](./monitoring-enable-diagnostic-logs-using-template.md) of nadat een bron wordt gemaakt van de pagina die resource in de portal.</span><span class="sxs-lookup"><span data-stu-id="5363c-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in the portal.</span></span> <span data-ttu-id="5363c-142">U kunt ook de verzameling op elk gewenst moment met behulp van Azure PowerShell of CLI-opdrachten of met behulp van de Monitor REST-API van Azure inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5363c-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="5363c-143">Deze instructies kunnen niet rechtstreeks toepassen op elke resource.</span><span class="sxs-lookup"><span data-stu-id="5363c-143">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="5363c-144">Zie de schema-koppelingen onder aan deze pagina om te begrijpen speciale stappen die van toepassing zijn op bepaalde resourcetypen.</span><span class="sxs-lookup"><span data-stu-id="5363c-144">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-the-portal"></a><span data-ttu-id="5363c-145">Verzamelen van diagnostische logboeken van de resource in de portal</span><span class="sxs-lookup"><span data-stu-id="5363c-145">Enable collection of resource diagnostic logs in the portal</span></span>
<span data-ttu-id="5363c-146">U kunt verzamelen van diagnostische logboeken van de resource in de Azure portal inschakelen nadat een resource is gemaakt door te gaan op een specifieke bron of door te navigeren naar de Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="5363c-146">You can enable collection of resource diagnostic logs in the Azure portal after a resource has been created either by going to a specific resource or by navigating to Azure Monitor.</span></span> <span data-ttu-id="5363c-147">Dit via Azure Monitor inschakelen:</span><span class="sxs-lookup"><span data-stu-id="5363c-147">To enable this via Azure Monitor:</span></span>

1. <span data-ttu-id="5363c-148">In de [Azure-portal](http://portal.azure.com), navigeer naar de Azure-Monitor en klikt u op **diagnostische instellingen**</span><span class="sxs-lookup"><span data-stu-id="5363c-148">In the [Azure portal](http://portal.azure.com), navigate to Azure Monitor and click on **Diagnostic Settings**</span></span>

    ![Sectie van de Monitor Azure bewaking](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="5363c-150">Optioneel de lijst filteren op resourcegroep of brontype en klik vervolgens op de bron die u wilt geen diagnostische instellen.</span><span class="sxs-lookup"><span data-stu-id="5363c-150">Optionally filter the list by resource group or resource type, then click on the resource for which you would like to set a diagnostic setting.</span></span>

3. <span data-ttu-id="5363c-151">Als er geen instellingen bestaan op de bron voor hebt u geselecteerd, u wordt gevraagd om een instelling te maken.</span><span class="sxs-lookup"><span data-stu-id="5363c-151">If no settings exist on the resource you have selected, you are prompted to create a setting.</span></span> <span data-ttu-id="5363c-152">Klik op "Diagnostische gegevens inschakelen."</span><span class="sxs-lookup"><span data-stu-id="5363c-152">Click "Turn on diagnostics."</span></span>

   ![Diagnostische instelling - geen bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="5363c-154">Als er bestaande instellingen op de bron, ziet u een lijst met instellingen die al zijn geconfigureerd op deze resource.</span><span class="sxs-lookup"><span data-stu-id="5363c-154">If there are existing settings on the resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="5363c-155">Klik op 'Diagnostische instelling toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="5363c-155">Click "Add diagnostic setting."</span></span>

   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="5363c-157">Geef een naam van de instelling, schakel de selectievakjes voor elk doel waarnaar u wilt gegevens verzenden, en welke resource wordt gebruikt voor elk doel configureren.</span><span class="sxs-lookup"><span data-stu-id="5363c-157">Give your setting a name, check the boxes for each destination to which you would like to send data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="5363c-158">Eventueel, stel een aantal dagen wilt bewaren van deze logboeken met behulp van de **bewaartermijn (dagen)** schuifregelaars (alleen van toepassing op de opslaglocatie voor de account).</span><span class="sxs-lookup"><span data-stu-id="5363c-158">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders (only applicable to the storage account destination).</span></span> <span data-ttu-id="5363c-159">Een bewaartermijn van nul dagen worden de logboeken voor onbepaalde tijd opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5363c-159">A retention of zero days stores the logs indefinitely.</span></span>
   
   ![Diagnostische instelling - bestaande instellingen toevoegen](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="5363c-161">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5363c-161">Click **Save**.</span></span>

<span data-ttu-id="5363c-162">De nieuwe instelling wordt weergegeven in de lijst met instellingen voor deze bron na enkele ogenblikken en logboeken met diagnostische gegevens worden verzonden naar de opgegeven bestemmingen zodra er nieuwe gebeurtenisgegevens wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5363c-162">After a few moments, the new setting appears in your list of settings for this resource, and diagnostic logs are sent to the specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="5363c-163">Verzamelen van diagnostische logboeken van de resource via PowerShell</span><span class="sxs-lookup"><span data-stu-id="5363c-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="5363c-164">Als u wilt verzamelen van diagnostische logboeken van de resource via Azure PowerShell, gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5363c-164">To enable collection of resource diagnostic logs via Azure PowerShell, use the following commands:</span></span>

<span data-ttu-id="5363c-165">Om opslag van diagnostische logboeken in een opslagaccount, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5363c-165">To enable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="5363c-166">De storage-account-ID is de resource-ID voor het opslagaccount waarnaar u wilt de logboeken verzenden.</span><span class="sxs-lookup"><span data-stu-id="5363c-166">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="5363c-167">Om streaming van logboeken met diagnostische gegevens naar een event hub, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5363c-167">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="5363c-168">De regel-ID van service bus is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="5363c-168">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="5363c-169">Gebruik deze opdracht zodat verzending van diagnostische logboeken naar een Log Analytics-werkruimte:</span><span class="sxs-lookup"><span data-stu-id="5363c-169">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="5363c-170">Kunt u de bron-ID van de werkruimte voor logboekanalyse met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5363c-170">You can obtain the resource ID of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="5363c-171">U kunt deze parameters zodat meerdere uitvoeropties combineren.</span><span class="sxs-lookup"><span data-stu-id="5363c-171">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="5363c-172">Verzamelen van diagnostische logboeken van de resource via CLI</span><span class="sxs-lookup"><span data-stu-id="5363c-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="5363c-173">Als u wilt verzamelen van diagnostische logboeken van de bron via de Azure CLI, gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5363c-173">To enable collection of resource diagnostic logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="5363c-174">Om opslag van diagnostische logboeken in een Opslagaccount, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5363c-174">To enable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="5363c-175">De storage-account-ID is de resource-ID voor het opslagaccount waarnaar u wilt de logboeken verzenden.</span><span class="sxs-lookup"><span data-stu-id="5363c-175">The storage account ID is the resource ID for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="5363c-176">Om streaming van logboeken met diagnostische gegevens naar een event hub, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5363c-176">To enable streaming of diagnostic logs to an event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="5363c-177">De regel-ID van service bus is een tekenreeks met deze indeling: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="5363c-177">The service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="5363c-178">Gebruik deze opdracht zodat verzending van diagnostische logboeken naar een Log Analytics-werkruimte:</span><span class="sxs-lookup"><span data-stu-id="5363c-178">To enable sending of diagnostic logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="5363c-179">U kunt deze parameters zodat meerdere uitvoeropties combineren.</span><span class="sxs-lookup"><span data-stu-id="5363c-179">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="5363c-180">Verzamelen van diagnostische logboeken van de resource via REST-API</span><span class="sxs-lookup"><span data-stu-id="5363c-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="5363c-181">Zie het wijzigen van diagnostische instellingen met de REST-API van Azure Monitor [dit document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="5363c-181">To change diagnostic settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-the-portal"></a><span data-ttu-id="5363c-182">Diagnostische instellingen van de resource in de portal beheren</span><span class="sxs-lookup"><span data-stu-id="5363c-182">Manage resource diagnostic settings in the portal</span></span>
<span data-ttu-id="5363c-183">Zorg ervoor dat alle resources met diagnostische instellingen zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5363c-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="5363c-184">Navigeer naar **Monitor** in de portal en open **diagnostische instellingen**.</span><span class="sxs-lookup"><span data-stu-id="5363c-184">Navigate to **Monitor** in the portal and open **Diagnostic settings**.</span></span>

![Diagnostische logboeken blade in de portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="5363c-186">Wellicht hebt u klikken op 'Meer services' vinden van de Monitor-sectie.</span><span class="sxs-lookup"><span data-stu-id="5363c-186">You may have to click "More services" to find the Monitor section.</span></span>

<span data-ttu-id="5363c-187">Hier kunt u bekijken en alle resources die ondersteuning bieden voor diagnostische instellingen om te zien als ze ingeschakeld diagnostische gegevens hebben filteren.</span><span class="sxs-lookup"><span data-stu-id="5363c-187">Here you can view and filter all resources that support diagnostic settings to see if they have diagnostics enabled.</span></span> <span data-ttu-id="5363c-188">U kunt ook inzoomen om te controleren als er meerdere instellingen zijn ingesteld op een resource en welke storage-account, de Event Hubs-naamruimte en/of de werkruimte voor logboekanalyse die gegevens om te stromen controleren.</span><span class="sxs-lookup"><span data-stu-id="5363c-188">You can also drill down to see if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Diagnostische logboeken resultaten in de portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="5363c-190">Een diagnostische instelling toe te voegen, wordt de weergave van de diagnostische instellingen, waar u kunt inschakelen, uitschakelen of wijzigen van de diagnostische instellingen voor de geselecteerde resource.</span><span class="sxs-lookup"><span data-stu-id="5363c-190">Adding a diagnostic setting brings up the Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="5363c-191">Ondersteunde services, categorieën en schema's voor resource diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="5363c-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="5363c-192">[Raadpleeg dit artikel](monitoring-diagnostic-logs-schema.md) voor een volledige lijst met ondersteunde services en de logboek-categorieën en schema's die worden gebruikt door deze services.</span><span class="sxs-lookup"><span data-stu-id="5363c-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and the log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5363c-193">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5363c-193">Next steps</span></span>

* [<span data-ttu-id="5363c-194">Diagnostische logboeken van de resource te streamen **Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="5363c-194">Stream resource diagnostic logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="5363c-195">Diagnostische instellingen voor bronnen met de REST-API van Azure Monitor wijzigen</span><span class="sxs-lookup"><span data-stu-id="5363c-195">Change resource diagnostic settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="5363c-196">Logboeken van de Azure-opslag met logboekanalyse analyseren</span><span class="sxs-lookup"><span data-stu-id="5363c-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
