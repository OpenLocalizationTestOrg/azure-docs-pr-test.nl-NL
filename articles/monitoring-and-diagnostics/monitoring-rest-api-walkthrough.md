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
# <a name="azure-monitoring-rest-api-walkthrough"></a>Azure Monitoring REST API-overzicht
Dit artikel ziet u hoe tooperform verificatie zodat uw code Hallo kunt [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello Azure Monitor-API maakt het mogelijk tooprogrammatically ophalen Hallo beschikbare standaardregels metrische definities (Hallo type metrische gegevens zoals CPU-tijd, aanvragen, enzovoort), granulatie en metrische waarden. Zodra opgehaald, kunnen Hallo gegevens worden opgeslagen in een afzonderlijke gegevensarchief, zoals Azure SQL Database, Azure Cosmos DB of Azure Data Lake. Van daaruit kan indien nodig aanvullende analyse worden uitgevoerd.

Naast het werken met verschillende punten van de metrische gegevens, zoals in dit artikel wordt gedemonstreerd, maakt Hallo Monitor-API het mogelijk toolist waarschuwingsregels, logboeken van de activiteit bekijken en nog veel meer. Zie voor een volledige lijst van beschikbare bewerkingen Hallo [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Monitor voor Azure aanvragen verifiëren
de eerste stap Hallo is tooauthenticate Hallo-aanvraag.

Alle Hallo taken uitgevoerd met hello Azure Monitor API gebruik hello Azure Resource Manager-verificatiemodel. Alle aanvragen moeten daarom worden geverifieerd bij Azure Active Directory (Azure AD). Een benadering tooauthenticate Hallo-clienttoepassing toocreate is een Azure AD-service-principal en Hallo verificatietoken (JWT) ophalen. Hallo volgende voorbeeldscript wordt gedemonstreerd maken van een Azure AD-service-principal via PowerShell. Raadpleeg voor een meer gedetailleerde procedure toohello documentatie op [met behulp van Azure PowerShell toocreate de bronnen van een service-principal tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Het kan ook te[maken van een service-principal via hello Azure-portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).

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

tooquery hello Azure Monitor API, client-toepassing hello gebruik Hallo service principal tooauthenticate eerder hebt gemaakt. Hallo volgende PowerShell-voorbeeldscript ziet u een benadering, met behulp van Hallo [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp verificatie van Hallo JWT-token ophalen. Hallo JWT-token is doorgegeven als onderdeel van een HTTP-autorisatie-parameter in aanvragen toohello REST-API van Azure-Monitor.

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

Zodra instellingsstap Hallo-verificatie voltooid is, kunnen query's tegen Hallo Monitor REST-API van Azure worden uitgevoerd. Er zijn twee handig query's:

1. Lijst Hallo metrische definities voor een bron
2. Hallo metrische waarden ophalen

## <a name="retrieve-metric-definitions"></a>Metrische definities ophalen
> [!NOTE]
> tooretrieve metrische definities met hello Azure Monitor REST-API gebruiken '2016-03-01' Hallo API-versie.
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
Voor een Azure Logic App zou Hallo metrische definities vergelijkbare toohello schermafbeelding volgende weergegeven:

![ALT 'Weergave van metrische definitie antwoord JSON'.](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Zie voor meer informatie, Hallo [lijst Hallo metrische definities voor een resource in de REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentatie.

## <a name="retrieve-metric-values"></a>Metrische waarden ophalen
Zodra de beschikbare metrische definities Hallo gekend zijn, is het vervolgens mogelijke tooretrieve Hallo verwante metrische waarden. Hallo-metric naam 'value' (geen hello 'localizedValue') gebruiken voor alle filtering aanvragen (bijvoorbeeld ophalen Hallo 'CpuTime' en 'Aanvragen' metrische gegevenspunten). Als er geen filters worden opgegeven, wordt de Hallo standaard metric geretourneerd.

> [!NOTE]
> tooretrieve metrische waarden met hello Azure Monitor REST API, gebruik '2016-06-01' als Hallo API-versie.
>
>

**Methode**: ophalen

**URI van de aanvraag**: https://management.azure.com/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource provider naamruimte}*/*{resourcetype}*/*{resourcenaam}*/providers/microsoft.insights/metrics?$filter=*{filter}*& api-version =*{apiVersion}*

Tooretrieve hello RunsSucceeded metrische gegevenspunten voor Hallo opgegeven tijdsbereik en voor een tijdgranulariteit op van 1 uur, Hallo aanvraag zou bijvoorbeeld als volgt zijn:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

Hallo resultaat zou vergelijkbaar toohello voorbeeld schermafbeelding volgende weergegeven:

![ALT "JSON-antwoord met metrische waarde voor gemiddelde reactietijd"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

zoals te zien is in het volgende voorbeeld Hallo meerdere gegevens of aggregatie verwijst, tooretrieve Hallo metrische definitie namen en aggregatie typen toohello filter toevoegen:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Gebruik ARMClient
Een alternatieve toousing PowerShell (zoals hierboven), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) op uw Windows-machine. ARMClient verwerkt automatisch hello Azure AD-verificatie (en resulterende JWT-token). Hallo volgende stappen wordt uitgelegd gebruik van ARMClient voor het ophalen van de metrische gegevens:

1. Installeer [Chocolatey](https://chocolatey.org/) en [ARMClient](https://github.com/projectkudu/ARMClient).
2. Typ in een terminalvenster *armclient.exe aanmelding*. Hiermee vraagt u toolog in tooAzure.
3. Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT 'Using ARMClient toowork Hello Azure bewaking REST-API'](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Hallo-bron-ID ophalen
Met behulp van Hallo REST-API kunt echt toounderstand Hallo beschikbaar metrische definities granulatie en bijbehorende waarden. Die informatie is nuttig wanneer u Hallo [Azure Management-bibliotheek](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Hallo resource-ID toouse is voor Hallo voorafgaand aan code, Hallo volledig pad toohello gewenst Azure-resource. Bijvoorbeeld: tooquery op basis van een Azure-Web-App Hallo resource-ID zou zijn:

*/Subscriptions/{Subscription-id}/resourceGroups/{resource-Group-Name}/providers/Microsoft.Web/sites/{site-name}/*

Hallo bevat volgende lijst enkele voorbeelden van resource-ID-notaties voor verschillende Azure-resources:

* **IoT Hub** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*
* **Elastische SQL-groep** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*
* **SQL-Database (v12)** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{servernaam}*/databases/*{databasenaam}*
* **Service Bus** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{naamruimte}*/*{servicebus-name}*
* **VM-Schaalsets** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-naam}*
* **Virtuele machines** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-naam}*
* **Event Hubs** -/subscriptions/*{abonnement-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-naamruimte}*

Er zijn alternatieve benaderingen tooretrieving Hallo resource-ID, inclusief het gebruik van Azure Resource Explorer, Hallo gewenst resource weergeven in hello Azure-portal en via PowerShell of hello Azure CLI.

### <a name="azure-resource-explorer"></a>Azure Resource Explorer
toofind hello resource-ID voor een gewenste resource, een handig aanpak is toouse hello [Azure Resource Explorer](https://resources.azure.com) hulpprogramma. Navigeer toohello gewenst resource en vervolgens kijkt weergegeven, zoals in de volgende schermafbeelding Hallo Hallo-ID:

![ALT 'Azure Resource Explorer'](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Azure Portal
Hallo-bron-ID kan ook worden opgehaald uit hello Azure-portal. toodo dus toohello gewenst resource navigeren en selecteer Eigenschappen. Hallo-bron-ID wordt weergegeven in de eigenschappenblade hello, zoals in de volgende schermafbeelding Hallo:

![ALT "Resource-ID weergegeven in de eigenschappenblade Hallo in hello Azure-portal](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Hallo-bron-ID kan worden opgehaald met behulp van Azure PowerShell-cmdlets. Bijvoorbeeld tooobtain Hallo resource-ID voor een Azure-Web-App, Hallo Get AzureRmWebApp cmdlet, zoals in de volgende schermafbeelding Hallo uitvoeren:

![ALT "Resource-ID verkregen met behulp van PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Azure CLI
tooretrieve Hallo resource-ID hello Azure CLI gebruiken, voert u Hallo 'azure webapp weergeven' opdracht geven Hallo '--json' optie, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![ALT "Resource-ID verkregen met behulp van PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Ophalen van de logboekgegevens van de activiteit
In aanvulling tooworking met metrische definities en de bijbehorende waarden is het ook mogelijk tooretrieve aanvullende interessante inzichten gerelateerde tooAzure bronnen. Als een voorbeeld is het mogelijk tooquery [activiteitenlogboek](https://msdn.microsoft.com/library/azure/dn931934.aspx) gegevens. Hallo volgende voorbeeld wordt gedemonstreerd met behulp van hello Azure Monitor REST-API tooquery activiteit logboekgegevens binnen een bepaald datumbereik voor een Azure-abonnement:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Volgende stappen
* Bekijk Hallo [overzicht van bewaking](monitoring-overview.md).
* Weergave Hallo [ondersteund met een Azure-Monitor](monitoring-supported-metrics.md).
* Bekijk Hallo [Microsoft Azure Monitor REST API-verwijzing](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Bekijk Hallo [Azure Management-bibliotheek](https://msdn.microsoft.com/library/azure/mt417623.aspx).
