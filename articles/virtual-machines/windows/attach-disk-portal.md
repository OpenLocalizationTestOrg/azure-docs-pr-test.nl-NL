---
title: Een niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows - Azure | Microsoft Docs
description: Klik hier voor meer informatie over het nieuwe of bestaande niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows in de Azure portal met het implementatiemodel van Resource Manager.
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
ms.openlocfilehash: c0886302c82641f8cc1a00d3972870d58ba8afb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-an-unmanaged-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="c71f2-103">Hoe u een niet-beheerde gegevensschijf koppelen aan een virtuele machine van Windows in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="c71f2-103">How to attach an unmanaged data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="c71f2-104">In dit artikel leest u hoe nieuwe en bestaande niet-beheerde schijven koppelen aan Windows virtuele machines via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="c71f2-104">This article shows you how to attach both new and existing unmanaged disks to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="c71f2-105">U kunt ook [een gegevensschijf met behulp van PowerShell koppelen](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c71f2-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="c71f2-106">Voordat u dit doet, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="c71f2-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="c71f2-107">De omvang van de virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="c71f2-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="c71f2-108">Zie voor meer informatie [grootten voor virtuele machines](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c71f2-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="c71f2-109">Premium-opslag gebruiken, moet u een virtuele machine DS-serie- of GS-serie.</span><span class="sxs-lookup"><span data-stu-id="c71f2-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="c71f2-110">Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="c71f2-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="c71f2-111">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="c71f2-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="c71f2-112">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71f2-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="c71f2-113">Voor een nieuwe schijf hoeft u niet eerst maken omdat Azure gemaakt wanneer u dit aansluit.</span><span class="sxs-lookup"><span data-stu-id="c71f2-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="c71f2-114">U kunt ook [een gegevensschijf met behulp van Powershell koppelen](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c71f2-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="c71f2-115">De virtuele machine gevonden</span><span class="sxs-lookup"><span data-stu-id="c71f2-115">Find the virtual machine</span></span>
1. <span data-ttu-id="c71f2-116">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c71f2-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c71f2-117">Klik in het menu aan de linkerkant op **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-117">In the menu on the left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="c71f2-118">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="c71f2-118">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="c71f2-119">Klik op de blade virtuele machines **schijven**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-119">In the Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="c71f2-120">Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="c71f2-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="c71f2-121">Optie 1: Koppelen en een nieuwe schijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="c71f2-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="c71f2-122">Op de **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-122">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="c71f2-123">In de **Attach-beheerde schijven** blade, typ een naam voor de schijf in **naam** en selecteer vervolgens **nieuwe (lege schijf)** in **gegevensbrontype**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-123">In the **Attach managed disk** blade, type a name for the disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="c71f2-124">Onder **opslagcontainer**, klikt u op de **Bladeren** knop en blader naar het opslagaccount en container waarin u wilt dat de nieuwe VHD worden opgeslagen en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-124">Under **Storage container**, click the **Browse** button and browse to the storage account and container where you would like the new VHD to be stored and then click **Select**.</span></span> 
  
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="c71f2-126">Wanneer u klaar bent met de instellingen voor de gegevensschijf, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-126">When you are done with the settings for the data disk, click **OK**.</span></span>
4. <span data-ttu-id="c71f2-127">Terug in de **schijven** blade, klikt u op **opslaan** de schijf toevoegen aan de VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="c71f2-127">Back in the **Disks** blade, click **Save** to add the disk to the VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="c71f2-128">Initialiseer de gegevensschijf van een nieuwe</span><span class="sxs-lookup"><span data-stu-id="c71f2-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="c71f2-129">Verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c71f2-129">Connect to the virtual machine.</span></span> <span data-ttu-id="c71f2-130">Zie voor instructies [verbinding maken met en meld u aan een virtuele machine van Azure waarop Windows wordt uitgevoerd bij](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71f2-130">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="c71f2-131">Klik op de **Start** menu binnen de virtuele machine en het type **diskmgmt.msc** en treffers **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-131">Click the **Start** menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="c71f2-132">Hiermee start u de module Schijfbeheer.</span><span class="sxs-lookup"><span data-stu-id="c71f2-132">This starts the Disk Management snap-in.</span></span>
2. <span data-ttu-id="c71f2-133">Schijfbeheer herkent dat u een nieuwe, niet-geïnitialiseerde schijf hebt en de schijf initialiseren-venster.</span><span class="sxs-lookup"><span data-stu-id="c71f2-133">Disk Management recognizes that you have a new, uninitialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="c71f2-134">Zorg ervoor dat de nieuwe schijf is geselecteerd en klik op **OK** voor het initialiseren.</span><span class="sxs-lookup"><span data-stu-id="c71f2-134">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="c71f2-135">De nieuwe schijf wordt nu weergegeven als **niet-toegewezen**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-135">The new disk now appears as **unallocated**.</span></span> <span data-ttu-id="c71f2-136">Klik met de rechtermuisknop op de schijf en selecteer **Nieuw eenvoudig volume**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-136">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="c71f2-137">De **Wizard Nieuw eenvoudig Volume** wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c71f2-137">The **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="c71f2-138">Doorloop de wizard, alle standaardinstellingen, houden wanneer u klaar bent Selecteer **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-138">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="c71f2-139">Sluit de module Schijfbeheer.</span><span class="sxs-lookup"><span data-stu-id="c71f2-139">Close Disk Management.</span></span>
7. <span data-ttu-id="c71f2-140">Krijgt u een pop-upvenster die u de nieuwe schijf formatteren moet voordat u deze kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c71f2-140">You get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="c71f2-141">Klik op **schijf formatteren**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="c71f2-142">In de **nieuwe schijf formatteren** dialoogvenster, Controleer de instellingen en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-142">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="c71f2-143">Krijg een waarschuwing dat de schijven formatteert, worden alle gegevens, klikt u **OK**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-143">You get a warning that formatting the disks erases all of the data, click **OK**.</span></span>
10. <span data-ttu-id="c71f2-144">Wanneer de indeling voltooid is, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-144">When the format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="c71f2-145">Optie 2: Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="c71f2-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="c71f2-146">Op de **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-146">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="c71f2-147">Op de **onbeheerde schijf koppelen** blade in **gegevensbrontype** Selecteer **bestaande blob**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-147">On the **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="c71f2-149">Klik op **Bladeren** om te navigeren naar het opslagaccount en container waarin de bestaande VHD zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c71f2-149">Click **Browse** to navigate to the storage account and container where the existing VHD is located.</span></span> <span data-ttu-id="c71f2-150">Klik op en de VHD en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c71f2-150">Click and the VHD and then click **Select**.</span></span>
4. <span data-ttu-id="c71f2-151">Klik op **OK** in de **onbeheerde schijf koppelen** blade.</span><span class="sxs-lookup"><span data-stu-id="c71f2-151">Click **OK** in the **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="c71f2-152">In de **schijven** blade, klikt u op **opslaan** de schijf toevoegen aan de configuratie voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c71f2-152">In the **Disks** blade, click **Save** to add the disk to the configuration for the VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="c71f2-153">Gebruik TRIM met standard-opslag</span><span class="sxs-lookup"><span data-stu-id="c71f2-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="c71f2-154">Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="c71f2-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="c71f2-155">TRIM worden niet-gebruikte blokken op de schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c71f2-155">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="c71f2-156">Dit kunt besparen op kosten als u grote bestanden maken en deze vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c71f2-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="c71f2-157">U kunt deze opdracht om te controleren van de beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c71f2-157">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="c71f2-158">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="c71f2-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="c71f2-159">Als de opdracht 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c71f2-159">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="c71f2-160">Als deze 1 retourneert, voert u de volgende opdracht voor het vrijmaken van opslagruimte inschakelen:</span><span class="sxs-lookup"><span data-stu-id="c71f2-160">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="c71f2-161">Na het verwijderen van gegevens van de schijf, kunt u ervoor zorgen dat de beperkende leegmaken goed door het uitvoeren van bewerkingen met ' trim ' defragmentatie:</span><span class="sxs-lookup"><span data-stu-id="c71f2-161">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="c71f2-162">U kunt er ook voor zorgen dat het hele volume wordt verkleind door het formatteren van het volume.</span><span class="sxs-lookup"><span data-stu-id="c71f2-162">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c71f2-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c71f2-163">Next steps</span></span>
<span data-ttu-id="c71f2-164">Als u een toepassing gebruikt de D: station voor het opslaan van gegevens, kunt u [wijzigen van de stationsletter van de tijdelijke schijf Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71f2-164">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

