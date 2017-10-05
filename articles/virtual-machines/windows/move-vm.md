---
title: Verplaatsen van een virtuele machine van Windows-resource in Azure | Microsoft Docs
description: Een Windows-VM verplaatsen naar een andere Azure-abonnement of de resource-groep in het Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 1db25a5d9ff5cb6aa2787a0cafa40cfb010e3b06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-windows-vm-to-another-azure-subscription-or-resource-group"></a><span data-ttu-id="721d7-103">Een Windows VM verplaatsen naar een andere Azure-abonnement of resourcegroep groep</span><span class="sxs-lookup"><span data-stu-id="721d7-103">Move a Windows VM to another Azure subscription or resource group</span></span>
<span data-ttu-id="721d7-104">Dit artikel begeleidt u bij het verplaatsen van een virtuele machine van Windows tussen resourcegroepen of abonnementen.</span><span class="sxs-lookup"><span data-stu-id="721d7-104">This article walks you through how to move a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="721d7-105">Verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine hebt gemaakt in een persoonlijke abonnement en wilt verplaatsen naar een abonnement van uw bedrijf om na te gaan met uw werk.</span><span class="sxs-lookup"><span data-stu-id="721d7-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want to move it to your company's subscription to continue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="721d7-106">U kunt beheerde schijven op dit moment niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="721d7-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="721d7-107">Nieuwe resource-id's worden gemaakt als onderdeel van de verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="721d7-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="721d7-108">Nadat de virtuele machine is verplaatst, moet u de hulpprogramma's en scripts die de nieuwe resource-ID bijwerken.</span><span class="sxs-lookup"><span data-stu-id="721d7-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-to-move-a-vm"></a><span data-ttu-id="721d7-109">Powershell gebruiken voor het verplaatsen van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="721d7-109">Use Powershell to move a VM</span></span>
<span data-ttu-id="721d7-110">Als een virtuele machine naar een andere resourcegroep verplaatsen, moet u ervoor zorgen dat u ook alle afhankelijke resources verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="721d7-110">To move a virtual machine to another resource group, you need to make sure that you also move all of the dependent resources.</span></span> <span data-ttu-id="721d7-111">Voor het gebruik van de cmdlet Move-AzureRMResource, moet u de naam van de bron en het type resource.</span><span class="sxs-lookup"><span data-stu-id="721d7-111">To use the Move-AzureRMResource cmdlet, you need the resource name and the type of resource.</span></span> <span data-ttu-id="721d7-112">U kunt beide van de cmdlet zoeken AzureRMResource ophalen.</span><span class="sxs-lookup"><span data-stu-id="721d7-112">You can get both from the Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="721d7-113">Voor het verplaatsen van een virtuele machine moet worden verplaatst van meerdere resources.</span><span class="sxs-lookup"><span data-stu-id="721d7-113">To move a VM we need to move multiple resources.</span></span> <span data-ttu-id="721d7-114">We kunnen alleen afzonderlijke variabelen voor elke resource maken en deze vervolgens te vermelden.</span><span class="sxs-lookup"><span data-stu-id="721d7-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="721d7-115">In dit voorbeeld bevat het merendeel van de algemene resources voor een virtuele machine, maar u kunt meer behoefte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="721d7-115">This example includes most of the basic resources for a VM, but you can add more as needed.</span></span>

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

<span data-ttu-id="721d7-116">De om resources te verplaatsen naar een ander abonnement, omvatten de **- DestinationSubscriptionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="721d7-116">To move the resources to different subscription, include the **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="721d7-117">U wordt gevraagd om te bevestigen dat u wilt verplaatsen van de opgegeven resources.</span><span class="sxs-lookup"><span data-stu-id="721d7-117">You will be asked to confirm that you want to move the specified resources.</span></span> <span data-ttu-id="721d7-118">Type **Y** om te bevestigen dat u wilt verplaatsen van de resources.</span><span class="sxs-lookup"><span data-stu-id="721d7-118">Type **Y** to confirm that you want to move the resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="721d7-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="721d7-119">Next steps</span></span>
<span data-ttu-id="721d7-120">U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="721d7-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="721d7-121">Zie voor meer informatie [Resources verplaatsen naar een nieuwe resourcegroep of een nieuw abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="721d7-121">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

