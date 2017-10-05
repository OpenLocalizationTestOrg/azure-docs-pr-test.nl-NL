---
title: Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen | Microsoft Docs
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
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="87b78-103">Fouten oplossen wanneer u Azure storage-accounts, containers of VHD's verwijderen</span><span class="sxs-lookup"><span data-stu-id="87b78-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="87b78-104">U kunt fouten ontvangt wanneer u probeert te verwijderen van een Azure storage-account, container of virtuele harde schijf (VHD) in de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87b78-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="87b78-105">Dit artikel bevat richtlijnen voor probleemoplossing om u te helpen bij het oplossen van het probleem in een Azure Resource Manager-implementatie.</span><span class="sxs-lookup"><span data-stu-id="87b78-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="87b78-106">Als dit artikel niet van toepassing uw Azure probleem, gaat u naar de Azure-forums op [MSDN en Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="87b78-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="87b78-107">U kunt het probleem op deze forums of boeken @AzureSupport op Twitter.</span><span class="sxs-lookup"><span data-stu-id="87b78-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="87b78-108">U kunt ook een ondersteuning van Azure-aanvraag indienen door te selecteren **ondersteuning krijgen** op de [ondersteuning van Azure](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="87b78-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="87b78-109">Symptomen</span><span class="sxs-lookup"><span data-stu-id="87b78-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="87b78-110">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="87b78-110">Scenario 1</span></span>
<span data-ttu-id="87b78-111">Wanneer u probeert te verwijderen van een VHD in een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="87b78-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="87b78-112">**Verwijderen van blob 'vhds/BlobName.vhd' is mislukt. Fout: Er is momenteel een lease op de blob en geen lease-ID is opgegeven in de aanvraag.**</span><span class="sxs-lookup"><span data-stu-id="87b78-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="87b78-113">Dit probleem kan optreden omdat een virtuele machine (VM) een lease op de VHD die u probeert heeft te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="87b78-114">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="87b78-114">Scenario 2</span></span>
<span data-ttu-id="87b78-115">Wanneer u probeert te verwijderen van een container in een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="87b78-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="87b78-116">**Storage-container 'VHD's ' verwijderen is mislukt. Fout: Er is momenteel een lease voor de container en geen lease-ID is opgegeven in de aanvraag.**</span><span class="sxs-lookup"><span data-stu-id="87b78-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="87b78-117">Dit probleem kan optreden omdat de container is een VHD die in de status van de lease is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="87b78-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="87b78-118">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="87b78-118">Scenario 3</span></span>
<span data-ttu-id="87b78-119">Wanneer u probeert te verwijderen van een opslagaccount in de implementatie van een Resource Manager, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="87b78-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="87b78-120">**Storage-account 'StorageAccountName' verwijderen is mislukt. Fout: Het storage-account kan niet worden verwijderd omdat de artefacten die in gebruik.**</span><span class="sxs-lookup"><span data-stu-id="87b78-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="87b78-121">Dit probleem kan optreden omdat het opslagaccount bevat een VHD met de status van de lease.</span><span class="sxs-lookup"><span data-stu-id="87b78-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="87b78-122">Oplossing</span><span class="sxs-lookup"><span data-stu-id="87b78-122">Solution</span></span> 
<span data-ttu-id="87b78-123">Om deze problemen wilt oplossen, moet u de VHD die de fout veroorzaakt en de bijbehorende virtuele machine vaststellen.</span><span class="sxs-lookup"><span data-stu-id="87b78-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="87b78-124">Vervolgens de VHD van de virtuele machine (voor gegevensschijven) ontkoppelen of verwijderen van de virtuele machine die van de VHD (voor OS-schijven gebruikmaakt).</span><span class="sxs-lookup"><span data-stu-id="87b78-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="87b78-125">Hiermee verwijdert u de lease van de VHD te kunnen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="87b78-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="87b78-126">U doet dit door een van de volgende methoden te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="87b78-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="87b78-127">Methode 1 - gebruik Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="87b78-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="87b78-128">Stap 1 identificeren de VHD die voorkomen dat het storage-account wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="87b78-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="87b78-129">Wanneer u het storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals het volgende:</span><span class="sxs-lookup"><span data-stu-id="87b78-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Wanneer het verwijderen van opslagaccount](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="87b78-131">Controleer de **schijf URL** voor het identificeren van de opslag-account en de VHD die voorkomt u dat het opslagaccount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="87b78-132">In het volgende voorbeeld wordt de tekenreeks voor '. blob.core.windows.net ' is de opslagaccountnaam en 'SCCM2012-2015-08-28.vhd' is de naam van de VHD.</span><span class="sxs-lookup"><span data-stu-id="87b78-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="87b78-133">Stap 2 de VHD verwijderen met behulp van Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="87b78-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="87b78-134">Download en installeer de nieuwste versie van [Azure Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="87b78-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="87b78-135">Dit hulpprogramma is een zelfstandige app van Microsoft waarmee u eenvoudig werken met Azure Storage-gegevens op Windows, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="87b78-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="87b78-136">Open Azure Storage Explorer, selecteer</span><span class="sxs-lookup"><span data-stu-id="87b78-136">Open Azure Storage Explorer, select</span></span> ![pictogram](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="87b78-138">Selecteer uw Azure-omgeving in de linkerbalk en vervolgens weer aanmelden.</span><span class="sxs-lookup"><span data-stu-id="87b78-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="87b78-139">Selecteer alle abonnementen of het abonnement dat u het opslagaccount bevat die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![Abonnement toevoegen](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="87b78-141">Ga naar het opslagaccount dat we van de URL van de schijf eerdere, selecteer verkregen de **Blob-Containers** > **VHD's** en zoekt u de VHD die voorkomt u dat het opslagaccount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="87b78-142">Als de VHD wordt gevonden, controleert u de **VM-naam** kolom vinden van de virtuele machine die van deze VHD gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="87b78-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Controleer de virtuele machine](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="87b78-144">De lease van de VHD verwijderen met behulp van Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="87b78-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="87b78-145">Zie voor meer informatie [verwijderen van de lease van de VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="87b78-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="87b78-146">Ga naar de Azure Storage Explorer, met de rechtermuisknop op de VHD en selecteer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="87b78-147">Hiermee wordt het opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="87b78-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="87b78-148">Methode 2: gebruik Azure-portal</span><span class="sxs-lookup"><span data-stu-id="87b78-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="87b78-149">Stap 1: De VHD die voorkomen dat wordt verwijderd van het opslagaccount identificeren</span><span class="sxs-lookup"><span data-stu-id="87b78-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="87b78-150">Wanneer u het storage-account verwijdert, ontvangt u een dialoogvenster weergegeven zoals het volgende:</span><span class="sxs-lookup"><span data-stu-id="87b78-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Wanneer het verwijderen van opslagaccount](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="87b78-152">Controleer de **schijf URL** voor het identificeren van de opslag-account en de VHD die voorkomt u dat het opslagaccount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="87b78-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="87b78-153">In het volgende voorbeeld wordt de tekenreeks voor '. blob.core.windows.net ' is de opslagaccountnaam en 'SCCM2012-2015-08-28.vhd' is de naam van de VHD.</span><span class="sxs-lookup"><span data-stu-id="87b78-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="87b78-154">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87b78-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="87b78-155">Selecteer in het menu Hub **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="87b78-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="87b78-156">Ga naar het storage-account en selecteer vervolgens **Blobs** > **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="87b78-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Schermafbeelding van de portal met de storage-account en de container 'VHD's ' is gemarkeerd](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="87b78-158">Zoek de VHD die we eerder van de URL van de schijf hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="87b78-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="87b78-159">Vervolgens bepalen welke VM maakt gebruik van de VHD.</span><span class="sxs-lookup"><span data-stu-id="87b78-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="87b78-160">Meestal kunt u bepalen welk VM bevat de VHD door het controleren van de naam van de VHD:</span><span class="sxs-lookup"><span data-stu-id="87b78-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="87b78-161">Virtuele machine in een model voor Resource Manager-ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="87b78-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="87b78-162">OS-schijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="87b78-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="87b78-163">Gegevensschijven in het algemeen volgt u deze naamconventie: VMName-jjjj-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="87b78-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="87b78-164">Virtuele machine in het model van de ontwikkeling klassiek</span><span class="sxs-lookup"><span data-stu-id="87b78-164">VM in Classic development model</span></span>

   * <span data-ttu-id="87b78-165">OS-schijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="87b78-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="87b78-166">Gegevensschijven in het algemeen volgt u deze naamconventie: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="87b78-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="87b78-167">Stap 2: De lease van de VHD verwijderen</span><span class="sxs-lookup"><span data-stu-id="87b78-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="87b78-168">[Verwijderen van de lease van de VHD](#remove-the-lease-from-the-vhd), en verwijder vervolgens het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="87b78-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="87b78-169">Wat is een lease?</span><span class="sxs-lookup"><span data-stu-id="87b78-169">What is a lease?</span></span>
<span data-ttu-id="87b78-170">Een lease is een vergrendeling die kan worden gebruikt voor het toegangsbeheer naar een blob-(bijvoorbeeld een VHD).</span><span class="sxs-lookup"><span data-stu-id="87b78-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="87b78-171">Wanneer de lease van een blob heeft alleen de eigenaren van de lease toegang tot de blob.</span><span class="sxs-lookup"><span data-stu-id="87b78-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="87b78-172">Een lease is het belangrijk om de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="87b78-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="87b78-173">Als meerdere eigenaren probeert te schrijven naar hetzelfde deel van de blob op hetzelfde moment kunnen beschadigde gegevens.</span><span class="sxs-lookup"><span data-stu-id="87b78-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="87b78-174">Dit voorkomt dat de blob wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).</span><span class="sxs-lookup"><span data-stu-id="87b78-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="87b78-175">Dit voorkomt dat het storage-account wordt verwijderd als er iets actief gebruikt wordt (bijvoorbeeld een VM).</span><span class="sxs-lookup"><span data-stu-id="87b78-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="87b78-176">Verwijderen van de lease van de VHD</span><span class="sxs-lookup"><span data-stu-id="87b78-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="87b78-177">Als de VHD een besturingssysteemschijf is, moet u de virtuele machine als u wilt verwijderen van de lease verwijderen:</span><span class="sxs-lookup"><span data-stu-id="87b78-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="87b78-178">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87b78-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87b78-179">Op de **Hub** selecteert u **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="87b78-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="87b78-180">Selecteer de virtuele machine die een lease op de VHD bevat.</span><span class="sxs-lookup"><span data-stu-id="87b78-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="87b78-181">Zorg ervoor dat er niets is actief met behulp van de virtuele machine, en dat u de virtuele machine niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="87b78-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="87b78-182">Aan de bovenkant van de **VM details** blade Selecteer **verwijderen**, en klik vervolgens op **Ja** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="87b78-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="87b78-183">De virtuele machine moet worden verwijderd, maar de VHD kan worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="87b78-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="87b78-184">De VHD moet niet langer een lease hebben erop.</span><span class="sxs-lookup"><span data-stu-id="87b78-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="87b78-185">Het kan enkele minuten duren voordat de lease worden vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="87b78-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="87b78-186">Om te bevestigen dat de lease is uitgebracht, gaat u naar **alle resources** > **Opslagaccountnaam** > **Blobs** > **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="87b78-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="87b78-187">In de **Blob-eigenschappen** deelvenster de **Lease Status** waarde moet **ontgrendeld**.</span><span class="sxs-lookup"><span data-stu-id="87b78-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="87b78-188">Als de VHD een gegevensschijf is, ontkoppel het VHD van de virtuele machine te verwijderen van de lease:</span><span class="sxs-lookup"><span data-stu-id="87b78-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="87b78-189">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87b78-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87b78-190">Op de **Hub** selecteert u **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="87b78-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="87b78-191">Selecteer de virtuele machine die een lease op de VHD bevat.</span><span class="sxs-lookup"><span data-stu-id="87b78-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="87b78-192">Selecteer **schijven** op de **VM details** blade.</span><span class="sxs-lookup"><span data-stu-id="87b78-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="87b78-193">Selecteer de gegevensschijf waarin een lease op de VHD.</span><span class="sxs-lookup"><span data-stu-id="87b78-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="87b78-194">Kunt u bepalen welk VHD is gekoppeld de schijf door het controleren van de URL van de VHD.</span><span class="sxs-lookup"><span data-stu-id="87b78-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="87b78-195">Bepalen met zekerheid dat er niets is actief met behulp van de gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="87b78-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="87b78-196">Klik op **Detach** op de **schijf details** blade.</span><span class="sxs-lookup"><span data-stu-id="87b78-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="87b78-197">De schijf moet nu worden ontkoppeld van de virtuele machine en de VHD mag niet langer een lease erop.</span><span class="sxs-lookup"><span data-stu-id="87b78-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="87b78-198">Het kan enkele minuten duren voordat de lease worden vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="87b78-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="87b78-199">Om te bevestigen dat de lease is vrijgegeven, gaat u naar **alle resources** > **Opslagaccountnaam** > **Blobs** > **VHD's**.</span><span class="sxs-lookup"><span data-stu-id="87b78-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="87b78-200">In de **Blob-eigenschappen** deelvenster de **Lease Status** waarde moet **ontgrendeld**.</span><span class="sxs-lookup"><span data-stu-id="87b78-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87b78-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87b78-201">Next steps</span></span>
* [<span data-ttu-id="87b78-202">Een opslagaccount verwijderen</span><span class="sxs-lookup"><span data-stu-id="87b78-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="87b78-203">Hoe u de vergrendelde lease van blob storage in Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="87b78-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
