---
title: Azure-resources voor logische organisatie tag | Microsoft Docs
description: Laat zien hoe de labels te organiseren Azure-resources voor facturerings- en beheren van toepassing.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 003a78e5-2ff8-4685-93b4-e94d6fb8ed5b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: AzurePortal
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tomfitz
ms.openlocfilehash: 4f52c30614ad39da8a34ff6ecfb707b75400517f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-tags-to-organize-your-azure-resources"></a>Tags gebruiken om uw Azure-resources te organiseren
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> U kunt tags toepassen alleen naar bronnen die ondersteuning bieden voor Azure Resource Manager-bewerkingen. Als u een virtuele machine, het virtuele netwerk of de storage-account via het klassieke implementatiemodel hebt gemaakt (bijvoorbeeld via de klassieke Azure portal), u een label niet toepassen op deze resource. Implementeren ter ondersteuning van labels, deze resources via Resource Manager. Alle andere bronnen ondersteuning voor codering.
> 
> 

## <a name="policies-for-tag-consistency"></a>Beleid voor consistentie van de tag

U kunt bronbeleid gebruiken voor het maken van standaardregels voor uw organisatie. U kunt beleidsregels die zorg ervoor dat resources worden gemarkeerd met de juiste waarden maken. Zie voor meer informatie [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Azure CLI

Gebruik het volgende om de bestaande tags van een *resourcegroep* te bekijken:

```azurecli
az group show -n examplegroup --query tags
```

Dat script retourneert de volgende indeling:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

Gebruik het volgende om de bestaande tags te bekijken van een *resource met een opgegeven bron-id*:

```azurecli
az resource show --id {resource-id} --query tags
```

Of, voor een overzicht van de bestaande codes voor een *resource met een opgegeven groep met de naam, type en resource*, gebruiken:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

Als u de brongroepen die beschikken over een specifiek label, gebruikt `az group list`:

```azurecli
az group list --tag Dept=IT
```

Als u alle resources die een bepaalde tag-waarde en, gebruikt `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Wanneer u tags op een resource of resourcegroep toepast, overschrijft u de bestaande tags van die resource of resourcegroep. Als u een resource of resourcegroep hebt met bestaande tags, gaat u anders te werk dan wanneer dat niet het geval is. 

Gebruik het volgende om tags toe te voegen aan een *resourcegroep zonder bestaande tags*:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

Gebruik het volgende om tags toe te voegen aan een *resource zonder bestaande tags*:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

Om labels toevoegen aan een resource die al labels is, ophalen van de bestaande labels, die waarde opnieuw indelen en pas de labels voor bestaande en nieuwe: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

Gebruik het volgende script als u alle tags van een resourcegroep op de bijbehorende resources wilt toepassen *zonder de bestaande tags voor de resources te behouden*:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    az resource tag --tags $t --id $resid
  done 
done
```

Alle tags toepassen van een resourcegroep tot de bronnen en *bestaande tags voor bronnen behouden*, gebruikt u het volgende script:

```azurecli
groups=$(az group list --query [].name --output tsv)
for rg in $groups 
do 
  jsontag=$(az group show -n $rg --query tags)
  t=$(echo $jsontag | tr -d '"{},' | sed 's/: /=/g')
  r=$(az resource list -g $rg --query [].id --output tsv) 
  for resid in $r 
  do 
    jsonrtag=$(az resource show --id $resid --query tags)
    rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
    az resource tag --tags $t$rt --id $resid
  done 
done
```


## <a name="templates"></a>Sjablonen

[!INCLUDE [resource-manager-tags-in-templates](../../includes/resource-manager-tags-in-templates.md)]

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]


## <a name="rest-api"></a>REST API
De Azure portal en PowerShell maken beide gebruik van de [REST-API van Resource Manager](https://docs.microsoft.com/rest/api/resources/) achter de schermen. Als u integreren in een andere omgeving-tagging wilt, kunt u de labels krijgen met behulp van **ophalen** op de resource-ID en werk de set van labels met behulp van een **PATCH** aanroepen.

## <a name="tags-and-billing"></a>Labels en facturering
Labels kunt u uw factureringsgegevens groep. Bijvoorbeeld, als u meerdere virtuele machines voor verschillende organisaties uitvoert, gebruiken de codes voor een groep gebruik door kostenplaats. U kunt ook tags gebruiken om kosten te categoriseren door de runtimeomgeving, zoals het gebruik van facturering voor VM's worden uitgevoerd in de productieomgeving.


Vindt u informatie over tags via de [Azure brongebruik en RateCard APIs](../billing/billing-usage-rate-card-overview.md) of het gebruik door komma's gescheiden waarden (CSV)-bestand. Downloaden van het bestand informatie over het gebruik van de [Azure accountportal](https://account.windowsazure.com/) of [EA portal](https://ea.azure.com). Zie voor meer informatie over de programmatische toegang tot factureringsgegevens [inzicht in uw Microsoft Azure-brongebruik](../billing/billing-usage-rate-card-overview.md). Zie voor REST-API-bewerkingen, [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Wanneer u het gebruik van CSV voor services die ondersteuning bieden voor tags met facturering downloadt, de labels worden weergegeven in de **labels** kolom. Zie voor meer informatie [inzicht in uw factuur voor Microsoft Azure](../billing/billing-understand-your-bill.md).

![Zie de labels in facturering](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Volgende stappen
* U kunt beperkingen en conventies met behulp van aangepaste beleidsregels toepassen voor uw abonnement. Een beleid dat u definieert mogelijk dat alle resources voor een bepaald label een waarde hebben. Zie voor meer informatie [beleid gebruiken voor het beheren van resources en toegangsbeheer](resource-manager-policy.md).
* Zie voor een inleiding tot Azure PowerShell gebruiken wanneer u resources implementeert, [Azure PowerShell gebruiken met Azure Resource Manager](powershell-azure-resource-manager.md).
* Zie voor een inleiding tot de Azure CLI gebruiken wanneer u resources implementeert, [met de Azure CLI voor Mac, Linux en Windows Azure Resource Manager](xplat-cli-azure-resource-manager.md).
* Zie voor een inleiding tot de portal, [met behulp van de Azure-portal voor het beheren van uw Azure-resources](resource-group-portal.md).  
* Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).

