---
title: een beheerde Azure Disk voor Back up aaaCopy | Microsoft Docs
description: Meer informatie over hoe toocreate een kopie van een Azure-schijf beheerd toouse voor reserve of probleemoplossing schijf uitgeeft.
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="c4e41-103">Maak een kopie van een VHD die is opgeslagen als een beheerde Azure-schijf met behulp van momentopnamen beheerd</span><span class="sxs-lookup"><span data-stu-id="c4e41-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="c4e41-104">Een momentopname van een beheerde-schijf voor back-up of een schijf beheerd vanuit Hallo momentopname maken en deze te koppelen tooa test virtuele machine tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="c4e41-104">Take a snapshot of a Managed disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="c4e41-105">Een momentopname van een beheerd is een volledige point-in-time-kopie van een schijf VM beheerd.</span><span class="sxs-lookup"><span data-stu-id="c4e41-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="c4e41-106">Deze maakt een alleen-lezen kopie van uw VHD en standaard opgeslagen als een standaard beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="c4e41-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> 

<span data-ttu-id="c4e41-107">Zie voor meer informatie over prijzen [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="c4e41-107">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> <!--Add link tootopic or blog post that explains managed disks. -->

<span data-ttu-id="c4e41-108">Beide hello Azure portal of hello Azure CLI 2.0 tootake een momentopname van Hallo beheerd schijf gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4e41-108">Use either hello Azure portal or hello Azure CLI 2.0 tootake a snapshot of hello Managed Disk.</span></span>

## <a name="use-azure-cli-20-tootake-a-snapshot"></a><span data-ttu-id="c4e41-109">Azure CLI 2.0 tootake een momentopname gebruiken</span><span class="sxs-lookup"><span data-stu-id="c4e41-109">Use Azure CLI 2.0 tootake a snapshot</span></span>

> [!NOTE] 
> <span data-ttu-id="c4e41-110">Hallo moet volgende voorbeeld hello Azure CLI 2.0 geïnstalleerd en geregistreerd in uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c4e41-110">hello following example requires hello Azure CLI 2.0 installed and logged into your Azure account.</span></span>

<span data-ttu-id="c4e41-111">Hallo volgende stappen laten zien hoe tooobtain en maak een momentopname van een beheerde OS schijf met Hallo `az snapshot create` opdracht Hello `--source-disk` parameter.</span><span class="sxs-lookup"><span data-stu-id="c4e41-111">hello following steps show how tooobtain and take a snapshot of a managed OS disk using hello `az snapshot create` command with hello `--source-disk` parameter.</span></span> <span data-ttu-id="c4e41-112">Hallo volgende voorbeeld wordt ervan uitgegaan dat er een virtuele machine aangeroepen `myVM` gemaakt met een beheerde besturingssysteemschijf in Hallo `myResourceGroup` resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c4e41-112">hello following example assumes that there is a VM called `myVM` created with a managed OS disk in hello `myResourceGroup` resource group.</span></span>

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

<span data-ttu-id="c4e41-113">Hallo-uitvoer ziet er ongeveer als:</span><span class="sxs-lookup"><span data-stu-id="c4e41-113">hello output should look something like:</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="c4e41-114">Azure portal tootake een momentopname gebruiken</span><span class="sxs-lookup"><span data-stu-id="c4e41-114">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="c4e41-115">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4e41-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4e41-116">Beginnen in de linkerbovenhoek hello, klikt u op **nieuw** en zoek naar **momentopname**.</span><span class="sxs-lookup"><span data-stu-id="c4e41-116">Starting in hello upper-left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="c4e41-117">Klik op Hallo momentopname blade **maken**.</span><span class="sxs-lookup"><span data-stu-id="c4e41-117">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="c4e41-118">Voer een **naam** voor Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="c4e41-118">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="c4e41-119">Selecteer een bestaande [resourcegroep](../../azure-resource-manager/resource-group-overview.md#resource-groups) of Hallo typenaam voor een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c4e41-119">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="c4e41-120">Selecteer een Azure-datacenter locatie.</span><span class="sxs-lookup"><span data-stu-id="c4e41-120">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="c4e41-121">Voor **bronschijf**, selecteer Hallo toosnapshot schijf beheerd.</span><span class="sxs-lookup"><span data-stu-id="c4e41-121">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="c4e41-122">Selecteer Hallo **accounttype** toouse toostore Hallo momentopname.</span><span class="sxs-lookup"><span data-stu-id="c4e41-122">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="c4e41-123">Het is raadzaam **Standard_LRS** tenzij u deze opgeslagen op een hoog presterende schijf nodig.</span><span class="sxs-lookup"><span data-stu-id="c4e41-123">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="c4e41-124">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4e41-124">Click **Create**.</span></span>

<span data-ttu-id="c4e41-125">Als u toouse Hallo momentopname toocreate van plan een schijf beheerd bent en koppelt u dit een virtuele machine die toobe hoge prestaties behoeften, gebruikt u Hallo parameter `--sku Premium_LRS` Hello `az snapshot create` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c4e41-125">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `--sku Premium_LRS` with hello `az snapshot create` command.</span></span> <span data-ttu-id="c4e41-126">Hiermee maakt u Hallo momentopname zodanig dat deze wordt opgeslagen als een schijf Premium beheerd.</span><span class="sxs-lookup"><span data-stu-id="c4e41-126">This creates hello snapshot so that it is stored as a Premium Managed Disk.</span></span> <span data-ttu-id="c4e41-127">Premium-schijven beheerd sneller omdat ze SSD-schijven (SSD's zijn), maar duurder dan standaardschijven (HDD's).</span><span class="sxs-lookup"><span data-stu-id="c4e41-127">Premium Managed Disks perform better because they are solid-state drives (SSDs), but cost more than Standard disks (HDDs).</span></span>


