---
title: Verwijderen van een Azure-cluster en de bijbehorende bronnen | Microsoft Docs
description: Informatie over hoe u een Service Fabric cluster volledig verwijderen van de resourcegroep met het cluster verwijderen of door de bronnen selectief te verwijderen.
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="87c62-103">Verwijderen van een Service Fabric-cluster op Azure en de resources die wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="87c62-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="87c62-104">Een Service Fabric-cluster is opgebouwd uit veel andere Azure-resources naast de clusterbron zelf.</span><span class="sxs-lookup"><span data-stu-id="87c62-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="87c62-105">Als u een Service Fabric-cluster volledig wilt verwijderen, moet u dus ook alle resources waar het cluster uit bestaat, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="87c62-106">Hebt u twee opties: ofwel de resourcegroep die het cluster verwijderen (die wist de clusterbron en alle andere resources in de resourcegroep) of de clusterbron specifiek verwijderen en de bijbehorende resources (maar geen andere resources in de resourcegroep).</span><span class="sxs-lookup"><span data-stu-id="87c62-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="87c62-107">Verwijderen van de clusterbron **heeft geen** verwijderen van alle andere resources die uw Service Fabric-cluster is samengesteld uit.</span><span class="sxs-lookup"><span data-stu-id="87c62-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="87c62-108">Verwijderen van de hele resourcegroep (RG) die de Service Fabric-cluster in gebruik is</span><span class="sxs-lookup"><span data-stu-id="87c62-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="87c62-109">Dit is de eenvoudigste manier om ervoor te zorgen dat u alle resources die zijn gekoppeld aan het cluster, met inbegrip van de resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="87c62-110">U kunt de resourcegroep met behulp van PowerShell verwijderen of via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="87c62-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="87c62-111">Als uw resourcegroep resources die niet zijn gerelateerd aan de Service fabric-cluster bevat, kunt u specifieke bronnen verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="87c62-112">De resourcegroep met Azure PowerShell verwijderen</span><span class="sxs-lookup"><span data-stu-id="87c62-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="87c62-113">U kunt ook de resourcegroep verwijderen door het uitvoeren van de volgende Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87c62-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="87c62-114">Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="87c62-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="87c62-115">Als u dit nog niet hebt gedaan, volgt u de stappen in [installeren en configureren van Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="87c62-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="87c62-116">Open een PowerShell-venster en voer de volgende PS-cmdlets:</span><span class="sxs-lookup"><span data-stu-id="87c62-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="87c62-117">Wordt u gevraagd om bevestiging als u niet gebruikt de *-Force* optie.</span><span class="sxs-lookup"><span data-stu-id="87c62-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="87c62-118">Op de bevestiging de RG en alle resources daarin verwijderd.</span><span class="sxs-lookup"><span data-stu-id="87c62-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="87c62-119">Verwijderen van een resourcegroep in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="87c62-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="87c62-120">Meld u aan bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87c62-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87c62-121">Ga naar het Service Fabric-cluster dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="87c62-122">Klik op de naam van de resourcegroep op de pagina van de essentials cluster.</span><span class="sxs-lookup"><span data-stu-id="87c62-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="87c62-123">Hiermee wordt de **Resource groep Essentials** pagina.</span><span class="sxs-lookup"><span data-stu-id="87c62-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="87c62-124">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="87c62-124">Click **Delete**.</span></span>
6. <span data-ttu-id="87c62-125">Volg de instructies op deze pagina om het verwijderen van de resourcegroep te voltooien.</span><span class="sxs-lookup"><span data-stu-id="87c62-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Verwijderen van resourcegroep][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="87c62-127">De clusterbron en de resources die wordt gebruikt, maar geen andere resources in de resourcegroep verwijderen</span><span class="sxs-lookup"><span data-stu-id="87c62-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="87c62-128">Als uw resourcegroep alleen bronnen die gerelateerd zijn aan de Service Fabric-cluster dat u wilt verwijderen heeft, is het eenvoudiger om de gehele resourcedatabase-groep te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="87c62-129">Als u de resources één voor één in uw resourcegroep selectief te verwijderen wilt, voert u deze stappen.</span><span class="sxs-lookup"><span data-stu-id="87c62-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="87c62-130">Als u uw cluster met behulp van de portal of via een van de Service Fabric-Resource Manager-sjablonen uit de sjablonengalerie hebt geïmplementeerd, zijn de resources die het cluster gebruikt gelabeld met de volgende twee codes.</span><span class="sxs-lookup"><span data-stu-id="87c62-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="87c62-131">U kunt deze gebruiken om te bepalen welke bronnen die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="87c62-132">***Label #1:*** sleutel = clusternaam, waarde = 'naam van het cluster'</span><span class="sxs-lookup"><span data-stu-id="87c62-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="87c62-133">***Label #2:*** sleutel = resourceName, waarde = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="87c62-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="87c62-134">Verwijderen van specifieke bronnen in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="87c62-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="87c62-135">Meld u aan bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87c62-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87c62-136">Ga naar het Service Fabric-cluster dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87c62-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="87c62-137">Ga naar **alle instellingen** op de blade essentials.</span><span class="sxs-lookup"><span data-stu-id="87c62-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="87c62-138">Klik op **labels** onder **bronbeheer** op de instellingenblade.</span><span class="sxs-lookup"><span data-stu-id="87c62-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="87c62-139">Klik op een van de **labels** in de blade labels voor een lijst van alle resources met dit label.</span><span class="sxs-lookup"><span data-stu-id="87c62-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Resourcelabels][ResourceTags]
6. <span data-ttu-id="87c62-141">Zodra u de lijst met gelabelde resources hebt, klikt u op elk van de resources en verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="87c62-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Resources met tags][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="87c62-143">Verwijderen van de resources met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="87c62-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="87c62-144">U kunt de resources één voor één verwijderen door het uitvoeren van de volgende Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87c62-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="87c62-145">Zorg ervoor dat Azure PowerShell 1.0 of hoger is geïnstalleerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="87c62-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="87c62-146">Als u dit nog niet hebt gedaan, volgt u de stappen in [installeren en configureren van Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="87c62-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="87c62-147">Open een PowerShell-venster en voer de volgende PS-cmdlets:</span><span class="sxs-lookup"><span data-stu-id="87c62-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="87c62-148">Voor elk van de resources wilt u verwijderen, voert u de volgende:</span><span class="sxs-lookup"><span data-stu-id="87c62-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="87c62-149">Als u wilt verwijderen van de cluster-bron, voert u de volgende:</span><span class="sxs-lookup"><span data-stu-id="87c62-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="87c62-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87c62-150">Next steps</span></span>
<span data-ttu-id="87c62-151">Lees het volgende wanneer u ook meer informatie over het upgraden van een cluster en partitionering services:</span><span class="sxs-lookup"><span data-stu-id="87c62-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="87c62-152">Meer informatie over de cluster-upgrades</span><span class="sxs-lookup"><span data-stu-id="87c62-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="87c62-153">Meer informatie over partitioneren stateful services voor maximale schaal</span><span class="sxs-lookup"><span data-stu-id="87c62-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
