---
title: aaaTag Azure-resources voor logische organisatie | Microsoft Docs
description: Toont hoe tooapply tags tooorganize Azure-resources voor facturerings- en beheren.
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
ms.openlocfilehash: e07470463d160f8cefe5c80bc91e66a96af6ca45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-tags-tooorganize-your-azure-resources"></a>Gebruik tags tooorganize uw Azure-resources
[!INCLUDE [resource-manager-tag-introduction](../../includes/resource-manager-tag-introduction.md)]

> [!NOTE]
> U kunt alleen tooresources labels die ondersteuning bieden voor Azure Resource Manager-bewerkingen toepassen. Als u een virtuele machine, het virtuele netwerk of de storage-account via de klassieke implementatiemodel hello (zoals als via Hallo klassieke Azure-portal) gemaakt, kunt u een label toothat resource niet toepassen. toosupport tagging, implementeert u deze resources via Resource Manager opnieuw. Alle andere bronnen ondersteuning voor codering.
> 
> 

## <a name="policies-for-tag-consistency"></a>Beleid voor consistentie van de tag

U kunt resource toocreate standaardregels-beleid gebruiken voor uw organisatie. U kunt beleidsregels die zorg ervoor dat resources worden gemarkeerd met de juiste waarden Hallo maken. Zie voor meer informatie [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).

## <a name="powershell"></a>PowerShell
[!INCLUDE [resource-manager-tag-resources-powershell](../../includes/resource-manager-tag-resources-powershell.md)]

## <a name="azure-cli"></a>Azure CLI

toosee Hallo bestaande codes voor een *resourcegroep*, gebruiken:

```azurecli
az group show -n examplegroup --query tags
```

Script retourneert Hallo volgende indeling:

```json
{
  "Dept"        : "IT",
  "Environment" : "Test"
}
```

toosee Hallo bestaande codes voor een *resource met een opgegeven bron-ID*, gebruiken:

```azurecli
az resource show --id {resource-id} --query tags
```

Of toosee Hallo bestaande codes voor een *resource met een opgegeven groep met de naam, type en resource*, gebruiken:

```azurecli
az resource show -n examplevnet -g examplegroup --resource-type "Microsoft.Network/virtualNetworks" --query tags
```

tooget-resourcegroepen die beschikken over een specifieke tag gebruiken `az group list`:

```azurecli
az group list --tag Dept=IT
```

alle Hallo-resources die een bepaalde tag en-waarde, gebruikt u tooget `az resource list`:

```azurecli
az resource list --tag Dept=Finance
```

Telkens wanneer u labels tooa resource of een resourcegroep hebt toegepast, kunt u bestaande labels op die resource of resourcegroep Hallo overschrijven. Daarom moet u een andere benadering, op basis van of Hallo resource of resourcegroep bestaande labels heeft. 

tooadd tags tooa *resourcegroep zonder bestaande tags*, gebruiken:

```azurecli
az group update -n examplegroup --set tags.Environment=Test tags.Dept=IT
```

tooadd tags tooa *resource zonder bestaande tags*, gebruiken:

```azurecli
az resource tag --tags Dept=IT Environment=Test -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
``` 

tooadd labels tooa resource die al is tags, Hallo bestaande labels ophalen, die waarde opnieuw indelen en Hallo bestaande en nieuwe tags toepassen: 

```azurecli
jsonrtag=$(az resource show -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks" --query tags)
rt=$(echo $jsonrtag | tr -d '"{},' | sed 's/: /=/g')
az resource tag --tags $rt Project=Redesign -g examplegroup -n examplevnet --resource-type "Microsoft.Network/virtualNetworks"
```

tooapply die alle labels van een resource tooits groepsbronnen en *bestaande labels op Hallo resources niet bewaren*, Hallo script volgende gebruiken:

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

tooapply die alle labels van een resource tooits groepsbronnen en *bestaande tags voor bronnen behouden*, Hallo script volgende gebruiken:

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
Hello Azure-portal en PowerShell gebruiken Hallo [REST-API van Resource Manager](https://docs.microsoft.com/rest/api/resources/) achter de schermen Hallo. Als u toointegrate labels in een andere omgeving nodig hebt, kunt u de labels krijgen met behulp van **ophalen** op Hallo resource-ID en update Hallo set van labels met behulp van een **PATCH** aanroepen.

## <a name="tags-and-billing"></a>Labels en facturering
U kunt uw factureringsgegevens toogroup labels. Bijvoorbeeld, als u meerdere virtuele machines voor verschillende organisaties uitvoert, gebruik Hallo labels toogroup gebruik door kostenplaats. U kunt ook labels toocategorize kosten door de runtimeomgeving, zoals facturering gebruik Hallo voor virtuele machines die worden uitgevoerd in de productieomgeving hello gebruiken.


U kunt informatie over tags via Hallo ophalen [Azure brongebruik en RateCard APIs](../billing/billing-usage-rate-card-overview.md) of Hallo-gebruik door komma's gescheiden waarden (CSV)-bestand. U Hallo gebruik bestand downloaden van Hallo [Azure accountportal](https://account.windowsazure.com/) of [EA portal](https://ea.azure.com). Zie voor meer informatie over toegang op programmeerniveau toobilling [inzicht in uw Microsoft Azure-brongebruik](../billing/billing-usage-rate-card-overview.md). Zie voor REST-API-bewerkingen, [Azure Billing REST API-verwijzing](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c).


Wanneer u Hallo gebruik CSV voor services die ondersteuning bieden voor facturerings-tags downloadt, Hallo labels worden weergegeven in Hallo **labels** kolom. Zie voor meer informatie [inzicht in uw factuur voor Microsoft Azure](../billing/billing-understand-your-bill.md).

![Zie de labels in facturering](./media/resource-group-using-tags/billing_csv.png)

## <a name="next-steps"></a>Volgende stappen
* U kunt beperkingen en conventies met behulp van aangepaste beleidsregels toepassen voor uw abonnement. Een beleid dat u definieert mogelijk dat alle resources voor een bepaald label een waarde hebben. Zie voor meer informatie [beleid toomanage resources gebruiken en toegangsbeheer](resource-manager-policy.md).
* Zie voor een inleiding toousing Azure PowerShell gebruiken wanneer u resources implementeert, [Azure PowerShell gebruiken met Azure Resource Manager](powershell-azure-resource-manager.md).
* Zie voor een inleiding toousing hello Azure CLI gebruiken wanneer u resources implementeert, [Using hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](xplat-cli-azure-resource-manager.md).
* Zie voor een inleiding toousing Hallo-portal [Using hello Azure portal toomanage uw Azure-resources](resource-group-portal.md).  
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

