---
title: aaaCreate en het uploaden van een virtuele machine een installatiekopie met behulp van Powershell | Microsoft Docs
description: Informatie over toocreate en uploaden van een algemene Windows Server-installatiekopie (VHD) met het klassieke implementatiemodel Hallo en Azure Powershell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="0bf55-103">Maken en uploaden van een Windows Server-VHD tooAzure</span><span class="sxs-lookup"><span data-stu-id="0bf55-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="0bf55-104">Dit artikel laat zien hoe tooupload uw eigen gegeneraliseerde VM afbeelding als een virtuele harde schijf (VHD) zodat u toocreate virtuele machines kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0bf55-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="0bf55-105">Zie voor meer informatie over schijven en VHD's in Microsoft Azure [over schijven en virtuele harde schijven voor virtuele Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0bf55-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0bf55-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0bf55-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0bf55-107">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0bf55-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0bf55-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0bf55-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0bf55-109">U kunt ook [uploaden](../upload-generalized-managed.md) Hallo Resource Manager-model met een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0bf55-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bf55-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0bf55-110">Prerequisites</span></span>
<span data-ttu-id="0bf55-111">In dit artikel wordt ervan uitgegaan dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="0bf55-111">This article assumes you have:</span></span>

* <span data-ttu-id="0bf55-112">**Een Azure-abonnement** -als u niet hebt, kunt u [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="0bf55-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="0bf55-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -u hebt Hallo Microsoft Azure PowerShell-module geïnstalleerd en geconfigureerd toouse uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0bf55-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="0bf55-114">**A. VHD-bestand** - ondersteunde Windows-besturingssysteem die zijn opgeslagen in een VHD-bestand en de gekoppelde tooa virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0bf55-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="0bf55-115">Controleer de toosee als Hallo-serverfuncties op Hallo VHD uitgevoerd worden ondersteund door Sysprep.</span><span class="sxs-lookup"><span data-stu-id="0bf55-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="0bf55-116">Zie voor meer informatie [Sysprep-ondersteuning voor serverrollen](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="0bf55-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0bf55-117">Hallo VHDX-indeling wordt niet ondersteund in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf55-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="0bf55-118">U kunt converteren Hallo tooVHD schijfindeling met Hyper-V-beheer of Hallo [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bf55-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="0bf55-119">Zie voor meer informatie dit [blogbericht](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bf55-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="0bf55-120">Stap 1: Prep Hallo VHD</span><span class="sxs-lookup"><span data-stu-id="0bf55-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="0bf55-121">Voordat u Hallo VHD tooAzure uploadt, moet deze toobe gegeneraliseerd met Sysprep-hulpprogramma Hallo.</span><span class="sxs-lookup"><span data-stu-id="0bf55-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="0bf55-122">Hallo VHD toobe gebruikt als een afbeelding wordt voorbereid.</span><span class="sxs-lookup"><span data-stu-id="0bf55-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="0bf55-123">Zie voor meer informatie over Sysprep [hoe tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bf55-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="0bf55-124">Back-up Hallo VM voordat Sysprep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0bf55-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="0bf55-125">Van Hallo virtuele machine die Hallo besturingssysteem is geïnstalleerd voor Hallo na procedure te voltooien:</span><span class="sxs-lookup"><span data-stu-id="0bf55-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="0bf55-126">Meld u aan toohello-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="0bf55-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="0bf55-127">Open een opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="0bf55-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="0bf55-128">Hallo directory ook wijzigen**%windir%\system32\sysprep**, en voer vervolgens `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="0bf55-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Open een opdrachtpromptvenster](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="0bf55-130">Hallo **hulpprogramma voor systeemvoorbereiding** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0bf55-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Sysprep starten](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="0bf55-132">In Hallo **hulpprogramma voor systeemvoorbereiding**, selecteer **Voer System Out of Box Experience (OOBE)** en zorg ervoor dat **Generalize** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="0bf55-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="0bf55-133">In **afsluitopties**, selecteer **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="0bf55-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="0bf55-134">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bf55-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="0bf55-135">Stap 2: Een opslagaccount en een container maken</span><span class="sxs-lookup"><span data-stu-id="0bf55-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="0bf55-136">U moet een opslagaccount in Azure, zodat u een plaats tooupload Hallo .vhd-bestand hebt.</span><span class="sxs-lookup"><span data-stu-id="0bf55-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="0bf55-137">In deze stap ziet u hoe Hallo info toocreate een account of get moet u van een bestaande account.</span><span class="sxs-lookup"><span data-stu-id="0bf55-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="0bf55-138">Vervang Hallo variabelen in &lsaquo; haken &rsaquo; met uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="0bf55-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="0bf55-139">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="0bf55-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="0bf55-140">Stel uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0bf55-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="0bf55-141">Maak een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0bf55-141">Create a new storage account.</span></span> <span data-ttu-id="0bf55-142">Hallo-naam van Hallo storage-account moet uniek zijn, 3 tot 24 tekens.</span><span class="sxs-lookup"><span data-stu-id="0bf55-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="0bf55-143">Hallo-naam mag een combinatie van letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="0bf55-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="0bf55-144">U moet ook een locatie zoals 'Oost ons' toospecify</span><span class="sxs-lookup"><span data-stu-id="0bf55-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="0bf55-145">Nieuw opslagaccount Hallo als Hallo standaard instellen.</span><span class="sxs-lookup"><span data-stu-id="0bf55-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="0bf55-146">Maak een nieuwe container.</span><span class="sxs-lookup"><span data-stu-id="0bf55-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="0bf55-147">Stap 3: Hallo .vhd-bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="0bf55-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="0bf55-148">Gebruik Hallo [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload Hallo VHD.</span><span class="sxs-lookup"><span data-stu-id="0bf55-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="0bf55-149">Van hello Azure PowerShell-venster u in de vorige stap Hallo gebruikt type Hallo volgende opdracht en vervangt Hallo variabelen in &lsaquo; haken &rsaquo; met uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="0bf55-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="0bf55-150">Stap 4: Hallo afbeeldingenlijst tooyour van aangepaste installatiekopieën toevoegen</span><span class="sxs-lookup"><span data-stu-id="0bf55-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="0bf55-151">Gebruik Hallo [toevoegen AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello toohello lijst met afbeeldingen van aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="0bf55-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="0bf55-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bf55-152">Next steps</span></span>
<span data-ttu-id="0bf55-153">U kunt nu [maken van een aangepaste VM](createportal.md) u geüpload met behulp van Hallo installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="0bf55-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
