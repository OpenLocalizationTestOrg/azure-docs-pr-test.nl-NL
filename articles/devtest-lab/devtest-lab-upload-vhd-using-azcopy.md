---
title: VHD-bestand uploaden naar Azure DevTest Labs met behulp van AzCopy | Microsoft Docs
description: VHD-bestand uploaden naar het lab-opslagaccount met behulp van AzCopy
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="79859-103">VHD-bestand uploaden naar het lab-opslagaccount met behulp van AzCopy</span><span class="sxs-lookup"><span data-stu-id="79859-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="79859-104">In Azure DevTest Labs kunnen VHD-bestanden worden gebruikt voor het maken van aangepaste installatiekopieën die worden gebruikt voor het inrichten van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="79859-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="79859-105">De volgende stappen doorlopen die u met het AzCopy-opdrachtregelprogramma een VHD-bestand uploaden naar een lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="79859-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="79859-106">Nadat u uw VHD-bestand hebt geüpload de [Vervolgstappen sectie](#next-steps) geeft een lijst van sommige artikelen die laten zien hoe u een aangepaste installatiekopie van het geüploade VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="79859-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="79859-107">Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="79859-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="79859-108">AzCopy is een alleen-Windows-opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="79859-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="79859-109">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="79859-109">Step-by-step instructions</span></span>

<span data-ttu-id="79859-110">De volgende stappen helpt u bij het uploaden van een VHD-bestand voor het gebruik van Azure DevTest Labs [AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="79859-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="79859-111">Haal de naam van het lab-opslagaccount met de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="79859-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="79859-112">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="79859-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="79859-113">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="79859-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="79859-114">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="79859-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="79859-115">Selecteer op de labblade **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="79859-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="79859-116">Op de testomgeving **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="79859-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="79859-117">Op de **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="79859-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="79859-118">Op de **aangepaste installatiekopie** blade Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="79859-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="79859-119">Op de **VHD** blade Selecteer **een VHD uploaden met PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="79859-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Virtuele harde schijf met behulp van PowerShell geüpload](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="79859-121">De **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van de **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="79859-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="79859-122">De eerste parameter (*bestemming*) bevat de URI voor een blob-container (*uploadt*) in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="79859-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="79859-123">Noteer de volledige URI omdat deze wordt gebruikt in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="79859-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="79859-124">Het VHD-bestand met behulp van AzCopy uploaden:</span><span class="sxs-lookup"><span data-stu-id="79859-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="79859-125">[Download en installeer de nieuwste versie van AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="79859-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="79859-126">Open een opdrachtvenster en navigeer naar de installatiemap van AzCopy.</span><span class="sxs-lookup"><span data-stu-id="79859-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="79859-127">U kunt eventueel de installatielocatie van AzCopy toevoegen aan het systeempad.</span><span class="sxs-lookup"><span data-stu-id="79859-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="79859-128">AzCopy is standaard geïnstalleerd op de volgende map:</span><span class="sxs-lookup"><span data-stu-id="79859-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="79859-129">Met behulp van de storage-account sleutel en de blob-container URI, voer de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="79859-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="79859-130">De *vhdFileName* waarde moet tussen aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="79859-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="79859-131">Het proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van het VHD-bestand en de verbindingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="79859-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="79859-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79859-132">Next steps</span></span>

- [<span data-ttu-id="79859-133">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="79859-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="79859-134">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="79859-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)