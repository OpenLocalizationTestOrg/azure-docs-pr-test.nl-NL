---
title: aaaUpload VHD-bestand met behulp van Microsoft Azure Storage Explorer van tooAzure DevTest Labs | Microsoft Docs
description: VHD-bestand toolab storage-account met behulp van Microsoft Azure Storage Explorer uploaden
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="84302-103">VHD-bestand toolab storage-account met behulp van Microsoft Azure Storage Explorer uploaden</span><span class="sxs-lookup"><span data-stu-id="84302-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="84302-104">VHD-bestanden kunnen gebruikte toocreate aangepaste installatiekopieën die gebruikt tooprovision virtuele machines zijn worden in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="84302-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="84302-105">Dit artikel wordt beschreven hoe toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload een VHD-bestand van tooa lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="84302-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="84302-106">Nadat u uw VHD-bestand hebt geüpload, Hallo [Vervolgstappen sectie](#next-steps) bevat enkele artikelen die aangeven hoe een aangepaste installatiekopie van Hallo toocreate VHD-bestand geüpload.</span><span class="sxs-lookup"><span data-stu-id="84302-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="84302-107">Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="84302-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="84302-108">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="84302-108">Step-by-step instructions</span></span>

<span data-ttu-id="84302-109">volgende stappen walk u via een VHD uploaden bestand tooDevTest Labs met Hallo [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="84302-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="84302-110">[Download en installeer de meest recente versie van Microsoft Azure Storage Explorer Hallo Hallo](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="84302-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="84302-111">Hallo-naam van de storage-account van het lab Hallo hello Azure-portal met opvragen:</span><span class="sxs-lookup"><span data-stu-id="84302-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="84302-112">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="84302-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="84302-113">Selecteer **meer services**, en selecteer vervolgens **DevTest Labs** uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="84302-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="84302-114">Selecteer de gewenste lab Hallo in lijst Hallo van labs.</span><span class="sxs-lookup"><span data-stu-id="84302-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="84302-115">Selecteer op Hallo van labblade, **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="84302-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="84302-116">Op Hallo lab **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="84302-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="84302-117">Op Hallo **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="84302-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="84302-118">Op Hallo **aangepaste installatiekopie** blade Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="84302-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="84302-119">Op Hallo **VHD** blade Selecteer **een VHD uploaden met PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="84302-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Virtuele harde schijf met behulp van PowerShell geüpload][0]
    
    1. <span data-ttu-id="84302-121">Hallo **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van toohello **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84302-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="84302-122">de eerste parameter Hallo (*bestemming*) opslagaccountnaam voor Hallo lab in de volgende indeling Hallo Hallo bevat:</span><span class="sxs-lookup"><span data-stu-id="84302-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="84302-123">https://<STORAGE-account-name>.BLOB.Core.Windows.NET/uploads/...</span><span class="sxs-lookup"><span data-stu-id="84302-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="84302-124">Noteer de opslagaccountnaam Hallo omdat deze wordt gebruikt in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="84302-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="84302-125">Verbinding maken met Azure-abonnementsrekening met Opslagverkenner tooan.</span><span class="sxs-lookup"><span data-stu-id="84302-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="84302-126">Opslagverkenner ondersteunt verschillende verbindingsopties.</span><span class="sxs-lookup"><span data-stu-id="84302-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="84302-127">Deze sectie ziet u verbindende tooa storage-account die is gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="84302-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="84302-128">toosee andere verbindingsopties ondersteund door Opslagverkenner hello, raadpleeg dan toohello artikel [aan de slag met Opslagverkenner](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="84302-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="84302-129">Open Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="84302-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="84302-130">Selecteer in Opslagverkenner **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="84302-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure-accountinstellingen][1]
    
    1. <span data-ttu-id="84302-132">Hallo linkerdeelvenster geeft Hallo hebt aangemeld bij Microsoft-accounts.</span><span class="sxs-lookup"><span data-stu-id="84302-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="84302-133">tooconnect tooanother account, selecteer **account toevoegen**, en volgt u Hallo dialoogvensters toosign met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="84302-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Een account toevoegen][2]
    
    1. <span data-ttu-id="84302-135">Zodra u zich hebt aangemeld met een Microsoft-account, het linkerdeelvenster Hallo gevuld met hello Azure-abonnementen die zijn gekoppeld aan dat account.</span><span class="sxs-lookup"><span data-stu-id="84302-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="84302-136">Selecteer hello Azure-abonnementen die u wilt toowork en selecteer vervolgens **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="84302-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="84302-137">(Selecteren **alle abonnementen** Schakelknoppen Hallo selectie van alle of geen van hello Azure-abonnementen vermeld.)</span><span class="sxs-lookup"><span data-stu-id="84302-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![Selecteer Azure-abonnementen][3]
    
    1. <span data-ttu-id="84302-139">Hallo linkerdeelvenster geeft Hallo storage-accounts die zijn gekoppeld aan Azure-abonnementen Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="84302-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![Geselecteerde Azure-abonnementen][4]

1. <span data-ttu-id="84302-141">Zoek de Hallo lab-opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="84302-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="84302-142">In Hallo Opslagverkenner linkerdeelvenster vinden en Hallo knooppunt voor hello Azure-abonnement dat eigenaar is van Hallo lab.</span><span class="sxs-lookup"><span data-stu-id="84302-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="84302-143">Vouw onder het knooppunt van het abonnement hello, **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="84302-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="84302-144">Vouw Hallo van storage account knooppunt tooreveal knooppunten van het testlab voor **Blob-Containers**, **bestandsshares**, **wachtrijen**, en **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="84302-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="84302-145">Vouw Hallo **Blob-Containers** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="84302-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="84302-146">Hallo uploads blob-container toodisplay van de inhoud in het rechterdeelvenster Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="84302-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![Directory uploaden][5]

1. <span data-ttu-id="84302-148">Hallo VHD-bestand met Opslagverkenner uploaden:</span><span class="sxs-lookup"><span data-stu-id="84302-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="84302-149">In Hallo Opslagverkenner rechterdeelvenster, ziet u een overzicht van de blobs in Hallo Hallo **uploadt** blob-container van het Hallo lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="84302-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="84302-150">Selecteer op de werkbalk van Hallo blob editor **uploaden**</span><span class="sxs-lookup"><span data-stu-id="84302-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![Knop uploaden][6]
    
    1. <span data-ttu-id="84302-152">Van Hallo **uploaden** vervolgkeuzelijst, selecteer **bestanden uploaden...** .</span><span class="sxs-lookup"><span data-stu-id="84302-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="84302-153">Op Hallo **bestanden uploaden** dialoogvenster, selecteer Hallo weglatingsteken.</span><span class="sxs-lookup"><span data-stu-id="84302-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![Bestand selecteren][8]  

    1. <span data-ttu-id="84302-155">Op Hallo **Selecteer bestanden tooupload** dialoogvenster Bladeren toohello gewenst VHD-bestand en selecteer vervolgens selecteert u het **Open**.</span><span class="sxs-lookup"><span data-stu-id="84302-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="84302-156">Wanneer geretourneerd toohello **bestanden uploaden** dialoogvenster wijziging **type Blob** te**pagina-Blob**.</span><span class="sxs-lookup"><span data-stu-id="84302-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="84302-157">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="84302-157">Select **Upload**.</span></span>

        ![Bestand selecteren][9]  
    
    1. <span data-ttu-id="84302-159">Hallo Opslagverkenner **activiteitenlogboek** deelvenster Hallo downloadstatus (samen met het uploaden van koppelingen toocancel Hallo) bevat.</span><span class="sxs-lookup"><span data-stu-id="84302-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="84302-160">Hallo-proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van de Hallo van Hallo VHD-bestand en de verbindingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="84302-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![Uploadbestand status][10]  

## <a name="next-steps"></a><span data-ttu-id="84302-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="84302-162">Next steps</span></span>

- [<span data-ttu-id="84302-163">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="84302-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="84302-164">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="84302-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
