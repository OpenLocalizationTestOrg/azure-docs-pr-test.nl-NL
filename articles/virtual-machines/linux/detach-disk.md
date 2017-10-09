---
title: een gegevensschijf van een Linux-VM - Azure aaaDetach | Microsoft Docs
description: Meer informatie over toodetach een gegevensschijf van een virtuele machine in Azure met behulp van de CLI 2.0 of hello Azure-portal.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="388b0-103">Hoe toodetach een schijf van een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="388b0-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="388b0-104">Wanneer u een gegevensschijf die is aangesloten tooa virtuele machine niet meer nodig hebt, kunt u deze eenvoudig loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="388b0-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="388b0-105">Deze taak verwijdert Hallo schijf uit de Hallo virtuele machine, maar niet verwijderd uit de opslag.</span><span class="sxs-lookup"><span data-stu-id="388b0-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="388b0-106">Als u een schijf die wordt niet automatisch verwijderd loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="388b0-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="388b0-107">Als u tooPremium opslag hebt geabonneerd, blijft u tooincur opslagkosten voor Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="388b0-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="388b0-108">Voor meer informatie raadpleegt u te[prijzen en facturering wanneer u Premium-opslag](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="388b0-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="388b0-109">Als u toouse Hallo bestaande gegevens op Hallo schijf opnieuw wilt, u kunt opnieuw het toohello dezelfde virtuele machine of een andere naam.</span><span class="sxs-lookup"><span data-stu-id="388b0-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="388b0-110">Een gegevensschijf met CLI 2.0 loskoppelen</span><span class="sxs-lookup"><span data-stu-id="388b0-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="388b0-111">Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="388b0-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="388b0-112">Een gegevensschijf met Hallo portal loskoppelen</span><span class="sxs-lookup"><span data-stu-id="388b0-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="388b0-113">Selecteer in de portal hub hello, **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="388b0-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="388b0-114">Selecteer Hallo virtuele machine met Hallo gegevensschijf toodetach en klik op **stoppen** toodeallocate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="388b0-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="388b0-115">Selecteer in de blade van de virtuele machine hello, **schijven**.</span><span class="sxs-lookup"><span data-stu-id="388b0-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="388b0-116">Hallo boven aan het Hallo **schijven** blade Selecteer **bewerken**.</span><span class="sxs-lookup"><span data-stu-id="388b0-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="388b0-117">In Hallo **schijven** blade toohello uiterst rechts in Hallo gegevensschijf dat u toodetach wilt, klikt u op Hallo ![Detach knopafbeelding](./media/detach-disk/detach.png) knop loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="388b0-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="388b0-118">Nadat het Hallo-schijf is verwijderd, klikt u op opslaan op Hallo Hallo blade bovenaan.</span><span class="sxs-lookup"><span data-stu-id="388b0-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="388b0-119">In de blade van de virtuele machine hello, klikt u op **overzicht** en klik vervolgens op Hallo **Start** knop bovenaan Hallo Hallo blade toorestart Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="388b0-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="388b0-120">Hallo schijf blijft in de opslag, maar is niet langer gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="388b0-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="388b0-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="388b0-121">Next steps</span></span>
<span data-ttu-id="388b0-122">Als u tooreuse Hallo gegevensschijf wilt, kunt u zojuist hebt [koppelt u dit tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="388b0-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

