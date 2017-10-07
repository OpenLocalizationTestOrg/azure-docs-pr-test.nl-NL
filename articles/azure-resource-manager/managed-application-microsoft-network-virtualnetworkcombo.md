---
title: Beheerde toepassing VirtualNetworkCombo UI-element aaaAzure | Microsoft Docs
description: Beschrijft Hallo Microsoft.Network.VirtualNetworkCombo UI-element voor beheerde Azure-toepassingen
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Microsoft.Network.VirtualNetworkCombo UI-element
Een groep besturingselementen voor het selecteren van een nieuw of bestaand virtueel netwerk. Gebruik van dit element wanneer [maken van een Azure-toepassing beheerd](managed-application-publishing.md).

## <a name="ui-sample"></a>Voorbeeld van de gebruikersinterface
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- In de bovenste draadmodel hello, heeft Hallo gebruiker een nieuw virtueel netwerk verzameld zodat Hallo gebruiker elk subnet naam en adres voorvoegsel kan aanpassen. Subnetten configureren is in dit geval optioneel.
- In Hallo onderaan draadmodel, Hallo gebruiker heeft gekozen een bestaand virtueel netwerk, zodat Hallo gebruiker moet worden toegewezen elk subnet Hallo-implementatiesjabloon bestaand subnet tooan vereist. Subnetten configureren is in dit geval vereist.

## <a name="schema"></a>Schema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Opmerkingen
- Indien opgegeven, de eerste niet-overlappende adresvoorvoegsel met een grootte van Hallo `defaultValue.addressPrefixSize` automatisch op basis van de bestaande virtuele netwerken in het abonnement van de gebruiker hello wordt bepaald.
- de standaardwaarde voor Hallo `defaultValue.name` en `defaultValue.addressPrefixSize` is **null**.
- `constraints.minAddressPrefixSize`moet worden opgegeven. Een bestaande virtuele netwerken met een adresruimte die kleiner is dan hello opgegeven waarde zijn niet beschikbaar voor selectie.
- `subnets`Er moet worden opgegeven en `constraints.minAddressPrefixSize` voor elk subnet moet worden opgegeven.
- Wanneer u een nieuw virtueel netwerk maakt, adresvoorvoegsel voor elk subnet wordt automatisch berekend op Hallo van het virtuele netwerk adresvoorvoegsel en de respectieve `addressPrefixSize`.
- Wanneer u een bestaande virtuele netwerk, kleiner is dan de respectieve subnetten `constraints.minAddressPrefixSize` zijn niet beschikbaar voor selectie. Bovendien, indien opgegeven, subnetten die bevatten geen ten minste `minAddressCount` beschikbare adressen zijn niet beschikbaar voor selectie.
de standaardwaarde Hallo is **0**. tooensure die Hallo beschikbare adressen zijn aaneengesloten, geeft u **true** voor `requireContiguousAddresses`. de standaardwaarde Hallo is **true**.
- Maken van subnetten in een bestaand virtueel netwerk wordt niet ondersteund.
- Als `options.hideExisting` is **true**, Hallo gebruiker een bestaand virtueel netwerk niet kiezen. de standaardwaarde Hallo is **false**.

## <a name="sample-output"></a>Voorbeelduitvoer
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een inleiding toomanaged toepassingen, [overzicht van Azure Managed toepassing](managed-application-overview.md).
* Zie voor een inleiding toocreating UI definities [aan de slag met CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Zie voor een beschrijving van de algemene eigenschappen in de UI-elementen, [CreateUiDefinition elementen](managed-application-createuidefinition-elements.md).
