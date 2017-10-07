---
title: een Windows-VHD van Azure aaaDownload | Microsoft Docs
description: Download een Windows-VHD met hello Azure-portal.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="968d0-103">Een Windows-VHD downloaden van Azure</span><span class="sxs-lookup"><span data-stu-id="968d0-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="968d0-104">In dit artikel leert u hoe toodownload een [Windows virtuele harde schijf (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) bestand van het gebruik van Azure hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="968d0-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="968d0-105">Virtuele machines (VM's) in Azure gebruik [schijven](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) als een plaats toostore een besturingssysteem, toepassingen en gegevens.</span><span class="sxs-lookup"><span data-stu-id="968d0-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="968d0-106">Alle Azure VM's hebben ten minste twee schijven: de schijf van een Windows-besturingssysteem en een tijdelijke schijf.</span><span class="sxs-lookup"><span data-stu-id="968d0-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="968d0-107">Hallo-besturingssysteemschijf in eerste instantie wordt gemaakt van een installatiekopie en besturingssysteemschijf Hallo zowel Hallo installatiekopie zijn VHD's opgeslagen in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="968d0-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="968d0-108">Virtuele machines hebben ook een of meer gegevensschijven die ook als virtuele harde schijven zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="968d0-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="968d0-109">Hallo VM stoppen</span><span class="sxs-lookup"><span data-stu-id="968d0-109">Stop hello VM</span></span>

<span data-ttu-id="968d0-110">Een VHD kan niet worden gedownload van Azure als het wordt aangesloten tooa VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="968d0-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="968d0-111">U moet toostop Hallo VM toodownload een VHD.</span><span class="sxs-lookup"><span data-stu-id="968d0-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="968d0-112">Als u wilt dat toouse een VHD als een [installatiekopie](tutorial-custom-images.md) toocreate andere VM's met nieuwe schijven, gebruikt u [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize Hallo besturingssysteem Hallo-bestand bevat en vervolgens stoppen Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="968d0-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="968d0-113">toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf u alleen toostop moet en Hallo VM ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="968d0-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="968d0-114">toouse Hallo VHD als een installatiekopie toocreate andere virtuele machines, voert u deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="968d0-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="968d0-115">Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="968d0-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="968d0-116">[Verbinding maken met toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="968d0-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="968d0-117">Open op Hallo VM, Hallo-opdrachtpromptvenster als administrator.</span><span class="sxs-lookup"><span data-stu-id="968d0-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="968d0-118">Hallo directory ook wijzigen*%windir%\system32\sysprep* en sysprep.exe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="968d0-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="968d0-119">Selecteer Hallo hulpprogramma voor systeemvoorbereiding in het dialoogvenster **System Voer Out-of-Box Experience (OOBE)**, en zorg ervoor dat **Generalize** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="968d0-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="968d0-120">Selecteer in de opties voor afsluiten **afsluiten**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="968d0-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="968d0-121">toouse hello VHD als een schijf voor een nieuw exemplaar van een bestaande virtuele machine of de gegevensschijf, voer deze stappen uit:</span><span class="sxs-lookup"><span data-stu-id="968d0-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="968d0-122">Klik op Hallo Hub-menu van hello Azure-portal, **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="968d0-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="968d0-123">Hallo VM in Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="968d0-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="968d0-124">Klik op de blade voor Hallo VM Hallo **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="968d0-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![VM stoppen](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="968d0-126">Genereren van SAS-URL</span><span class="sxs-lookup"><span data-stu-id="968d0-126">Generate SAS URL</span></span>

<span data-ttu-id="968d0-127">toodownload hello VHD-bestand, moet u toogenerate een [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="968d0-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="968d0-128">Als het Hallo-URL wordt gegenereerd, is een verlooptijd toohello URL toegewezen.</span><span class="sxs-lookup"><span data-stu-id="968d0-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="968d0-129">Klik op het menu van Hallo blade voor Hallo VM Hallo **schijven**.</span><span class="sxs-lookup"><span data-stu-id="968d0-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="968d0-130">Hallo besturingssysteemschijf voor Hallo VM selecteren en klik vervolgens op **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="968d0-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="968d0-131">Hallo verlooptijd van Hallo-URL te ingesteld*36000*.</span><span class="sxs-lookup"><span data-stu-id="968d0-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="968d0-132">Klik op **URL genereren**.</span><span class="sxs-lookup"><span data-stu-id="968d0-132">Click **Generate URL**.</span></span>

    ![URL genereren](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="968d0-134">Hallo verlooptijd is verhoogd van Hallo standaard tooprovide voldoende tijd toodownload Hallo grote VHD-bestand voor een Windows Server-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="968d0-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="968d0-135">U kunt een VHD-bestand met de Hallo Windows Server-besturingssysteem tootake enkele uren toodownload, afhankelijk van uw verbinding verwachten.</span><span class="sxs-lookup"><span data-stu-id="968d0-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="968d0-136">Als u een VHD voor een gegevensschijf downloadt, is Hallo standaardtijd voldoende.</span><span class="sxs-lookup"><span data-stu-id="968d0-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="968d0-137">VHD downloaden</span><span class="sxs-lookup"><span data-stu-id="968d0-137">Download VHD</span></span>

1.  <span data-ttu-id="968d0-138">Klik op downloaden Hallo VHD-bestand onder Hallo-URL die is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="968d0-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![VHD downloaden](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="968d0-140">Mogelijk moet u tooclick **opslaan** in Hallo browser toostart Hallo downloaden.</span><span class="sxs-lookup"><span data-stu-id="968d0-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="968d0-141">Hallo-standaardnaam voor Hallo VHD-bestand is *abcd*.</span><span class="sxs-lookup"><span data-stu-id="968d0-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Klik op opslaan in de browser Hallo](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="968d0-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="968d0-143">Next steps</span></span>

- <span data-ttu-id="968d0-144">Meer informatie over hoe te[uploaden van een VHD-bestand tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="968d0-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="968d0-145">[Beheerde schijven maken van niet-beheerde schijven in een opslagaccount](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="968d0-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="968d0-146">[Azure-schijven met PowerShell beheren](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="968d0-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

