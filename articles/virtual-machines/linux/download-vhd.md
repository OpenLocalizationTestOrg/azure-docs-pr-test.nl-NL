---
title: een VHD Linux van Azure aaaDownload | Microsoft Docs
description: Download een Linux-VHD met hello Azure CLI en hello Azure-portal.
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
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="2f8ca-103">Downloaden van een VHD Linux van Azure</span><span class="sxs-lookup"><span data-stu-id="2f8ca-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="2f8ca-104">In dit artikel leert u hoe toodownload een [Linux virtuele harde schijf (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) bestand van het gebruik van Azure hello Azure CLI en Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="2f8ca-105">Virtuele machines (VM's) in Azure gebruik [schijven](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) als een plaats toostore een besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="2f8ca-106">Alle Azure VM's hebben ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="2f8ca-107">Hallo-besturingssysteemschijf in eerste instantie wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn VHD's opgeslagen in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="2f8ca-108">Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="2f8ca-109">Als u dit nog niet hebt gedaan, installeert u [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="2f8ca-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="2f8ca-110">Hallo VM stoppen</span><span class="sxs-lookup"><span data-stu-id="2f8ca-110">Stop hello VM</span></span>

<span data-ttu-id="2f8ca-111">Een VHD kan niet worden gedownload van Azure als het wordt aangesloten tooa VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="2f8ca-112">U moet toostop Hallo VM toodownload een VHD.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="2f8ca-113">Als u een VHD als toouse wilt een [installatiekopie](tutorial-custom-images.md) toocreate andere VM's met nieuwe schijven u moet toodeprovision en generalize Hallo-besturingssysteem die is opgenomen in het Hallo-bestand en Hallo VM stoppen.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="2f8ca-114">toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf u alleen toostop moet en Hallo VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="2f8ca-115">toouse Hallo VHD als een installatiekopie toocreate andere virtuele machines, voert u deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2f8ca-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="2f8ca-116">SSH, Hallo-accountnaam en het openbare IP-adres Hallo van Hallo VM tooconnect tooit gebruiken en deze inrichting ervan ongedaan maakt.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="2f8ca-117">Hallo + gebruiker parameter Hallo laatste ingerichte gebruikersaccount, worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="2f8ca-118">Als u de accountreferenties in toohello VM zijn bakken, laat u uit dit + parameter user.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="2f8ca-119">Hallo volgende voorbeeld verwijdert u Hallo laatste ingerichte gebruikersaccount:</span><span class="sxs-lookup"><span data-stu-id="2f8ca-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="2f8ca-120">Meld u aan tooyour Azure-account met [az aanmelding](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2f8ca-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="2f8ca-121">Stop en Hallo VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="2f8ca-122">Hallo VM generalize.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="2f8ca-123">toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2f8ca-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="2f8ca-124">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f8ca-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="2f8ca-125">Klik op het menu Hub Hallo **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="2f8ca-126">Hallo VM in Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="2f8ca-127">Klik op de blade voor Hallo VM Hallo **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM stoppen](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="2f8ca-129">Genereren van SAS-URL</span><span class="sxs-lookup"><span data-stu-id="2f8ca-129">Generate SAS URL</span></span>

<span data-ttu-id="2f8ca-130">toodownload hello VHD-bestand, moet u toogenerate een [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="2f8ca-131">Als het Hallo-URL wordt gegenereerd, is een verlooptijd toohello URL toegewezen.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="2f8ca-132">Klik op het menu van Hallo blade voor Hallo VM Hallo **schijven**.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="2f8ca-133">Hallo besturingssysteemschijf voor Hallo VM selecteren en klik vervolgens op **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="2f8ca-134">Klik op **URL genereren**.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-134">Click **Generate URL**.</span></span>

    ![URL genereren](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="2f8ca-136">VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="2f8ca-136">Download VHD</span></span>

1.  <span data-ttu-id="2f8ca-137">Klik op downloaden Hallo VHD-bestand onder Hallo-URL die is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD downloaden](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="2f8ca-139">Mogelijk moet u tooclick **opslaan** in Hallo browser toostart Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="2f8ca-140">Hallo-standaardnaam voor Hallo VHD-bestand is *abcd*.</span><span class="sxs-lookup"><span data-stu-id="2f8ca-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Klik op opslaan in de browser Hallo](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="2f8ca-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f8ca-142">Next steps</span></span>

- <span data-ttu-id="2f8ca-143">Meer informatie over hoe te[uploaden en Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f8ca-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="2f8ca-144">[Beheren van Azure-schijven hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f8ca-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

