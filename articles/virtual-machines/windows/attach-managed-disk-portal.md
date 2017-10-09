---
title: een beheerde gegevens schijf tooa Windows VM - Azure aaaAttach | Microsoft Docs
description: De wijze waarop tooattach nieuwe gegevens schijf tooa beheerd Hallo Windows virtuele machine in Azure portal met behulp van Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="3dda6-103">Hoe een beheerde gegevens tooattach schijf tooa Windows VM in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3dda6-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="3dda6-104">Dit artikel laat zien hoe een nieuwe beheerde gegevens tooattach schijf tooWindows virtuele machines via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3dda6-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="3dda6-105">Voordat u dit doet, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="3dda6-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="3dda6-106">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="3dda6-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="3dda6-107">Zie voor meer informatie [grootten voor virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3dda6-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="3dda6-108">Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.</span><span class="sxs-lookup"><span data-stu-id="3dda6-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="3dda6-109">U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3dda6-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="3dda6-110">Een gegevensschijf toevoegen</span><span class="sxs-lookup"><span data-stu-id="3dda6-110">Add a data disk</span></span>
1. <span data-ttu-id="3dda6-111">Klik in het menu aan de linkerkant Hallo Hallo op **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="3dda6-112">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dda6-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="3dda6-113">Klik op Hallo virtuele machineblade **schijven**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="3dda6-114">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="3dda6-115">Selecteer in de vervolgkeuzelijst voor de nieuwe schijf Hallo Hallo, **maken leeg**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="3dda6-116">In Hallo **-beheerde schijven maken** blade, typ een naam voor Hallo schijf en pas Hallo van andere instellingen zo nodig.</span><span class="sxs-lookup"><span data-stu-id="3dda6-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="3dda6-117">Wanneer u klaar bent, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="3dda6-118">In Hallo **schijven** blade, klik op Opslaan toosave Hallo nieuwe schijf-configuratie voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="3dda6-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="3dda6-119">Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="3dda6-120">Initialiseer de gegevensschijf van een nieuwe</span><span class="sxs-lookup"><span data-stu-id="3dda6-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="3dda6-121">Verbinding maken met toohello VM.</span><span class="sxs-lookup"><span data-stu-id="3dda6-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="3dda6-122">Klik op Hallo startmenu binnen Hallo VM en typ **diskmgmt.msc** en treffers **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="3dda6-123">Hiermee start u Hallo schijf-beheermodule.</span><span class="sxs-lookup"><span data-stu-id="3dda6-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="3dda6-124">Schijfbeheer constateert dat er een nieuwe, niet-geïnitialiseerde schijf en Hallo schijf initialiseren-venster.</span><span class="sxs-lookup"><span data-stu-id="3dda6-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="3dda6-125">Zorg ervoor dat de nieuwe schijf Hallo is geselecteerd en klik op **OK** tooinitialize deze.</span><span class="sxs-lookup"><span data-stu-id="3dda6-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="3dda6-126">Hallo nieuwe schijf wordt nu weergegeven als **niet-toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="3dda6-127">Klik met de rechtermuisknop op Hallo schijf en selecteer **Nieuw eenvoudig volume**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="3dda6-128">Hallo **Wizard Nieuw eenvoudig Volume** wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3dda6-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="3dda6-129">Ga in de wizard hello, alle standaardinstellingen hello, houden wanneer u klaar bent Selecteer **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="3dda6-130">Sluit de module Schijfbeheer.</span><span class="sxs-lookup"><span data-stu-id="3dda6-130">Close Disk Management.</span></span>
7. <span data-ttu-id="3dda6-131">U ontvangt een pop-upvenster die u moet tooformat Hallo nieuwe schijf voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3dda6-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="3dda6-132">Klik op **schijf formatteren**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="3dda6-133">In Hallo **nieuwe schijf formatteren** dialoogvenster, selectievakje Hallo instellingen en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="3dda6-134">U ontvangt een waarschuwing dat Hallo schijven formatteren worden gewist door alle Hallo gegevens, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="3dda6-135">Wanneer het Hallo-indeling is voltooid, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dda6-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="3dda6-136">Gebruik TRIM met standard-opslag</span><span class="sxs-lookup"><span data-stu-id="3dda6-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="3dda6-137">Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3dda6-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="3dda6-138">TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3dda6-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="3dda6-139">Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3dda6-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="3dda6-140">U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3dda6-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="3dda6-141">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="3dda6-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="3dda6-142">Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3dda6-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="3dda6-143">Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:</span><span class="sxs-lookup"><span data-stu-id="3dda6-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="3dda6-144">Na het verwijderen van gegevens van de schijf, kunt u ervoor zorgen dat Hallo TRIM operations leegmaken goed door het uitvoeren van defragmentatiefase met ' trim ':</span><span class="sxs-lookup"><span data-stu-id="3dda6-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="3dda6-145">U kunt er ook voor zorgen Hallo hele volume wordt door het Hallo-volume formatteren bijgesneden.</span><span class="sxs-lookup"><span data-stu-id="3dda6-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dda6-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3dda6-146">Next steps</span></span>
<span data-ttu-id="3dda6-147">Als u een toepassing toouse Hallo D: station toostore gegevens nodig zijn, kunt u [stationsletter op Hallo van Hallo Windows tijdelijke schijf wijzigen](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3dda6-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
