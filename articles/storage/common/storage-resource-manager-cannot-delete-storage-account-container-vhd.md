---
title: aaaTroubleshoot fouten wanneer u Azure storage-accounts, containers of VHD's verwijderen | Microsoft Docs
description: Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 33261562a2dd2614b35bc1118924513f8c624d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="e3443-103">Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen</span><span class="sxs-lookup"><span data-stu-id="e3443-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="e3443-104">U bijvoorbeeld fouten ontvangt wanneer u toodelete een Azure storage-account, container of virtuele harde schijf (VHD probeert) in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3443-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e3443-105">Dit artikel bevat richtlijnen toohelp los Hallo probleem in een Azure Resource Manager-implementatie op te lossen.</span><span class="sxs-lookup"><span data-stu-id="e3443-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="e3443-106">Als u dit artikel niet van toepassing uw Azure probleem, gaat u naar Azure-forums op Hallo [MSDN en Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e3443-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e3443-107">U kunt het probleem op deze forums boeken of too@AzureSupport op Twitter.</span><span class="sxs-lookup"><span data-stu-id="e3443-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="e3443-108">U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op Hallo [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="e3443-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="e3443-109">Symptomen</span><span class="sxs-lookup"><span data-stu-id="e3443-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="e3443-110">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="e3443-110">Scenario 1</span></span>
<span data-ttu-id="e3443-111">Wanneer u een VHD in een opslagaccount in de implementatie van een Resource Manager toodelete, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e3443-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="e3443-112">**Kan geen toodelete blob 'vhds/BlobName.vhd'. Fout: Er is momenteel een lease op Hallo blob en geen lease-ID is opgegeven in Hallo-aanvraag.**</span><span class="sxs-lookup"><span data-stu-id="e3443-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="e3443-113">Dit probleem kan optreden omdat een virtuele machine (VM) een lease op Hallo heeft dat u toodelete probeert VHD.</span><span class="sxs-lookup"><span data-stu-id="e3443-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="e3443-114">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="e3443-114">Scenario 2</span></span>
<span data-ttu-id="e3443-115">Wanneer u een container in een opslagaccount in de implementatie van een Resource Manager toodelete probeert, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e3443-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="e3443-116">**Kan geen VHD-container 'toodelete opslag's '. Fout: Er is momenteel een lease op Hallo-container en geen lease-ID is opgegeven in Hallo-aanvraag.**</span><span class="sxs-lookup"><span data-stu-id="e3443-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="e3443-117">Dit probleem kan optreden omdat het Hallo-container is een VHD die is vergrendeld in Hallo lease staat.</span><span class="sxs-lookup"><span data-stu-id="e3443-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="e3443-118">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="e3443-118">Scenario 3</span></span>
<span data-ttu-id="e3443-119">Wanneer u een opslagaccount in de implementatie van een Resource Manager toodelete, ontvangen Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e3443-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="e3443-120">**Kan geen toodelete storage-account 'StorageAccountName'. Fout: Hallo storage-account kan niet worden verwijderd vanwege tooits artefacten die in gebruik.**</span><span class="sxs-lookup"><span data-stu-id="e3443-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="e3443-121">Dit probleem kan optreden omdat het Hallo-opslagaccount bevat een VHD die Hallo lease status heeft.</span><span class="sxs-lookup"><span data-stu-id="e3443-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="e3443-122">Oplossing</span><span class="sxs-lookup"><span data-stu-id="e3443-122">Solution</span></span> 
<span data-ttu-id="e3443-123">tooresolve deze problemen, moet u vaststellen Hallo VHD die Hallo fout veroorzaakt en Hallo VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="e3443-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="e3443-124">Vervolgens loskoppelen Hallo VHD van Hallo VM (voor gegevensschijven) of verwijderen Hallo VM die van Hallo VHD (voor OS-schijven gebruikmaakt).</span><span class="sxs-lookup"><span data-stu-id="e3443-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="e3443-125">Dit Hallo lease verwijdert uit Hallo VHD en toestaat dat deze toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e3443-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="e3443-126">toodo dit, gebruik een van de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="e3443-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="e3443-127">Methode 1 - gebruik Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="e3443-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="e3443-128">Stap 1 identificeren Hallo VHD die voorkomen dat Hallo storage-account wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="e3443-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="e3443-129">Wanneer u Hallo storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e3443-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![bericht wanneer het Hallo-storage-account verwijderen](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="e3443-131">Controleer de Hallo **schijf URL** tooidentify Hallo storage-account en Hallo VHD waardoor het Hallo-opslagaccount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3443-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="e3443-132">Hallo in Hallo voorbeeld te volgen, tekenreeks vóór '. blob.core.windows.net ' hello opslagaccountnaam is en 'SCCM2012-2015-08-28.vhd' hello VHD-naam.</span><span class="sxs-lookup"><span data-stu-id="e3443-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="e3443-133">Stap 2 Hallo VHD verwijderen met behulp van Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e3443-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="e3443-134">Download en installeer Hallo meest recente versie van [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="e3443-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="e3443-135">Dit hulpprogramma is een zelfstandige app van Microsoft waarmee u tooeasily werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="e3443-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="e3443-136">Open Azure Storage Explorer, selecteer</span><span class="sxs-lookup"><span data-stu-id="e3443-136">Open Azure Storage Explorer, select</span></span> ![pictogram](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="e3443-138">Selecteer uw Azure-omgeving op Hallo linkerbalk en vervolgens weer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e3443-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="e3443-139">Selecteer alle abonnementen of Hallo-abonnement dat Hallo storage-account dat u wilt dat toodelete bevat.</span><span class="sxs-lookup"><span data-stu-id="e3443-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![Abonnement toevoegen](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="e3443-141">Ga toohello storage-account die wordt verkregen door Hallo schijf URL eerdere, selecteer Hallo **Blob-Containers** > **VHD's** en zoek naar Hallo VHD die u niet kunt verwijderen Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3443-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="e3443-142">Als Hallo VHD wordt gevonden, controleert u Hallo **VM-naam** kolom toofind Hallo VM die van deze VHD gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="e3443-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![Controleer de virtuele machine](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="e3443-144">Hallo lease van Hallo VHD verwijderen met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e3443-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="e3443-145">Zie voor meer informatie [verwijderen Hallo lease van Hallo VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="e3443-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="e3443-146">Ga toohello Azure Storage Explorer, met de rechtermuisknop op Hallo VHD en selecteer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3443-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="e3443-147">Hallo storage-account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3443-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="e3443-148">Methode 2: gebruik Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e3443-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="e3443-149">Stap 1: Identificeren Hallo VHD die voorkomen dat Hallo storage-account wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="e3443-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="e3443-150">Wanneer u Hallo storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="e3443-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![bericht wanneer het Hallo-storage-account verwijderen](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="e3443-152">Controleer de Hallo **schijf URL** tooidentify Hallo storage-account en Hallo VHD waardoor het Hallo-opslagaccount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e3443-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="e3443-153">Hallo in Hallo voorbeeld te volgen, tekenreeks vóór '. blob.core.windows.net ' hello opslagaccountnaam is en 'SCCM2012-2015-08-28.vhd' hello VHD-naam.</span><span class="sxs-lookup"><span data-stu-id="e3443-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="e3443-154">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3443-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="e3443-155">Selecteer op de Hub-menu Hallo **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="e3443-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="e3443-156">Ga toohello storage-account en selecteer vervolgens **Blobs** > **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="e3443-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Schermopname van het Hallo-portal, met het Hallo-opslagaccount en Hallo "VHD" container gemarkeerd](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="e3443-158">Zoek Hallo VHD die we eerder van Hallo schijf URL hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="e3443-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="e3443-159">Vervolgens bepalen welke VM maakt gebruik van Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="e3443-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="e3443-160">Meestal kunt u bepalen welk VM Hallo VHD door het controleren van de naam van de VHD Hallo bevat:</span><span class="sxs-lookup"><span data-stu-id="e3443-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="e3443-161">Virtuele machine in een model voor Resource Manager-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="e3443-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="e3443-162">OS-schijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="e3443-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="e3443-163">Gegevensschijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="e3443-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="e3443-164">Virtuele machine in het model van de ontwikkeling klassiek</span><span class="sxs-lookup"><span data-stu-id="e3443-164">VM in Classic development model</span></span>

   * <span data-ttu-id="e3443-165">OS-schijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="e3443-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="e3443-166">Gegevensschijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="e3443-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="e3443-167">Stap 2: Hallo lease uit Hallo VHD verwijderen</span><span class="sxs-lookup"><span data-stu-id="e3443-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="e3443-168">[Hallo lease verwijderen uit Hallo VHD](#remove-the-lease-from-the-vhd), en verwijder vervolgens Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3443-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="e3443-169">Wat is een lease?</span><span class="sxs-lookup"><span data-stu-id="e3443-169">What is a lease?</span></span>
<span data-ttu-id="e3443-170">Een lease is een vergrendeling die gebruikt toocontrol toegang tooa-blob (bijvoorbeeld een VHD worden kan).</span><span class="sxs-lookup"><span data-stu-id="e3443-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="e3443-171">Als de lease van een blob toegang alleen Hallo eigenaars van de lease Hallo Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="e3443-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="e3443-172">Een lease is belangrijk voor Hallo volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="e3443-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="e3443-173">Deze voorkomt dat gegevensbeschadiging als meerdere eigenaren toowrite toohello probeert hetzelfde deel van de Hallo blob op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="e3443-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="e3443-174">Dit voorkomt dat Hallo blob wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).</span><span class="sxs-lookup"><span data-stu-id="e3443-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="e3443-175">Dit voorkomt dat Hallo storage-account wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).</span><span class="sxs-lookup"><span data-stu-id="e3443-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="e3443-176">Hallo lease uit Hallo VHD verwijderen</span><span class="sxs-lookup"><span data-stu-id="e3443-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="e3443-177">Als een besturingssysteemschijf is Hallo VHD, moet u Hallo VM tooremove Hallo lease verwijderen:</span><span class="sxs-lookup"><span data-stu-id="e3443-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="e3443-178">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3443-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e3443-179">Op Hallo **Hub** selecteert u **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="e3443-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="e3443-180">Hallo VM waarin een lease op Hallo VHD selecteren.</span><span class="sxs-lookup"><span data-stu-id="e3443-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="e3443-181">Zorg ervoor dat er niets is actief Hallo virtuele machine, en dat u niet langer nodig Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e3443-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="e3443-182">Hallo boven aan het Hallo **VM details** blade Selecteer **verwijderen**, en klik vervolgens op **Ja** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e3443-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="e3443-183">Hallo VM moet worden verwijderd, maar Hallo VHD kan worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="e3443-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="e3443-184">Hallo VHD mag niet langer een lease hebben erop.</span><span class="sxs-lookup"><span data-stu-id="e3443-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="e3443-185">Het kan enkele minuten duren voordat Hallo lease toobe uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="e3443-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="e3443-186">tooverify die lease Hallo wordt uitgebracht, gaat u te**alle resources** > **Opslagaccountnaam** > **Blobs**  >  **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="e3443-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="e3443-187">In Hallo **Blob-eigenschappen** deelvenster, Hallo **Lease Status** waarde moet **ontgrendeld**.</span><span class="sxs-lookup"><span data-stu-id="e3443-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="e3443-188">Ontkoppel de Hallo VHD van Hallo VM tooremove Hallo lease als een gegevensschijf Hallo VHD is:</span><span class="sxs-lookup"><span data-stu-id="e3443-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="e3443-189">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3443-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e3443-190">Op Hallo **Hub** selecteert u **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="e3443-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="e3443-191">Hallo VM waarin een lease op Hallo VHD selecteren.</span><span class="sxs-lookup"><span data-stu-id="e3443-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="e3443-192">Selecteer **schijven** op Hallo **VM details** blade.</span><span class="sxs-lookup"><span data-stu-id="e3443-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="e3443-193">Hallo-gegevensschijf waarin een lease op Hallo VHD selecteren.</span><span class="sxs-lookup"><span data-stu-id="e3443-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="e3443-194">Kunt u bepalen welk VHD is gekoppeld Hallo schijf door te controleren URL Hallo Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="e3443-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="e3443-195">Bepalen met zekerheid dat niets Hallo gegevensschijf actief wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e3443-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="e3443-196">Klik op **Detach** op Hallo **schijf details** blade.</span><span class="sxs-lookup"><span data-stu-id="e3443-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="e3443-197">Hallo-schijf moet nu worden ontkoppeld van Hallo VM en Hallo VHD moet niet langer een lease erop.</span><span class="sxs-lookup"><span data-stu-id="e3443-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="e3443-198">Het kan enkele minuten duren voordat Hallo lease toobe uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="e3443-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="e3443-199">tooverify die lease Hallo is vrijgegeven, gaat u te**alle resources** > **Opslagaccountnaam** > **Blobs**  >  **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="e3443-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="e3443-200">In Hallo **Blob-eigenschappen** deelvenster, Hallo **Lease Status** waarde moet **ontgrendeld**.</span><span class="sxs-lookup"><span data-stu-id="e3443-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3443-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3443-201">Next steps</span></span>
* [<span data-ttu-id="e3443-202">Een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="e3443-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="e3443-203">Hoe toobreak Hallo lease van blob storage vergrendeld in Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e3443-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
