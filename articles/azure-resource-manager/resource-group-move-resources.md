---
title: Azure-resources naar nieuwe abonnement of de resource-groep verplaatsen | Microsoft Docs
description: Azure Resource Manager gebruiken voor resources verplaatsen naar een nieuwe resourcegroep of abonnement.
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
ms.openlocfilehash: e138f80e808968ab4bf5c11cfd5fd46fe4a1bcce
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a>Resources verplaatsen naar de nieuwe resourcegroep of abonnement
Dit onderwerp leest u hoe u resources verplaatsen naar een nieuw abonnement of een nieuwe resourcegroep in hetzelfde abonnement. U kunt de portal, PowerShell, Azure CLI of de REST-API resource verplaatsen. De verplaatsing bewerkingen in dit onderwerp voor u beschikbaar zijn zonder eventuele hulp van de ondersteuning van Azure.

Bij het verplaatsen van resources, worden zowel de bronnengroep als de doelgroep vergrendeld tijdens de bewerking. Schrijven en verwijderen van bewerkingen op de brongroepen worden geblokkeerd totdat de verplaatsing is voltooid. Deze vergrendeling betekent dat u niet kunt toevoegen, bijwerken of verwijderen van resources in de resourcegroepen, maar dit betekent niet dat de bronnen worden bevroren. Als u een SQL-Server en de bijbehorende database naar een nieuwe resourcegroep verplaatst, ervaringen een toepassing die gebruikmaakt van de database zonder uitvaltijd. Dit kan nog steeds lezen en schrijven naar de database.

U kunt de locatie van de resource niet wijzigen. Het verplaatsen van een resource alleen verplaatst naar een nieuwe resourcegroep. De nieuwe resourcegroep mag een andere locatie hebben, maar die niet de locatie van de bron wordt gewijzigd.

> [!NOTE]
> Dit artikel wordt beschreven hoe u resources binnen een bestaande Azure-account aanbieden verplaatst. Als u daadwerkelijk wijzigen van uw Azure-account biedt (zoals een upgrade van betalen naar gebruik vooraf betalen wilt) maar blijft werken met uw bestaande bronnen, Zie [overschakelen van uw Azure-abonnement op een andere aanbieding](../billing/billing-how-to-switch-azure-offer.md).
>
>

## <a name="checklist-before-moving-resources"></a>Controlelijst voor het verplaatsen van resources
Voordat u een resource verplaatst, moeten er enkele belangrijke stappen worden uitgevoerd. U kunt fouten voorkomen door te controleren of aan de volgende voorwaarden is voldaan.

1. De bron- en doelserver abonnementen moeten bestaan binnen dezelfde [Azure Active Directory-tenant](../active-directory/active-directory-howto-tenant.md). Om te controleren of beide abonnementen dezelfde tenant-ID hebben, gebruikt u Azure PowerShell of Azure CLI.

  Azure PowerShell gebruiken:

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  Voor Azure CLI 2.0 gebruiken:

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  Als de tenant-id's voor de bron- en doelserver abonnementen niet hetzelfde zijn zijn, kunt u proberen de map voor het abonnement wilt wijzigen. Deze optie is echter alleen beschikbaar voor Service-beheerders die zijn aangemeld met een Microsoft-account (niet in een organisatie-account). Om te proberen de map wordt gewijzigd, moet u zich aanmelden bij de [klassieke portal](https://manage.windowsazure.com/), en selecteer **instellingen**, en selecteer het abonnement. Als de **Directory bewerken** pictogram beschikbaar is, selecteert u het wijzigen van de gekoppelde Azure Active Directory.

  ![directory bewerken](./media/resource-group-move-resources/edit-directory.png)

  Als dit pictogram niet beschikbaar is, moet u contact op met ondersteuning om de resources verplaatsen naar een nieuwe tenant.

2. De service moet de mogelijkheid activeren om resources te verplaatsen. Dit onderwerp vindt u welke services kunnen verplaatsen bronnen en welke services de zwevende resources niet inschakelt.
3. Het doelabonnement moet zijn geregistreerd voor de resourceprovider van de resource die wordt verplaatst. Als u niet het geval is, er een foutbericht met de mededeling dat de **abonnement is niet geregistreerd voor een brontype**. U kunt dit probleem tegenkomen bij het verplaatsen van een resource naar een nieuw abonnement, terwijl dat abonnement nooit is gebruikt met dat type resource. Raadpleeg [Resourceproviders en typen](resource-manager-supported-services.md) om te leren hoe u de registratiestatus controleert en resourceproviders registreert.

## <a name="when-to-call-support"></a>Het aanroepen van ondersteuning
U kunt de meeste resources via de selfservice bewerkingen die wordt weergegeven in dit onderwerp kunt verplaatsen. De bewerkingen selfservice gebruiken:

