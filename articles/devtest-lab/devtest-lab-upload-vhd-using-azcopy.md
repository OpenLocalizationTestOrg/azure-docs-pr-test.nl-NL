---
title: aaaUpload VHD-bestand met behulp van AzCopy van tooAzure DevTest Labs | Microsoft Docs
description: Uploaden van de VHD-bestand toolab storage-account met behulp van AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="140d1-103">Uploaden van de VHD-bestand toolab storage-account met behulp van AzCopy</span><span class="sxs-lookup"><span data-stu-id="140d1-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="140d1-104">VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="140d1-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="140d1-105">Hallo stappen doorlopen met behulp van Hallo AzCopy-opdrachtregelprogramma tooupload een VHD-bestand tooa lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="140d1-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="140d1-106">Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="140d1-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="140d1-107">Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="140d1-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="140d1-108">AzCopy is een alleen-Windows-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="140d1-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="140d1-109">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="140d1-109">Step-by-step instructions</span></span>

<span data-ttu-id="140d1-110">volgende stappen walk u via een VHD uploaden bestand tooAzure DevTest Labs met Hallo [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="140d1-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="140d1-111">Hallo-naam van de storage-account van het lab Hallo hello Azure-portal met opvragen:</span><span class="sxs-lookup"><span data-stu-id="140d1-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="140d1-112">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="140d1-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="140d1-113">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="140d1-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="140d1-114">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="140d1-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="140d1-115">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="140d1-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="140d1-116">Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="140d1-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="140d1-117">Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="140d1-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="140d1-118">Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="140d1-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="140d1-119">Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="140d1-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Virtuele harde schijf met behulp van PowerShell geüpload](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="140d1-121">Hallo **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="140d1-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="140d1-122">de eerste parameter Hallo (*bestemming*) bevat Hallo URI voor een blob-container (*uploadt*) in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="140d1-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="140d1-123">Noteer Hallo volledige URI omdat deze wordt gebruikt in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="140d1-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="140d1-124">Hallo VHD-bestand met behulp van AzCopy uploaden:</span><span class="sxs-lookup"><span data-stu-id="140d1-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="140d1-125">[Download en installeer de meest recente versie van AzCopy hello](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="140d1-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="140d1-126">Open een opdrachtvenster en navigeer toohello AzCopy-installatiemap.</span><span class="sxs-lookup"><span data-stu-id="140d1-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="140d1-127">U kunt eventueel Hallo AzCopy locatie tooyour system installatiepad toevoegen.</span><span class="sxs-lookup"><span data-stu-id="140d1-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="140d1-128">AzCopy is standaard geïnstalleerd toohello directory te volgen:</span><span class="sxs-lookup"><span data-stu-id="140d1-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="140d1-129">Hallo volgende opdracht achter de opdrachtprompt Hallo Hallo storage account sleutel en de blob-container URI gebruikt, worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="140d1-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="140d1-130">Hallo *vhdFileName* waarde moet toobe tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="140d1-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="140d1-131">Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="140d1-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="140d1-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="140d1-132">Next steps</span></span>

- [<span data-ttu-id="140d1-133">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="140d1-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="140d1-134">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="140d1-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)