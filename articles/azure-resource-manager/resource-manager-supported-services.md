---
title: aaaAzure resourceproviders en brontypen | Microsoft Docs
description: Beschrijft Hallo resourceproviders die ondersteuning bieden voor Resource Manager, hun schema's en de beschikbare API-versies en Hallo-regio's die kunnen Hallo-bronnen hosten.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Resourceproviders en typen

Bij het implementeren van resources, moet u vaak tooretrieve informatie over de resourceproviders hello en typen. In dit artikel leert hoe u u kunt:

* Alle resourceproviders bekijken in Azure
* Controleer de status van de registratie van een resourceprovider
* Een resourceprovider registreren
* Weergave brontypen die voor een resourceprovider
* Geldige locaties van de weergave voor een brontype
* Geldige API-versies voor een resourcetype weergeven

U kunt deze stappen via Hallo-portal, PowerShell of Azure CLI kunt uitvoeren.

## <a name="powershell"></a>PowerShell

toosee gebruiken voor alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Die resultaten weer die vergelijkbaar is met:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider. Hallo-bereik voor de registratie is altijd Hallo-abonnement. Veel resourceproviders worden standaard automatisch geregistreerd. Echter, moet u mogelijk toomanually sommige resourceproviders registreren. een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider. Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Die resultaten weer die vergelijkbaar is met:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.

toosee-informatie voor een bepaalde bron-provider, gebruiken:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Die resultaten weer die vergelijkbaar is met:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

toosee hello brontypen die voor een resourceprovider gebruiken:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Die wordt geretourneerd:

```powershell
batchAccounts
operations
locations
locations/quotas
```

Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider. Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API. 

tooget hello beschikbare API-versies voor een brontype gebruiken:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Die wordt geretourneerd:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's. Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken. 

tooget hello ondersteunde locaties voor een resourcetype gebruiken.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Die wordt geretourneerd:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>Azure CLI
toosee gebruiken voor alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Die resultaten weer die vergelijkbaar is met:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider. Hallo-bereik voor de registratie is altijd Hallo-abonnement. Veel resourceproviders worden standaard automatisch geregistreerd. Echter, moet u mogelijk toomanually sommige resourceproviders registreren. een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider. Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen.

```azurecli
az provider register --namespace Microsoft.Batch
```

Retourneert het bericht van deze inschrijving is continu.

U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.

toosee-informatie voor een bepaalde bron-provider, gebruiken:

```azurecli
az provider show --namespace Microsoft.Batch
```

Die resultaten weer die vergelijkbaar is met:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

toosee hello brontypen die voor een resourceprovider gebruiken:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Die wordt geretourneerd:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider. Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API. 

tooget hello beschikbare API-versies voor een brontype gebruiken:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Die wordt geretourneerd:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's. Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken. 

tooget hello ondersteunde locaties voor een resourcetype gebruiken.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Die wordt geretourneerd:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portal

alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement, selecteert u toosee **abonnementen**.

![Selecteer abonnementen](./media/resource-manager-supported-services/select-subscriptions.png)

Hallo abonnement tooview kiezen.

![abonnement opgeven](./media/resource-manager-supported-services/subscription.png)

Selecteer **resourceproviders** en Hallo lijst met beschikbare resourceproviders bekijken.

![resourceproviders weergeven](./media/resource-manager-supported-services/show-resource-providers.png)

Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider. Hallo-bereik voor de registratie is altijd Hallo-abonnement. Veel resourceproviders worden standaard automatisch geregistreerd. Echter, moet u mogelijk toomanually sommige resourceproviders registreren. een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider. Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen. Selecteer tooregister een resourceprovider **registreren**.

![de registerbronprovider](./media/resource-manager-supported-services/register-provider.png)

U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.

toosee-informatie voor een bepaalde bron-provider, selecteer **meer services**.

![meer services selecteren](./media/resource-manager-supported-services/more-services.png)

Zoeken naar **Resource Explorer** en selecteer het uit de beschikbare opties Hallo.

![Selecteer resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

Selecteer **Providers**.

![Providers selecteren](./media/resource-manager-supported-services/select-providers.png)

Selecteer Hallo resourceprovider en resource typt de gewenste tooview.

![Brontype selecteren](./media/resource-manager-supported-services/select-resource-type.png)

Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's. Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken. Hallo resource explorer weergegeven geldige locaties voor Hallo brontype.

![Locaties weergeven](./media/resource-manager-supported-services/show-locations.png)

Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider. Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API. Hallo resource explorer geeft geldige API-versies voor het brontype Hallo weer.

![API-versies weergeven](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Volgende stappen
* toolearn over het maken van Resource Manager-sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toolearn over het implementeren van resources, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).
* Zie tooview Hallo bewerkingen voor een resourceprovider [REST API van Azure](/rest/api/).

