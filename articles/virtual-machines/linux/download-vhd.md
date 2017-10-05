---
title: Downloaden van een VHD Linux van Azure | Microsoft Docs
description: Download een Linux-VHD met behulp van de Azure CLI en de Azure-portal.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 3eb88478b43f8e3a36ae04bf3703f238e8cb1f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="3853f-103">Downloaden van een VHD Linux van Azure</span><span class="sxs-lookup"><span data-stu-id="3853f-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="3853f-104">In dit artikel leert u hoe voor het downloaden van een [Linux virtuele harde schijf (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bestand van Azure met behulp van de Azure CLI en de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3853f-104">In this article, you learn how to download a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using the Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="3853f-105">Virtuele machines (VM's) in Azure gebruik [schijven](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) als gebruikt voor het opslaan van een besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="3853f-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="3853f-106">Alle Azure VM's hebben ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="3853f-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="3853f-107">De besturingssysteemschijf in eerste instantie wordt gemaakt van een installatiekopie en de schijf van het besturingssysteem en de installatiekopie zijn beide VHD's opgeslagen in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="3853f-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="3853f-108">Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3853f-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="3853f-109">Als u dit nog niet hebt gedaan, installeert u [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3853f-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="3853f-110">De virtuele machine stoppen</span><span class="sxs-lookup"><span data-stu-id="3853f-110">Stop the VM</span></span>

<span data-ttu-id="3853f-111">Een VHD kan niet worden gedownload vanuit Azure als deze is gekoppeld aan een actieve virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3853f-111">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="3853f-112">U moet de virtuele machine voor het downloaden van een VHD te stoppen.</span><span class="sxs-lookup"><span data-stu-id="3853f-112">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="3853f-113">Als u wilt gebruiken van een VHD als een [installatiekopie](tutorial-custom-images.md) als andere virtuele machines maken met nieuwe schijven, moet u inrichting ervan ongedaan en het besturingssysteem die is opgenomen in het bestand generaliseren en stop de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3853f-113">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you need to deprovision and generalize the operating system contained in the file and stop the VM.</span></span> <span data-ttu-id="3853f-114">Voor het gebruik van de VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, hoeft u alleen te stoppen en de VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3853f-114">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="3853f-115">De VHD gebruiken als een installatiekopie van een andere virtuele machines maken, voert u deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3853f-115">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1. <span data-ttu-id="3853f-116">SSH, de accountnaam en het openbare IP-adres van de virtuele machine verbinding maken met het en inrichting ervan ongedaan maakt het gebruik.</span><span class="sxs-lookup"><span data-stu-id="3853f-116">Use SSH, the account name, and the public IP address of the VM to connect to it and deprovision it.</span></span> <span data-ttu-id="3853f-117">De + parameter van de gebruiker de laatste ingerichte gebruiker-account, worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3853f-117">The +user parameter also removes the last provisioned user account.</span></span> <span data-ttu-id="3853f-118">Als u de referenties in voor de VM zijn bakken, laat u uit dit + parameter user.</span><span class="sxs-lookup"><span data-stu-id="3853f-118">If you are baking account credentials in to the VM, leave out this +user parameter.</span></span> <span data-ttu-id="3853f-119">Het volgende voorbeeld verwijdert u de laatste ingerichte gebruikersaccount:</span><span class="sxs-lookup"><span data-stu-id="3853f-119">The following example removes the last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="3853f-120">Aanmelden bij uw Azure-account met [az aanmelding](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3853f-120">Sign in to your Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="3853f-121">Stop en toewijzing van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3853f-121">Stop and deallocate the VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="3853f-122">De virtuele machine generalize.</span><span class="sxs-lookup"><span data-stu-id="3853f-122">Generalize the VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="3853f-123">Voor het gebruik van de VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, voert u deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="3853f-123">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="3853f-124">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3853f-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="3853f-125">Klik in het menu Hub op **Virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="3853f-125">On the Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="3853f-126">Selecteer de virtuele machine in de lijst.</span><span class="sxs-lookup"><span data-stu-id="3853f-126">Select the VM from the list.</span></span>
4.  <span data-ttu-id="3853f-127">Klik op de blade voor de virtuele machine op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="3853f-127">On the blade for the VM, click **Stop**.</span></span>

    ![VM stoppen](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="3853f-129">Genereren van SAS-URL</span><span class="sxs-lookup"><span data-stu-id="3853f-129">Generate SAS URL</span></span>

<span data-ttu-id="3853f-130">Voor het downloaden van het VHD-bestand, moet u voor het genereren van een [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="3853f-130">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="3853f-131">Wanneer de URL wordt gegenereerd, wordt een verlooptijd is toegewezen aan de URL.</span><span class="sxs-lookup"><span data-stu-id="3853f-131">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="3853f-132">Klik op het menu aan de blade voor de virtuele machine **schijven**.</span><span class="sxs-lookup"><span data-stu-id="3853f-132">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="3853f-133">De besturingssysteemschijf voor de virtuele machine selecteren en klik vervolgens op **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="3853f-133">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="3853f-134">Klik op **URL genereren**.</span><span class="sxs-lookup"><span data-stu-id="3853f-134">Click **Generate URL**.</span></span>

    ![URL genereren](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="3853f-136">VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="3853f-136">Download VHD</span></span>

1.  <span data-ttu-id="3853f-137">Klik onder de URL die is gegenereerd, Download het VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="3853f-137">Under the URL that was generated, click Download the VHD file.</span></span>

    ![VHD downloaden](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="3853f-139">Mogelijk moet u op **opslaan** in de browser om het downloaden te starten.</span><span class="sxs-lookup"><span data-stu-id="3853f-139">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="3853f-140">De standaardnaam voor het VHD-bestand is *abcd*.</span><span class="sxs-lookup"><span data-stu-id="3853f-140">The default name for the VHD file is *abcd*.</span></span>

    ![Klik op opslaan in de browser](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="3853f-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3853f-142">Next steps</span></span>

- <span data-ttu-id="3853f-143">Meer informatie over hoe [uploaden en Linux-VM te maken van aangepaste schijf met de Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3853f-143">Learn how to [upload and create a Linux VM from custom disk with the Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="3853f-144">[Beheren van Azure-schijven die de Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3853f-144">[Manage Azure disks the Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

