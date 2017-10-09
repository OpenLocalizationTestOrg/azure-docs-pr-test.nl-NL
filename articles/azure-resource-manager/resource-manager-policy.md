---
title: bronbeleid aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure Resource Manager-beleid tooensure consistent broneigenschappen zijn ingesteld tijdens de implementatie. Beleidsregels kunnen worden toegepast op Hallo abonnement of de resource-groepen.
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Overzicht van de resource-beleid
Bronbeleid inschakelen tooestablish conventies voor bronnen in uw organisatie. Door het definiëren van conventies u kosten kunt beheren en meer eenvoudig beheren van uw resources. U kunt bijvoorbeeld opgeven dat alleen bepaalde typen virtuele machines zijn toegestaan. Of u kunt vereisen dat alle resources een bepaald label hebben. Beleidsregels worden overgenomen door alle onderliggende resources. Dus als een beleid toegepast tooa resourcegroep is, van toepassing tooall Hallo resources in die resourcegroep is.

Er zijn twee concepten toounderstand over beleid:

* de beleidsdefinitie - beschrijft u wanneer Hallo beleid wordt afgedwongen en welke actie tootake
* Wanneer u Hallo beleid definitie tooa bereik (abonnement of resourcegroep) beleidstoewijzing - toepassen

Dit onderwerp richt zich op de beleidsdefinitie van het. Zie voor meer informatie over de toewijzing van configuratiebeleid [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md) of [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).

Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).

> [!NOTE]
> Beleid evalueren op dit moment niet brontypen die tags, type en locatie, zoals Hallo Microsoft.Resources/deployments brontype niet ondersteunen. Deze ondersteuning wordt toegevoegd op een later tijdstip. problemen met tooavoid achterwaartse compatibiliteit, moet u expliciet opgeven type tijdens het opstellen van beleid. Bijvoorbeeld, een tag beleid waarvoor geen typen toegepast voor alle typen. In dat geval een sjabloonimplementatie kan mislukken als er een geneste resource die biedt geen ondersteuning voor labels en Hallo resource implementatietype toopolicy evaluatie is toegevoegd. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Wat is het verschil van RBAC?
Er zijn enkele belangrijke verschillen tussen het beleid en op rollen gebaseerde toegangsbeheer (RBAC). RBAC is gericht op **gebruiker** acties op verschillende bereiken. U wordt bijvoorbeeld toohello de rol van inzender voor een resourcegroep toegevoegd bij Hallo gewenst bereik, zodat u de resourcegroep voor toothat wijzigingen kunt aanbrengen. Beleid is gericht op **resource** eigenschappen tijdens de implementatie. U kunt bijvoorbeeld via het beleid, Hallo typen resources die kunnen worden ingericht beheren. Of u kunt beperken Hallo locaties waarin Hallo resources kunnen worden ingericht. In tegenstelling tot RBAC, beleid is een standaard toestaan en expliciete system weigeren. 

beleid voor toouse u moet worden geverifieerd via RBAC. In het bijzonder uw account moet het:

* `Microsoft.Authorization/policydefinitions/write`machtiging toodefine een beleid
* `Microsoft.Authorization/policyassignments/write`machtiging tooassign een beleid 

Deze machtigingen niet zijn opgenomen in Hallo **Inzender** rol.

## <a name="built-in-policies"></a>Ingebouwde beleid

Azure biedt een aantal ingebouwde beleidsdefinities die Hallo beperken mogelijk van beleidsregels die u hebt toodefine. Voordat u doorgaat met de beleidsdefinities, moet u overwegen of een ingebouwde beleid al Hallo definitie u moet biedt. Hallo ingebouwde beleidsdefinities zijn:

* Toegestane locaties
* Toegestane brontypen
* Storage-account SKU's toegestaan
* Virtuele machine SKU's toegestaan
* Label en de standaardwaarde toepassen
* Label en waarde afdwingen.
* Brontypen die toegestaan niet
* SQL Server versie 12.0 vereisen
* Storage-accountversleuteling vereisen

