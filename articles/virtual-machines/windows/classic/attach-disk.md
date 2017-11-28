---
title: een schijf tooa aaaAttach klassieke virtuele machine in Azure | Microsoft Docs
description: Een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo koppelen en het initialiseren.
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="e4ad4-103">Een data schijf tooa Windows virtuele machine gemaakt met het klassieke implementatiemodel Hallo koppelen</span><span class="sxs-lookup"><span data-stu-id="e4ad4-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="e4ad4-104">Dit artikel laat zien hoe tooattach nieuwe en bestaande schijven gemaakt met de Hallo Classic deployment model tooa Windows virtuele machine met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="e4ad4-105">U kunt ook [koppelen van een data schijf tooa Linux VM in hello Azure-portal](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="e4ad4-106">Voordat u een schijf koppelen, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="e4ad4-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="e4ad4-107">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="e4ad4-108">Zie voor meer informatie [grootten voor virtuele machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="e4ad4-109">Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="e4ad4-110">Met deze virtuele machines kunt u schijven uit zowel Premium en Standard-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="e4ad4-111">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="e4ad4-112">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="e4ad4-113">Voor een nieuwe schijf, hoeft u niet toocreate het eerste omdat Azure gemaakt wanneer u dit aansluit.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="e4ad4-114">U kunt ook [een gegevensschijf met behulp van Powershell koppelen](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4ad4-115">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="e4ad4-116">Hallo virtuele machine gevonden</span><span class="sxs-lookup"><span data-stu-id="e4ad4-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="e4ad4-117">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e4ad4-118">Selecteer Hallo virtuele machine van Hallo resource in de lijst op Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="e4ad4-119">In het linkerdeelvenster onder Hallo **instellingen**, klikt u op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Instellingen voor de schijf openen](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="e4ad4-121">Instructies voor het koppelen van een volgende om door te gaan een [nieuwe schijf](#option-1-attach-a-new-disk) of een [bestaande schijf](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="e4ad4-122">Optie 1: Koppelen en een nieuwe schijf initialiseren</span><span class="sxs-lookup"><span data-stu-id="e4ad4-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="e4ad4-123">Op Hallo **schijven** blade, klikt u op **Attach nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="e4ad4-124">Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Controleer de Schijfinstellingen](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="e4ad4-126">Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="e4ad4-127">Initialiseer de gegevensschijf van een nieuwe</span><span class="sxs-lookup"><span data-stu-id="e4ad4-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="e4ad4-128">Verbinding maken met toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="e4ad4-129">Zie voor instructies [hoe tooconnect en aanmelden tooan Azure virtuele machine met Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="e4ad4-130">Nadat u zich aanmeldt toohello virtuele machine, opent u **Serverbeheer**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="e4ad4-131">Selecteer in het linkerdeelvenster Hallo **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Open Serverbeheer](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="e4ad4-133">Selecteer **schijven**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-133">Select **Disks**.</span></span>
4. <span data-ttu-id="e4ad4-134">Hallo **schijven** sectie vindt u Hallo-schijven.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="e4ad4-135">De meeste gevallen heeft een virtuele machine schijf 0, schijf van 1 en 2 schijf.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="e4ad4-136">Schijf 0 besturingssysteemschijf hello, schijf 1 Hallo tijdelijke schijf en schijf 2 is Hallo gegevensschijf gekoppeld zojuist toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="e4ad4-137">Hallo gegevens schijf lijsten Hallo partitie als **onbekende**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="e4ad4-138">Met de rechtermuisknop op Hallo schijf en selecteer **initialiseren**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="e4ad4-139">U wordt gewaarschuwd dat alle gegevens worden gewist wanneer het Hallo-schijf is geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="e4ad4-140">Klik op **Ja** tooacknowledge Hallo waarschuwings- en initialisatie Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="e4ad4-141">Hierna kunt Hallo partitie wordt weergegeven als **GPT**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="e4ad4-142">Opnieuw met de rechtermuisknop op Hallo schijf en selecteer **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="e4ad4-143">Met de standaardwaarden Hallo Hallo-wizard te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="e4ad4-144">Als het Hallo-wizard is voltooid, Hallo **Volumes** sectie vindt u Hallo nieuw volume.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="e4ad4-145">Hallo-schijf is nu online en gereed toostore gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-145">hello disk is now online and ready toostore data.</span></span>

    ![Volume is geïnitialiseerd](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="e4ad4-147">Optie 2: Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="e4ad4-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="e4ad4-148">Op Hallo **schijven** blade, klikt u op **Attach bestaande**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="e4ad4-149">Onder **bestaande schijf koppelen**, klikt u op **locatie**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Bestaande schijf koppelen](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="e4ad4-151">Onder **opslagaccounts**, Hallo-account en -container met Hallo .vhd-bestand selecteren.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Locatie van de VHD vinden](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="e4ad4-153">Selecteer Hallo .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="e4ad4-154">Onder **bestaande schijf koppelen**, Hallo bestand dat u zojuist hebt geselecteerd wordt vermeld onder **VHD-bestand**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="e4ad4-155">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-155">Click **OK**.</span></span>
6. <span data-ttu-id="e4ad4-156">Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="e4ad4-157">Gebruik TRIM met standard-opslag</span><span class="sxs-lookup"><span data-stu-id="e4ad4-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="e4ad4-158">Als u een standard-opslag (HDD) gebruikt, moet u TRIM inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="e4ad4-159">TRIM worden niet-gebruikte blokken op Hallo schijf verwijderd, zodat u wordt alleen gefactureerd voor opslag die u daadwerkelijk gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="e4ad4-160">Met ' trim ', kun kosten, met inbegrip van niet-gebruikte blokken die het gevolg zijn van grote bestanden worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="e4ad4-161">U kunt deze opdracht toocheck Hallo beperkende instelling uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="e4ad4-162">Open een opdrachtprompt op de virtuele machine van Windows en typ:</span><span class="sxs-lookup"><span data-stu-id="e4ad4-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="e4ad4-163">Als de opdracht Hallo 0 retourneert, wordt ' trim ' correct ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e4ad4-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="e4ad4-164">Als deze 1 retourneert, voert u de volgende opdracht tooenable ' trim ' Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4ad4-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="e4ad4-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4ad4-165">Next steps</span></span>
<span data-ttu-id="e4ad4-166">Als uw toepassing toouse Hallo D: station toostore gegevens nodig zijn, kunt u [stationsletter op Hallo van Hallo Windows tijdelijke schijf wijzigen](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="e4ad4-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4ad4-167">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e4ad4-167">Additional resources</span></span>
[<span data-ttu-id="e4ad4-168">Over schijven en virtuele harde schijven voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="e4ad4-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
