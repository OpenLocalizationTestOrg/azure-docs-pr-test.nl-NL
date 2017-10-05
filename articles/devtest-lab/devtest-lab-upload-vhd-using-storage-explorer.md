---
title: VHD-bestand uploaden naar Azure DevTest Labs met behulp van Microsoft Azure Storage Explorer | Microsoft Docs
description: VHD-bestand uploaden naar het lab storage-account met behulp van Microsoft Azure Storage Explorer
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
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="9f12e-103">VHD-bestand uploaden naar het lab storage-account met behulp van Microsoft Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="9f12e-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="9f12e-104">In Azure DevTest Labs kunnen VHD-bestanden worden gebruikt voor het maken van aangepaste installatiekopieën die worden gebruikt voor het inrichten van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9f12e-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="9f12e-105">In dit artikel laat zien hoe u [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) een VHD-bestand uploaden naar een lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9f12e-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="9f12e-106">Nadat u uw VHD-bestand hebt geüpload de [Vervolgstappen sectie](#next-steps) geeft een lijst van sommige artikelen die laten zien hoe u een aangepaste installatiekopie van het geüploade VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="9f12e-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="9f12e-107">Zie voor meer informatie over schijven en VHD's in Azure [over schijven en virtuele harde schijven voor virtuele machines](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="9f12e-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="9f12e-108">Stapsgewijze instructies</span><span class="sxs-lookup"><span data-stu-id="9f12e-108">Step-by-step instructions</span></span>

