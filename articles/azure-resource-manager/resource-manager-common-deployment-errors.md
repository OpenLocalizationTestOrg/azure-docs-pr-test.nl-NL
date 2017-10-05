---
title: Veelvoorkomende fouten van de Azure-implementatie oplossen | Microsoft Docs
description: Beschrijft hoe u veelvoorkomende fouten oplossen wanneer u resources in Azure met Azure Resource Manager implementeert.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren in azure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager oplossen
Dit onderwerp wordt beschreven hoe u een aantal gemeenschappelijke kunt oplossen Azure-implementatiefouten kunnen optreden.

De volgende foutcodes worden beschreven in dit onderwerp:

* [AccountNameInvalid](#accountnameinvalid)
* [Verificatie mislukt](#authorization-failed)
* [BadRequest](#badrequest)
* [Implementatie mislukt](#deploymentfailed)
* [DisallowedOperation](#disallowedoperation)
* [InvalidContentLink](#invalidcontentlink)
* [InvalidTemplate](#invalidtemplate)
* [MissingSubscriptionRegistration](#noregisteredproviderfound)
* [NotFound](#notfound)
* [NoRegisteredProviderFound](#noregisteredproviderfound)
* [OperationNotAllowed](#quotaexceeded)
* [ParentResourceNotFound](#parentresourcenotfound)
* [QuotaExceeded](#quotaexceeded)
* [RequestDisallowedByPolicy](#requestdisallowedbypolicy)
* [ResourceNotFound](#notfound)
* [SkuNotAvailable](#skunotavailable)
* [StorageAccountAlreadyExists](#storagenamenotunique)
* [StorageAccountAlreadyTaken](#storagenamenotunique)

## <a name="deploymentfailed"></a>Implementatie mislukt

Deze foutcode geeft een algemene implementatiefout, maar het is niet de foutcode die u wilt beginnen met het oplossen. De foutcode die daadwerkelijk helpt u los het probleem is meestal één niveau onder deze fout. Bijvoorbeeld de volgende afbeelding toont de **RequestDisallowedByPolicy** foutcode die zich in de implementatiefout.

![foutcode weergeven](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Bij het implementeren van een resource (meestal een virtuele machine), wordt de volgende foutcode en een foutbericht weergegeven:

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

U ontvangt deze foutmelding wanneer de SKU die u hebt geselecteerd (zoals VM-grootte) van de resource is niet beschikbaar voor de locatie die u hebt geselecteerd. U lost dit probleem, moet u bepalen welke SKU's zijn beschikbaar in een regio. U kunt PowerShell, de portal of REST-bewerking gebruiken om te zoeken naar beschikbare SKU's.

- Gebruik voor PowerShell [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) en filteren op locatie. U kunt de nieuwste versie van PowerShell voor deze opdracht moet hebben.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  De resultaten bevatten een lijst van SKU's voor de locatie en beperkingen voor deze SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Gebruik de [portal](https://portal.azure.com), aanmelden bij de portal en toevoegen van een bron via de interface. Als u de waarden instelt, ziet u de beschikbare SKU's voor die bron. U hoeft niet om de implementatie te vervolledigen.

    ![beschikbare SKU 's](./media/resource-manager-common-deployment-errors/view-sku.png)

- Voor het gebruik van de REST-API voor virtuele machines, moet u de volgende aanvraag verzenden:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Deze retourneert beschikbare SKU's en regio's in de volgende indeling:

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

Als u niet een geschikte SKU gevonden in deze regio of een alternatieve regio die voldoet aan uw bedrijf moet, dienen een [SKU aanvraag](https://aka.ms/skurestriction) voor ondersteuning van Azure.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

Als deze fout wordt weergegeven, gebruikt u een abonnement dat is niet toegestaan voor toegang tot alle Azure-services dan Azure Active Directory. Dit type abonnement wellicht op wanneer u moet toegang hebben tot de klassieke portal, maar zijn niet toegestaan voor het implementeren van resources. U lost dit probleem, moet u een abonnement dat gemachtigd is om resources implementeren.  

Als u wilt weergeven van de beschikbare abonnementen met PowerShell, gebruikt u:

```powershell
Get-AzureRmSubscription
```

En u kunt het huidige abonnement instellen met:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

Als u wilt weergeven van de beschikbare abonnementen met Azure CLI 2.0, gebruiken:

```azurecli
az account list
```

En u kunt het huidige abonnement instellen met:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Deze fout kan leiden tot verschillende typen fouten.

- Syntaxisfout

   Als u een foutbericht dat aangeeft de validatie van de sjabloon is mislukt ontvangt dat, hebt u mogelijk een probleem met de syntaxis in de sjabloon.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Dit is een fout gemakkelijk maken omdat sjabloonexpressies kunnen ingewikkeld zijn. De naamtoewijzing van de volgende voor een opslagaccount bevat bijvoorbeeld een reeks vierkante haken, drie functies drie sets van haakjes, één set met enkele aanhalingstekens en één eigenschap:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Als u de syntaxis van de overeenkomende niet opgeeft, wordt in de sjabloon een waarde die is anders dan uw bedoeling produceert.

   Wanneer u dit type fout ontvangt, zorgvuldig door de expressiesyntaxis van de. Overweeg het gebruik van een JSON-editor, zoals [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) of [Visual Studio Code](resource-manager-vs-code.md), die u kunt gewaarschuwd over syntaxisfouten.

- Onjuiste segment lengten

   Een andere ongeldige sjabloon-fout treedt op wanneer de resourcenaam niet de juiste indeling is.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Een bron voor het niveau van hoofdmap moet één minder segment hebben van de naam dan in het brontype. Elk segment wordt onderscheiden door een slash. In het volgende voorbeeld wordt het type heeft twee segmenten en de naam van de één segment dus is het een **geldige naam**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Maar het volgende voorbeeld is **niet de naam van een geldige** omdat er hetzelfde aantal segmenten als het type.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Hebben hetzelfde aantal segmenten voor onderliggende resources, het type en de naam. Dit aantal segmenten zin omdat de volledige naam en type voor het onderliggende element bevat de naam van het bovenliggende en het type. Daarom heeft de volledige naam nog steeds één minder segment dan het volledige type.

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   Ophalen van de segmenten rechts is lastig met Resource Manager-typen die worden toegepast op de resourceproviders. Bijvoorbeeld, een resource-vergrendeling wordt toegepast op een website, is een type met vier segmenten vereist. Daarom is de naam van de drie segmenten:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Index van de kopie wordt niet verwacht.

   U tegenkomt dit **InvalidTemplate** fout wanneer u hebt toegepast de **kopie** element een deel van de sjabloon die geen ondersteuning biedt voor dit element. U kunt het element kopiëren alleen toepassen op een resourcetype. U kunt kopiëren niet toepassen op een eigenschap binnen een resourcetype. Bijvoorbeeld, u kopie toepassen op een virtuele machine, maar u kunt deze toepassen op de OS-schijven voor een virtuele machine. In sommige gevallen kunt u een onderliggende resource niet converteren naar een bovenliggende resource voor het maken van een kopie-lus. Zie voor meer informatie over het gebruik van kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).

- Parameter is niet geldig

   Als de sjabloon toegestane waarden voor een parameter worden, en u een waarde die niet een van deze waarden opgeven, ontvangt u een bericht dat lijkt op de volgende fout:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   Dubbele de toegestane waarden in de sjabloon en geef een tijdens de implementatie.

- Kringafhankelijkheid gedetecteerd

   U ontvangt deze foutmelding wanneer resources afhankelijk van elkaar op een manier waardoor de implementatie zijn niet worden gestart. Een combinatie van afhankelijkheden maakt twee of meer resources, wacht u totdat de andere bronnen die ook wachten. Bijvoorbeeld resource1 is afhankelijk van resource3, resource2, is afhankelijk van resource1 en resource3 is afhankelijk van resource2. Meestal kunt u dit probleem oplossen door het verwijderen van onnodige afhankelijkheden. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound en ResourceNotFound
Wanneer de sjabloon de naam van een resource die niet kan worden omgezet bevat, wordt een foutbericht zoals:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Als u probeert de ontbrekende resource in de sjabloon te implementeren, controleert u of u moet een afhankelijkheid toevoegen. Resource Manager optimaliseert implementatie door het maken van resources parallel indien mogelijk. Als een resource moet worden geïmplementeerd nadat een andere resource, moet u de **dependsOn** element in de sjabloon voor het maken van een afhankelijkheid op de andere resource. Bijvoorbeeld, wanneer u een web-app implementeert, moet de App Service-abonnement bestaan. Als de web-app is afhankelijk van de App Service-abonnement is niet opgegeven, wordt met Resource Manager beide resources maakt op hetzelfde moment. U ontvangt een foutmelding weergegeven dat de resource voor de App Service-abonnement kan niet worden gevonden, omdat deze niet bestaat nog bij een poging tot een eigenschap instellen voor de web-app. U kunt deze fout voorkomen door het instellen van de afhankelijkheid in de web-app.

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

Zie voor suggesties over het oplossen van afhankelijkheidsfouten [volgorde van de implementatie controleren](#check-deployment-sequence).

Deze fout wordt ook zien wanneer de bron bestaat in een andere resourcegroep dan de versie die wordt geïmplementeerd. In dat geval gebruiken de [resourceId functie](resource-group-template-functions-resource.md#resourceid) ophalen van de volledig gekwalificeerde naam van de resource.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Als u probeert te gebruiken de [verwijzing](resource-group-template-functions-resource.md#reference) of [listKeys](resource-group-template-functions-resource.md#listkeys) werkt in combinatie met een resource die niet kunnen worden omgezet, het volgende foutbericht:

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Zoek naar een expressie met de **verwijzing** functie. Controleer of de parameterwaarden juist zijn.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Wanneer een bron een bovenliggend item naar een andere bron is, moet de bovenliggende resource bestaan voordat u de onderliggende resource maakt. Als deze nog niet bestaat, wordt het volgende foutbericht weergegeven:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

De naam van de onderliggende resource bevat de naam van de bovenliggende. Bijvoorbeeld, kunnen een SQL-Database worden gedefinieerd als:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Maar als u een afhankelijkheid op de bovenliggende resource niet opgeeft, de onderliggende resource kan ophalen geïmplementeerd voordat u de bovenliggende. U lost deze fout, bevatten een afhankelijkheid.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists en StorageAccountAlreadyTaken
U moet een naam voor de resource die uniek is voor alle Azure opgeven voor de storage-accounts. Als u niet een unieke naam opgeeft, wordt een fout als volgt:

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

U kunt een unieke naam maken door het samenvoegen van de naamconventie met het resultaat van de [uniqueString](resource-group-template-functions-string.md#uniquestring) functie.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Als u een opslagaccount met dezelfde naam als een bestaand opslagaccount in uw abonnement implementeren, maar een andere locatie opgeven, ontvangt u een foutbericht retourneren over dat de storage-account bestaat al in een andere locatie. Verwijder de bestaande opslagaccount of geef dezelfde locatie als het bestaande opslagaccount.

## <a name="accountnameinvalid"></a>AccountNameInvalid
U ziet de **AccountNameInvalid** fout bij poging een storage-account een naam te geven met tekens verboden. Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken. De [uniqueString](resource-group-template-functions-string.md#uniquestring) functie retourneert 13 tekens. Als het samenvoegen van een voorvoegsel van de **uniqueString** leiden, geeft u een voorvoegsel 11 tekens of minder.

## <a name="badrequest"></a>BadRequest

De status van een BadRequest kunnen optreden wanneer u een ongeldige waarde voor een eigenschap opgeeft. Bijvoorbeeld, als u een onjuiste waarde voor de SKU voor een opslagaccount opgeeft, mislukt de implementatie. Kijken om te bepalen van geldige waarden voor de eigenschap, de [REST-API](/rest/api) voor het brontype dat u implementeert.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound en MissingSubscriptionRegistration
Bij het implementeren van de resource wordt de volgende foutcode en het bericht:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Of een vergelijkbaar bericht waarin wordt vermeld:

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

U ontvangt deze fouten voor een van drie redenen:

1. De resourceprovider is niet geregistreerd voor uw abonnement
2. API-versie niet ondersteund voor het brontype
3. Locatie niet ondersteund voor het brontype

Het foutbericht geeft suggesties voor de ondersteunde locaties en API-versies. U kunt uw sjabloon wijzigen in een van de voorgestelde waarden. De meeste providers zijn geregistreerde automatisch door de Azure-portal of de opdrachtregelinterface die u gebruikt, maar niet alle. Als u niet een bepaalde bron-provider voorafgaand aan hebt gebruikt, moet u wellicht dat de provider te registreren. U kunt meer informatie over resourceproviders via PowerShell of Azure CLI detecteren.

**Portal**

U kunt de registratiestatus zien en de naamruimte via de portal een resourceprovider registreren.

1. Selecteer voor uw abonnement, **resourceproviders**.

   ![resourceproviders selecteren](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Bekijk de lijst met resourceproviders en selecteer indien nodig de **registreren** koppeling naar de registerbronprovider is van het type dat u probeert te implementeren.

   ![resourceproviders vermelden](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

Als de registratiestatus van uw wilt weergeven, gebruikt **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

Gebruik voor het registreren van een provider **registreren AzureRmResourceProvider** en geef de naam van de resourceprovider die u wilt registreren.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

Als u de ondersteunde locaties voor een bepaald type resource, gebruikt u:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Als u de ondersteunde API-versies voor een bepaald type resource, gebruikt u:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure-CLI**

U kunt controleren of de provider is geregistreerd, gebruiken de `azure provider list` opdracht.

```azurecli
az provider list
```

Voor het registreren van een resourceprovider, gebruiken de `azure provider register` opdracht in en geef de *naamruimte* te registreren.

```azurecli
az provider register --namespace Microsoft.Cdn
```

Overzicht van de ondersteunde locaties en API-versies voor een brontype gebruiken:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded en OperationNotAllowed
Mogelijk hebt u problemen als implementatie groter is dan een quotum die kan per resourcegroep, abonnementen, accounts en andere bereiken worden. Uw abonnement kan bijvoorbeeld worden geconfigureerd om te beperken het aantal kernen voor een regio. Als u een virtuele machine met meer cores dan de toegestane hoeveelheid implementeren probeert, ontvangt u een foutmelding weergegeven dat het quotum is overschreden.
Zie voor informatie voltooid quotum [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).

Als u wilt onderzoeken quota's voor uw abonnement voor kernen, kunt u de `azure vm list-usage` opdracht in de Azure CLI. Het volgende voorbeeld ziet u dat de kerngeheugenquotum voor een gratis proefaccount 4 is:

```azurecli
az vm list-usage --location "South Central US"
```

Die wordt geretourneerd:

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

Als u een sjabloon die meer dan vier kernen in de regio VS-West maakt implementeert, kunt u een implementatiefout dat lijkt op krijgen:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

In PowerShell kunt u de **Get-AzureRmVMUsage** cmdlet.

```powershell
Get-AzureRmVMUsage
```

Die wordt geretourneerd:

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

In dergelijke gevallen moet u gaat u naar de portal en het bestand een probleem met ondersteuning voor het genereren van uw quotum voor de regio waarin u wilt implementeren.

> [!NOTE]
> Vergeet niet dat voor de resourcegroepen het quotum voor elke afzonderlijke regio, niet voor het hele abonnement. Als u implementeren, 30 kernen in VS-West wilt, hebt u vragen om 30 Resource Manager kernen in VS-West. Als u implementeren, 30 kernen in een van de regio's waartoe u toegang hebt wilt, vraagt u 30 Resource Manager kernen in alle regio's.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Wanneer u ontvangt het foutbericht weergegeven:

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

U hebt waarschijnlijk geprobeerd om te koppelen aan een geneste sjabloon die niet beschikbaar. Controleer de URI die u hebt opgegeven voor de geneste sjabloon. Als de sjabloon in een opslagaccount bestaat, zorg er dan voor dat de URI is toegankelijk. U moet mogelijk een SAS-token doorgeven. Zie voor meer informatie [Gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
U ontvangt deze foutmelding wanneer uw abonnement bevat een bronbeleid een actie die u probeert uit te voeren tijdens de implementatie wordt verhinderd. Zoek naar de beleids-id in het foutbericht.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

In **PowerShell**, bieden die beleids-id als de **Id** parameter voor het ophalen van informatie over het beleid dat uw implementatie geblokkeerd.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

In **Azure CLI**, geef de naam van de definitie voor:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Raadpleeg voor meer informatie de volgende artikelen:

- [RequestDisallowedByPolicy-fout](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Beleid gebruiken voor het beheren van resources en toegangsbeheer](resource-manager-policy.md).

## <a name="authorization-failed"></a>Verificatie mislukt
Wordt een fout opgetreden tijdens de implementatie omdat het account of de service-principal het implementeren van de bronnen geen toegang heeft tot het uitvoeren van deze acties. Azure Active Directory kunt u of uw beheerder om te bepalen welke identiteiten hebben toegang tot welke bronnen in grote mate van precisie. Bijvoorbeeld, als uw account is toegewezen aan de rol Lezer, zich u niet om resources te maken. In dat geval ziet u een foutmelding autorisatie is mislukt.

Zie voor meer informatie over op rollen gebaseerde toegangsbeheer [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het controleren van acties, [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* Zie voor meer informatie over acties om de fouten tijdens de implementatie, [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
