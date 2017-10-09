---
title: aaaMove Azure-resources toonew abonnement of resourcegroep groep | Microsoft Docs
description: Gebruik Azure Resource Manager toomove resources tooa nieuwe resourcegroep of abonnement.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a>Verplaatsen van resources toonew resourcegroep of abonnement
Dit onderwerp leest u hoe toomove resources tooeither een nieuw abonnement of een nieuwe bron groeperen in Hallo hetzelfde abonnement. U kunt Hallo-portal, PowerShell, Azure CLI of Hallo REST-API toomove resource gebruiken. Hallo migratiebewerkingen in dit onderwerp zijn beschikbaar tooyou zonder eventuele hulp van de ondersteuning van Azure.

Bij het verplaatsen van resources, worden zowel Hallo brongroep en de doelgroep Hallo Hallo tijdens vergrendeld. Schrijf- en verwijderbewerkingen op Hallo resourcegroepen worden geblokkeerd totdat Hallo verplaatsen is voltooid. Deze vergrendeling betekent dat u niet kunt toevoegen, bijwerken of verwijderen van resources in resourcegroepen hello, maar dit betekent niet dat Hallo resources worden bevroren. Als u een SQL-Server en de database tooa nieuwe resourcegroep hebt verplaatst, ervaringen een toepassing die gebruikmaakt van Hallo database zonder uitvaltijd. Dit kan nog steeds lezen en schrijven van toohello-database.

U kunt Hallo-locatie van Hallo-bron niet wijzigen. Door een resource alleen verplaatst u deze tooa nieuwe resourcegroep. de nieuwe resourcegroep Hallo mag een andere locatie hebben, maar die verandert niet Hallo-locatie van het Hallo-resource.

