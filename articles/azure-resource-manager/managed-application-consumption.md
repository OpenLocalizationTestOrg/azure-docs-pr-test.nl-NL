---
title: een Azure aaaConsume beheerde toepassing | Microsoft Docs
description: Beschrijft hoe een klant maakt u een Azure beheerde toepassing uit gepubliceerde bestanden.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a>Een interne beheerde toepassing gebruiken

U kunt Azure verbruiken [beheerde toepassingen](managed-application-overview.md) die bestemd zijn voor leden van uw organisatie. Bijvoorbeeld, kunt u beheerde toepassingen van uw IT-afdeling die de organisatie-normen te waarborgen. Deze beheerde toepassingen zijn beschikbaar via Hallo Servicecatalogus, het niet hello Azure Marketplace.

Voordat u doorgaat met dit artikel, moet u een beheerde toepassing beschikbaar is in de Servicecatalogus Hallo hebben voor uw abonnement. Als iemand zich in uw organisatie geen beheerde toepassingen gemaakt nog, raadpleegt u [publiceren van een beheerde toepassingsservices voor intern verbruik](managed-application-publishing.md).

Op dit moment kunt u Azure CLI of hello Azure portal tooconsume beheerde toepassingen.

## <a name="create-hello-managed-application-by-using-hello-portal"></a>Hallo beheerde toepassing maken met behulp van Hallo-portal

toodeploy een beheerde toepassing via Hallo-portal, als volgt te werk:

1. Ga toohello Azure-portal. Zoeken naar **Servicecatalogus beheerde toepassing**.

   ![Servicecatalogus voor beheerde toepassing](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. Selecteer Hallo beheerde toepassing die u wilt dat toocreate uit de lijst met beschikbare oplossingen Hallo. Selecteer **Maken**.

   ![Selectie van de beheerde toepassing](./media/managed-application-consumption/select-offer.png)

1. Geef waarden op voor het Hallo-parameters die vereist tooprovision Hallo resources zijn. Selecteer **West-Centraal VS** voor de locatie. Selecteer **OK**.

   ![Parameters voor de beheerde toepassing](./media/managed-application-consumption/input-parameters.png)

1. Hallo sjabloon valideert Hallo-waarden die u hebt opgegeven. Als de validatie slaagt, selecteert u **OK** toostart Hallo-implementatie.

   ![Validatie van de beheerde toepassing](./media/managed-application-consumption/validation.png)

Nadat Hallo-implementatie is voltooid, worden de juiste resources Hallo in Hallo sjabloon worden gedefinieerd ingericht in beheerde resourcegroep Hallo die u hebt opgegeven.

## <a name="create-hello-managed-application-by-using-azure-cli"></a>Hallo beheerde toepassing maken met Azure CLI

Er zijn twee manieren toocreate een beheerde toepassing met Azure CLI:

* Hallo-opdracht voor het maken van beheerde toepassingen gebruiken.
* Hallo reguliere sjabloon implementatieopdracht gebruiken.

### <a name="use-hello-template-deployment-command"></a>Implementatieopdracht Hallo-sjabloon gebruiken

Implementeer Hallo applianceMainTemplate.json bestand die Hallo leverancier gemaakt.

Vervolgens maakt u twee resourcegroepen. Hallo eerste resourcegroep is waar hello bron beheerde toepassing wordt gemaakt: Microsoft.Solutions/appliances. Hallo tweede resourcegroep bevat alle Hallo resources die zijn gedefinieerd in mainTemplate.json. Deze resourcegroep wordt beheerd door Hallo ISV.

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> Gebruik `westcentralus` als locatie van resourcegroep Hallo Hallo.
>

toodeploy applianceMainTemplate.json in mainResourceGroup, gebruik Hallo volgende opdracht:

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

Na het Hallo voorafgaand aan de sjabloon wordt uitgevoerd, wordt u gevraagd waarden Hallo Hallo-parameters die zijn gedefinieerd in de sjabloon Hallo. Bovendien toohello parameters die zijn vereist voor tooprovision resources in een sjabloon, moet u twee belangrijke parameterwaarden:

- **managedResourceGroupId**: Hallo-ID van Hallo resource met Hallo resources groeperen in applianceMainTemplate.json gedefinieerd. Hallo-ID is van het formulier Hallo `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`. In de Hallo voorgaande voorbeeld, het Hallo-ID van `managedResourceGroup`.
- **applianceDefinitionId**: Hallo-ID van Hallo beheerd bron van de definitie van toepassing. Deze waarde wordt verstrekt door Hallo ISV.

> [!NOTE]
> Hallo uitgever moet verlenen toegang toohello resourcegroep met definitie van de toepassing hello beheerd. Hallo definitie resource is gemaakt in Hallo publisher abonnement. Daarom moet een gebruiker, groep of toepassing in Hallo klant tenant leestoegang toothis resource.

Nadat het Hallo-implementatie wordt voltooid, ziet u Hallo beheerde toepassing in mainResourceGroup wordt gemaakt. Hallo storageAccount resource is gemaakt in managedResourceGroup.

### <a name="use-hello-create-command"></a>Gebruik Hallo opdracht maken

U kunt Hallo `az managedapp create` opdracht toocreate een beheerde toepassing hello beheerd definitie van toepassingen.

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* **apparaat-definitie-Id**: Hallo bron-ID van Hallo definitie van toepassing is gemaakt in de voorgaande stap Hallo beheerd. tooobtain deze ID Hallo volgende opdracht uitvoeren:

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  Deze opdracht retourneert de definitie van de toepassing hello beheerd. U moet Hallo-waarde van eigenschap van Hallo-ID.

* **beheerde-rg-id**: Hallo-naam van Hallo resource met Hallo resources groeperen in applianceMainTemplate.json gedefinieerd. Deze resourcegroep hoort Hallo beheerde resourcegroep. Het wordt beheerd door Hallo uitgever. Als deze nog niet bestaat, wordt deze voor u gemaakt.
* **resourcegroep**: Hallo resourcegroep waar Hallo toepassingsbron beheerd wordt gemaakt. Hallo Microsoft.Solutions/appliance resource woont in deze resourcegroep.
* **parameters**: Hallo parameters die nodig zijn voor het Hallo-resources die zijn gedefinieerd in applianceMainTemplate.json.

## <a name="known-issues"></a>Bekende problemen

Deze preview-versie bevat Hallo problemen te volgen:

* Een interne serverfout 500 wordt weergegeven tijdens het maken van de toepassing hello beheerd Hallo. Als u dit probleem ondervindt, is het waarschijnlijk toobe onregelmatige. Hallo-bewerking opnieuw uit.
* Een nieuwe resourcegroep is nodig voor beheerde Hallo-resourcegroep. Als u een bestaande resourcegroep gebruikt, mislukt de Hallo-implementatie.
* Hallo resourcegroep met Hallo Microsoft.Solutions/appliances bron moet worden gemaakt in Hallo **westcentralus** locatie.

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).
* Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).
* Zie voor meer informatie over publiceren beheerde toepassingen toohello Azure Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).
* Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).
