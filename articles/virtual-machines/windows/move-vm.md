---
title: een virtuele machine van Windows-resource in Azure aaaMove | Microsoft Docs
description: Een tooanother van de virtuele machine van Windows Azure-abonnement of resourcegroep verplaatsen Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="183b6-103">Een tooanother van de virtuele machine van Windows Azure-abonnement of resourcegroep verplaatsen</span><span class="sxs-lookup"><span data-stu-id="183b6-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="183b6-104">In dit artikel leert u hoe u een Windows-VM tussen resourcegroepen of abonnementen toomove.</span><span class="sxs-lookup"><span data-stu-id="183b6-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="183b6-105">Verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine hebt gemaakt in een persoonlijke abonnement en nu wilt toomove deze van het bedrijf tooyour abonnement toocontinue uw werk.</span><span class="sxs-lookup"><span data-stu-id="183b6-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="183b6-106">U kunt beheerde schijven op dit moment niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="183b6-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="183b6-107">Nieuwe resource-id's worden gemaakt als onderdeel van Hallo verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="183b6-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="183b6-108">Als hello VM is verplaatst, moet u tooupdate de hulpprogramma's en scripts toouse Hallo nieuwe resource-id.</span><span class="sxs-lookup"><span data-stu-id="183b6-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="183b6-109">Gebruik Powershell toomove een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="183b6-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="183b6-110">een resourcegroep van de virtuele machine tooanother toomove, moet u ervoor dat u ook Verplaats alle afhankelijke resources Hallo toomake.</span><span class="sxs-lookup"><span data-stu-id="183b6-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="183b6-111">toouse hello verplaatsen AzureRMResource cmdlet, moet u Hallo resourcenaam en Hallo type resource.</span><span class="sxs-lookup"><span data-stu-id="183b6-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="183b6-112">U kunt zowel vanuit Hallo zoeken AzureRMResource cmdlet ophalen.</span><span class="sxs-lookup"><span data-stu-id="183b6-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="183b6-113">toomove een virtuele machine moet toomove meerdere resources.</span><span class="sxs-lookup"><span data-stu-id="183b6-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="183b6-114">We kunnen alleen afzonderlijke variabelen voor elke resource maken en deze vervolgens te vermelden.</span><span class="sxs-lookup"><span data-stu-id="183b6-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="183b6-115">In dit voorbeeld bevat de meest Hallo basic resources voor een virtuele machine, maar u kunt meer behoefte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="183b6-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

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

<span data-ttu-id="183b6-116">toomove Hallo resources toodifferent abonnement, omvatten Hallo **- DestinationSubscriptionId** parameter.</span><span class="sxs-lookup"><span data-stu-id="183b6-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="183b6-117">U wordt gevraagd dat u wilt dat toomove hello tooconfirm opgegeven resources.</span><span class="sxs-lookup"><span data-stu-id="183b6-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="183b6-118">Type **Y** tooconfirm dat u wilt dat toomove Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="183b6-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="183b6-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="183b6-119">Next steps</span></span>
<span data-ttu-id="183b6-120">U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="183b6-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="183b6-121">Zie voor meer informatie [verplaatsen van resources toonew resourcegroep of abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="183b6-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

