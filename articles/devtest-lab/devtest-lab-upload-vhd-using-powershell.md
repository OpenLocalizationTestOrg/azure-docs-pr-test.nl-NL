---
title: aaaUpload VHD-bestand tooAzure DevTest Labs met behulp van PowerShell | Microsoft Docs
description: Uploaden van de VHD-bestand toolab storage-account met behulp van PowerShell
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="e344d-103">Uploaden van de VHD-bestand toolab storage-account met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e344d-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="e344d-104">VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="e344d-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="e344d-105">Hallo doorlopen volgende stappen met behulp van PowerShell tooupload een VHD-bestand tooa lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e344d-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="e344d-106">Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="e344d-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="e344d-107">Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="e344d-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="e344d-108">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="e344d-108">Step-by-step instructions</span></span>

<span data-ttu-id="e344d-109">Hallo volgende stappen walk u via een VHD uploaden bestand tooAzure DevTest Labs met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e344d-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="e344d-110">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e344d-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="e344d-111">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="e344d-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="e344d-112">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="e344d-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="e344d-113">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="e344d-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="e344d-114">Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="e344d-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="e344d-115">Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="e344d-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="e344d-116">Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="e344d-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="e344d-117">Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e344d-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![Virtuele harde schijf met behulp van PowerShell geüpload](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="e344d-119">Op Hallo **een installatiekopie uploaden met PowerShell** blade, kopie Hallo gegenereerd PowerShell script tooa teksteditor.</span><span class="sxs-lookup"><span data-stu-id="e344d-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="e344d-120">Hallo wijzigen **LocalFilePath** parameter Hallo **Add-AzureVhd** cmdlet toopoint toohello locatie Hallo gewenste tooupload VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="e344d-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="e344d-121">Uitvoeren op een PowerShell-prompt Hallo **Add-AzureVhd** cmdlet (Hello gewijzigd **LocalFilePath** parameter).</span><span class="sxs-lookup"><span data-stu-id="e344d-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="e344d-122">Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="e344d-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e344d-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e344d-123">Next steps</span></span>

- [<span data-ttu-id="e344d-124">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e344d-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="e344d-125">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e344d-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
