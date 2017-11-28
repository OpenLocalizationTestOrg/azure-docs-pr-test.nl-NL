---
title: aaaAzure bewaking REST-API-overzicht | Microsoft Docs
description: Hoe aanvragen tooauthenticate tooand gebruik hello Azure Monitoring REST-API.
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="a2932-103">Azure Monitoring REST API-overzicht</span><span class="sxs-lookup"><span data-stu-id="a2932-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="a2932-104">Dit artikel ziet u hoe tooperform verificatie zodat uw code Hallo kunt [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2932-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="a2932-105">Hello Azure Monitor-API maakt het mogelijk tooprogrammatically ophalen Hallo beschikbare standaardregels metrische definities (Hallo type metrische gegevens zoals CPU-tijd, aanvragen, enzovoort), granulatie en metrische waarden.</span><span class="sxs-lookup"><span data-stu-id="a2932-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="a2932-106">Zodra opgehaald, kunnen Hallo gegevens worden opgeslagen in een afzonderlijke gegevensarchief, zoals Azure SQL Database, Azure Cosmos DB of Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a2932-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="a2932-107">Van daaruit kan indien nodig aanvullende analyse worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2932-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="a2932-108">Naast het werken met verschillende punten van de metrische gegevens, zoals in dit artikel wordt gedemonstreerd, maakt Hallo Monitor-API het mogelijk toolist waarschuwingsregels, logboeken van de activiteit bekijken en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="a2932-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="a2932-109">Zie voor een volledige lijst van beschikbare bewerkingen Hallo [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2932-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="a2932-110">Monitor voor Azure aanvragen verifiëren</span><span class="sxs-lookup"><span data-stu-id="a2932-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="a2932-111">de eerste stap Hallo is tooauthenticate Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a2932-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="a2932-112">Alle Hallo taken uitgevoerd met hello Azure Monitor API gebruik hello Azure Resource Manager-verificatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a2932-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="a2932-113">Alle aanvragen moeten daarom worden geverifieerd bij Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2932-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a2932-114">Een benadering tooauthenticate Hallo-clienttoepassing toocreate is een Azure AD-service-principal en Hallo verificatietoken (JWT) ophalen.</span><span class="sxs-lookup"><span data-stu-id="a2932-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="a2932-115">Hallo volgende voorbeeldscript wordt gedemonstreerd maken van een Azure AD-service-principal via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2932-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="a2932-116">Raadpleeg voor een meer gedetailleerde procedure toohello documentatie op [met behulp van Azure PowerShell toocreate de bronnen van een service-principal tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="a2932-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="a2932-117">Het kan ook te[maken van een service-principal via hello Azure-portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2932-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

<span data-ttu-id="a2932-118">tooquery hello Azure Monitor API, client-toepassing hello gebruik Hallo service principal tooauthenticate eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a2932-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="a2932-119">Hallo volgende PowerShell-voorbeeldscript ziet u een benadering, met behulp van Hallo [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp verificatie van Hallo JWT-token ophalen.</span><span class="sxs-lookup"><span data-stu-id="a2932-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="a2932-120">Hallo JWT-token is doorgegeven als onderdeel van een HTTP-autorisatie-parameter in aanvragen toohello REST-API van Azure-Monitor.</span><span class="sxs-lookup"><span data-stu-id="a2932-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

<span data-ttu-id="a2932-121">Zodra instellingsstap Hallo-verificatie voltooid is, kunnen query's tegen Hallo Monitor REST-API van Azure worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a2932-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="a2932-122">Er zijn twee handig query's:</span><span class="sxs-lookup"><span data-stu-id="a2932-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="a2932-123">Lijst Hallo metrische definities voor een bron</span><span class="sxs-lookup"><span data-stu-id="a2932-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="a2932-124">Hallo metrische waarden ophalen</span><span class="sxs-lookup"><span data-stu-id="a2932-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="a2932-125">Metrische definities ophalen</span><span class="sxs-lookup"><span data-stu-id="a2932-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="a2932-126">tooretrieve metrische definities met hello Azure Monitor REST-API gebruiken '2016-03-01' Hallo API-versie.</span><span class="sxs-lookup"><span data-stu-id="a2932-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
<span data-ttu-id="a2932-127">Voor een Azure Logic App zou Hallo metrische definities vergelijkbare toohello schermafbeelding volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a2932-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![ALT 'Weergave van metrische definitie antwoord JSON'.](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="a2932-129">Zie voor meer informatie, Hallo [lijst Hallo metrische definities voor een resource in de REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentatie.</span><span class="sxs-lookup"><span data-stu-id="a2932-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="a2932-130">Metrische waarden ophalen</span><span class="sxs-lookup"><span data-stu-id="a2932-130">Retrieve Metric Values</span></span>
<span data-ttu-id="a2932-131">Zodra de beschikbare metrische definities Hallo gekend zijn, is het vervolgens mogelijke tooretrieve Hallo verwante metrische waarden.</span><span class="sxs-lookup"><span data-stu-id="a2932-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="a2932-132">Hallo-metric naam 'value' (geen hello 'localizedValue') gebruiken voor alle filtering aanvragen (bijvoorbeeld ophalen Hallo 'CpuTime' en 'Aanvragen' metrische gegevenspunten).</span><span class="sxs-lookup"><span data-stu-id="a2932-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="a2932-133">Als er geen filters worden opgegeven, wordt de Hallo standaard metric geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a2932-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="a2932-134">tooretrieve metrische waarden met hello Azure Monitor REST API, gebruik '2016-06-01' als Hallo API-versie.</span><span class="sxs-lookup"><span data-stu-id="a2932-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="a2932-135">**Methode**: ophalen</span><span class="sxs-lookup"><span data-stu-id="a2932-135">**Method**: GET</span></span>

<span data-ttu-id="a2932-136">**URI van de aanvraag**: https://management.azure.com/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource provider naamruimte}*/*{resourcetype}*/*{resourcenaam}*/providers/microsoft.insights/metrics?$filter=*{filter}*& api-version =*{apiVersion}*</span><span class="sxs-lookup"><span data-stu-id="a2932-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="a2932-137">Tooretrieve hello RunsSucceeded metrische gegevenspunten voor Hallo opgegeven tijdsbereik en voor een tijdgranulariteit op van 1 uur, Hallo aanvraag zou bijvoorbeeld als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="a2932-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="a2932-138">Hallo resultaat zou vergelijkbaar toohello voorbeeld schermafbeelding volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a2932-138">hello result would appear similar toohello example following screenshot:</span></span>

![ALT "JSON-antwoord met metrische waarde voor gemiddelde reactietijd"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="a2932-140">zoals te zien is in het volgende voorbeeld Hallo meerdere gegevens of aggregatie verwijst, tooretrieve Hallo metrische definitie namen en aggregatie typen toohello filter toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a2932-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="a2932-141">Gebruik ARMClient</span><span class="sxs-lookup"><span data-stu-id="a2932-141">Use ARMClient</span></span>
<span data-ttu-id="a2932-142">Een alternatieve toousing PowerShell (zoals hierboven), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) op uw Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="a2932-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="a2932-143">ARMClient verwerkt automatisch hello Azure AD-verificatie (en resulterende JWT-token).</span><span class="sxs-lookup"><span data-stu-id="a2932-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="a2932-144">Hallo volgende stappen wordt uitgelegd gebruik van ARMClient voor het ophalen van de metrische gegevens:</span><span class="sxs-lookup"><span data-stu-id="a2932-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="a2932-145">Installeer [Chocolatey](https://chocolatey.org/) en [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="a2932-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="a2932-146">Typ in een terminalvenster *armclient.exe aanmelding*.</span><span class="sxs-lookup"><span data-stu-id="a2932-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="a2932-147">Hiermee vraagt u toolog in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a2932-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="a2932-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span><span class="sxs-lookup"><span data-stu-id="a2932-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="a2932-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span><span class="sxs-lookup"><span data-stu-id="a2932-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT 'Using ARMClient toowork Hello Azure bewaking REST-API'](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="a2932-151">Hallo-bron-ID ophalen</span><span class="sxs-lookup"><span data-stu-id="a2932-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="a2932-152">Met behulp van Hallo REST-API kunt echt toounderstand Hallo beschikbaar metrische definities granulatie en bijbehorende waarden.</span><span class="sxs-lookup"><span data-stu-id="a2932-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="a2932-153">Die informatie is nuttig wanneer u Hallo [Azure Management-bibliotheek](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2932-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="a2932-154">Hallo resource-ID toouse is voor Hallo voorafgaand aan code, Hallo volledig pad toohello gewenst Azure-resource.</span><span class="sxs-lookup"><span data-stu-id="a2932-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="a2932-155">Bijvoorbeeld: tooquery op basis van een Azure-Web-App Hallo resource-ID zou zijn:</span><span class="sxs-lookup"><span data-stu-id="a2932-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="a2932-156">*/Subscriptions/{Subscription-id}/resourceGroups/{resource-Group-Name}/providers/Microsoft.Web/sites/{site-name}/*</span><span class="sxs-lookup"><span data-stu-id="a2932-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="a2932-157">Hallo bevat volgende lijst enkele voorbeelden van resource-ID-notaties voor verschillende Azure-resources:</span><span class="sxs-lookup"><span data-stu-id="a2932-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="a2932-158">**IoT Hub** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span><span class="sxs-lookup"><span data-stu-id="a2932-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="a2932-159">**Elastische SQL-groep** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span><span class="sxs-lookup"><span data-stu-id="a2932-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="a2932-160">**SQL-Database (v12)** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{servernaam}*/databases/*{databasenaam}*</span><span class="sxs-lookup"><span data-stu-id="a2932-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="a2932-161">**Service Bus** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{naamruimte}*/*{servicebus-name}*</span><span class="sxs-lookup"><span data-stu-id="a2932-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="a2932-162">**VM-Schaalsets** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-naam}*</span><span class="sxs-lookup"><span data-stu-id="a2932-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="a2932-163">**Virtuele machines** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-naam}*</span><span class="sxs-lookup"><span data-stu-id="a2932-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="a2932-164">**Event Hubs** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-naamruimte}*</span><span class="sxs-lookup"><span data-stu-id="a2932-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="a2932-165">Er zijn alternatieve benaderingen tooretrieving Hallo resource-ID, inclusief het gebruik van Azure Resource Explorer, Hallo gewenst resource weergeven in hello Azure-portal en via PowerShell of hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a2932-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="a2932-166">Azure Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="a2932-166">Azure Resource Explorer</span></span>
<span data-ttu-id="a2932-167">toofind hello resource-ID voor een gewenste resource, een handig aanpak is toouse hello [Azure Resource Explorer](https://resources.azure.com) hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="a2932-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="a2932-168">Navigeer toohello gewenst resource en vervolgens kijkt weergegeven, zoals in de volgende schermafbeelding Hallo Hallo-ID:</span><span class="sxs-lookup"><span data-stu-id="a2932-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![ALT 'Azure Resource Explorer'](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="a2932-170">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a2932-170">Azure portal</span></span>
<span data-ttu-id="a2932-171">Hallo-bron-ID kan ook worden opgehaald uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a2932-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="a2932-172">toodo dus toohello gewenst resource navigeren en selecteer Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="a2932-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="a2932-173">Hallo-bron-ID wordt weergegeven in de eigenschappenblade hello, zoals in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="a2932-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT "Resource-ID weergegeven in de eigenschappenblade Hallo in hello Azure-portal](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="a2932-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2932-175">Azure PowerShell</span></span>
<span data-ttu-id="a2932-176">Hallo-bron-ID kan worden opgehaald met behulp van Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a2932-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="a2932-177">Bijvoorbeeld tooobtain Hallo resource-ID voor een Azure-Web-App, Hallo Get AzureRmWebApp cmdlet, zoals in de volgende schermafbeelding Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a2932-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![ALT "Resource-ID verkregen met behulp van PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="a2932-179">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a2932-179">Azure CLI</span></span>
<span data-ttu-id="a2932-180">tooretrieve Hallo resource-ID hello Azure CLI gebruiken, voert u Hallo 'azure webapp weergeven' opdracht geven Hallo '--json' optie, zoals wordt weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="a2932-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![ALT "Resource-ID verkregen met behulp van PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="a2932-182">Ophalen van de logboekgegevens van de activiteit</span><span class="sxs-lookup"><span data-stu-id="a2932-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="a2932-183">In aanvulling tooworking met metrische definities en de bijbehorende waarden is het ook mogelijk tooretrieve aanvullende interessante inzichten gerelateerde tooAzure bronnen.</span><span class="sxs-lookup"><span data-stu-id="a2932-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="a2932-184">Als een voorbeeld is het mogelijk tooquery [activiteitenlogboek](https://msdn.microsoft.com/library/azure/dn931934.aspx) gegevens.</span><span class="sxs-lookup"><span data-stu-id="a2932-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="a2932-185">Hallo volgende voorbeeld wordt gedemonstreerd met behulp van hello Azure Monitor REST-API tooquery activiteit logboekgegevens binnen een bepaald datumbereik voor een Azure-abonnement:</span><span class="sxs-lookup"><span data-stu-id="a2932-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="a2932-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a2932-186">Next steps</span></span>
* <span data-ttu-id="a2932-187">Bekijk Hallo [overzicht van bewaking](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2932-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="a2932-188">Weergave Hallo [ondersteund met een Azure-Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a2932-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="a2932-189">Bekijk Hallo [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2932-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="a2932-190">Bekijk Hallo [Azure Management-bibliotheek](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="a2932-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
