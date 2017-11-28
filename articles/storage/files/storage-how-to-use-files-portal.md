---
title: aaaHow toomanage Azure File storage uit hello Azure-portal | Microsoft Docs
description: Meer informatie over toouse hello Azure portal toomanage Azure File storage.
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="09801-103">Hoe Azure File storage toouse van hello Azure Portal</span><span class="sxs-lookup"><span data-stu-id="09801-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="09801-104">Hallo [Azure-portal](https://portal.azure.com) biedt een gebruikersinterface voor het beheren van Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="09801-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="09801-105">U kunt de volgende acties uit uw webbrowser Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="09801-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="09801-106">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="09801-106">Create a File Share</span></span>
* <span data-ttu-id="09801-107">Uploaden en downloaden van bestanden tooand van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="09801-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="09801-108">Hallo werkelijke gebruik van elke bestandsshare controleren.</span><span class="sxs-lookup"><span data-stu-id="09801-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="09801-109">Quotum voor de grootte van de bestandsshare Hallo aanpassen.</span><span class="sxs-lookup"><span data-stu-id="09801-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="09801-110">Hallo koppelpunt opdrachten toouse toomount delen van het bestand kopiëren van een Windows- of Linux-client.</span><span class="sxs-lookup"><span data-stu-id="09801-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="09801-111">Bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="09801-111">Create file share</span></span>
1. <span data-ttu-id="09801-112">Meld u aan toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="09801-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="09801-113">Klik op Hallo navigatiemenu **opslagaccounts** of **opslagaccounts (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="09801-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="09801-115">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="09801-115">Choose your storage account.</span></span>

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="09801-117">Kies de service Bestanden.</span><span class="sxs-lookup"><span data-stu-id="09801-117">Choose "Files" service.</span></span>

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="09801-119">Klik op 'Bestandsshares' en volg Hallo koppeling toocreate uw eerste bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="09801-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="09801-121">Naam van bestandsshare Hallo en invullen Hallo grootte van Hallo file share (omhoog too5120 GB) toocreate uw eerste bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="09801-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="09801-122">Zodra het Hallo-bestandsshare is gemaakt, kunt u deze koppelen vanuit elk bestandssysteem dat SMB 2.1 of SMB 3.0 ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="09801-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="09801-123">U kunt klikken op **quotum** op Hallo toochange Hallo grootte van de bestandsshare van Hallo bestand up too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="09801-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="09801-124">Raadpleeg het te[Azure Prijscalculator](https://azure.microsoft.com/pricing/calculator/) tooestimate Hallo opslagkosten van het gebruik van Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="09801-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Schermopname die laat zien hoe toocreate-bestandsshare in Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="09801-126">Bestanden uploaden en downloaden</span><span class="sxs-lookup"><span data-stu-id="09801-126">Upload and download files</span></span>
1. <span data-ttu-id="09801-127">Kies een bestandsshare die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09801-127">Choose one file share your have already created.</span></span>

    ![Schermopname die laat zien hoe tooupload en downloaden van bestanden van de portal Hallo](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="09801-129">Klik op **uploaden** Hallo-gebruikersinterface voor het uploaden van bestanden te openen.</span><span class="sxs-lookup"><span data-stu-id="09801-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Schermopname die laat zien hoe tooupload bestanden van Hallo-portal](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="09801-131">Verbinding maken met share toofile</span><span class="sxs-lookup"><span data-stu-id="09801-131">Connect toofile share</span></span>
-  <span data-ttu-id="09801-132">Klik op **Connect** Hallo vanaf de opdrachtregel voor koppelen Hallo bestandsshare ophalen van Windows en Linux.</span><span class="sxs-lookup"><span data-stu-id="09801-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="09801-133">Voor Linux-gebruikers, kunt u ook verwijzen te[hoe toouse Azure File storage met Linux](../storage-how-to-use-files-linux.md) voor montage instructies voor het andere Linux-distributies.</span><span class="sxs-lookup"><span data-stu-id="09801-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Schermopname die laat zien hoe toomount Hallo bestandsshare](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="09801-135">U kunt kopiëren Hallo opdrachten voor het koppelen van bestand delen op Windows of Linux- en virtuele machine in Azure of on-premises machine uitvoeren van u.</span><span class="sxs-lookup"><span data-stu-id="09801-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Schermafbeelding van Hallo mount-opdrachten voor Windows en Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="09801-137">**Tip:**</span><span class="sxs-lookup"><span data-stu-id="09801-137">**Tip:**</span></span>  
<span data-ttu-id="09801-138">toofind hello toegangssleutel voor opslagaccount voor koppelen, klikt u op **toegangssleutels weergeven voor dit opslagaccount** onderin Hallo Hallo pagina verbinden.</span><span class="sxs-lookup"><span data-stu-id="09801-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="09801-139">Zie ook</span><span class="sxs-lookup"><span data-stu-id="09801-139">See also</span></span>
<span data-ttu-id="09801-140">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="09801-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="09801-141">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="09801-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="09801-142">Problemen oplossen in Windows</span><span class="sxs-lookup"><span data-stu-id="09801-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="09801-143">Problemen oplossen in Linux</span><span class="sxs-lookup"><span data-stu-id="09801-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    