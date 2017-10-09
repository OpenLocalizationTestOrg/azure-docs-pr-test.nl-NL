---
title: een data schijf tooa Linux VM aaaAttach | Microsoft Docs
description: Hoe Hallo tooattach nieuwe of bestaande gegevens schijf tooa Linux VM in hello Azure portal met behulp van Resource Manager-implementatiemodel.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="96234-103">Hoe tooattach data schijf tooa Linux VM in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="96234-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="96234-104">Dit artikel laat zien hoe tooattach zowel nieuwe als bestaande schijven tooa virtuele Linux-machine via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="96234-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="96234-105">U kunt ook [koppelen van een data schijf tooa virtuele Windows-machine in Azure-portal Hallo](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96234-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="96234-106">U kunt toouse beide schijven Azure beheerd of onbeheerd schijven.</span><span class="sxs-lookup"><span data-stu-id="96234-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="96234-107">Beheerde schijven worden afgehandeld door hello Azure-platform en hoeven niet alle toostore voorbereidings- of locatie ze.</span><span class="sxs-lookup"><span data-stu-id="96234-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="96234-108">Niet-beheerde schijven is een opslagaccount vereist en beschikt over sommige [quota en limieten die van toepassing](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="96234-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="96234-109">Zie [Overzicht van Azure Managed Disks](../windows/managed-disks-overview.md) voor meer informatie over Azure Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="96234-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="96234-110">Voordat u schijven tooyour VM koppelt, controleert u de volgende tips:</span><span class="sxs-lookup"><span data-stu-id="96234-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="96234-111">Hallo-grootte van Hallo virtuele machine bepaalt hoeveel gegevensschijven die u kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="96234-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="96234-112">Zie voor meer informatie [grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96234-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="96234-113">Premium-opslag toouse, moet u een virtuele machine DS-serie- of GS-serie.</span><span class="sxs-lookup"><span data-stu-id="96234-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="96234-114">U kunt zowel Premium en Standard schijven met deze virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="96234-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="96234-115">Premium-opslag is beschikbaar in bepaalde regio's.</span><span class="sxs-lookup"><span data-stu-id="96234-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="96234-116">Zie voor meer informatie [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96234-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="96234-117">Schijven gekoppelde toovirtual machines zijn daadwerkelijk .vhd bestanden die zijn opgeslagen in Azure.</span><span class="sxs-lookup"><span data-stu-id="96234-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="96234-118">Zie voor meer informatie [over schijven en virtuele harde schijven voor virtuele machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96234-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="96234-119">Hallo virtuele machine gevonden</span><span class="sxs-lookup"><span data-stu-id="96234-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="96234-120">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="96234-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="96234-121">Klik op het menu Hub Hallo **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="96234-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="96234-122">Selecteer Hallo virtuele machine uit de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="96234-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="96234-123">toohello virtuele machines blade in **Essentials**, klikt u op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="96234-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Instellingen voor de schijf openen](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="96234-125">Instructies voor het koppelen van een volgende om door te gaan een [beheerde schijven](#use-azure-managed-disks) of [onbeheerde schijf](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="96234-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="96234-126">Azure-beheerde schijven gebruiken</span><span class="sxs-lookup"><span data-stu-id="96234-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="96234-127">Een nieuwe schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="96234-127">Attach a new disk</span></span>

1. <span data-ttu-id="96234-128">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="96234-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="96234-129">Klik op Hallo vervolgkeuzelijst voor **naam** en selecteer **maken-schijf**:</span><span class="sxs-lookup"><span data-stu-id="96234-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Maken van Azure beheerde schijven](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="96234-131">Voer een naam voor de beheerde schijf.</span><span class="sxs-lookup"><span data-stu-id="96234-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="96234-132">Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="96234-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="96234-134">Klik op **opslaan** toocreate Hallo beheerd schijf en update Hallo VM-configuratie:</span><span class="sxs-lookup"><span data-stu-id="96234-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Nieuwe Azure beheerd schijf opslaan](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="96234-136">Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="96234-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="96234-137">Als beheerde schijven een bron op het hoogste niveau zijn, wordt in de hoofdmap Hallo van resourcegroep Hallo Hallo schijf weergegeven:</span><span class="sxs-lookup"><span data-stu-id="96234-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Azure-schijf beheerd in de resourcegroep](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="96234-139">Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="96234-139">Attach an existing disk</span></span>
1. <span data-ttu-id="96234-140">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="96234-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="96234-141">Klik op Hallo vervolgkeuzelijst voor **naam** tooview een lijst met bestaande schijven toegankelijk tooyour Azure-abonnement beheerd.</span><span class="sxs-lookup"><span data-stu-id="96234-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="96234-142">Selecteer Hallo beheerd schijf tooattach:</span><span class="sxs-lookup"><span data-stu-id="96234-142">Select hello managed disk tooattach:</span></span>

   ![Bestaande Azure beheerd schijf koppelen](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="96234-144">Klik op **opslaan** tooattach Hallo bestaande schijf en update Hallo VM-configuratie worden beheerd:</span><span class="sxs-lookup"><span data-stu-id="96234-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Beheerde Azure-schijf updates opslaan](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="96234-146">Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="96234-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="96234-147">Niet-beheerde schijven gebruiken</span><span class="sxs-lookup"><span data-stu-id="96234-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="96234-148">Een nieuwe schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="96234-148">Attach a new disk</span></span>

1. <span data-ttu-id="96234-149">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="96234-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="96234-150">Controleer Hallo standaardinstellingen, indien nodig bijwerken en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="96234-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Controleer de Schijfinstellingen](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="96234-152">Nadat Azure Hallo schijf wordt gemaakt en gekoppeld toohello virtuele machine, Hallo nieuwe schijf wordt weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="96234-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="96234-153">Een bestaande schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="96234-153">Attach an existing disk</span></span>
1. <span data-ttu-id="96234-154">Op Hallo **schijven** blade, klikt u op **+ gegevensschijf toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="96234-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="96234-155">Onder **bestaande schijf koppelen**, klikt u op **VHD-bestand**.</span><span class="sxs-lookup"><span data-stu-id="96234-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Bestaande schijf koppelen](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="96234-157">Onder **opslagaccounts**, Hallo-account en -container met Hallo .vhd-bestand selecteren.</span><span class="sxs-lookup"><span data-stu-id="96234-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Locatie van de VHD vinden](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="96234-159">Selecteer Hallo .vhd-bestand.</span><span class="sxs-lookup"><span data-stu-id="96234-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="96234-160">Onder **bestaande schijf koppelen**, Hallo bestand dat u zojuist hebt geselecteerd wordt vermeld onder **VHD-bestand**.</span><span class="sxs-lookup"><span data-stu-id="96234-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="96234-161">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="96234-161">Click **OK**.</span></span>
6. <span data-ttu-id="96234-162">Nadat Azure wordt hello schijf toohello virtuele machine, wordt deze weergegeven in de instellingen voor de schijf Hallo virtuele machine onder **gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="96234-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="96234-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96234-163">Next steps</span></span>
<span data-ttu-id="96234-164">Nadat het Hallo-schijf wordt toegevoegd, moet u tooprepare voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="96234-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="96234-165">Zie voor meer informatie [hoe: initialiseren van een nieuwe gegevensschijf in Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="96234-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