<span data-ttu-id="9f12e-109">De volgende stappen helpt u bij het uploaden van een VHD-bestand voor het gebruik van DevTest Labs [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9f12e-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="9f12e-110">[Download en installeer de nieuwste versie van Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="9f12e-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="9f12e-111">Haal de naam van het lab-opslagaccount met de Azure portal:</span><span class="sxs-lookup"><span data-stu-id="9f12e-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="9f12e-112">Meld u aan bij [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="9f12e-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="9f12e-113">Selecteer **Meer services** en selecteer in de lijst vervolgens **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="9f12e-114">Selecteer de gewenste testomgeving uit de lijst van labs.</span><span class="sxs-lookup"><span data-stu-id="9f12e-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="9f12e-115">Selecteer op de labblade **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="9f12e-116">Op de testomgeving **configuratie** blade Selecteer **aangepaste installatiekopieën (VHD's)**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="9f12e-117">Op de **aangepaste installatiekopieën** blade Selecteer **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="9f12e-118">Op de **aangepaste installatiekopie** blade Selecteer **VHD**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="9f12e-119">Op de **VHD** blade Selecteer **een VHD uploaden met PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![Virtuele harde schijf met behulp van PowerShell geüpload][0]
    
    1. <span data-ttu-id="9f12e-121">De **een installatiekopie uploaden met PowerShell** blade wordt een aanroep van de **Add-AzureVhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f12e-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="9f12e-122">De eerste parameter (*bestemming*) bevat de naam van het opslagaccount voor de testomgeving in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="9f12e-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="9f12e-123">https://<STORAGE-account-name>.BLOB.Core.Windows.NET/uploads/...</span><span class="sxs-lookup"><span data-stu-id="9f12e-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="9f12e-124">Noteer de opslagaccountnaam omdat deze wordt gebruikt in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="9f12e-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="9f12e-125">Verbinding maken met een Azure-abonnementsrekening met Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="9f12e-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="9f12e-126">Opslagverkenner ondersteunt verschillende verbindingsopties.</span><span class="sxs-lookup"><span data-stu-id="9f12e-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="9f12e-127">Deze sectie ziet u verbinding maakt met een opslagaccount die is gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9f12e-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="9f12e-128">Overzicht van de andere verbindingsopties ondersteund door Opslagverkenner verwijzen naar het artikel [aan de slag met Opslagverkenner](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9f12e-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="9f12e-129">Open Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="9f12e-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="9f12e-130">Selecteer in Opslagverkenner **Azure Accountinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure-accountinstellingen][1]
    
    1. <span data-ttu-id="9f12e-132">Het linkerdeelvenster geeft de Microsoft-accounts die u hebt aangemeld.</span><span class="sxs-lookup"><span data-stu-id="9f12e-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="9f12e-133">Selecteer **Een account toevoegen** om verbinding te maken met een ander account en volg de dialoogvensters om aan te melden met een Microsoft-account dat is gekoppeld aan ten minste één actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9f12e-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![Een account toevoegen][2]
    
    1. <span data-ttu-id="9f12e-135">Wanneer u bent aangemeld met een Microsoft-account, worden in het linkerdeelvenster de Azure-abonnementen weergegeven die aan dat account zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="9f12e-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="9f12e-136">Selecteer de Azure-abonnementen waarmee u wilt werken en selecteer vervolgens **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="9f12e-137">(Selecteren **alle abonnementen** Hiermee wordt de selectie van alle of geen van de vermelde Azure-abonnementen.)</span><span class="sxs-lookup"><span data-stu-id="9f12e-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![Selecteer Azure-abonnementen][3]
    
    1. <span data-ttu-id="9f12e-139">In het linkerdeelvenster worden de opslagaccounts weergegeven die aan de geselecteerde Azure-abonnementen zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="9f12e-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![Geselecteerde Azure-abonnementen][4]

1. <span data-ttu-id="9f12e-141">Zoek in het lab-opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="9f12e-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="9f12e-142">Zoek in het linkerdeelvenster van Opslagverkenner en vouw het knooppunt voor de Azure-abonnement dat eigenaar is van de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="9f12e-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="9f12e-143">Vouw onder het knooppunt van het abonnement, **Opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="9f12e-144">De testomgeving storage accountknooppunt uitvouwen om te onthullen knooppunten voor **Blob-Containers**, **bestandsshares**, **wachtrijen**, en **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="9f12e-145">Vouw de **Blob-Containers** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9f12e-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="9f12e-146">Selecteer de blob-container uploads aan de inhoud in het rechterdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="9f12e-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![Directory uploaden][5]

1. <span data-ttu-id="9f12e-148">Het VHD-bestand met Opslagverkenner uploaden:</span><span class="sxs-lookup"><span data-stu-id="9f12e-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="9f12e-149">In het rechterdeelvenster Opslagverkenner ziet u een overzicht van de blobs in de **uploadt** blob-container van het lab-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9f12e-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="9f12e-150">Selecteer op de werkbalk van de editor blob **uploaden**</span><span class="sxs-lookup"><span data-stu-id="9f12e-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![Knop uploaden][6]
    
    1. <span data-ttu-id="9f12e-152">Van de **uploaden** vervolgkeuzelijst, selecteer **bestanden uploaden...** .</span><span class="sxs-lookup"><span data-stu-id="9f12e-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="9f12e-153">Op de **bestanden uploaden** dialoogvenster, selecteer het weglatingsteken.</span><span class="sxs-lookup"><span data-stu-id="9f12e-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![Bestand selecteren][8]  

    1. <span data-ttu-id="9f12e-155">Op de **Selecteer bestanden uploaden** dialoogvenster, blader naar het gewenste VHD-bestand en selecteer vervolgens selecteert u het **Open**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="9f12e-156">Wanneer u keert terug naar de **bestanden uploaden** dialoogvenster wijziging **Blob-type** naar **pagina-Blob**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="9f12e-157">Selecteer **Uploaden**.</span><span class="sxs-lookup"><span data-stu-id="9f12e-157">Select **Upload**.</span></span>

        ![Bestand selecteren][9]  
    
    1. <span data-ttu-id="9f12e-159">Opslagverkenner **activiteitenlogboek** deelvenster toont de downloadstatus (samen met koppelingen naar de upload geannuleerd).</span><span class="sxs-lookup"><span data-stu-id="9f12e-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="9f12e-160">Het proces van het uploaden van een VHD-bestand kan worden langdurige, afhankelijk van de grootte van het VHD-bestand en de verbindingssnelheid.</span><span class="sxs-lookup"><span data-stu-id="9f12e-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![Uploadbestand status][10]  

## <a name="next-steps"></a><span data-ttu-id="9f12e-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f12e-162">Next steps</span></span>

- [<span data-ttu-id="9f12e-163">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met de Azure portal</span><span class="sxs-lookup"><span data-stu-id="9f12e-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="9f12e-164">Een aangepaste installatiekopie maken in Azure DevTest Labs van een VHD-bestand met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f12e-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
