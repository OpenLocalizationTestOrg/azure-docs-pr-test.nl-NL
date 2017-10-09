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
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="00c0b-103">Verwijderen van een Service Fabric-cluster op Azure en Hallo bronnen die wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="00c0b-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="00c0b-104">Een Service Fabric-cluster bestaat uit veel andere Azure-resources verder toohello clusterbron zelf.</span><span class="sxs-lookup"><span data-stu-id="00c0b-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="00c0b-105">Zodat toocompletely verwijdert een Service Fabric-cluster moet u ook alle resources die wordt gemaakt van Hallo toodelete.</span><span class="sxs-lookup"><span data-stu-id="00c0b-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="00c0b-106">Hebt u twee opties: beide verwijderen Hallo resourcegroep bevindt die Hallo cluster zich in (die wist Hallo clusterbron en alle andere resources in de resourcegroep Hallo) of specifiek Hallo cluster resource verwijderen en de bijbehorende resources (maar geen andere resources in de resourcegroep Hallo).</span><span class="sxs-lookup"><span data-stu-id="00c0b-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="00c0b-107">Verwijderen van de clusterbron Hallo **heeft geen** alle andere resources die uw Service Fabric-cluster is samengesteld uit Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="00c0b-108">Hallo hele resourcegroep verwijderen (RG) die Hallo Service Fabric-cluster in gebruik is</span><span class="sxs-lookup"><span data-stu-id="00c0b-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="00c0b-109">Dit is Hallo gemakkelijkste manier tooensure dat u alle Hallo resources die zijn gekoppeld aan uw cluster, inclusief Hallo resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="00c0b-110">U kunt verwijderen Hallo resourcegroep met PowerShell of via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="00c0b-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="00c0b-111">Als uw resourcegroep resources die geen gerelateerde tooService fabric-cluster bevat, kunt u specifieke bronnen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="00c0b-112">Hallo-resourcegroep met Azure PowerShell verwijderen</span><span class="sxs-lookup"><span data-stu-id="00c0b-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="00c0b-113">U kunt ook Hallo resourcegroep verwijderen door het uitvoeren van hello Azure PowerShell-cmdlets te volgen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="00c0b-114">Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="00c0b-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="00c0b-115">Als u dit nog niet hebt gedaan, volgt u Hallo-stappen die worden beschreven in [hoe tooinstall en configureer Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="00c0b-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="00c0b-116">Open een PowerShell-venster en Voer Hallo PS-cmdlets te volgen:</span><span class="sxs-lookup"><span data-stu-id="00c0b-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="00c0b-117">U krijgt een prompt tooconfirm Hallo verwijdering als u Hallo niet gebruikt *-Force* optie.</span><span class="sxs-lookup"><span data-stu-id="00c0b-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="00c0b-118">Op de bevestiging Hallo RG en alle Hallo resources bevat worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="00c0b-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="00c0b-119">Verwijderen van een resourcegroep in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="00c0b-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="00c0b-120">Aanmelding toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00c0b-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00c0b-121">Navigeer toohello gewenste toodelete Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="00c0b-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="00c0b-122">Klik op Hallo naam resourcegroep op Hallo cluster essentials pagina.</span><span class="sxs-lookup"><span data-stu-id="00c0b-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="00c0b-123">Hiermee wordt Hallo **Resource groep Essentials** pagina.</span><span class="sxs-lookup"><span data-stu-id="00c0b-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="00c0b-124">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="00c0b-124">Click **Delete**.</span></span>
6. <span data-ttu-id="00c0b-125">Hallo instructies op die pagina toocomplete Hallo verwijdering van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="00c0b-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Verwijderen van resourcegroep][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="00c0b-127">Hallo-clusterbron en Hallo-resources die wordt gebruikt, maar geen andere resources in de resourcegroep Hallo verwijderen</span><span class="sxs-lookup"><span data-stu-id="00c0b-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="00c0b-128">Als de resourcegroep is alleen de resources die gerelateerd toohello Service Fabric-cluster zijn gewenste toodelete, is het eenvoudiger toodelete Hallo hele resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="00c0b-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="00c0b-129">Als u wilt dat tooselectively verwijderen Hallo resources één voor één in de resourcegroep, voert u deze stappen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="00c0b-130">Als u uw cluster met behulp van Hallo portal of via een van de Service Fabric Resource Manager-sjablonen Hallo van Hallo sjablonengalerie hebt geïmplementeerd, worden alle Hallo resources Hallo cluster gebruikt gelabeld met Hallo na twee labels.</span><span class="sxs-lookup"><span data-stu-id="00c0b-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="00c0b-131">U kunt ze toodecide welke resources u wilt dat toodelete.</span><span class="sxs-lookup"><span data-stu-id="00c0b-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="00c0b-132">***Label #1:*** sleutel = clusternaam, waarde = 'naam van het cluster Hallo'</span><span class="sxs-lookup"><span data-stu-id="00c0b-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="00c0b-133">***Label #2:*** sleutel = resourceName, waarde = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="00c0b-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="00c0b-134">Verwijderen van specifieke bronnen in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="00c0b-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="00c0b-135">Aanmelding toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="00c0b-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="00c0b-136">Navigeer toohello gewenste toodelete Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="00c0b-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="00c0b-137">Ga te**alle instellingen** op Hallo essentials blade.</span><span class="sxs-lookup"><span data-stu-id="00c0b-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="00c0b-138">Klik op **labels** onder **bronbeheer** op de blade Hallo-instellingen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="00c0b-139">Klik op een van de Hallo **labels** in Hallo labels blade tooget een lijst met alle Hallo resources met dit label.</span><span class="sxs-lookup"><span data-stu-id="00c0b-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Resourcelabels][ResourceTags]
6. <span data-ttu-id="00c0b-141">Zodra u Hallo lijst met gelabelde resources hebt, klikt u op elk van de Hallo resources en verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="00c0b-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Resources met tags][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="00c0b-143">Hallo-resources met Azure PowerShell verwijderen</span><span class="sxs-lookup"><span data-stu-id="00c0b-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="00c0b-144">Door het uitvoeren van hello Azure PowerShell-cmdlets te volgen, kunt u Hallo bronnen, één voor één verwijderen.</span><span class="sxs-lookup"><span data-stu-id="00c0b-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="00c0b-145">Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="00c0b-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="00c0b-146">Als u dit nog niet hebt gedaan, volgt u Hallo-stappen die worden beschreven in [hoe tooinstall en configureer Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="00c0b-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="00c0b-147">Open een PowerShell-venster en Voer Hallo PS-cmdlets te volgen:</span><span class="sxs-lookup"><span data-stu-id="00c0b-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="00c0b-148">Voor elk van de resources Hallo toodelete wilt, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="00c0b-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="00c0b-149">toodelete hello clusterbron, voert u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="00c0b-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="00c0b-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="00c0b-150">Next steps</span></span>
<span data-ttu-id="00c0b-151">Lezen Hallo tooalso na meer over het upgraden van een cluster en partitionering services:</span><span class="sxs-lookup"><span data-stu-id="00c0b-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="00c0b-152">Meer informatie over de cluster-upgrades</span><span class="sxs-lookup"><span data-stu-id="00c0b-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="00c0b-153">Meer informatie over partitioneren stateful services voor maximale schaal</span><span class="sxs-lookup"><span data-stu-id="00c0b-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
