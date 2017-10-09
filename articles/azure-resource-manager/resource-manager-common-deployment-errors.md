---
title: aaaTroubleshoot algemene Azure-implementatiefouten | Microsoft Docs
description: Hierin wordt beschreven hoe tooresolve veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren tooazure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a>Veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager oplossen
Dit onderwerp wordt beschreven hoe u een aantal gemeenschappelijke kunt oplossen Azure-implementatiefouten kunnen optreden.

Hallo volgende foutcodes worden beschreven in dit onderwerp:

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

Deze foutcode geeft een algemene implementatiefout, maar is geen foutcode Hallo moet u toostart het oplossen van problemen. Hallo-foutcode die u kunt Hallo probleem oplossen door daadwerkelijk helpt is meestal één niveau onder deze fout. Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **RequestDisallowedByPolicy** foutcode die onder Hallo implementatiefout optreedt.

![foutcode weergeven](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a>SkuNotAvailable

Bij het implementeren van een resource (meestal een virtuele machine), wordt het foutbericht Hallo foutbericht code en de fout te volgen:

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

U ontvangt deze foutmelding wanneer Hallo resource SKU die u hebt geselecteerd (zoals VM-grootte) is niet beschikbaar voor Hallo locatie die u hebt geselecteerd. tooresolve dit probleem, moet u toodetermine die SKU's beschikbaar in een regio zijn. U kunt PowerShell, Hallo portal of een REST-bewerking toofind beschikbare SKU's.

- Gebruik voor PowerShell [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) en filteren op locatie. U kunt Hallo meest recente versie van PowerShell voor deze opdracht moet hebben.

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  Hallo resultaten bevatten een lijst van SKU's voor de locatie van Hallo en eventuele beperkingen voor deze SKU.

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- Hallo toouse [portal](https://portal.azure.com), toohello portal aanmelden en toevoegen van een resource via Hallo-interface. Als u Hallo waarden instelt, ziet u Hallo beschikbare SKU's voor die bron. U hoeft niet toocomplete Hallo-implementatie.

    ![beschikbare SKU 's](./media/resource-manager-common-deployment-errors/view-sku.png)

- toouse hello REST-API voor virtuele machines, Hallo na aanvraag verzenden:

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  Het resulteert beschikbare SKU's en regio's in Hallo volgende indeling:

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

Als u toofind een geschikte SKU in deze regio of een alternatieve regio die voldoet aan de behoeften van uw bedrijf bent, dient u een [SKU aanvraag](https://aka.ms/skurestriction) tooAzure ondersteuning.

## <a name="disallowedoperation"></a>DisallowedOperation

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

Als deze fout wordt weergegeven, gebruikt u een abonnement dat is niet toegestaan tooaccess alle Azure-services dan Azure Active Directory. Dit type abonnement wellicht op als u tooaccess Hallo klassieke portal moet maar zijn niet toegestaan voor toodeploy resources. tooresolve dit probleem, moet u een abonnement dat machtiging toodeploy bronnen heeft.  

tooview uw beschikbare abonnementen met PowerShell kunt gebruiken:

```powershell
Get-AzureRmSubscription
```

En tooset Hallo huidige abonnement, gebruik:

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

tooview uw beschikbare abonnementen met Azure CLI 2.0, gebruiken:

```azurecli
az account list
```

En tooset Hallo huidige abonnement, gebruik:

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a>InvalidTemplate
Deze fout kan leiden tot verschillende typen fouten.

- Syntaxisfout

   Als u een foutbericht dat aangeeft dat de validatie van Hallo-sjabloon is mislukt ontvangt, hebt u mogelijk een probleem met de syntaxis in de sjabloon.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   Dit is een fout eenvoudig toomake omdat sjabloonexpressies kunnen ingewikkeld zijn. Hallo bevat naamtoewijzing van de volgende voor een opslagaccount bijvoorbeeld een reeks vierkante haken, drie functies drie sets van haakjes, één set met enkele aanhalingstekens en één eigenschap:

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   Als u geen overeenkomende Hallo-syntaxis, produceert Hallo sjabloon een waarde die anders is dan uw bedoeling is.

   Wanneer u dit type fout ontvangt, moet u zorgvuldig Hallo-expressiesyntaxis controleren. Overweeg het gebruik van een JSON-editor, zoals [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) of [Visual Studio Code](resource-manager-vs-code.md), die u kunt gewaarschuwd over syntaxisfouten.

- Onjuiste segment lengten

   Een andere ongeldige sjabloon-fout treedt op wanneer Hallo resourcenaam niet de juiste indeling Hallo is.

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   Een bron voor het niveau van hoofdmap moet één minder segment in Hallo naam heeft dan in brontype Hallo hebben. Elk segment wordt onderscheiden door een slash. In de Hallo voorbeeld te volgen, Hallo type twee segmenten Hallo heeft en één segment dus is het een **geldige naam**.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   Maar is het volgende voorbeeld Hallo **niet de naam van een geldige** omdat hieraan Hallo hetzelfde aantal segmenten als Hallo-type.

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   Voor onderliggende resources Hallo type en de naam Hallo hebben hetzelfde aantal segmenten. Dit aantal segmenten zin omdat Hallo volledige naam en type op voor de onderliggende hello omvat Hallo bovenliggende naam en type. Volledige naam Hallo heeft daarom nog steeds één minder segment dan volledige Hallo-type.

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

   Ophalen Hallo segmenten rechts is lastig met Resource Manager-typen die worden toegepast op de resourceproviders. Bijvoorbeeld, vereist een type met vier segmenten toepassen van de website van een resource vergrendeling tooa. Daarom is de naam van de Hallo drie segmenten:

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- Index van de kopie wordt niet verwacht.

   U tegenkomt dit **InvalidTemplate** fout bij het toepassen van Hallo **kopie** element tooa deel van Hallo-sjabloon die geen ondersteuning biedt voor dit element. U kunt alleen Hallo kopiëren tooa resource elementtype toepassen. U kunt kopiëren tooa eigenschap binnen een brontype niet toepassen. Bijvoorbeeld, u kopiëren tooa virtuele machine hebt toegepast, maar u toohello OS-schijven voor een virtuele machine niet toepassen. In sommige gevallen kunt u een onderliggende resource tooa bovenliggende resource toocreate een lus exemplaar converteren. Zie voor meer informatie over het gebruik van kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).

- Parameter is niet geldig

   Als het Hallo-sjabloon bevat de toegestane waarden voor een parameter, en u een waarde die niet een van deze waarden opgeven, ontvangt u een bericht vergelijkbaar toohello volgende fout:

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   Controleer Hallo toegestane waarden in de sjabloon Hallo en bieden een tijdens de implementatie.

- Kringafhankelijkheid gedetecteerd

   U ontvangt deze foutmelding wanneer resources afhankelijk van elkaar op een manier waardoor het Hallo-implementatie zijn niet worden gestart. Een combinatie van afhankelijkheden maakt twee of meer resources, wacht u totdat de andere bronnen die ook wachten. Bijvoorbeeld resource1 is afhankelijk van resource3, resource2, is afhankelijk van resource1 en resource3 is afhankelijk van resource2. Meestal kunt u dit probleem oplossen door het verwijderen van onnodige afhankelijkheden. 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a>NotFound en ResourceNotFound
Wanneer de sjabloon Hallo-naam van een resource die niet kan worden omgezet bevat, wordt een foutbericht zoals:

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

Als u toodeploy Hallo resource in de sjabloon Hallo ontbreekt probeert, controleert u of u een afhankelijkheid tooadd moet. Resource Manager optimaliseert implementatie door het maken van resources parallel indien mogelijk. Als een resource moet worden geïmplementeerd nadat een andere resource, moet u toouse hello **dependsOn** -element in de sjabloon toocreate een afhankelijkheid van Hallo andere resource. Bijvoorbeeld, wanneer u een web-app implementeert, moet Hallo App Service-abonnement bestaan. Als u niet hebt opgegeven dat Hallo web-app, is afhankelijk van Hallo App Service-abonnement, Resource Manager beide resources maakt op Hallo hetzelfde moment. U ontvangt een foutmelding weergegeven dat Hallo App Service plan bron kan niet worden gevonden, omdat deze niet bestaat nog tijdens een poging de tooset een eigenschap op Hallo web-app. U kunt deze fout voorkomen door in te stellen Hallo afhankelijkheid in Hallo web-app.

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

Deze fout wordt ook zien wanneer Hallo resource bestaat in een andere resourcegroep dan Hallo een wordt geïmplementeerd. Gebruik in dat geval Hallo [resourceId functie](resource-group-template-functions-resource.md#resourceid) tooget Hallo volledig gekwalificeerde naam van Hallo resource.

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

Als u toouse hello probeert [verwijzing](resource-group-template-functions-resource.md#reference) of [listKeys](resource-group-template-functions-resource.md#listkeys) werkt in combinatie met een resource die niet kunnen worden omgezet, u Hallo volgende fout ontvangen:

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

Zoek naar een expressie met Hallo **verwijzing** functie. Controleer of de parameterwaarden Hallo juist zijn.

## <a name="parentresourcenotfound"></a>ParentResourceNotFound

Wanneer een bron een bovenliggende tooanother resource is, moet Hallo bovenliggende resource bestaan voordat u Hallo onderliggende resource maakt. Als deze nog niet bestaat, ontvangt u Hallo volgende fout:

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

Hallo-naam van Hallo onderliggende resource bevat de naam van de bovenliggende Hallo. Bijvoorbeeld, kunnen een SQL-Database worden gedefinieerd als:

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

Maar als u een afhankelijkheid op Hallo bovenliggende resource niet opgeeft, Hallo onderliggende resource kan ophalen geïmplementeerd voordat u Hallo bovenliggende. tooresolve deze fout, bevatten een afhankelijkheid.

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a>StorageAccountAlreadyExists en StorageAccountAlreadyTaken
U moet een naam voor het Hallo-resource die uniek is voor alle Azure opgeven voor de storage-accounts. Als u niet een unieke naam opgeeft, wordt een fout als volgt:

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

U kunt een unieke naam maken met de naamgevingsconventie met Hallo resultaat Hallo cookievalidatie [uniqueString](resource-group-template-functions-string.md#uniquestring) functie.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

Als u een opslagaccount met Hallo implementeert dezelfde naam als een bestaand opslagaccount in uw abonnement, maar bieden een andere locatie, er een foutbericht die duiden Hallo storage-account al in een andere locatie bestaat. Verwijder de bestaande opslagaccount Hallo of bieden Hallo dezelfde locatie als Hallo bestaand opslagaccount.

## <a name="accountnameinvalid"></a>AccountNameInvalid
U ziet Hallo **AccountNameInvalid** fout bij poging een storage account een naam met toogive tekens verboden. Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken. Hallo [uniqueString](resource-group-template-functions-string.md#uniquestring) functie retourneert 13 tekens. Als u een voorvoegsel toohello samenvoegen **uniqueString** leiden, geeft u een voorvoegsel 11 tekens of minder.

## <a name="badrequest"></a>BadRequest

De status van een BadRequest kunnen optreden wanneer u een ongeldige waarde voor een eigenschap opgeeft. Bijvoorbeeld, als u een onjuiste waarde voor de SKU voor een opslagaccount, Hallo-implementatie is mislukt. geldige waarden voor de eigenschap toodetermine bekijkt hello [REST-API](/rest/api) voor Hallo brontype u implementeert.

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a>NoRegisteredProviderFound en MissingSubscriptionRegistration
Bij het implementeren van de resource kan u ontvangt Hallo foutcode te volgen en bericht:

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

Of een vergelijkbaar bericht waarin wordt vermeld:

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

U ontvangt deze fouten voor een van drie redenen:

1. Hallo-resourceprovider is niet geregistreerd voor uw abonnement
2. API-versie niet ondersteund voor het brontype Hallo
3. Locatie niet ondersteund voor het brontype Hallo

Fout bij het Hallo-bericht geeft suggesties voor Hallo ondersteund locaties en API-versies. U kunt uw sjabloon tooone Hallo wijzigen voorgestelde waarden. De meeste providers worden automatisch door hello Azure portal of Hallo-opdrachtregelinterface u gebruikt, maar niet alle geregistreerd. Als u niet een bepaalde bron-provider voorafgaand aan hebt gebruikt, moet u mogelijk tooregister die provider. U kunt meer informatie over resourceproviders via PowerShell of Azure CLI detecteren.

**Portal**

U kunt zien Hallo registratiestatus en de naamruimte via Hallo portal een resourceprovider registreren.

1. Selecteer voor uw abonnement, **resourceproviders**.

   ![resourceproviders selecteren](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. Bekijkt hello lijst met resourceproviders en indien nodig, selecteer Hallo **registreren** koppeling tooregister Hallo resourceprovider van het type Hallo u toodeploy probeert.

   ![resourceproviders vermelden](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

**PowerShell**

toosee uw registratiestatus, gebruik **Get-AzureRmResourceProvider**.

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

tooregister een provider, gebruik **registreren AzureRmResourceProvider** en geef de naam Hallo Hallo resourceprovider dat u wenst dat tooregister.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

tooget hello ondersteunde locaties voor een bepaald type resource, gebruiken:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

tooget hello ondersteunde API-versies voor een bepaald type resource, gebruiken:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

**Azure-CLI**

toosee of Hallo-provider is geregistreerd, gebruikt u Hallo `azure provider list` opdracht.

```azurecli
az provider list
```

een resourceprovider tooregister gebruiken Hallo `azure provider register` opdracht in en geef Hallo *naamruimte* tooregister.

```azurecli
az provider register --namespace Microsoft.Cdn
```

Gebruik toosee Hallo ondersteund locaties en API-versies voor een brontype:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a>QuotaExceeded en OperationNotAllowed
Mogelijk hebt u problemen als implementatie groter is dan een quotum die kan per resourcegroep, abonnementen, accounts en andere bereiken worden. Bijvoorbeeld, uw abonnement mogelijk geconfigureerd toolimit Hallo aantal kernen voor een regio. Als u een virtuele machine met meer cores dan Hallo toegestaan bedrag toodeploy probeert, foutbericht er een waarin Hallo quotum is overschreden.
Zie voor informatie voltooid quotum [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).

tooexamine quota's voor uw abonnement voor kernen, kunt u Hallo `azure vm list-usage` opdracht in hello Azure CLI. Hallo volgende voorbeeld illustreert Hallo core quotum voor een gratis proefaccount 4 is:

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

Als u een sjabloon die meer dan vier kernen in de regio VS-West Hallo maakt implementeert, kunt u een implementatiefout dat lijkt op krijgen:

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

In PowerShell kunt u Hallo **Get-AzureRmVMUsage** cmdlet.

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

In dergelijke gevallen moet u toohello portal gaan en het bestand een probleem ondersteuning tooraise het quotum voor Hallo regio waarin u toodeploy wilt.

> [!NOTE]
> Vergeet niet dat voor de resourcegroepen Hallo quotum voor elke afzonderlijke regio, niet voor de hele abonnement Hallo. Als u nodig hebt toodeploy 30 kernen in VS-West, hebt u tooask voor 30 Resource Manager kernen in VS-West. Als u toodeploy 30 kernen in een Hallo regio's toowhich moet hebt u toegang, moet u de vragen voor 30 Resource Manager kernen in alle regio's.
>
>

## <a name="invalidcontentlink"></a>InvalidContentLink
Wanneer u wordt Hallo foutbericht weergegeven:

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

U hebt waarschijnlijk geprobeerd toolink tooa geneste sjabloon die niet beschikbaar. Controleer hello URI die u hebt opgegeven voor geneste Hallo-sjabloon. Als Hallo sjabloon in een opslagaccount bestaat, zorg er dan voor dat Hallo URI toegankelijk is. Mogelijk moet u toopass een SAS-token. Zie voor meer informatie [Gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).

## <a name="requestdisallowedbypolicy"></a>RequestDisallowedByPolicy
U ontvangt deze foutmelding wanneer uw abonnement bevat een bronbeleid een actie die u probeert tooperform tijdens de implementatie wordt verhinderd. In het foutbericht hello, zoekt u Hallo beleids-id.

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

In **PowerShell**, bieden die beleids-id als Hallo **Id** parameter tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd.

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

In **Azure CLI**, Hallo-naam van de beleidsdefinitie Hallo bieden:

```azurecli
az policy definition show --name regionPolicyAssignment
```

Zie voor meer informatie Hallo artikelen te volgen:

- [RequestDisallowedByPolicy-fout](resource-manager-policy-requestdisallowedbypolicy-error.md)
- [Gebruik beleid toomanage bronnen en toegangsbeheer](resource-manager-policy.md).

## <a name="authorization-failed"></a>Verificatie mislukt
Wordt een fout opgetreden tijdens de implementatie omdat Hallo-account of service-principal probeert toodeploy Hallo bronnen geen toegang tooperform die acties heeft. Azure Active Directory kunt u of uw beheerder toocontrol welke identiteiten toegang welke bronnen in grote mate van precisie tot. Bijvoorbeeld, als uw account is toegewezen met de rol Lezer toohello, bent u niet kunt toocreate resources. In dat geval ziet u een foutmelding autorisatie is mislukt.

Zie voor meer informatie over op rollen gebaseerde toegangsbeheer [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).


## <a name="next-steps"></a>Volgende stappen
* toolearn over het controleren van acties, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).
* Zie toolearn over acties toodetermine Hallo fouten tijdens de implementatie van [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).
