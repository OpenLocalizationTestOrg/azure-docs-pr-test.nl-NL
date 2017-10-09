---
title: verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie aaaTroubleshoot | Microsoft Docs
description: Verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie oplossen
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="e6e17-103">Verwijderen van Azure storage-accounts, containers of VHD's in een klassieke implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="e6e17-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="e6e17-104">Er kunnen fouten optreden wanneer u toodelete hello Azure storage-account, container of VHD in Hallo probeert [Azure-portal](https://portal.azure.com/) of Hallo [klassieke Azure-portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6e17-104">You might receive errors when you try toodelete hello Azure storage account, container, or VHD in hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="e6e17-105">Hallo problemen kunnen zijn veroorzaakt door Hallo volgende omstandigheden:</span><span class="sxs-lookup"><span data-stu-id="e6e17-105">hello issues can be caused by hello following circumstances:</span></span>

* <span data-ttu-id="e6e17-106">Wanneer u een virtuele machine verwijdert, Hallo schijf en de VHD niet automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e6e17-106">When you delete a VM, hello disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="e6e17-107">Die mogelijk Hallo reden voor fout van storage-account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e6e17-107">That might be hello reason for failure on storage account deletion.</span></span> <span data-ttu-id="e6e17-108">We kunt Hallo schijf niet verwijderen, zodat u Hallo schijf toomount een andere virtuele machine kunt.</span><span class="sxs-lookup"><span data-stu-id="e6e17-108">We don't delete hello disk so that you can use hello disk toomount another VM.</span></span>
* <span data-ttu-id="e6e17-109">Er is nog steeds een lease op een schijf of Hallo blob die is gekoppeld aan het Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="e6e17-109">There is still a lease on a disk or hello blob that's associated with hello disk.</span></span>
* <span data-ttu-id="e6e17-110">Er is nog steeds een VM-installatiekopie die een blob-container of storage-account wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e6e17-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="e6e17-111">Als uw Azure probleem niet wordt besproken in dit artikel, gaat u naar Azure-forums op Hallo [MSDN en Hallo Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e6e17-111">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e6e17-112">U kunt het probleem op deze forums boeken of too@AzureSupport op Twitter.</span><span class="sxs-lookup"><span data-stu-id="e6e17-112">You can post your issue on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="e6e17-113">U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="e6e17-113">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="e6e17-114">Symptomen</span><span class="sxs-lookup"><span data-stu-id="e6e17-114">Symptoms</span></span>
<span data-ttu-id="e6e17-115">Hallo volgende sectie bevat algemene fouten die wordt weergegeven mogelijk wanneer u toodelete hello Azure storage-accounts, containers of VHD's probeert.</span><span class="sxs-lookup"><span data-stu-id="e6e17-115">hello following section lists common errors that you might receive when you try toodelete hello Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-toodelete-a-storage-account"></a><span data-ttu-id="e6e17-116">Scenario 1: Kan geen toodelete storage-account</span><span class="sxs-lookup"><span data-stu-id="e6e17-116">Scenario 1: Unable toodelete a storage account</span></span>
<span data-ttu-id="e6e17-117">Wanneer u toohello klassieke storage-account in Hallo navigeert [Azure-portal](https://portal.azure.com/) en selecteer **verwijderen**, worden weergegeven met een lijst met objecten die verhinderen het verwijderen van opslagaccount Hallo dat:</span><span class="sxs-lookup"><span data-stu-id="e6e17-117">When you navigate toohello classic storage account in hello [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of hello storage account:</span></span>

  ![Afbeelding van de fout als het verwijderen van opslagaccount Hallo](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="e6e17-119">Wanneer u toohello storage-account in Hallo navigeert [klassieke Azure-portal](https://manage.windowsazure.com/) en selecteer **verwijderen**, ziet u mogelijk een Hallo volgende fouten:</span><span class="sxs-lookup"><span data-stu-id="e6e17-119">When you navigate toohello storage account in hello [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of hello following errors:</span></span>

- <span data-ttu-id="e6e17-120">*Opslagaccount StorageAccountName bevat VM-installatiekopieën. Zorg ervoor dat deze VM-installatiekopieën zijn verwijderd voordat u dit opslagaccount verwijdert.*</span><span class="sxs-lookup"><span data-stu-id="e6e17-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="e6e17-121">*Kan geen toodelete storage-account < vm-opslag-account-name >. Kan geen toodelete storage-account < vm-opslag-account-name >: "Storage-account < vm-opslag-account-name > heeft een aantal actieve installatiekopieën en/of de schijven. Zorg ervoor dat deze installatiekopieën en/of een of meer schijven zijn verwijderd voordat u dit opslagaccount verwijdert.'.*</span><span class="sxs-lookup"><span data-stu-id="e6e17-121">*Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="e6e17-122">*Storage-account < vm-opslag-account-name > heeft een aantal actieve installatiekopieën en/of schijven, bijvoorbeeld xxxxxxxxx-xxxxxxxxx-O-209490240936090599. Zorg ervoor dat deze installatiekopieën en/of een of meer schijven zijn verwijderd voordat u dit opslagaccount verwijdert.*</span><span class="sxs-lookup"><span data-stu-id="e6e17-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="e6e17-123">*Storage-account < vm-opslag-account-name > heeft 1 container (s) waarvoor een actieve installatiekopie en/of de schijf artefacten. Zorg ervoor dat deze artefacten zijn verwijderd uit het Hallo-opslagplaats voor installatiekopieën voordat u dit opslagaccount verwijdert*.</span><span class="sxs-lookup"><span data-stu-id="e6e17-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="e6e17-124">*Verzenden is mislukt Storage-account < vm-opslag-account-name > is 1 container (s) waarvoor een actieve installatiekopie en/of de schijf artefacten. Zorg ervoor dat deze artefacten zijn verwijderd uit het Hallo-opslagplaats voor installatiekopieën voordat u dit opslagaccount verwijdert. Als u een opslagaccount toodelete probeert en er nog steeds actief schijven die zijn gekoppeld zijn, ziet u een bericht dat u er nog actieve schijven die toobe verwijderd moeten*.</span><span class="sxs-lookup"><span data-stu-id="e6e17-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account. When you attempt toodelete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need toobe deleted*.</span></span>

### <a name="scenario-2-unable-toodelete-a-container"></a><span data-ttu-id="e6e17-125">Scenario 2: Kan geen toodelete een container</span><span class="sxs-lookup"><span data-stu-id="e6e17-125">Scenario 2: Unable toodelete a container</span></span>
<span data-ttu-id="e6e17-126">Wanneer u toodelete Hallo storage-container, ziet u mogelijk Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="e6e17-126">When you try toodelete hello storage container, you might see hello following error:</span></span>

<span data-ttu-id="e6e17-127">*Mislukte toodelete storage-container <container name>. Fout: "Er is momenteel een lease op Hallo-container en geen lease-ID is opgegeven in de aanvraag Hallo*.</span><span class="sxs-lookup"><span data-stu-id="e6e17-127">*Failed toodelete storage container <container name>. Error: 'There is currently a lease on hello container and no lease ID was specified in hello request*.</span></span>

<span data-ttu-id="e6e17-128">of</span><span class="sxs-lookup"><span data-stu-id="e6e17-128">Or</span></span>

<span data-ttu-id="e6e17-129">*Hallo schijven op virtuele machine na blobs in deze container gebruiken, zodat het Hallo-container kan niet worden verwijderd: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="e6e17-129">*hello following virtual machine disks use blobs in this container, so hello container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-toodelete-a-vhd"></a><span data-ttu-id="e6e17-130">Scenario 3: Kan geen toodelete een VHD</span><span class="sxs-lookup"><span data-stu-id="e6e17-130">Scenario 3: Unable toodelete a VHD</span></span>
<span data-ttu-id="e6e17-131">Nadat u een virtuele machine verwijderen en vervolgens probeert toodelete Hallo blobs voor Hallo VHD's gekoppeld, kan Hallo volgende bericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e6e17-131">After you delete a VM and then try toodelete hello blobs for hello associated VHDs, you might receive hello following message:</span></span>

<span data-ttu-id="e6e17-132">*Mislukte toodelete blob ' pad/XXXXXX-XXXXXX-os-1447379084699.vhd'. Fout: "Er is momenteel een lease op Hallo blob en geen lease-ID is opgegeven in Hallo-aanvraag.*</span><span class="sxs-lookup"><span data-stu-id="e6e17-132">*Failed toodelete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on hello blob and no lease ID was specified in hello request.*</span></span>

<span data-ttu-id="e6e17-133">of</span><span class="sxs-lookup"><span data-stu-id="e6e17-133">Or</span></span>

<span data-ttu-id="e6e17-134">*BLOB 'BlobName.vhd' is in gebruik als de schijf van de virtuele machine 'VirtualMachineDiskName' hello blob kan niet worden verwijderd.*</span><span class="sxs-lookup"><span data-stu-id="e6e17-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so hello blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="e6e17-135">Oplossing</span><span class="sxs-lookup"><span data-stu-id="e6e17-135">Solution</span></span>
<span data-ttu-id="e6e17-136">meest voorkomende problemen tooresolve hello, proberen Hallo methode te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6e17-136">tooresolve hello most common issues, try hello following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a><span data-ttu-id="e6e17-137">Stap 1: Geen schijven die verhinderen het verwijderen van opslagaccount hello, container of VHD dat verwijderen</span><span class="sxs-lookup"><span data-stu-id="e6e17-137">Step 1: Delete any disks that are preventing deletion of hello storage account, container, or VHD</span></span>
1. <span data-ttu-id="e6e17-138">Overschakelen van toohello [klassieke Azure-portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6e17-138">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e6e17-139">Selecteer **virtuele MACHINE** > **schijven**.</span><span class="sxs-lookup"><span data-stu-id="e6e17-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Afbeelding van schijven op virtuele machines in de klassieke Azure-portal.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="e6e17-141">Hallo-schijven die gekoppeld aan Hallo storage-account, container of VHD zijn die u wilt dat toodelete vinden.</span><span class="sxs-lookup"><span data-stu-id="e6e17-141">Locate hello disks that are associated with hello storage account, container, or VHD that you want toodelete.</span></span> <span data-ttu-id="e6e17-142">Wanneer u de locatie van de schijf Hallo Hallo controleert, vindt u Hallo storage-account-container of VHD die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e6e17-142">When you check hello location of hello disk, you will find hello associated storage account, container, or VHD.</span></span>

    ![Afbeelding die laat zien van locatiegegevens voor schijven in de klassieke Azure-portal](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="e6e17-144">Hallo schijven verwijderen met behulp van een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="e6e17-144">Delete hello disks by using one of hello following methods:</span></span>

  - <span data-ttu-id="e6e17-145">Als er geen virtuele machine moet worden weergegeven op Hallo **aangesloten op** veld van Hallo schijf, kunt u rechtstreeks Hallo schijf verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e6e17-145">If  there is no VM listed on hello **Attached To** field of hello disk, you can delete hello disk directly.</span></span>

  - <span data-ttu-id="e6e17-146">Als het Hallo-schijf is een gegevensschijf, volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="e6e17-146">If hello disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="e6e17-147">Controleer de naam van de Hallo Hallo VM die Hallo schijf is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="e6e17-147">Check hello name of hello VM that hello disk is attached to.</span></span>
    2. <span data-ttu-id="e6e17-148">Ga te**virtuele Machines** > **exemplaren**, en ga vervolgens naar Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e6e17-148">Go too**Virtual Machines** > **Instances**, and then locate hello VM.</span></span>
    3. <span data-ttu-id="e6e17-149">Zorg ervoor dat er niets is actief Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="e6e17-149">Make sure that nothing is actively using hello disk.</span></span>
    4. <span data-ttu-id="e6e17-150">Selecteer **schijf loskoppelen** onderaan Hallo Hallo portal toodetach Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="e6e17-150">Select **Detach Disk** at hello bottom of hello portal toodetach hello disk.</span></span>
    5. <span data-ttu-id="e6e17-151">Ga te**virtuele Machines** > **schijven**, en wachten op Hallo **aangesloten op** veld tooturn leeg.</span><span class="sxs-lookup"><span data-stu-id="e6e17-151">Go too**Virtual Machines** > **Disks**, and wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="e6e17-152">Hiermee wordt aangegeven met het Hallo-schijf met succes is losgekoppeld van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e6e17-152">This indicates hello disk has successfully detached from hello VM.</span></span>
    6. <span data-ttu-id="e6e17-153">Selecteer **verwijderen** Hallo onderaan in **virtuele Machines** > **schijven** toodelete Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="e6e17-153">Select **Delete** at hello bottom of **Virtual Machines** > **Disks** toodelete hello disk.</span></span>

  - <span data-ttu-id="e6e17-154">Als de schijf Hallo een besturingssysteemschijf (Hallo **bevat OS** veld heeft een waarde zoals Windows) en gekoppelde tooa VM, als volgt te werk toodelete Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e6e17-154">If hello disk is an OS disk (hello **Contains OS** field has a value like Windows) and attached tooa VM, follow these steps toodelete hello VM.</span></span> <span data-ttu-id="e6e17-155">Hallo besturingssysteemschijf kan niet worden ontkoppeld zodat we toodelete Hallo VM toorelease Hallo lease hebben.</span><span class="sxs-lookup"><span data-stu-id="e6e17-155">hello OS disk cannot be detached, so we have toodelete hello VM toorelease hello lease.</span></span>

    1. <span data-ttu-id="e6e17-156">Controleer de naam van de Hallo Hallo virtuele Machine Hallo die gegevensschijf is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="e6e17-156">Check hello name of hello Virtual Machine hello Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="e6e17-157">Ga te**virtuele Machines** > **exemplaren**, en vervolgens selecteert Hallo VM die Hallo schijf is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="e6e17-157">Go too**Virtual Machines** > **Instances**, and then select hello VM that hello disk is attached to.</span></span>
    3. <span data-ttu-id="e6e17-158">Zorg ervoor dat er niets is actief Hallo virtuele machine, en dat u niet langer nodig Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e6e17-158">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
    4. <span data-ttu-id="e6e17-159">Selecteer Hallo VM Hallo schijf is gekoppeld aan, schakelt u **verwijderen** > **verwijderen Hallo gekoppelde schijven**.</span><span class="sxs-lookup"><span data-stu-id="e6e17-159">Select hello VM hello disk is attached to, then select **Delete** > **Delete hello attached disks**.</span></span>
    5. <span data-ttu-id="e6e17-160">Ga te**virtuele Machines** > **schijven**, en wachten op Hallo schijf toodisappear.</span><span class="sxs-lookup"><span data-stu-id="e6e17-160">Go too**Virtual Machines** > **Disks**, and wait for hello disk toodisappear.</span></span>  <span data-ttu-id="e6e17-161">Het kan enkele minuten duren voordat deze toooccur en moet u mogelijk toorefresh Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="e6e17-161">It may take a few minutes for this toooccur, and you may need toorefresh hello page.</span></span>
    6. <span data-ttu-id="e6e17-162">Als het Hallo-schijf niet verdwijnt, wacht u totdat Hallo **aangesloten op** veld tooturn leeg.</span><span class="sxs-lookup"><span data-stu-id="e6e17-162">If hello disk does not disappear, wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="e6e17-163">Hiermee wordt aangegeven Hallo schijf volledig is losgekoppeld van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e6e17-163">This indicates hello disk has fully detached from hello VM.</span></span>  <span data-ttu-id="e6e17-164">Vervolgens selecteert u Hallo schijf en selecteer **verwijderen** onderaan Hallo Hallo pagina toodelete Hallo-schijf.</span><span class="sxs-lookup"><span data-stu-id="e6e17-164">Then, select hello disk, and select **Delete** at hello bottom of hello page toodelete hello disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="e6e17-165">Als een schijf aangesloten tooa VM is, u zich niet kunnen toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="e6e17-165">If a disk is attached tooa VM, you will not be able toodelete it.</span></span> <span data-ttu-id="e6e17-166">Schijven zijn asynchroon losgekoppeld van een verwijderde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e6e17-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="e6e17-167">Het duurt een paar minuten nadat Hallo VM voor deze tooclear veld van wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e6e17-167">It might take a few minutes after hello VM is deleted for this field tooclear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a><span data-ttu-id="e6e17-168">Stap 2: Verwijdert u alle VM-installatiekopieën die verhinderen verwijderen van opslagaccount Hallo of container dat</span><span class="sxs-lookup"><span data-stu-id="e6e17-168">Step 2: Delete any VM Images that are preventing deletion of hello storage account or container</span></span>
1. <span data-ttu-id="e6e17-169">Overschakelen van toohello [klassieke Azure-portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6e17-169">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e6e17-170">Selecteer **virtuele MACHINE** > **INSTALLATIEKOPIEËN**, en verwijder vervolgens Hallo installatiekopieën die gekoppeld aan Hallo storage-account-container of VHD zijn.</span><span class="sxs-lookup"><span data-stu-id="e6e17-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete hello images that are associated with hello storage account, container, or VHD.</span></span>

    <span data-ttu-id="e6e17-171">Daarna opnieuw toodelete Hallo storage-account-container of VHD.</span><span class="sxs-lookup"><span data-stu-id="e6e17-171">After that, try toodelete hello storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="e6e17-172">Ervoor tooback niets worden u toosave voordat u Hallo account verwijdert.</span><span class="sxs-lookup"><span data-stu-id="e6e17-172">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="e6e17-173">Als u een VHD, blob, table, wachtrij of bestand verwijdert, wordt deze permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e6e17-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="e6e17-174">Zorg ervoor dat Hallo resource niet in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="e6e17-174">Ensure that hello resource is not in use.</span></span>
>
>

## <a name="about-hello-stopped-deallocated-status"></a><span data-ttu-id="e6e17-175">Over Hallo status gestopt (toewijzing opgeheven)</span><span class="sxs-lookup"><span data-stu-id="e6e17-175">About hello Stopped (deallocated) status</span></span>
<span data-ttu-id="e6e17-176">Virtuele machines die zijn gemaakt in het klassieke implementatiemodel Hallo en die gehandhaafd blijft heeft Hallo **gestopt (toewijzing opgeheven)** status op beide Hallo [Azure-portal](https://portal.azure.com/) of [klassieke Azure-portal ](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e6e17-176">VMs that were created in hello classic deployment model and that have been retained will have hello **Stopped (deallocated)** status on either hello [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="e6e17-177">**Klassieke Azure-portal**:</span><span class="sxs-lookup"><span data-stu-id="e6e17-177">**Azure classic portal**:</span></span>

![Gestopt (Deallocated) status voor virtuele machines in Azure portal.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="e6e17-179">**Azure-portal**:</span><span class="sxs-lookup"><span data-stu-id="e6e17-179">**Azure portal**:</span></span>

![Gestopt (toewijzing ongedaan gemaakt) status voor virtuele machines op de klassieke Azure-portal.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="e6e17-181">De status 'Gestopt (toewijzing opgeheven)' versies Hallo computerresources, zoals Hallo CPU, geheugen en het netwerk.</span><span class="sxs-lookup"><span data-stu-id="e6e17-181">A "Stopped (deallocated)" status releases hello computer resources, such as hello CPU, memory, and network.</span></span> <span data-ttu-id="e6e17-182">Hallo-schijven, blijven echter nog steeds behouden zodat u snel opnieuw kunt maken Hallo VM indien nodig.</span><span class="sxs-lookup"><span data-stu-id="e6e17-182">hello disks, however, are still retained so that you can quickly re-create hello VM if necessary.</span></span> <span data-ttu-id="e6e17-183">Deze schijven worden gemaakt op de virtuele harde schijven die worden ondersteund door Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="e6e17-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="e6e17-184">Hallo storage-account heeft deze VHD's en Hallo schijven leases hebben op deze virtuele harde schijven.</span><span class="sxs-lookup"><span data-stu-id="e6e17-184">hello storage account has these VHDs, and hello disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6e17-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6e17-185">Next steps</span></span>
* [<span data-ttu-id="e6e17-186">Een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="e6e17-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