* Resource Manager-resources wilt verplaatsen.
* Verplaatsen van klassieke resources volgens de [klassieke implementatie beperkingen](#classic-deployment-limitations).

Wanneer u moet contact op met ondersteuning:

* Uw resources verplaatsen naar een nieuwe Azure-account (en Azure Active Directory-tenant).
* Klassieke resources verplaatsen, maar hebben problemen met de beperkingen.

## <a name="services-that-enable-move"></a>Services waarmee verplaatsen
Op dit moment zijn de services die verplaatsen naar een nieuwe resourcegroep en een abonnement inschakelen:

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
* SQL Database-server - database en server moet zich bevinden in dezelfde resourcegroep. Wanneer u een SQL-server hebt verplaatst, worden ook alle databases die zijn verplaatst.
* Traffic Manager
* Virtuele machines
* Virtuele Machines met een certificaat wordt opgeslagen in de Sleutelkluis - verplaatsen naar de nieuwe resource groep in hetzelfde abonnement is ingeschakeld, maar het verplaatsen van cross-abonnement is niet ingeschakeld.
* Virtuele Machines (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Schaalsets voor virtuele machines
* Virtuele netwerken - momenteel, een peered virtueel netwerk kan niet worden verplaatst tot VNet-peering is uitgeschakeld. Als uitgeschakeld, het virtuele netwerk kan worden verplaatst en de VNet-peering kan worden ingeschakeld. Bovendien kan niet een virtueel netwerk worden verplaatst naar een ander abonnement, als het virtuele netwerk subnet met resourcenavigatiekoppelingen bevat. Een virtueel netwerksubnet heeft bijvoorbeeld een resource navigatiekoppeling wanneer een bron van de redis Microsoft.Cache wordt geïmplementeerd in dit subnet.
* VPN Gateway


## <a name="services-that-do-not-enable-move"></a>Services die niet verplaatsen inschakelen
De services die op dit moment niet inschakelen voor het verplaatsen van een resource zijn:

* AD-domeinservices
* Hybride AD Health-Service
* Application Gateway
* Beschikbaarheidssets met virtuele Machines met schijven beheerd
* BizTalk Services
* Container Service
* ExpressRoute
* DevTest Labs - te verplaatsen naar een nieuwe resourcegroep in hetzelfde abonnement is ingeschakeld, maar cross abonnement verplaatsen is niet ingeschakeld.
* Dynamics LCS
* Installatiekopieën die zijn gemaakt op basis van schijven beheerd
* Beheerde schijven
* Beheerde toepassingen
* Recovery Services-kluis - ook komen niet verplaatsen van de Compute, Network en Storage-resources die zijn gekoppeld aan de Recovery Services-kluis, Zie [Recovery Services-beperkingen](#recovery-services-limitations).
* Beveiliging
* Momentopnamen die zijn gemaakt op basis van schijven beheerd
* StorSimple-Apparaatbeheer
* Virtuele Machines met beheerde schijven
* Virtuele netwerken (klassiek) - Zie [klassieke implementatie beperkingen](#classic-deployment-limitations)
* Virtuele Machines die zijn gemaakt op basis van bronnen van de Marketplace - kan niet worden verplaatst tussen abonnementen. Resource moet worden gemaakt in het huidige abonnement en opnieuw wordt geïmplementeerd in het nieuwe abonnement

## <a name="app-service-limitations"></a>App Service-beperkingen
Als u werkt met App Service-apps, kunt u alleen een App Service-abonnement niet verplaatsen. Uw opties zijn beschikbaar voor het verplaatsen van App Service-apps:

* De App Service-abonnement en alle andere App Service-resources in die resourcegroep verplaatsen naar een nieuwe resourcegroep die geen App Service-resources. Deze vereiste betekent dat u zelfs de App Service-resources die niet gekoppeld aan de App Service-abonnement zijn te verplaatsen.
* De apps naar een andere resourcegroep verplaatsen, maar blijven alle App Service-abonnementen in de oorspronkelijke resourcegroep.

De App Service-abonnement hoeft niet te bevinden zich in dezelfde resourcegroep als de app voor de app te laten functioneren.

Bijvoorbeeld, als uw resourcegroep bevat:

* **Web-a** die is gekoppeld aan **plan een**
* **Web-b** die is gekoppeld aan **plan b**

Uw opties zijn:

* Verplaats **web-a**, **plan een**, **web-b**, en **plan b**
* Verplaats **web-a** en **web-b**
* Verplaats **web-a**
* Verplaats **web-b**

Alle andere combinaties hebben betrekking op verlaten achter een brontype dat bij het verplaatsen van een App Service-abonnement (type van de bron-App Service) kan niet worden achtergelaten.

Als uw web-app bevindt zich in een andere resourcegroep dan de App Service-abonnement, maar u wilt zowel voor een nieuwe resourcegroep te verplaatsen, moet u de verplaatsing in twee stappen uitvoeren. Bijvoorbeeld:

* **Web-a** bevindt zich in **web-groep**
* **plan een** bevindt zich in **plan-groep**
* Gewenste **web-a** en **plan een** zich bevinden **gecombineerd groep**

Voer hiertoe verplaatsing twee afzonderlijke migratiebewerkingen in de volgende volgorde:

1. Verplaats de **web-a** naar **plan-groep**
2. Verplaats **web-a** en **plan een** naar **gecombineerd groep**.

U kunt een App Service-certificaat verplaatsen naar een nieuwe resourcegroep of abonnement zonder problemen. Als uw web-app een SSL-certificaat dat u hebt aangeschaft extern en geüpload naar de app bevat, moet u het certificaat verwijderen voordat u de web-app. U kunt bijvoorbeeld de volgende stappen uitvoeren:

1. Het geüploade certificaat verwijderen van de web-app
2. Verplaatsen van de web-app
3. Upload het certificaat naar de web-app

## <a name="recovery-services-limitations"></a>Recovery Services-beperkingen
Verplaatsen is niet ingeschakeld voor de opslag, netwerk, of Compute-resources die worden gebruikt voor het instellen van herstel na noodgevallen met Azure Site Recovery.

Stel dat u de replicatie van uw lokale machines naar een opslagaccount (Storage1) hebt ingesteld en wilt dat de beveiligde machine actief na een failover naar Azure als een virtuele machine (VM1) gekoppeld aan een virtueel netwerk (Network1). U kunt deze Azure-resources - Storage1, VM1 en Network1 - niet verplaatsen, tussen resourcegroepen binnen hetzelfde abonnement of tussen abonnementen.

## <a name="hdinsight-limitations"></a>HDInsight-beperkingen

U kunt de HDInsight-clusters verplaatsen naar een nieuw abonnement of resourcegroep. U kunt echter niet verplaatsen tussen abonnementen de netwerkresources die zijn gekoppeld aan het HDInsight-cluster (zoals het virtuele netwerk, een NIC of een load balancer). Bovendien verplaatsen u niet naar een nieuwe resourcegroep een NIC die is gekoppeld aan een virtuele machine voor het cluster.

Wanneer u een HDInsight-cluster naar een nieuw abonnement verplaatst, moet u eerst andere bronnen (zoals het storage-account) verplaatsen. Verplaats het HDInsight-cluster op zichzelf.

## <a name="classic-deployment-limitations"></a>Beperkingen voor klassieke implementatie
De opties voor het verplaatsen van resources die zijn geïmplementeerd via het klassieke model verschillen op basis van of het verplaatsen van de resources binnen een abonnement of in een nieuw abonnement.

### <a name="same-subscription"></a>Hetzelfde abonnement
Bij het verplaatsen van resources van een resourcegroep naar een andere resourcegroep binnen hetzelfde abonnement, gelden de volgende beperkingen:

* Virtuele netwerken (klassiek) kunnen niet worden verplaatst.
* Virtuele machines (klassiek) moeten worden verplaatst met de cloudservice.
* Cloudservice kan alleen worden verplaatst, wanneer de verplaatsing alle virtuele machines bevat.
* Slechts één cloudservice kan tegelijk worden verplaatst.
* Slechts één opslagaccount (klassiek) kan tegelijk worden verplaatst.
* Storage-account (klassiek) kan niet worden verplaatst in dezelfde bewerking met een virtuele machine of een cloudservice.

Klassieke om resources te verplaatsen naar een nieuwe resourcegroep binnen hetzelfde abonnement, gebruiken de standaard migratiebewerkingen via de [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), of [REST-API](#use-rest-api). U dezelfde bewerkingen zoals u voor het verplaatsen van Resource Manager-resources.

### <a name="new-subscription"></a>Nieuw abonnement
Bij het verplaatsen van resources in een nieuw abonnement, gelden de volgende beperkingen:

* Alle klassieke resources in het abonnement moeten worden verplaatst in dezelfde bewerking.
* Het doelabonnement mag geen andere klassieke resources bevatten.
* De verplaatsing kan alleen worden aangevraagd via een afzonderlijke REST-API voor klassieke verplaatst. De standaardopdrachten verplaatsen van Resource Manager werken niet bij het klassieke resources verplaatsen naar een nieuw abonnement.

Klassieke om resources te verplaatsen naar een nieuw abonnement, de REST-bewerkingen die specifiek voor klassieke resources zijn te gebruiken. Voor het gebruik van REST, moet u de volgende stappen uitvoeren:

1. Controleer als het bronabonnement deel uitmaken van een verplaatsing abonnementoverschrijdende. Gebruik de volgende bewerking:

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     In de aanvraagtekst zijn onder andere:

  ```json
  {
    "role": "source"
  }
  ```

     De reactie voor de validatiebewerking is in de volgende indeling:

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. Controleer of het doelabonnement in een verplaatsing abonnementoverschrijdende deelnemen kan. Gebruik de volgende bewerking:

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     In de aanvraagtekst zijn onder andere:

  ```json
  {
    "role": "target"
  }
  ```

     De reactie is in dezelfde indeling als de validatie van het abonnement.
3. Verplaats alle klassieke resources uit één abonnement als beide abonnementen gevalideerd worden, een ander abonnement met de volgende bewerking:

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    In de aanvraagtekst zijn onder andere:

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

De bewerking kan enkele minuten uitgevoerd.

## <a name="use-portal"></a>De portal gebruiken
Selecteer de resourcegroep met deze bronnen om resources te verplaatsen, en selecteer vervolgens de **verplaatsen** knop.

![Verplaatsen van resources](./media/resource-group-move-resources/select-move.png)

Selecteer of u de resources naar een nieuwe resourcegroep of een nieuw abonnement verplaatsen wilt.

Selecteer de resources te verplaatsen en de resourcegroep voor de bestemming. Bevestig dat u wilt bijwerken scripts voor deze bronnen, en selecteer **OK**. Als u het pictogram van het abonnement bewerken in de vorige stap hebt geselecteerd, moet u ook het doelabonnement.

![Selecteer bestemming](./media/resource-group-move-resources/select-destination.png)

In **meldingen**, ziet u dat de move-bewerking wordt uitgevoerd.

![verplaatsing status weergeven](./media/resource-group-move-resources/show-status.png)

Wanneer deze is voltooid, wordt u gewaarschuwd van het resultaat.

![resultaat van de verplaatsing weergeven](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a>PowerShell gebruiken
U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `Move-AzureRmResource` opdracht.

Het eerste voorbeeld laat zien hoe één resource verplaatsen naar een nieuwe resourcegroep.

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

Het tweede voorbeeld laat zien hoe meerdere resources verplaatsen naar een nieuwe resourcegroep.

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

Als u wilt verplaatsen naar een nieuw abonnement, een waarde bevatten voor de `DestinationSubscriptionId` parameter.

U wordt gevraagd te bevestigen dat u wilt verplaatsen van de opgegeven resources.

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a>Azure CLI 2.0 gebruiken
U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `az resource move` opdracht. Geef de bron-id's van de resources te verplaatsen. U kunt krijgen resource-id's met de volgende opdracht:

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

Het volgende voorbeeld ziet hoe u een opslagaccount naar een nieuwe resourcegroep. In de `--ids` parameter, Geef een door spaties gescheiden lijst van de resource-id's te verplaatsen.

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

Als u wilt verplaatsen naar een nieuw abonnement, bieden de `--destination-subscription-id` parameter.

## <a name="use-azure-cli-10"></a>Azure CLI 1.0 gebruiken
U kunt bestaande resources verplaatsen naar een andere resourcegroep of abonnement met de `azure resource move` opdracht. Geef de bron-id's van de resources te verplaatsen. U kunt krijgen resource-id's met de volgende opdracht:

```azurecli
azure resource list -g sourceGroup --json
```

Dit retourneert de volgende indeling:

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

Het volgende voorbeeld ziet hoe u een opslagaccount naar een nieuwe resourcegroep. In de `-i` parameter, voorzien in een door komma's gescheiden lijst van de resource-id's te verplaatsen.

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

U wordt gevraagd te bevestigen dat u wilt verplaatsen van de opgegeven resource.

## <a name="use-rest-api"></a>REST API gebruiken
Bestaande om resources te verplaatsen naar een andere resourcegroep of abonnement, uitvoeren:

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

In de aanvraagtekst geeft u de doelresourcegroep en de resources te verplaatsen. Zie voor meer informatie over de REST-verplaatsbewerking [verplaatsen van resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over PowerShell-cmdlets voor het beheren van uw abonnement, [Azure PowerShell gebruiken met Resource Manager](powershell-azure-resource-manager.md).
* Zie voor meer informatie over Azure CLI-opdrachten voor het beheren van uw abonnement, [met de Azure CLI met Resource Manager](xplat-cli-azure-resource-manager.md).
* Zie voor meer informatie over portal functies voor het beheren van uw abonnement, [om resources te beheren met behulp van de Azure-portal](resource-group-portal.md).
* Zie voor meer informatie over het toepassen van een logische organisatie op uw resources, [met labels om uw resources te organiseren](resource-group-using-tags.md).
