---
title: Azure file storage vanuit een Windows Azure VM aaaMount | Microsoft Docs
description: Opslaan van het bestand in de cloud met Azure file storage Hallo en uw cloud-bestandsshare koppelen vanuit Azure een virtuele machine (VM).
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
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="7b5ea-103">Azure-bestandsshares gebruiken met Windows VM 's</span><span class="sxs-lookup"><span data-stu-id="7b5ea-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="7b5ea-104">U kunt Azure-bestandsshares gebruiken als een manier toostore en toegang tot de bestanden van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="7b5ea-105">U kunt bijvoorbeeld een script of een toepassingsconfiguratiebestand dat u wilt dat alle tooshare van uw virtuele machines opslaan.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="7b5ea-106">In dit onderwerp laten we zien u hoe toocreate en koppelpunten een Azure-bestandsshare en hoe bestanden tooupload en downloaden.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="7b5ea-107">Verbinding maken met de bestandsshare tooa van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7b5ea-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="7b5ea-108">Deze sectie wordt ervan uitgegaan dat u hebt al een bestand dat u wilt dat tooconnect te delen.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="7b5ea-109">Als u toocreate een moet, Zie [een bestandsshare maken](#create-a-file-share) verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="7b5ea-110">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b5ea-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b5ea-111">Klik op Hallo linkermenu **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="7b5ea-112">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-112">Choose your storage account.</span></span>
4. <span data-ttu-id="7b5ea-113">In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="7b5ea-114">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-114">Select a file share.</span></span>
6. <span data-ttu-id="7b5ea-115">Klik op **Connect** tooopen een pagina met de opdrachtregelsyntaxis Hallo voor het Hallo-bestandsshare koppelen van Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="7b5ea-116">Markeer Hallo syntaxis van Hallo opdracht en plak deze in Kladblok of ergens anders waar u eenvoudig toegang toe.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="7b5ea-117">Hallo syntaxis tooremove Hallo voorloopspaties bewerken ** > ** en vervang *[stationsaanduiding]* met Hallo stationsletter (bijvoorbeeld **Y:**) waar u wilt toomount Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="7b5ea-118">Tooyour VM sluit en open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="7b5ea-119">Plakken in Hallo bewerkt u de syntaxis van de verbinding en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="7b5ea-120">Als het Hallo-verbinding is gemaakt, krijgt u het Hallo-bericht **Hallo-opdracht is uitgevoerd.**</span><span class="sxs-lookup"><span data-stu-id="7b5ea-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="7b5ea-121">Hallo-verbinding controleren door te typen in Hallo letter tooswitch toothat schijf en typ vervolgens **dir** toosee Hallo inhoud van de bestandsshare Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="7b5ea-122">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="7b5ea-122">Create a file share</span></span> 
1. <span data-ttu-id="7b5ea-123">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b5ea-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b5ea-124">Klik op Hallo linkermenu **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="7b5ea-125">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-125">Choose your storage account.</span></span>
4. <span data-ttu-id="7b5ea-126">In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="7b5ea-127">Hallo File Service pagina, klikt u op **+ bestandsshare** toocreate uw eerste bestandsshare. \\</span><span class="sxs-lookup"><span data-stu-id="7b5ea-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="7b5ea-128">Naam van bestandsshare Hallo invullen.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-128">Fill in hello file share name.</span></span> <span data-ttu-id="7b5ea-129">De namen van bestandsshares kunnen gebruiken, kleine letters, cijfers en afbreekstreepjes één.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="7b5ea-130">Hallo-naam kan niet beginnen met een afbreekstreepje en u kunt niet meerdere, gebruiken afbreekstreepjes achter elkaar voorkomen.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="7b5ea-131">Vul in een limiet op hoe groot Hallo-bestand mag up too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="7b5ea-132">Klik op **OK** toodeploy Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="7b5ea-133">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="7b5ea-133">Upload files</span></span>
1. <span data-ttu-id="7b5ea-134">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b5ea-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b5ea-135">Klik op Hallo linkermenu **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="7b5ea-136">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-136">Choose your storage account.</span></span>
4. <span data-ttu-id="7b5ea-137">In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="7b5ea-138">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-138">Select a file share.</span></span>
6. <span data-ttu-id="7b5ea-139">Klik op **uploaden** tooopen hello **bestanden uploaden** pagina.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="7b5ea-140">Klik op Hallo map pictogram toobrowse voor een bestand tooupload het lokale bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="7b5ea-141">Klik op **uploaden** tooupload hello toohello bestand bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="7b5ea-142">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="7b5ea-142">Download files</span></span>
1. <span data-ttu-id="7b5ea-143">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b5ea-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b5ea-144">Klik op Hallo linkermenu **opslagaccounts**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="7b5ea-145">Kies uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-145">Choose your storage account.</span></span>
4. <span data-ttu-id="7b5ea-146">In Hallo **overzicht** pagina onder **Services**, selecteer **bestanden**.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="7b5ea-147">Selecteer een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-147">Select a file share.</span></span>
6. <span data-ttu-id="7b5ea-148">Met de rechtermuisknop op het Hallo-bestand en kies **downloaden** toodownload het tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="7b5ea-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b5ea-149">Next steps</span></span>

<span data-ttu-id="7b5ea-150">U kunt ook maken en beheren van bestandsshares met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7b5ea-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="7b5ea-151">Zie voor meer informatie [aan de slag met Azure File storage in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="7b5ea-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