> [!NOTE]
> Dit artikel wordt beschreven hoe toomove resources binnen een bestaande Azure-account aanbieden. Als u daadwerkelijk wilt toochange uw Azure-account biedt (zoals een upgrade van betalen naar gebruik toopre betalen) terwijl u toowork met uw bestaande bronnen, Zie [overschakelen van uw Azure-abonnement tooanother aanbieding](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Controlelijst voor het verplaatsen van resources
Er zijn een aantal belangrijke stappen tooperform voordat u doorgaat een resource. U kunt fouten voorkomen door te controleren of aan de volgende voorwaarden is voldaan.

1. Hallo bron- en doelserver abonnementen moeten bestaan binnen Hallo dezelfde [Azure Active Directory-tenant](../active-directory/active-directory-howto-tenant.md). beide abonnementen hebben dezelfde Hallo toocheck tenant-ID, gebruikt u Azure PowerShell of Azure CLI.

  Azure PowerShell gebruiken:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Voor Azure CLI 2.0 gebruiken:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Als Hallo tenant-id's voor zijn Hallo bron- en doelserver geen abonnementen Hallo dezelfde, kunt u proberen toochange Hallo directory voor Hallo-abonnement. Deze optie is echter alleen beschikbaar tooService beheerders die zijn aangemeld met een Microsoft-account (niet in een organisatie-account). Hallo-directory, aanmelden toohello wijzigen tooattempt [klassieke portal](https://manage.windowsazure.com/), en selecteer **instellingen**, en Hallo abonnement te selecteren. Als hello **Directory bewerken** pictogram beschikbaar is, selecteert u deze toochange hello Azure Active Directory die is gekoppeld.

  ![directory bewerken](./media/resource-group-move-resources/edit-directory.png)

  Als dit pictogram niet beschikbaar is, moet u contact op met de ondersteuning toomove Hallo resources tooa nieuwe tenant.

2. Hallo-service moet Hallo mogelijkheid toomove bronnen inschakelen. Dit onderwerp vindt u welke services kunnen verplaatsen bronnen en welke services de zwevende resources niet inschakelt.
3. Hallo doelabonnement moet zijn geregistreerd voor de resourceprovider Hallo Hallo resource worden verplaatst. Als niet zo is, u ontvangt een foutmelding weergegeven dat Hallo **abonnement is niet geregistreerd voor een brontype**. U kunt dit probleem tegenkomen bij het verplaatsen van een nieuw abonnement van bron tooa, maar dat abonnement nog nooit is gebruikt met dat resourcetype. toolearn hoe toocheck Hallo registratiestatus en registreren van de resourceproviders, Zie [resourceproviders en typen](resource-manager-supported-services.md).

## <a name="when-toocall-support"></a>Wanneer toocall ondersteunt
U kunt de meeste bronnen via Hallo selfservice operations weergegeven in dit onderwerp kunt verplaatsen. Hallo selfservice bewerkingen om te gebruiken:

* Resource Manager-resources wilt verplaatsen.
* Klassieke resources op basis van toohello verplaatsen [klassieke implementatie beperkingen](#classic-deployment-limitations).

Wanneer u moet contact op met ondersteuning:

* Verplaats uw resources tooa nieuwe Azure-account (en Azure Active Directory-tenant).
* Klassieke resources verplaatsen, maar hebben problemen met Hallo beperkingen.

## <a name="services-that-enable-move"></a>Services waarmee verplaatsen
Op dit moment zijn Hallo-services die bewegende tooboth een nieuwe resourcegroep en abonnement inschakelen:

* API Management
* App Service-apps (web-apps) - Zie [App Service-beperkingen](#app-service-limitations)
* Application Insights
* Automatisering
* Batch
* Bing-kaarten
* CDN
* Cloud Services - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Cognitive Services
* Content Moderator
* Data Catalog
* Data Factory
* Data Lake Analytics
* Data Lake Store
* DNS
* Azure Cosmos DB
* Event Hubs
* HDInsight-clusters - Zie [HDInsight-beperkingen](#hdinsight-limitations)
* IoT-Hubs
* Key Vault
* Taakverdelers
* Logic Apps
* Machine Learning
* Media Services
* Mobile Engagement
* Notification Hubs
* Operational Insights
* Operations Management
* Power BI
* Redis Cache
* Scheduler
* Search
* Server Management
* Service Bus
* Service Fabric
* Storage
* Opslag (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Stream Analytics - Stream Analytics-taken kunnen niet worden verplaatst, bij uitvoering in status.
* SQL Database-server - hello database en de server moeten zich bevinden in Hallo dezelfde resourcegroep. Wanneer u een SQL-server hebt verplaatst, worden ook alle databases die zijn verplaatst.
* Traffic Manager
* Virtuele machines
* Virtuele Machines met een certificaat dat is opgeslagen in de Sleutelkluis - verplaatsen toonew resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross abonnement verplaatsen is niet ingeschakeld.
* Virtuele Machines (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Schaalsets voor virtuele machines
* Virtuele netwerken - momenteel, een peered virtueel netwerk kan niet worden verplaatst tot VNet-peering is uitgeschakeld. Als uitgeschakeld, Hallo virtueel netwerk kan worden verplaatst en Hallo VNet-peering kan worden ingeschakeld. Bovendien kan een virtueel netwerk verplaatste tooa ander abonnement niet als Hallo virtueel netwerk subnet met resourcenavigatiekoppelingen bevat. Een virtueel netwerksubnet heeft bijvoorbeeld een resource navigatiekoppeling wanneer een bron van de redis Microsoft.Cache wordt geïmplementeerd in dit subnet.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Services die niet verplaatsen inschakelen
Hallo-services die op dit moment niet inschakelen voor het verplaatsen van een resource zijn:

* AD-domeinservices
* Hybride AD Health-Service
* Application Gateway
* Beschikbaarheidssets met virtuele Machines met schijven beheerd
* BizTalk Services
* Container Service
* ExpressRoute
* DevTest Labs - verplaatsen toonew resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross-abonnement verplaatsen is niet ingeschakeld.
* Dynamics LCS
* Installatiekopieën die zijn gemaakt op basis van schijven beheerd
* Beheerde schijven
* Beheerde toepassingen
* Recovery Services-kluis: ook doen door niet verplaatsen Hallo Compute, netwerk en opslag van de resources die zijn gekoppeld aan de Recovery Services Hallo-kluis, Zie [Recovery Services-beperkingen](#recovery-services-limitations).
* Beveiliging
* Momentopnamen die zijn gemaakt op basis van schijven beheerd
* StorSimple-Apparaatbeheer
* Virtuele Machines met beheerde schijven
* Virtuele netwerken (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Virtuele Machines die zijn gemaakt op basis van bronnen van de Marketplace - kan niet worden verplaatst tussen abonnementen. Resource moet toobe gemaakt in het huidige abonnement Hallo en opnieuw wordt geïmplementeerd in een nieuw abonnement Hallo

## <a name="app-service-limitations"></a>App Service-beperkingen
Als u werkt met App Service-apps, kunt u alleen een App Service-abonnement niet verplaatsen. toomove App Service-apps, uw opties zijn:

* Hallo App Service-abonnement en alle andere App Service-resources in die groep tooa nieuwe resource resourcegroep die geen App Service-resources verplaatsen. Deze vereiste manier die moet u zelfs verplaatsen Hallo App Service-resources die niet zijn gekoppeld aan Hallo App Service-abonnement.
* Hallo apps tooa andere resourcegroep verplaatsen, maar alle App Service-abonnementen in de oorspronkelijke resourcegroep Hallo houden.

Hallo Hallo App Service plan hoeft niet tooreside in dezelfde resourcegroep als Hallo-app voor Hallo app toofunction correct.

Bijvoorbeeld, als uw resourcegroep bevat:

* **Web-a** die is gekoppeld aan **plan een**
* **Web-b** die is gekoppeld aan **plan b**

Uw opties zijn:

* Verplaats **web-a**, **plan een**, **web-b**, en **plan b**
* Verplaats **web-a** en **web-b**
* Verplaats **web-a**
* Verplaats **web-b**

Alle andere combinaties hebben betrekking op verlaten achter een brontype dat bij het verplaatsen van een App Service-abonnement (type van de bron-App Service) kan niet worden achtergelaten.

Als uw web-app bevindt zich in een andere resourcegroep dan de App Service-abonnement, maar u toomove beide tooa nieuwe resourcegroep wilt, moet u Hallo verplaatsen in twee stappen uitvoeren. Bijvoorbeeld:

* **Web-a** bevindt zich in **web-groep**
* **plan een** bevindt zich in **plan-groep**
* Gewenste **web-a** en **plan een** tooreside in **gecombineerd groep**

tooaccomplish dit verplaatst, twee afzonderlijke move-bewerkingen uitvoeren in Hallo volgende volgorde:

1. Hallo verplaatsen **web-a** te**plan-groep**
2. Verplaats **web-a** en **plan een** te**gecombineerd groep**.

U kunt een nieuwe App Service-certificaat tooa-resourcegroep of abonnement zonder problemen verplaatsen. Als uw web-app een SSL-certificaat bevat dat u hebt aangeschaft extern en toohello-app geüpload, moet u Hallo-certificaat voordat zwevend Hallo web-app verwijderen. U kunt bijvoorbeeld Hallo stappen uitvoeren:

1. Hallo geüpload certificaat verwijderen uit Hallo web-app
2. Hallo-web-app te verplaatsen
3. Hallo certificaat toohello web-app uploaden

## <a name="recovery-services-limitations"></a>Recovery Services-beperkingen
Verplaatsing is niet ingeschakeld voor de opslag, netwerk, of rekenresources tooset van herstel na noodgevallen gebruikt met Azure Site Recovery.

Bijvoorbeeld, Stel dat u de replicatie van uw lokale machines tooa storage-account (Storage1) hebt ingesteld en Hallo beveiligd machine toocome-up wilt na failover tooAzure als een virtuele machine (VM1) tooa virtueel netwerk (Network1 gekoppelde). U kunt een van deze Azure-resources - Storage1, VM1, niet verplaatsen en Network1 - via resource groepen binnen Hallo dezelfde abonnement of tussen abonnementen.

## <a name="hdinsight-limitations"></a>HDInsight-beperkingen

U kunt de HDInsight-clusters tooa nieuw abonnement of resourcegroep verplaatsen. U kunt echter niet verplaatsen tussen abonnementen Hallo networking resources toohello gekoppelde HDInsight-cluster (zoals Hallo virtueel netwerk, een NIC of een load balancer). U kunt bovendien tooa nieuwe resourcegroep een NIC die is aangesloten tooa virtuele machine voor het Hallo-cluster niet verplaatsen.

Wanneer u een nieuw abonnement voor HDInsight-cluster tooa verplaatst, moet u eerst andere bronnen (zoals Hallo storage-account) verplaatsen. Verplaats Hallo HDInsight-cluster op zichzelf.

## <a name="classic-deployment-limitations"></a>Beperkingen voor klassieke implementatie
Hallo verschillen opties voor het verplaatsen van resources die zijn geïmplementeerd via het klassieke model Hallo op basis van of het verplaatsen van resources binnen een abonnement of een nieuw abonnement tooa Hallo.

### <a name="same-subscription"></a>Hetzelfde abonnement
Wanneer u resources van één resource groep tooanother resourcegroep binnen hetzelfde abonnement behoren, Hallo volgen beperkingen van toepassing hello verplaatst:

* Virtuele netwerken (klassiek) kunnen niet worden verplaatst.
* Virtuele machines (klassiek) moeten worden verplaatst met Hallo-cloudservice.
* Cloudservice kan alleen worden verplaatst als Hallo verplaatsen alle virtuele machines bevat.
* Slechts één cloudservice kan tegelijk worden verplaatst.
* Slechts één opslagaccount (klassiek) kan tegelijk worden verplaatst.
* Storage-account (klassiek) kan niet worden verplaatst in Hallo dezelfde bewerking met een virtuele machine of een cloudservice.

toomove klassieke resources tooa nieuwe resourcegroep binnen hetzelfde abonnement hello, gebruikt u Hallo standaard migratiebewerkingen via Hallo [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), of [REST-API](#use-rest-api). U dezelfde bewerkingen Hallo terwijl u gebruikt voor het verplaatsen van Resource Manager-resources.

### <a name="new-subscription"></a>Nieuw abonnement
Bij het verplaatsen van resources tooa nieuw abonnement toepassing hello volgende beperkingen:

* Alle klassieke resources in het Hallo-abonnement moeten worden verplaatst in Hallo dezelfde bewerking.
* Hallo doelabonnement mag geen andere klassieke resources bevatten.
* Hallo verplaatsen kan alleen worden aangevraagd via een afzonderlijke REST-API voor klassieke verplaatst. Hallo-opdrachten voor het verplaatsen van standaard Resource Manager werken niet bij het verplaatsen van klassieke resources tooa nieuw abonnement.

toomove klassieke resources tooa nieuw abonnement, gebruik Hallo REST-bewerkingen die specifieke tooclassic resources zijn. toouse REST, Voer Hallo stappen te volgen:

1. Controleer als Hallo bronabonnement kan deelnemen in een abonnementoverschrijdende verplaatsen. Volgende bewerking hello gebruiken:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     In de aanvraagtekst hello, zijn onder andere:

  ```json
  {
    "role": "source"
  }
  ```

     Hallo-antwoord voor Hallo validatiebewerking heeft Hallo volgende indeling:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Controleer als Hallo doelabonnement kan deelnemen in een abonnementoverschrijdende verplaatsen. Volgende bewerking hello gebruiken:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     In de aanvraagtekst hello, zijn onder andere:

  ```json
  {
    "role": "target"
  }
  ```

     Hallo-reactie is in dezelfde notatie als de validatie van abonnement Hallo Hallo.
3. Verplaats alle klassieke resources uit één abonnement tooanother abonnement als beide abonnementen gevalideerd worden, met de volgende bewerking Hallo:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    In de aanvraagtekst hello, zijn onder andere:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

Hallo mogelijk voor enkele minuten uitgevoerd.

## <a name="use-portal"></a>De portal gebruiken
toomove resources, selecteer Hallo resourcegroep met deze bronnen, en selecteer vervolgens Hallo **verplaatsen** knop.

![Verplaatsen van resources](./media/resource-group-move-resources/select-move.png)

Selecteer of u Hallo resources tooa nieuwe resourcegroep of een nieuw abonnement overstapt.

Selecteer Hallo resources toomove en Hallo bestemming resourcegroep. Bevestig dat u voor deze resources en selecteer tooupdate scripts moet **OK**. Als u in de vorige stap Hallo Hallo abonnement bewerkingspictogram hebt geselecteerd, moet u ook het doelabonnement Hallo selecteren.

![Selecteer bestemming](./media/resource-group-move-resources/select-destination.png)

In **meldingen**, ziet u dat Hallo verplaatsen bewerking wordt uitgevoerd.

![verplaatsing status weergeven](./media/resource-group-move-resources/show-status.png)

Wanneer deze is voltooid, wordt u gewaarschuwd van Hallo resultaat.

![resultaat van de verplaatsing weergeven](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>PowerShell gebruiken
toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `Move-AzureRmResource` opdracht.

Hallo eerste voorbeeld laat zien hoe toomove één resource tooa nieuwe resourcegroep.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Hallo tweede voorbeeld wordt getoond hoe toomove meerdere resources tooa nieuwe resourcegroep.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

toomove tooa nieuw abonnement, een waarde bevatten voor Hallo `DestinationSubscriptionId` parameter.

U wordt gevraagd dat u wilt dat toomove hello tooconfirm opgegeven resources.

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Azure CLI 2.0 gebruiken
toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `az resource move` opdracht. Hallo resource-id's van Hallo resources toomove bieden. U kunt resource-id's met de volgende opdracht Hallo krijgen:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Hallo volgende voorbeeld ziet u hoe toomove een storage account tooa nieuwe resourcegroep. In Hallo `--ids` parameter, Geef een door spaties gescheiden lijst met Hallo resource-id's toomove.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

toomove tooa nieuw abonnement, bieden Hallo `--destination-subscription-id` parameter.

## <a name="use-azure-cli-10"></a>Azure CLI 1.0 gebruiken
toomove bestaande resources tooanother resourcegroep of abonnement, gebruikt u Hallo `azure resource move` opdracht. Hallo resource-id's van Hallo resources toomove bieden. U kunt resource-id's met de volgende opdracht Hallo krijgen:

```azurecli
azure resource list -g sourceGroup --json
```

Welke retourneert Hallo volgende indeling:

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

Hallo volgende voorbeeld ziet u hoe toomove een storage account tooa nieuwe resourcegroep. In Hallo `-i` parameter, Geef een door komma's gescheiden lijst met Hallo resource-id's toomove.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

U wordt gevraagd dat u wilt dat toomove hello tooconfirm van de opgegeven bron.

## <a name="use-rest-api"></a>REST API gebruiken
toomove bestaande resources tooanother resourcegroep of abonnement, uitvoeren:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

In de aanvraagtekst hello geeft u de doelresourcegroep hello en Hallo resources toomove. Zie voor meer informatie over Hallo move REST-bewerking [verplaatsen van resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Volgende stappen
* toolearn over PowerShell-cmdlets voor het beheren van uw abonnement, Zie [Azure PowerShell gebruiken met Resource Manager](powershell-azure-resource-manager.md).
* toolearn over Azure CLI-opdrachten voor het beheren van uw abonnement, Zie [Using hello Azure CLI met Resource Manager](xplat-cli-azure-resource-manager.md).
* toolearn over portal functies voor het beheren van uw abonnement, Zie [hello Azure portal toomanage bronnen](resource-group-portal.md).
* toolearn over het toepassen van een logische tooyour organisatiebronnen, Zie [Using tags tooorganize uw resources](resource-group-using-tags.md).
