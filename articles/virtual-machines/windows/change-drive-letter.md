---
title: 'Controleer Hallo D: station van een virtuele machine een gegevensschijf | Microsoft Docs'
description: 'Hierin wordt beschreven hoe toochange stationsletters voor een Windows-VM zodat u Hallo D: station als een gegevensstation gebruiken kunt.'
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="65116-103">Hallo D: station gebruiken als een gegevensstation op een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="65116-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="65116-104">Als uw toepassing toouse Hallo D-station toostore gegevens moet, volgt u deze instructies toouse een andere stationsletter voor de tijdelijke schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="65116-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="65116-105">Gebruik nooit Hallo tijdelijke schijf toostore gegevens dat u nodig hebt tookeep.</span><span class="sxs-lookup"><span data-stu-id="65116-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="65116-106">Als u de grootte of **stoppen (Deallocate)** een virtuele machine, kan dit de plaatsing van Hallo virtuele machine tooa nieuwe hypervisor activeren.</span><span class="sxs-lookup"><span data-stu-id="65116-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="65116-107">Een gebeurtenis gepland of ongepland onderhoud activeren mogelijk ook deze plaatsing.</span><span class="sxs-lookup"><span data-stu-id="65116-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="65116-108">In dit scenario worden de tijdelijke schijf Hallo opnieuw toegewezen toohello eerste beschikbare letter.</span><span class="sxs-lookup"><span data-stu-id="65116-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="65116-109">Als u een toepassing die specifiek Hallo D: station moet hebt, moet u toofollow deze stappen tootemporarily verplaatsen Hallo pagefile.sys, een nieuwe gegevensschijf koppelen en wijs deze Hallo letter D en verplaatsen Hallo pagefile.sys back-toohello tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="65116-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="65116-110">Hierna kunt Azure niet terug te nemen Hallo D: als Hallo VM tooa andere hypervisor verplaatst.</span><span class="sxs-lookup"><span data-stu-id="65116-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="65116-111">Zie voor meer informatie over hoe Azure gebruikt voor de tijdelijke schijf Hallo [begrijpen Hallo tijdelijke station op Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="65116-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="65116-112">Hallo gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="65116-112">Attach hello data disk</span></span>
<span data-ttu-id="65116-113">Eerst moet u tooattach Hallo gegevens schijf toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="65116-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="65116-114">toodo deze Hallo portal gebruikt, Zie [hoe tooattach een beheerde gegevens in Azure-portal Hallo schijf](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65116-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="65116-115">Tijdelijk verplaatst pagefile.sys tooC station</span><span class="sxs-lookup"><span data-stu-id="65116-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="65116-116">Verbinding maken met toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="65116-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="65116-117">Klik met de rechtermuisknop Hallo **Start** menu en selecteer **System**.</span><span class="sxs-lookup"><span data-stu-id="65116-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="65116-118">Selecteer in het menu Hallo links, **Geavanceerde systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="65116-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="65116-119">In Hallo **prestaties** sectie **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="65116-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="65116-120">Selecteer Hallo **Geavanceerd** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65116-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="65116-121">In Hallo **virtueel geheugen** sectie **wijziging**.</span><span class="sxs-lookup"><span data-stu-id="65116-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="65116-122">Selecteer Hallo **C** station en klik vervolgens op **systeem beheerde grootte** en klik vervolgens op **ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="65116-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="65116-123">Selecteer Hallo **D** station en klik vervolgens op **geen wisselbestand** en klik vervolgens op **ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="65116-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="65116-124">Klik op toepassen.</span><span class="sxs-lookup"><span data-stu-id="65116-124">Click Apply.</span></span> <span data-ttu-id="65116-125">U ontvangt een waarschuwing dat die Hallo-computer moet opnieuw worden opgestart voor Hallo wijzigingen tootake invloed toobe.</span><span class="sxs-lookup"><span data-stu-id="65116-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="65116-126">Hallo virtuele machine opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="65116-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="65116-127">Hallo stationsletters wijzigen</span><span class="sxs-lookup"><span data-stu-id="65116-127">Change hello drive letters</span></span>
1. <span data-ttu-id="65116-128">Eenmaal Hallo VM opnieuw wordt opgestart, meld u opnieuw aan toohello VM.</span><span class="sxs-lookup"><span data-stu-id="65116-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="65116-129">Klik op Hallo **Start** menu en typ **diskmgmt.msc** en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="65116-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="65116-130">Schijfbeheer wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="65116-130">Disk Management will start.</span></span>
3. <span data-ttu-id="65116-131">Met de rechtermuisknop op **D**, Hallo station voor tijdelijke opslag en selecteert u **wijziging stationsletter en paden**.</span><span class="sxs-lookup"><span data-stu-id="65116-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="65116-132">Selecteer onder de stationsletter, een nieuw station, zoals **T** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="65116-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="65116-133">Met de rechtermuisknop op de gegevensschijf Hallo en selecteer **wijziging stationsletter en paden**.</span><span class="sxs-lookup"><span data-stu-id="65116-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="65116-134">Selecteer onder de stationsletter, station **D** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="65116-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="65116-135">Pagefile.sys back toohello tijdelijke opslagstation verplaatsen</span><span class="sxs-lookup"><span data-stu-id="65116-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="65116-136">Klik met de rechtermuisknop Hallo **Start** menu en selecteer **systeem**</span><span class="sxs-lookup"><span data-stu-id="65116-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="65116-137">Selecteer in het menu Hallo links, **Geavanceerde systeeminstellingen**.</span><span class="sxs-lookup"><span data-stu-id="65116-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="65116-138">In Hallo **prestaties** sectie **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="65116-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="65116-139">Selecteer Hallo **Geavanceerd** tabblad.</span><span class="sxs-lookup"><span data-stu-id="65116-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="65116-140">In Hallo **virtueel geheugen** sectie **wijziging**.</span><span class="sxs-lookup"><span data-stu-id="65116-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="65116-141">Selecteer Hallo OS station **C** en klik op **geen wisselbestand** en klik vervolgens op **ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="65116-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="65116-142">Selecteer Hallo tijdelijke opslagstation **T** en klik vervolgens op **systeem beheerde grootte** en klik vervolgens op **ingesteld**.</span><span class="sxs-lookup"><span data-stu-id="65116-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="65116-143">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="65116-143">Click **Apply**.</span></span> <span data-ttu-id="65116-144">U ontvangt een waarschuwing dat die Hallo-computer moet opnieuw worden opgestart voor Hallo wijzigingen tootake invloed toobe.</span><span class="sxs-lookup"><span data-stu-id="65116-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="65116-145">Hallo virtuele machine opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="65116-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65116-146">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65116-146">Next steps</span></span>
* <span data-ttu-id="65116-147">U kunt verhogen Hallo opslag beschikbaar tooyour virtuele machine door [koppelen van een extra gegevensschijf](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="65116-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

