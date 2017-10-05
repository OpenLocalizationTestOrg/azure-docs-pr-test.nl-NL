---
title: Azure File Storage beheren vanuit Azure Portal | Microsoft Docs
description: Meer informatie over het gebruik van Azure Portal om Azure File Storage te beheren.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: d5ffa7cff0a31e36f5a96aaa4b2d477fa39333fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="14aa3-103">Azure File Storage gebruiken vanuit Azure Portal</span><span class="sxs-lookup"><span data-stu-id="14aa3-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="14aa3-104">[Azure Portal](https://portal.azure.com) biedt een gebruikersinterface voor het beheren van Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="14aa3-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="14aa3-105">U kunt de volgende acties uitvoeren vanuit de webbrowser:</span><span class="sxs-lookup"><span data-stu-id="14aa3-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="14aa3-106">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="14aa3-106">Create a File Share</span></span>
* <span data-ttu-id="14aa3-107">Bestanden uploaden naar en downloaden van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="14aa3-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="14aa3-108">Het werkelijke gebruik van elke bestandsshare controleren.</span><span class="sxs-lookup"><span data-stu-id="14aa3-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="14aa3-109">Het quotum van de sharegrootte aanpassen.</span><span class="sxs-lookup"><span data-stu-id="14aa3-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="14aa3-110">De te gebruiken koppelingsopdrachten kopiëren om uw bestandsshare te koppelen vanuit een Windows- of Linux-client.</span><span class="sxs-lookup"><span data-stu-id="14aa3-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="14aa3-111">Bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="14aa3-111">Create file share</span></span>
1. <span data-ttu-id="14aa3-112">Meld u aan bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="14aa3-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="14aa3-113">Klik in het navigatiemenu op **Opslagaccounts** of **Opslagaccounts (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="14aa3-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Schermafbeelding van het maken van een bestandsshare in de portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="14aa3-115">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="14aa3-115">Choose your storage account.</span></span>

    ![Schermafbeelding van het maken van een bestandsshare in de portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="14aa3-117">Kies de service Bestanden.</span><span class="sxs-lookup"><span data-stu-id="14aa3-117">Choose "Files" service.</span></span>

    ![Schermafbeelding van het maken van een bestandsshare in de portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="14aa3-119">Klik op Bestandsshares en volg de koppeling om uw eerste bestandsshare te maken.</span><span class="sxs-lookup"><span data-stu-id="14aa3-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![Schermafbeelding van het maken van een bestandsshare in de portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="14aa3-121">Vul de naam en de grootte (maximaal 5120 GB) van de bestandsshare in om uw eerste bestandsshare te maken.</span><span class="sxs-lookup"><span data-stu-id="14aa3-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="14aa3-122">Wanneer de bestandsshare is gemaakt, kunt u deze koppelen vanuit elk bestandssysteem dat SMB 2.1 of SMB 3.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="14aa3-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="14aa3-123">U kunt in de bestandsshare op **Quotum** klikken om de grootte van het bestand van maximaal 5120 GB te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="14aa3-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="14aa3-124">Raadpleeg de [Azure-prijscalculator](https://azure.microsoft.com/pricing/calculator/) voor een indicatie van de opslagkosten van het gebruik van Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="14aa3-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![Schermafbeelding van het maken van een bestandsshare in de portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="14aa3-126">Bestanden uploaden en downloaden</span><span class="sxs-lookup"><span data-stu-id="14aa3-126">Upload and download files</span></span>
1. <span data-ttu-id="14aa3-127">Kies een bestandsshare die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14aa3-127">Choose one file share your have already created.</span></span>

    ![Schermafbeelding van het uploaden en downloaden van bestanden vanuit de portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="14aa3-129">Klik op **Uploaden** om de gebruikersinterface voor het uploaden van bestanden te openen.</span><span class="sxs-lookup"><span data-stu-id="14aa3-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![Schermafbeelding van het uploaden van bestanden vanuit de portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="14aa3-131">Verbinding maken met de bestandsshare</span><span class="sxs-lookup"><span data-stu-id="14aa3-131">Connect to file share</span></span>
-  <span data-ttu-id="14aa3-132">Klik op **Verbinden** om de opdrachtregel op te halen voor het koppelen van de bestandsshare vanuit Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="14aa3-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="14aa3-133">Voor Linux-gebruikers kunt u ook verwijzen naar [Azure File Storage gebruiken met Linux](../storage-how-to-use-files-linux.md) voor koppelingsinstructies voor andere Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="14aa3-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Schermafbeelding van het koppelen van de bestandsshare](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="14aa3-135">U kunt de opdrachten voor het koppelen van de bestandsshare in Windows of Linux kopiëren en deze uitvoeren vanaf uw Azure VM of lokale machine.</span><span class="sxs-lookup"><span data-stu-id="14aa3-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Schermafbeelding van de koppelingsopdrachten voor Windows en Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="14aa3-137">**Tip:**</span><span class="sxs-lookup"><span data-stu-id="14aa3-137">**Tip:**</span></span>  
<span data-ttu-id="14aa3-138">Voor het vinden van de toegangssleutel voor de opslagaccount die u wilt gebruiken voor het koppelen, klikt u op **Toegangssleutels voor dit opslagaccount weergeven** onder aan de pagina waar u verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="14aa3-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="14aa3-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="14aa3-139">See also</span></span>
<span data-ttu-id="14aa3-140">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="14aa3-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="14aa3-141">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="14aa3-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="14aa3-142">Problemen oplossen in Windows</span><span class="sxs-lookup"><span data-stu-id="14aa3-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="14aa3-143">Problemen oplossen in Linux</span><span class="sxs-lookup"><span data-stu-id="14aa3-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    