---
title: Verplaatsen van een virtuele Linux-machine in Azure | Microsoft Docs
description: Linux-VM verplaatsen naar een andere Azure-abonnement of de resource-groep in het Resource Manager-implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4695a9c934f97f2b2d448c4990e7ad5533e38e9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="cfb7b-103">Linux-VM verplaatsen naar een ander abonnement of de resource-groep</span><span class="sxs-lookup"><span data-stu-id="cfb7b-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="cfb7b-104">In dit artikel leert u hoe u een Linux-VM verplaatsen tussen resourcegroepen of abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="cfb7b-105">Een virtuele machine verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine in een persoonlijke abonnement hebt gemaakt en wilt verplaatsen naar een abonnement van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="cfb7b-106">U kunt beheerde schijven op dit moment niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="cfb7b-107">Nieuwe resource-id's worden gemaakt als onderdeel van de verplaatsing.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="cfb7b-108">Nadat de virtuele machine is verplaatst, moet u de hulpprogramma's en scripts die de nieuwe resource-ID bijwerken.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="cfb7b-109">De Azure CLI gebruiken om te verplaatsen van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="cfb7b-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="cfb7b-110">Als u wilt een virtuele machine is verplaatst, moet u de virtuele machine en de ondersteunende resources verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="cfb7b-111">Gebruik de **azure-groep weergeven** opdracht om een lijst van alle resources in een resourcegroep en de id's.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="cfb7b-112">Het nuttig om de uitvoer van deze opdracht doorsluizen naar een bestand, zodat u kunt kopiëren en plakken van de id's in latere opdrachten.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="cfb7b-113">U kunt een virtuele machine en de bijbehorende resources verplaatsen naar een andere resourcegroep met de **azure-resource verplaatsen** CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="cfb7b-114">Het volgende voorbeeld laat zien hoe verplaatsen van een virtuele machine en de meest voorkomende bronnen die is vereist.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="cfb7b-115">We gebruiken de **-i** parameter en geeft u een door komma's gescheiden lijst (zonder spaties) met id's voor de resources te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="cfb7b-116">Als u wilt dat de virtuele machine en de bijbehorende resources verplaatsen naar een ander abonnement, voegt u de **--bestemming subscriptionId &#60; destinationSubscriptionID &#62;** parameter om het doelabonnement.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="cfb7b-117">Als u vanaf de opdrachtprompt op een Windows-computer werkt, moet u toevoegen een  **$**  voor de namen van variabelen wanneer u ze declareren.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="cfb7b-118">Dit is niet nodig in Linux.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="cfb7b-119">U wordt gevraagd te bevestigen dat u wilt verplaatsen van de opgegeven resource.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="cfb7b-120">Type **Y** om te bevestigen dat u wilt verplaatsen van de resources.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="cfb7b-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cfb7b-121">Next steps</span></span>
<span data-ttu-id="cfb7b-122">U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cfb7b-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="cfb7b-123">Zie voor meer informatie [Resources verplaatsen naar een nieuwe resourcegroep of een nieuw abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cfb7b-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

