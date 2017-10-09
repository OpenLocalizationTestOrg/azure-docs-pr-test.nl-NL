---
title: aaaMove een Linux VM in Azure | Microsoft Docs
description: Verplaatsen van een Linux-VM tooanother Azure-abonnement of resourcegroep in Hallo Resource Manager-implementatiemodel.
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
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="71d8a-103">Een groep Linux VM tooanother abonnement of resourcegroep verplaatsen</span><span class="sxs-lookup"><span data-stu-id="71d8a-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="71d8a-104">In dit artikel leert u hoe u een Linux-VM tussen resourcegroepen of abonnementen toomove.</span><span class="sxs-lookup"><span data-stu-id="71d8a-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="71d8a-105">Een virtuele machine verplaatsen tussen abonnementen kan handig zijn als u een virtuele machine in een persoonlijke abonnement hebt gemaakt en nu wilt toomove het tooyour bedrijfsabonnement.</span><span class="sxs-lookup"><span data-stu-id="71d8a-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="71d8a-106">U kunt beheerde schijven op dit moment niet verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="71d8a-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="71d8a-107">Nieuwe resource-id's worden gemaakt als onderdeel van Hallo verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="71d8a-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="71d8a-108">Als hello VM is verplaatst, moet u tooupdate de hulpprogramma's en scripts toouse Hallo nieuwe resource-id.</span><span class="sxs-lookup"><span data-stu-id="71d8a-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="71d8a-109">Hello Azure CLI toomove een virtuele machine gebruiken</span><span class="sxs-lookup"><span data-stu-id="71d8a-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="71d8a-110">toosuccessfully een virtuele machine verplaatsen, moet u toomove Hallo VM en de bijbehorende ondersteunende bronnen.</span><span class="sxs-lookup"><span data-stu-id="71d8a-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="71d8a-111">Gebruik Hallo **azure-groep weergeven** opdracht toolist alle Hallo resources in een resourcegroep en de id's.</span><span class="sxs-lookup"><span data-stu-id="71d8a-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="71d8a-112">Het helpt toopipe Hallo uitvoer van deze opdracht tooa-bestand zodat u kunt kopiëren en Hallo id's in latere opdrachten plakken.</span><span class="sxs-lookup"><span data-stu-id="71d8a-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="71d8a-113">toomove een virtuele machine en de resourcegroep resources tooanother gebruiken Hallo **azure-resource verplaatsen** CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="71d8a-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="71d8a-114">Hallo volgende voorbeeld ziet u hoe toomove een virtuele machine en de meest voorkomende bronnen Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="71d8a-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="71d8a-115">We gebruiken Hallo **-i** parameter en geeft u een door komma's gescheiden lijst (zonder spaties) met id's voor Hallo resources toomove.</span><span class="sxs-lookup"><span data-stu-id="71d8a-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="71d8a-116">Als u wilt dat toomove Hallo virtuele machine en bijbehorende resources tooa ander abonnement, het toevoegen van Hallo **--bestemming subscriptionId &#60; destinationSubscriptionID &#62;** parameter toospecify Hallo doelabonnement.</span><span class="sxs-lookup"><span data-stu-id="71d8a-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="71d8a-117">Als u op Hallo opdrachtprompt op een Windows-computer werkt, moet u tooadd een  **$**  voor variabelenamen Hallo wanneer u ze declareren.</span><span class="sxs-lookup"><span data-stu-id="71d8a-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="71d8a-118">Dit is niet nodig in Linux.</span><span class="sxs-lookup"><span data-stu-id="71d8a-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="71d8a-119">U wordt gevraagd dat u wilt dat toomove hello tooconfirm van de opgegeven bron.</span><span class="sxs-lookup"><span data-stu-id="71d8a-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="71d8a-120">Type **Y** tooconfirm dat u wilt dat toomove Hallo resources.</span><span class="sxs-lookup"><span data-stu-id="71d8a-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="71d8a-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71d8a-121">Next steps</span></span>
<span data-ttu-id="71d8a-122">U kunt verschillende soorten resources verplaatsen tussen resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="71d8a-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="71d8a-123">Zie voor meer informatie [verplaatsen van resources toonew resourcegroep of abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="71d8a-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

