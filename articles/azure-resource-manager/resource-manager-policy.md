---
title: Azure bronbeleid | Microsoft Docs
description: Beschrijft hoe u Azure Resource Manager-beleid gebruiken om ervoor te zorgen consistent broneigenschappen zijn ingesteld tijdens de implementatie. Beleidsregels kunnen worden toegepast op de groepen abonnement of resourcegroep.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a>Overzicht van de resource-beleid
Bronbeleid kunnen u tot stand brengen conventies voor resources in uw organisatie. Door het definiëren van conventies u kosten kunt beheren en meer eenvoudig beheren van uw resources. U kunt bijvoorbeeld opgeven dat alleen bepaalde typen virtuele machines zijn toegestaan. Of u kunt vereisen dat alle resources een bepaald label hebben. Beleidsregels worden overgenomen door alle onderliggende resources. Dus als een beleid wordt toegepast op een resourcegroep, is van toepassing op alle resources in die resourcegroep.

Er zijn twee concepten over het beleid begrijpen:

* de beleidsdefinitie - beschrijft u wanneer het beleid wordt afgedwongen en welke actie moet worden uitgevoerd
* de toewijzing van configuratiebeleid - u beleidsdefinitie toepassen op een bereik (abonnement of de resource-group)

Dit onderwerp richt zich op de beleidsdefinitie van het. Zie voor meer informatie over de toewijzing van configuratiebeleid [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md) of [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).

Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).

> [!NOTE]
> Beleid evalueren op dit moment niet brontypen die tags, type en locatie, zoals het brontype Microsoft.Resources/deployments niet ondersteunen. Deze ondersteuning wordt toegevoegd op een later tijdstip. Compatibiliteit met eerdere versies om problemen te voorkomen, moet u expliciet type opgeven tijdens het opstellen van beleid. Bijvoorbeeld, een tag beleid waarvoor geen typen toegepast voor alle typen. In dat geval een sjabloonimplementatie kan mislukken als er een geneste resource die biedt geen ondersteuning voor labels en het implementatietype van de resource is toegevoegd aan de evaluatie van het beleid. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Wat is het verschil van RBAC?
Er zijn enkele belangrijke verschillen tussen het beleid en op rollen gebaseerde toegangsbeheer (RBAC). RBAC is gericht op **gebruiker** acties op verschillende bereiken. U wordt bijvoorbeeld toegevoegd aan de rol Inzender voor een resourcegroep op het gewenste bereik, zodat u wijzigingen in die resourcegroep aanbrengen kunt. Beleid is gericht op **resource** eigenschappen tijdens de implementatie. U kunt bijvoorbeeld via het beleid, de typen bronnen die kunnen worden ingericht beheren. Of u de locaties waar resources kunnen worden ingericht kunt beperken. In tegenstelling tot RBAC, beleid is een standaard toestaan en expliciete system weigeren. 

Voor gebruik van beleid, moet u eerst worden geverifieerd via RBAC. In het bijzonder uw account moet het:

* `Microsoft.Authorization/policydefinitions/write`machtiging voor het definiëren van een beleid
* `Microsoft.Authorization/policyassignments/write`machtiging voor het toewijzen van een beleid 

Deze machtigingen niet zijn opgenomen in de **Inzender** rol.

## <a name="built-in-policies"></a>Ingebouwde beleid

Azure biedt een aantal ingebouwde beleidsdefinities die wellicht minder van beleidsregels die u hebt om te definiëren. Voordat u doorgaat met de beleidsdefinities, moet u overwegen of een ingebouwde beleid al biedt de definitie die u nodig hebt. De ingebouwde beleidsdefinities zijn:

* Toegestane locaties
* Toegestane brontypen
* Storage-account SKU's toegestaan
* Virtuele machine SKU's toegestaan
* Label en de standaardwaarde toepassen
* Label en waarde afdwingen.
* Brontypen die toegestaan niet
* SQL Server versie 12.0 vereisen
* Storage-accountversleuteling vereisen

