---
title: Bestandsopslag op Azure koppelen vanuit een Windows Azure VM | Microsoft Docs
description: Bestand opslaan in de cloud met Azure file storage en uw cloud-bestandsshare koppelen vanuit Azure een virtuele machine (VM).
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="f8cbb-103">Azure-bestandsshares gebruiken met Windows VM 's</span><span class="sxs-lookup"><span data-stu-id="f8cbb-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="f8cbb-104">U kunt Azure-bestandsshares gebruiken als een manier om bestanden opslaan en openen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="f8cbb-105">U kunt bijvoorbeeld een script of een toepassingsconfiguratiebestand die u wilt dat alle virtuele machines te delen opslaan.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="f8cbb-106">In dit onderwerp zien we u hoe maken en koppelen van een Azure-bestandsshare en hoe bestanden uploaden en downloaden.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="f8cbb-107">Verbinding maken met een bestandsshare vanaf een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f8cbb-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="f8cbb-108">Deze sectie wordt ervan uitgegaan dat u hebt al een bestandsshare die u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="f8cbb-109">Als u maken wilt, Zie [een bestandsshare maken](#create-a-file-share) verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="f8cbb-110">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8cbb-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8cbb-111">Klik in het menu links op **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f8cbb-112">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-112">Choose your storage account.</span></span>
4. <span data-ttu-id="f8cbb-113">In de **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f8cbb-114">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-114">Select a file share.</span></span>
6. <span data-ttu-id="f8cbb-115">Klik op **Connect** opent een pagina met de syntaxis van de opdrachtregel voor het koppelen van de bestandsshare vanuit Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="f8cbb-116">Markeer de syntaxis van de opdracht en plak deze in Kladblok of ergens anders waar u eenvoudig toegang toe.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="f8cbb-117">De syntaxis voor het verwijderen van de voorloopspaties bewerken ** > ** en vervang *[stationsaanduiding]* met de stationsletter (bijvoorbeeld **Y:**) waarin u wilt de bestandsshare koppelen.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="f8cbb-118">Verbinding maken met uw virtuele machine en open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="f8cbb-119">Plak in de bewerkte verbinding-syntaxis en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="f8cbb-120">Als de verbinding is gemaakt, krijgt u het bericht **de opdracht is voltooid.**</span><span class="sxs-lookup"><span data-stu-id="f8cbb-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="f8cbb-121">Controleer de verbinding door te typen in de stationsletter overschakelen naar dat station en typ vervolgens **dir** om te zien van de inhoud van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="f8cbb-122">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="f8cbb-122">Create a file share</span></span> 
1. <span data-ttu-id="f8cbb-123">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8cbb-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8cbb-124">Klik in het menu links op **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f8cbb-125">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-125">Choose your storage account.</span></span>
4. <span data-ttu-id="f8cbb-126">In de **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f8cbb-127">Klik op de pagina File-Service op **+ bestandsshare** om uw eerste bestandsshare te maken. \\</span><span class="sxs-lookup"><span data-stu-id="f8cbb-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="f8cbb-128">Vul in de naam van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-128">Fill in the file share name.</span></span> <span data-ttu-id="f8cbb-129">De namen van bestandsshares kunnen gebruiken, kleine letters, cijfers en afbreekstreepjes één.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="f8cbb-130">De naam mag niet beginnen met een afbreekstreepje en u kunt niet meerdere, gebruiken afbreekstreepjes achter elkaar voorkomen.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="f8cbb-131">Vul in een limiet op hoe lang het bestand kunnen zijn, maximaal 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="f8cbb-132">Klik op **OK** voor het implementeren van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="f8cbb-133">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="f8cbb-133">Upload files</span></span>
1. <span data-ttu-id="f8cbb-134">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8cbb-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8cbb-135">Klik in het menu links op **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f8cbb-136">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-136">Choose your storage account.</span></span>
4. <span data-ttu-id="f8cbb-137">In de **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f8cbb-138">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-138">Select a file share.</span></span>
6. <span data-ttu-id="f8cbb-139">Klik op **uploaden** openen de **bestanden uploaden** pagina.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="f8cbb-140">Klik op het pictogram van de map te bladeren naar een bestand voor het uploaden van het lokale bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="f8cbb-141">Klik op **uploaden** het bestand te uploaden naar de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="f8cbb-142">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="f8cbb-142">Download files</span></span>
1. <span data-ttu-id="f8cbb-143">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8cbb-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8cbb-144">Klik in het menu links op **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f8cbb-145">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-145">Choose your storage account.</span></span>
4. <span data-ttu-id="f8cbb-146">In de **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f8cbb-147">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-147">Select a file share.</span></span>
6. <span data-ttu-id="f8cbb-148">Met de rechtermuisknop op het bestand en kies **downloaden** om deze te downloaden naar uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="f8cbb-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8cbb-149">Next steps</span></span>

<span data-ttu-id="f8cbb-150">U kunt ook maken en beheren van bestandsshares met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f8cbb-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="f8cbb-151">Zie voor meer informatie [aan de slag met Azure File storage in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="f8cbb-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