U kunt een van deze beleidsregels via Hallo [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), of [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Definitie beleidsstructuur
U JSON toocreate een beleidsdefinitie. de beleidsdefinitie Hallo bevat-elementen voor:

* parameters
* Weergavenaam
* description
* Beleidsregel
  * logische evaluatie
  * effect

Hallo volgende voorbeeld ziet u een beleid dat wordt beperkt welke resources zijn geïmplementeerd:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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
Met parameters, kunt u uw beleidsbeheer vereenvoudigen doordat het aantal beleidsdefinities Hallo. U definieert een beleid voor een broneigenschap (zoals beperken Hallo locaties waar resources kunnen worden geïmplementeerd) en parameters in Hallo definitie bevatten. U opnieuw gebruiken die beleidsdefinitie voor verschillende scenario's door door te geven in verschillende waarden (zoals het opgeven van een reeks locaties voor een abonnement) wanneer Hallo beleid toe te wijzen.

U kunt parameters declareren bij het maken van beleidsdefinities.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

Hallo-type van een parameter is tekenreeks of matrix. Hallo metagegevenseigenschap wordt voor hulpprogramma's als Azure portal toodisplay gebruiksvriendelijke informatie gebruikt. 

In de beleidsregel hello, verwijzen u parameters naar Hello de volgende syntaxis: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Weergavenaam en beschrijving

Gebruik van Hallo **displayName** en **beschrijving** tooidentify beleidsdefinitie Hallo en voorzien in context wanneer deze wordt gebruikt.

## <a name="policy-rule"></a>Beleidsregel

Hallo beleidsregel bestaat uit **als** en **vervolgens** blokken. In Hallo **als** blok definiëren van een of meer voorwaarden die opgeven wanneer Hallo beleid wordt afgedwongen. U kunt logische operators toothese voorwaarden toepassen tooprecisely Hallo scenario voor een beleid definiëren. In Hallo **vervolgens** blok, definieert u Hallo effect dat gebeurt er wanneer hello **als** voorwaarden is voldaan.

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
logische operators Hallo ondersteund zijn:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Hallo **niet** syntaxis keert Hallo resultaat van het Hallo-voorwaarde. Hallo **zet** syntaxis (vergelijkbaar toohello logische **en** bewerking) alle voorwaarden toobe waar vereist. Hallo **dragen** syntaxis (vergelijkbaar toohello logische **of** bewerking) vereist een of meer voorwaarden toobe true.

U kunt logische operators nesten. Hallo volgende voorbeeld ziet u een **niet** bewerking die is genest binnen een **zet** bewerking. 

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
Hallo voorwaarde wordt geëvalueerd of een **veld** aan bepaalde criteria voldoet. Hallo ondersteund voorwaarden zijn:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Wanneer u Hallo **zoals** voorwaarde, kunt u een jokerteken (*) in Hallo-waarde opgeven.

Wanneer u Hallo **overeen met** voorwaarde, bieden `#` toorepresent een cijfer `?` voor een letter en een ander toorepresent Werkelijke teken teken. Zie voor voorbeelden [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Velden
Voorwaarden zijn samengesteld op basis van velden. Hiermee geeft u een veld eigenschappen in de aanvraaglading van de resource Hallo die gebruikte toodescribe Hallo status van Hallo resource.  

Hallo volgende velden worden ondersteund:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* eigenschap aliassen - Zie voor een lijst [aliassen](#aliases).

### <a name="effect"></a>Effect
Beleid ondersteunt drie typen effect - `deny`, `audit`, en `append`. 

* **Weigeren** wordt een gebeurtenis gegenereerd in het controlelogboek Hallo en Hallo-aanvraag is mislukt
* **Audit** genereert een waarschuwingsgebeurtenis in controlelogboek maar mislukt niet Hallo-aanvraag
* **Append** voegt Hallo gedefinieerd set velden toohello aanvraag 

Voor **toevoegen**, moet u de volgende details Hallo opgeven:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

Hallo-waarde is een tekenreeks of een object van JSON-indeling. 

## <a name="aliases"></a>Aliassen

U gebruikt eigenschap aliassen tooaccess specifieke eigenschappen voor een resourcetype. Aliassen inschakelen toorestrict welke waarden of de voorwaarden zijn toegestaan voor een eigenschap van een resource. Elke alias toegewezen toopaths in verschillende versies van de API voor een bepaald brontype. Tijdens de evaluatie van het beleid haalt de beleidsengine Hallo Hallo eigenschapspad voor die API-versie.

**Microsoft.Cache/Redis**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Instellen is of Redis-server voor Hallo niet-ssl-poort (6379) ingeschakeld. |
| Microsoft.Cache/Redis/shardCount | Het aantal shards toobe gemaakt op een Cluster Premium Cache Hallo instellen.  |
| Microsoft.Cache/Redis/sku.capacity | Hallo-grootte van Hallo Redis-cache toodeploy instellen.  |
| Microsoft.Cache/Redis/sku.family | Hallo SKU-familie toouse ingesteld. |
| Microsoft.Cache/Redis/sku.name | Hallo-type van Redis-Cache toodeploy instellen. |

**Microsoft.Cdn/profiles**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Naam van de Hallo Hallo prijscategorie. |

**Microsoft.Compute/disks**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imagePublisher | Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageSku | Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageVersion | Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |


**Microsoft.Compute/virtualMachines**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageId | Hallo-id van de afbeelding Hallo gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageOffer | Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imagePublisher | Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageSku | Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageVersion | Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/licenseType | Instellen dat Hallo installatiekopie of schijf gelicentieerde lokaal is. Deze waarde wordt alleen gebruikt voor installatiekopieën die Windows Server-besturingssysteem Hallo bevatten.  |
| Microsoft.Compute/virtualMachines/imageOffer | Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/virtualMachines/imagePublisher | Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/virtualMachines/imageSku | Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/virtualMachines/imageVersion | Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Stel Hallo vhd-URI. |
| Microsoft.Compute/virtualMachines/sku.name | Hallo-grootte van Hallo virtuele machine instellen. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Hallo-naam van uitgever Hallo-extensie instellen. |
| Microsoft.Compute/virtualMachines/extensions/type | Hallo-type van extensie instellen. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Hallo-versie van de uitbreiding van Hallo ingesteld. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Compute/imageId | Hallo-id van de afbeelding Hallo gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageOffer | Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imagePublisher | Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageSku | Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/imageVersion | Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine. |
| Microsoft.Compute/licenseType | Instellen dat Hallo installatiekopie of schijf gelicentieerde lokaal is. Deze waarde wordt alleen gebruikt voor installatiekopieën die Windows Server-besturingssysteem Hallo bevatten. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Voorvoegsel voor de computernaam Hallo voor alle Hallo virtuele machines in de schaalset Hallo ingesteld. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Hallo blob-URI voor de gebruikersinstallatiekopie van de instellen. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Hallo container-URL's die gebruikt toostore besturingssysteem schijven voor Hallo scale set zijn instellen. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Hallo-grootte van virtuele machines in een scale-set instellen. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Hallo-laag van virtuele machines in een scale-set instellen. |
  
**Microsoft.Network/applicationGateways**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Hallo-grootte van Hallo gateway instellen. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Hallo-type van deze virtuele netwerkgateway instellen. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Hallo-gateway SKU-naam worden ingesteld. |

**Microsoft.Sql/servers**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Hallo-versie van Hallo server instellen. |

**Microsoft.Sql/databases**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Hallo-editie van Hallo database instellen. |
| Microsoft.Sql/servers/databases/elasticPoolName | Naam van de set Hallo van elastische groepdatabase Hallo Hallo is in. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Hallo geconfigureerd service level objective-ID van Hallo database instellen. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Hallo-naam van serviceniveaudoelstelling van Hallo database Hallo geconfigureerd instellen.  |

**Microsoft.Sql/elasticpools**

| Alias | Beschrijving |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Set Hallo totaal gedeeld DTU voor de elastische pool Hallo-database. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Hallo-editie van de elastische pool Hallo ingesteld. |

**Microsoft.Storage/storageAccounts**

| Alias | Beschrijving |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Set gebruikt voor facturering Hallo toegangslaag. |
| Microsoft.Storage/storageAccounts/accountType | Hallo SKU-naam worden ingesteld. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Instellen of Hallo service Hallo gegevens versleutelt zoals deze is opgeslagen in Hallo blob storage-service. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Instellen of Hallo service Hallo gegevens versleutelt zoals deze is opgeslagen in Hallo file storage-service. |
| Microsoft.Storage/storageAccounts/sku.name | Hallo SKU-naam worden ingesteld. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Tooallow alleen https-verkeer toostorage service ingesteld. |


## <a name="policy-examples"></a>Voorbeelden van beleid

Hallo volgende onderwerpen bevatten voorbeelden van beleid:

* Zie voor voorbeelden van de tag beleidsregels, [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).
* Zie voor voorbeelden van naamgeving en tekst patronen [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).
* Zie voor voorbeelden van beleidsregels voor opslag [toepassen resourceaccounts beleid toostorage](resource-manager-policy-storage.md).
* Zie voor voorbeelden van beleidsregels voor virtuele machine [toepassen resource beleid tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en [resource beleid tooWindows virtuele machines toepassen](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Volgende stappen
* Na het definiëren van een beleidsregel toewijzen tooa bereik. tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md). tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).
* Hallo beleid schema wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

