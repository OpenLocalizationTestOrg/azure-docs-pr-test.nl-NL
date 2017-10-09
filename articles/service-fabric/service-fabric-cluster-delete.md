---
title: aaaDelete een Azure-cluster en de bijbehorende bronnen | Microsoft Docs
description: Meer informatie over hoe toocompletely verwijderen, een Service Fabric-cluster beide verwijderen Hallo resourcegroep Hallo-cluster met of door de bronnen selectief te verwijderen.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Verwijderen van een Service Fabric-cluster op Azure en Hallo bronnen die wordt gebruikt
Een Service Fabric-cluster bestaat uit veel andere Azure-resources verder toohello clusterbron zelf. Zodat toocompletely verwijdert een Service Fabric-cluster moet u ook alle resources die wordt gemaakt van Hallo toodelete.
Hebt u twee opties: beide verwijderen Hallo resourcegroep bevindt die Hallo cluster zich in (die wist Hallo clusterbron en alle andere resources in de resourcegroep Hallo) of specifiek Hallo cluster resource verwijderen en de bijbehorende resources (maar geen andere resources in de resourcegroep Hallo).

> [!NOTE]
> Verwijderen van de clusterbron Hallo **heeft geen** alle andere resources die uw Service Fabric-cluster is samengesteld uit Hallo verwijderen.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>Hallo hele resourcegroep verwijderen (RG) die Hallo Service Fabric-cluster in gebruik is
Dit is Hallo gemakkelijkste manier tooensure dat u alle Hallo resources die zijn gekoppeld aan uw cluster, inclusief Hallo resourcegroep verwijderen. U kunt verwijderen Hallo resourcegroep met PowerShell of via hello Azure-portal. Als uw resourcegroep resources die geen gerelateerde tooService fabric-cluster bevat, kunt u specifieke bronnen verwijderen.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Hallo-resourcegroep met Azure PowerShell verwijderen
U kunt ook Hallo resourcegroep verwijderen door het uitvoeren van hello Azure PowerShell-cmdlets te volgen. Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer. Als u dit nog niet hebt gedaan, volgt u Hallo-stappen die worden beschreven in [hoe tooinstall en configureer Azure PowerShell.](/powershell/azure/overview)

Open een PowerShell-venster en Voer Hallo PS-cmdlets te volgen:

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

U krijgt een prompt tooconfirm Hallo verwijdering als u Hallo niet gebruikt *-Force* optie. Op de bevestiging Hallo RG en alle Hallo resources bevat worden verwijderd.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Verwijderen van een resourcegroep in hello Azure-portal
1. Aanmelding toohello [Azure-portal](https://portal.azure.com).
2. Navigeer toohello gewenste toodelete Service Fabric-cluster.
3. Klik op Hallo naam resourcegroep op Hallo cluster essentials pagina.
4. Hiermee wordt Hallo **Resource groep Essentials** pagina.
5. Klik op **Verwijderen**.
6. Hallo instructies op die pagina toocomplete Hallo verwijdering van de resourcegroep Hallo.

![Verwijderen van resourcegroep][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>Hallo-clusterbron en Hallo-resources die wordt gebruikt, maar geen andere resources in de resourcegroep Hallo verwijderen
Als de resourcegroep is alleen de resources die gerelateerd toohello Service Fabric-cluster zijn gewenste toodelete, is het eenvoudiger toodelete Hallo hele resourcegroep. Als u wilt dat tooselectively verwijderen Hallo resources één voor één in de resourcegroep, voert u deze stappen.

Als u uw cluster met behulp van Hallo portal of via een van de Service Fabric Resource Manager-sjablonen Hallo van Hallo sjablonengalerie hebt geïmplementeerd, worden alle Hallo resources Hallo cluster gebruikt gelabeld met Hallo na twee labels. U kunt ze toodecide welke resources u wilt dat toodelete.

***Label #1:*** sleutel = clusternaam, waarde = 'naam van het cluster Hallo'

***Label #2:*** sleutel = resourceName, waarde = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Verwijderen van specifieke bronnen in hello Azure-portal
1. Aanmelding toohello [Azure-portal](https://portal.azure.com).
2. Navigeer toohello gewenste toodelete Service Fabric-cluster.
3. Ga te**alle instellingen** op Hallo essentials blade.
4. Klik op **labels** onder **bronbeheer** op de blade Hallo-instellingen.
5. Klik op een van de Hallo **labels** in Hallo labels blade tooget een lijst met alle Hallo resources met dit label.
   
    ![Resourcelabels][ResourceTags]
6. Zodra u Hallo lijst met gelabelde resources hebt, klikt u op elk van de Hallo resources en verwijder deze.
   
    ![Resources met tags][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Hallo-resources met Azure PowerShell verwijderen
Door het uitvoeren van hello Azure PowerShell-cmdlets te volgen, kunt u Hallo bronnen, één voor één verwijderen. Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer. Als u dit nog niet hebt gedaan, volgt u Hallo-stappen die worden beschreven in [hoe tooinstall en configureer Azure PowerShell.](/powershell/azure/overview)

Open een PowerShell-venster en Voer Hallo PS-cmdlets te volgen:

```powershell
Login-AzureRmAccount
```
Voor elk van de resources Hallo toodelete wilt, voert u de volgende Hallo:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

toodelete hello clusterbron, voert u de volgende Hallo:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>Volgende stappen
Lezen Hallo tooalso na meer over het upgraden van een cluster en partitionering services:

* [Meer informatie over de cluster-upgrades](service-fabric-cluster-upgrade.md)
* [Meer informatie over partitioneren stateful services voor maximale schaal](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