U kunt een van deze beleidsregels via de [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), of [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Definitie beleidsstructuur
JSON kunt u een beleidsdefinitie maken. De beleidsdefinitie bevat-elementen voor:

* Parameters
* Weergavenaam
* Beschrijving
* Beleidsregel
  * logische evaluatie
  * effect

Het volgende voorbeeld ziet u een beleid dat wordt beperkt welke resources zijn geïmplementeerd:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>Parameters
Met parameters, kunt u uw beleidsbeheer vereenvoudigen doordat het aantal beleidsdefinities. U definieert een beleid voor een broneigenschap (zoals het beperken van de locaties waar resources kunnen worden geïmplementeerd) en parameters opnemen in de definitie. U opnieuw gebruiken die beleidsdefinitie voor verschillende scenario's door door te geven in verschillende waarden (zoals het opgeven van een reeks locaties voor een abonnement) wanneer het toewijzen van beleid.

U kunt parameters declareren bij het maken van beleidsdefinities.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

Het type van een parameter kan tekenreeks- of matrixtype zijn. De metagegevenseigenschap wordt gebruikt voor hulpmiddelen zoals Azure-portal om gebruiksvriendelijke informatie weer te geven. 

In de beleidsregel verwijzen naar parameters met de volgende syntaxis: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Weergavenaam en beschrijving

U gebruikt de **displayName** en **beschrijving** om te bepalen van de beleidsdefinitie en voorzien in context wanneer deze wordt gebruikt.

## <a name="policy-rule"></a>Beleidsregel

De beleidsregel bestaat uit **als** en **vervolgens** blokken. In de **als** blok definiëren van een of meer voorwaarden die opgeven wanneer het beleid wordt afgedwongen. U kunt logische operators toepassen op deze voorwaarden precies bepalen het scenario voor een beleid. In de **vervolgens** blok, definieert u het effect dat gebeurt wanneer de **als** voorwaarden is voldaan.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Logische operators
De ondersteunde logische operators zijn:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

De **niet** syntaxis keert het resultaat van de voorwaarde. De **zet** syntaxis (vergelijkbaar met de logische **en** bewerking) moet u alle voorwaarden wordt voldaan. De **dragen** syntaxis (vergelijkbaar met de logische **of** bewerking) vereist een of meer voorwaarden wordt voldaan.

U kunt logische operators nesten. Het volgende voorbeeld wordt een **niet** bewerking die is genest binnen een **zet** bewerking. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Voorwaarden
De voorwaarde wordt geëvalueerd of een **veld** aan bepaalde criteria voldoet. De ondersteunde voorwaarden zijn:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Wanneer u de **zoals** voorwaarde, kunt u een jokerteken (*) in de waarde opgeven.

Wanneer u de **overeen met** voorwaarde, bieden `#` vertegenwoordigt een cijfer `?` voor een letter en een ander teken dat werkelijke teken vertegenwoordigt. Zie voor voorbeelden [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Velden
Voorwaarden zijn samengesteld op basis van velden. Een veld geeft eigenschappen in de nettolading van de resource-aanvraag die wordt gebruikt om de status van de resource te beschrijven.  

De volgende velden worden ondersteund:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* eigenschap aliassen - Zie voor een lijst [aliassen](#aliases).

### <a name="effect"></a>Effect
Beleid ondersteunt drie typen effect - `deny`, `audit`, en `append`. 

* **Weigeren** wordt een gebeurtenis gegenereerd in het controlelogboek en de aanvraag is mislukt
* **Audit** genereert een waarschuwingsgebeurtenis in controlelogboek maar mislukt de aanvraag niet
* **Append** voegt de gedefinieerde set velden toe aan de aanvraag 

Voor **toevoegen**, moet u de volgende details opgeven:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

De waarde kan niet een tekenreeks of een object van JSON-indeling. 

## <a name="aliases"></a>Aliassen

U eigenschap aliassen gebruiken voor toegang tot specifieke eigenschappen voor een resourcetype. Aliassen kunnen u beperken welke waarden of de voorwaarden zijn toegestaan voor een eigenschap van een resource. Elke alias wordt toegewezen aan paden in verschillende API-versies voor een bepaald brontype. Tijdens de evaluatie van het beleid haalt de beleidsengine het eigenschapspad voor die API-versie.

**Microsoft.Cache/Redis**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Instellen is of de Redis-server niet-ssl-poort (6379) ingeschakeld. |
| Microsoft.Cache/Redis/shardCount | Stel het aantal shards op een Cluster Premium Cache moeten worden gemaakt.  |
| Microsoft.Cache/Redis/sku.capacity | Stel de grootte van de Redis-cache te implementeren.  |
| Microsoft.Cache/Redis/sku.family | Stel de SKU-serie te gebruiken. |
| Microsoft.Cache/Redis/sku.name | Instellen van het type van Redis-Cache te implementeren. |

**Microsoft.Cdn/profiles**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | De naam van de prijscategorie instellen. |

**Microsoft.Compute/disks**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imagePublisher | Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageSku | Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageVersion | Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |


**Microsoft.Compute/virtualMachines**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageId | De id van de afbeelding die wordt gebruikt voor het maken van de virtuele machine instellen. |
| Microsoft.Compute/imageOffer | Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imagePublisher | Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageSku | Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageVersion | Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/licenseType | Instellen dat de installatiekopie of schijf gelicentieerde lokaal is. Deze waarde wordt alleen gebruikt voor afbeeldingen die het besturingssysteem Windows Server bevatten.  |
| Microsoft.Compute/virtualMachines/imageOffer | Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/virtualMachines/imagePublisher | Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/virtualMachines/imageSku | Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/virtualMachines/imageVersion | Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Stel de vhd-URI. |
| Microsoft.Compute/virtualMachines/sku.name | Stel de grootte van de virtuele machine. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | De naam van de uitgever de extensie instellen. |
| Microsoft.Compute/virtualMachines/extensions/type | Het type van extensie instellen. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Stel de versie van de uitbreiding. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageId | De id van de afbeelding die wordt gebruikt voor het maken van de virtuele machine instellen. |
| Microsoft.Compute/imageOffer | Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imagePublisher | Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageSku | Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/imageVersion | Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine. |
| Microsoft.Compute/licenseType | Instellen dat de installatiekopie of schijf gelicentieerde lokaal is. Deze waarde wordt alleen gebruikt voor afbeeldingen die het besturingssysteem Windows Server bevatten. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Het voorvoegsel van de computer voor de virtuele machines in de schaalset instellen. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Stel de blob-URI voor de gebruikersinstallatiekopie van de. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | De container-URL's die worden gebruikt voor het opslaan van besturingssysteem schijven voor de schaalaanpassingsset ingesteld. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | De grootte van virtuele machines in een scale-set instellen. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | De laag van virtuele machines in een scale-set instellen. |
  
**Microsoft.Network/applicationGateways**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | De grootte van de gateway instellen. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Het type van deze virtuele netwerkgateway instellen. |
| Microsoft.Network/virtualNetworkGateways/sku.name | De naam van de gateway-SKU ingesteld. |

**Microsoft.Sql/servers**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Stel de versie van de server. |

**Microsoft.Sql/databases**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Stel de versie van de database. |
| Microsoft.Sql/servers/databases/elasticPoolName | De naam van de elastische groep die de database is ingesteld. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Stel de geconfigureerde service level objective-ID van de database. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | De naam van de geconfigureerde serviceniveaudoelstelling van de database instellen.  |

**Microsoft.Sql/elasticpools**

| Alias | Beschrijving |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Stel de totale gedeelde DTU voor een elastische pool in de database. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Stel de versie van de elastische groep. |

**Microsoft.Storage/storageAccounts**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Stel de toegangslaag gebruikt voor facturering. |
| Microsoft.Storage/storageAccounts/accountType | De SKU-naam instellen. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Instellen of de service de gegevens versleutelt die wordt opgeslagen in de blob storage-service. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Instellen of de service de gegevens versleutelt die in de storage-service van het bestand wordt opgeslagen. |
| Microsoft.Storage/storageAccounts/sku.name | De SKU-naam instellen. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Stel in dat alleen https-verkeer met storage-service. |


## <a name="policy-examples"></a>Voorbeelden van beleid

De volgende onderwerpen bevatten voorbeelden van beleid:

* Zie voor voorbeelden van de tag beleidsregels, [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).
* Zie voor voorbeelden van naamgeving en tekst patronen [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).
* Zie voor voorbeelden van beleidsregels voor opslag [resource beleid toepassen op opslagaccounts](resource-manager-policy-storage.md).
* Zie voor voorbeelden van beleidsregels voor virtuele machine [resource beleid toepassen op virtuele Linux-machines](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en [resource beleid toepassen op Windows-VM's](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel, moet u het toewijzen aan een bereik. Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md). Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).
* Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).
* Het schema van het beleid wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

