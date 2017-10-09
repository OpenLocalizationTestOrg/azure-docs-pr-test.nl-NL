---
title: een niet-beheerde gegevens schijf tooa Windows VM - Azure aaaAttach | Microsoft Docs
description: Hoe tooattach nieuwe of bestaande niet-beheerde gegevens schijf tooa virtuele Windows-machine in Azure portal met behulp van Hallo Hallo Resource Manager-implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="5d110-103">Hoe gegevens in een niet-beheerde tooattach schijf tooa Windows VM in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5d110-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="5d110-104">Dit artikel ziet u hoe tooattach zowel nieuwe als bestaande zonder begeleiding schijven tooWindows virtuele machines via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5d110-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="5d110-105">U kunt ook [een gegevensschijf met behulp van PowerShell koppelen](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5d110-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="5d110-106">Voordat u dit doet, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="5d110-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="5d110-107">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="5d110-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5d110-108">Zie voor meer informatie [grootten voor virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5d110-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="5d110-109">Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie.</span><span class="sxs-lookup"><span data-stu-id="5d110-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5d110-110">Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="5d110-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="5d110-111">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="5d110-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5d110-112">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d110-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5d110-113">Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.</span><span class="sxs-lookup"><span data-stu-id="5d110-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="5d110-114">U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5d110-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="5d110-115">Hallo virtuele machine gevonden</span><span class="sxs-lookup"><span data-stu-id="5d110-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="5d110-116">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5d110-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5d110-117">Klik in het menu aan de linkerkant Hallo Hallo op **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="5d110-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="5d110-118">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d110-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="5d110-119">Klik op Hallo virtuele machines blade **schijven**.</span><span class="sxs-lookup"><span data-stu-id="5d110-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="5d110-120">Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="5d110-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="5d110-121">Optie 1: Koppelen en een nieuwe schijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="5d110-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="5d110-122">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5d110-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5d110-123">In Hallo **Attach-beheerde schijven** blade een naam voor de schijf Hallo in **naam** en selecteer vervolgens **nieuwe (lege schijf)** in **gegevensbrontype**.</span><span class="sxs-lookup"><span data-stu-id="5d110-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="5d110-124">Onder **opslagcontainer**, klikt u op Hallo **Bladeren** knop en blader toohello opslagaccount en container waar u Hallo nieuwe VHD toobe opgeslagen, zoals en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="5d110-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="5d110-126">Wanneer u klaar bent met instellingen voor de gegevensschijf Hallo Hallo, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d110-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="5d110-127">Terug in Hallo **schijven** blade, klikt u op **opslaan** tooadd Hallo schijf toohello VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="5d110-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="5d110-128">Initialiseer de gegevensschijf van een nieuwe</span><span class="sxs-lookup"><span data-stu-id="5d110-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="5d110-129">Verbinding maken met toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5d110-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="5d110-130">Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d110-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="5d110-131">Klik op Hallo **Start** menu binnen Hallo VM en het type **diskmgmt.msc** en treffers **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5d110-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="5d110-132">Hiermee start u Hallo schijf-beheermodule.</span><span class="sxs-lookup"><span data-stu-id="5d110-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="5d110-133">Schijfbeheer herkent dat u een nieuwe, niet-geïnitialiseerde schijf hebt en Hallo schijf initialiseren-venster.</span><span class="sxs-lookup"><span data-stu-id="5d110-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="5d110-134">Zorg ervoor dat de nieuwe schijf Hallo is geselecteerd en klik op **OK** tooinitialize deze.</span><span class="sxs-lookup"><span data-stu-id="5d110-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="5d110-135">Hallo nieuwe schijf wordt nu weergegeven als **niet-toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="5d110-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="5d110-136">Klik met de rechtermuisknop op Hallo schijf en selecteer **Nieuw eenvoudig volume**.</span><span class="sxs-lookup"><span data-stu-id="5d110-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="5d110-137">Hallo **Wizard Nieuw eenvoudig Volume** wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="5d110-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="5d110-138">Ga in de wizard hello, alle standaardinstellingen hello, houden wanneer u klaar bent Selecteer **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5d110-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="5d110-139">Sluit de module Schijfbeheer.</span><span class="sxs-lookup"><span data-stu-id="5d110-139">Close Disk Management.</span></span>
7. <span data-ttu-id="5d110-140">U krijgt een pop-upvenster dat u moet tooformat Hallo nieuwe schijf voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d110-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="5d110-141">Klik op **schijf formatteren**.</span><span class="sxs-lookup"><span data-stu-id="5d110-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="5d110-142">In Hallo **nieuwe schijf formatteren** dialoogvenster, selectievakje Hallo instellingen en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="5d110-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="5d110-143">Krijg een waarschuwing dat Hallo schijven formatteert, worden alle gegevens hello, klikt u **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d110-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="5d110-144">Wanneer het Hallo-indeling is voltooid, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d110-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="5d110-145">Optie 2: Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="5d110-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="5d110-146">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5d110-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5d110-147">Op Hallo **onbeheerde schijf koppelen** blade in **gegevensbrontype** Selecteer **bestaande blob**.</span><span class="sxs-lookup"><span data-stu-id="5d110-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="5d110-149">Klik op **Bladeren** toonavigate toohello opslagaccount en container waar hello bestaande VHD zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="5d110-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="5d110-150">Klik op en Hallo VHD en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="5d110-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="5d110-151">Klik op **OK** in Hallo **onbeheerde schijf koppelen** blade.</span><span class="sxs-lookup"><span data-stu-id="5d110-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="5d110-152">In Hallo **schijven** blade, klikt u op **opslaan** tooadd hello toohello schijfconfiguratie voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="5d110-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="5d110-153">Gebruik TRIM met standard-opslag</span><span class="sxs-lookup"><span data-stu-id="5d110-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="5d110-154">Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5d110-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="5d110-155">TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5d110-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="5d110-156">Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5d110-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="5d110-157">U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5d110-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="5d110-158">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="5d110-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="5d110-159">Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5d110-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="5d110-160">Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:</span><span class="sxs-lookup"><span data-stu-id="5d110-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="5d110-161">Na het verwijderen van gegevens van de schijf, kunt u ervoor zorgen dat Hallo TRIM operations leegmaken goed door het uitvoeren van defragmentatiefase met ' trim ':</span><span class="sxs-lookup"><span data-stu-id="5d110-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="5d110-162">U kunt er ook voor zorgen Hallo hele volume wordt door het Hallo-volume formatteren bijgesneden.</span><span class="sxs-lookup"><span data-stu-id="5d110-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5d110-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d110-163">Next steps</span></span>
<span data-ttu-id="5d110-164">Als u een toepassing toouse Hallo D: station toostore gegevens nodig zijn, kunt u [stationsletter op Hallo van Hallo Windows tijdelijke schijf wijzigen](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d110-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

