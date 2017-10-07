---
title: aaaPersist bestanden in de Azure-Cloud-Shell (Preview) | Microsoft Docs
description: Overzicht van hoe Azure Cloud Shell zich blijft bestanden voordoen.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="15f47-103">Bestanden in de Azure-Cloud-Shell behouden</span><span class="sxs-lookup"><span data-stu-id="15f47-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="15f47-104">Cloud-Shell maakt gebruik van Azure File storage toopersist bestanden over de sessies.</span><span class="sxs-lookup"><span data-stu-id="15f47-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="15f47-105">Instellen van een `clouddrive` bestandsshare</span><span class="sxs-lookup"><span data-stu-id="15f47-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="15f47-106">Op de eerste start Cloud Shell wordt u gevraagd een nieuwe of bestaande bestandsshare toopersist bestanden tussen sessies tooassociate.</span><span class="sxs-lookup"><span data-stu-id="15f47-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="15f47-107">Maken van nieuwe opslag</span><span class="sxs-lookup"><span data-stu-id="15f47-107">Create new storage</span></span>

<span data-ttu-id="15f47-108">Wanneer u basisinstellingen en alleen een abonnement selecteren, maakt Cloud Shell drie bronnen namens jou in Hallo ondersteund regio die zich het dichtst bij tooyou:</span><span class="sxs-lookup"><span data-stu-id="15f47-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="15f47-109">Resourcegroep:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="15f47-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="15f47-110">Storage-account:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="15f47-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="15f47-111">Bestandsshare:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="15f47-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Hallo-instelling voor Cloudabonnement](media/basic-storage.png)

<span data-ttu-id="15f47-113">Hallo-bestandsshare koppelt als `clouddrive` in uw `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="15f47-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="15f47-114">Hallo bestandsshare is ook gebruikte toostore een afbeelding 5 GB die automatisch voor u en die wordt gemaakt, bijgewerkt en zich blijft voordoen uw `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="15f47-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="15f47-115">Dit is een eenmalige bewerking en Hallo-bestandsshare in de volgende sessies automatisch koppelt.</span><span class="sxs-lookup"><span data-stu-id="15f47-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="15f47-116">Bestaande bronnen gebruiken</span><span class="sxs-lookup"><span data-stu-id="15f47-116">Use existing resources</span></span>

<span data-ttu-id="15f47-117">U kunt met behulp van de geavanceerde optie Hallo bestaande resources koppelen.</span><span class="sxs-lookup"><span data-stu-id="15f47-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="15f47-118">Wanneer Hallo opslag setup prompt wordt weergegeven, selecteert u **weergeven geavanceerde instellingen** tooview extra opties.</span><span class="sxs-lookup"><span data-stu-id="15f47-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="15f47-119">Bestaande bestandsshares ontvangen van een afbeelding 5 GB gebruiker toopersist uw `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="15f47-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="15f47-120">Hallo vervolgkeuzemenu's worden gefilterd voor de regio van uw Cloud-Shell en lokaal redundante & geo-redundant storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="15f47-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![instelling van de Resource Hallo](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="15f47-122">Bron maken met een Azure-resource beleid beperken</span><span class="sxs-lookup"><span data-stu-id="15f47-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="15f47-123">Storage-accounts die u in de Cloud-Shell maakt zijn gelabeld met `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="15f47-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="15f47-124">Als u wilt dat gebruikers van het storage-accounts maken in de Cloud-Shell toodisallow, maakt u een [Azure bronbeleid voor tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) die worden geactiveerd door deze specifieke tag.</span><span class="sxs-lookup"><span data-stu-id="15f47-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="15f47-125">De werking van Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="15f47-125">How Cloud Shell works</span></span>
<span data-ttu-id="15f47-126">Cloud-Shell aanhoudt bestanden via beide Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="15f47-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="15f47-127">Maken van de installatiekopie van een schijf van uw `$Home` directory toopersist alle inhoud binnen Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="15f47-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="15f47-128">Hallo-installatiekopie wordt opgeslagen in de opgegeven bestandsshare als `acc_<User>.img` op `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, en worden wijzigingen automatisch gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="15f47-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="15f47-129">Koppelen van de opgegeven bestandsshare als `clouddrive` in uw `$Home` map voor interactie met de share rechtstreeks bestand.</span><span class="sxs-lookup"><span data-stu-id="15f47-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="15f47-130">`/Home/<User>/clouddrive`is toegewezen te`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="15f47-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="15f47-131">Alle bestanden in uw `$Home` directory, zoals SSH-sleutels worden doorgevoerd in uw schijfimage gebruiker die is opgeslagen in de gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="15f47-132">Aanbevolen procedures van toepassing wanneer u deze persistent maken informatie in uw `$Home` directory en gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="15f47-133">Gebruik Hallo `clouddrive` opdracht</span><span class="sxs-lookup"><span data-stu-id="15f47-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="15f47-134">Met Cloud-Shell, kunt u een opdracht uitvoeren `clouddrive`, dit kunt u toomanually update Hallo-bestandsshare die gekoppelde tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="15f47-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="15f47-135">![Hallo 'clouddrive' opdracht uit te voeren](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="15f47-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="15f47-136">Een nieuwe koppelen`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="15f47-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="15f47-137">Vereisten voor de handmatige koppelen</span><span class="sxs-lookup"><span data-stu-id="15f47-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="15f47-138">U kunt bijwerken Hallo-bestandsshare die is gekoppeld aan Cloud-Shell met behulp van Hallo `clouddrive mount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="15f47-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="15f47-139">Als u een bestaande bestandsshare koppelt, moet Hallo storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="15f47-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="15f47-140">Lokaal redundante opslag of geografisch redundante opslag toosupport bestandsshares.</span><span class="sxs-lookup"><span data-stu-id="15f47-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="15f47-141">Bevindt zich in uw regio toegewezen.</span><span class="sxs-lookup"><span data-stu-id="15f47-141">Located in your assigned region.</span></span> <span data-ttu-id="15f47-142">Als u de voorbereiding, Hallo regio aan u zijn toegewezen die worden vermeld in de naam van resourcegroep Hallo toois `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="15f47-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="15f47-143">Ondersteunde opslagregio</span><span class="sxs-lookup"><span data-stu-id="15f47-143">Supported storage regions</span></span>
<span data-ttu-id="15f47-144">Hello Azure bestanden moeten zich bevinden in Hallo dezelfde regio bevinden als Hallo Cloud Shell machine die u ze wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="15f47-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="15f47-145">Cloud-Shell clusters is momenteel beschikbaar zijn in Hallo gebieden te volgen:</span><span class="sxs-lookup"><span data-stu-id="15f47-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="15f47-146">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="15f47-146">Area</span></span>|<span data-ttu-id="15f47-147">Regio</span><span class="sxs-lookup"><span data-stu-id="15f47-147">Region</span></span>|
|---|---|
|<span data-ttu-id="15f47-148">Noord- en Zuid-Amerika</span><span class="sxs-lookup"><span data-stu-id="15f47-148">Americas</span></span>|<span data-ttu-id="15f47-149">VS-Oost, Zuid-centraal VS, VS-West</span><span class="sxs-lookup"><span data-stu-id="15f47-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="15f47-150">Europa</span><span class="sxs-lookup"><span data-stu-id="15f47-150">Europe</span></span>|<span data-ttu-id="15f47-151">Noord-Europa, West-Europa</span><span class="sxs-lookup"><span data-stu-id="15f47-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="15f47-152">Azië en Stille Oceaan</span><span class="sxs-lookup"><span data-stu-id="15f47-152">Asia Pacific</span></span>|<span data-ttu-id="15f47-153">India centraal, Zuidoost-Azië</span><span class="sxs-lookup"><span data-stu-id="15f47-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="15f47-154">Hallo `clouddrive mount` opdracht</span><span class="sxs-lookup"><span data-stu-id="15f47-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="15f47-155">Als u een nieuwe bestandsshare koppelen wilt, een nieuwe gebruikersinstallatiekopie is gemaakt voor uw `$Home` directory, omdat uw vorige `$Home` installatiekopie wordt opgeslagen in de vorige bestandsshare Hallo.</span><span class="sxs-lookup"><span data-stu-id="15f47-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="15f47-156">Voer Hallo `clouddrive mount` opdracht Hello volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="15f47-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="15f47-157">tooview meer details uitvoeren `clouddrive mount -h`, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="15f47-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Actieve Hallo ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="15f47-159">Ontkoppelen`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="15f47-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="15f47-160">U kunt een bestandsshare die gekoppelde tooCloud-Shell op elk gewenst moment ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="15f47-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="15f47-161">Wanneer de bestandsshare ontkoppeld is, kunt u zich na vragen aan gebruiker toomount een nieuw bestandsshare voorafgaande tooyour volgende sessie.</span><span class="sxs-lookup"><span data-stu-id="15f47-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="15f47-162">een bestand tooremove delen van Cloud-Shell:</span><span class="sxs-lookup"><span data-stu-id="15f47-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="15f47-163">Voer `clouddrive unmount` uit.</span><span class="sxs-lookup"><span data-stu-id="15f47-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="15f47-164">Erkent en hello wordt u gevraagd te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="15f47-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="15f47-165">De bestandsshare blijven tooexist tenzij u deze handmatig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="15f47-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="15f47-166">Cloud-Shell zoekt op de volgende sessies niet meer naar deze bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="15f47-167">tooview meer details uitvoeren `clouddrive unmount -h`, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="15f47-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Actieve Hallo ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="15f47-169">Alle resources worden niet verwijderd als u deze opdracht uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="15f47-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="15f47-170">Handmatig verwijderen van een resourcegroep, het opslagaccount of de bestandsshare die is toegewezen tooCloud Shell wordt permanent verwijderd. uw `$Home` directory installatiekopie en andere bestanden in de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="15f47-171">Deze actie kan niet ongedaan worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="15f47-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="15f47-172">Lijst `clouddrive` bestandsshares</span><span class="sxs-lookup"><span data-stu-id="15f47-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="15f47-173">welke bestandsshare is gekoppeld als toodiscover `clouddrive`, voert u de volgende Hallo `df` opdracht.</span><span class="sxs-lookup"><span data-stu-id="15f47-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="15f47-174">Hallo bestand pad tooclouddrive ziet u dat de naam van het opslagaccount en bestandsshare in Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="15f47-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="15f47-175">Bijvoorbeeld: `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="15f47-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="15f47-176">Overdracht lokale bestanden tooCloud Shell</span><span class="sxs-lookup"><span data-stu-id="15f47-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="15f47-177">Hallo `clouddrive` directory wordt gesynchroniseerd met Azure portal-opslag-blade Hallo.</span><span class="sxs-lookup"><span data-stu-id="15f47-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="15f47-178">Gebruik deze blade tootransfer lokale bestanden tooor van de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="15f47-179">Bijwerken van bestanden vanuit Cloud Shell wordt doorgevoerd in Hallo bestandsopslag GUI wanneer u de blade Hallo vernieuwt.</span><span class="sxs-lookup"><span data-stu-id="15f47-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="15f47-180">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="15f47-180">Download files</span></span>

![Lijst van lokale bestanden](media/download.png)
1. <span data-ttu-id="15f47-182">Ga in hello Azure-portal, toohello gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="15f47-183">Selecteer het doelbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="15f47-183">Select hello target file.</span></span>
3. <span data-ttu-id="15f47-184">Selecteer Hallo **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="15f47-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="15f47-185">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="15f47-185">Upload files</span></span>

![Lokale bestanden toobe geüpload](media/upload.png)
1. <span data-ttu-id="15f47-187">Ga tooyour gekoppelde bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="15f47-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="15f47-188">Selecteer Hallo **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="15f47-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="15f47-189">Selecteer Hallo of bestanden die u tooupload wilt.</span><span class="sxs-lookup"><span data-stu-id="15f47-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="15f47-190">Bevestig Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="15f47-190">Confirm hello upload.</span></span>

<span data-ttu-id="15f47-191">U ziet nu Hallo-bestanden die toegankelijk zijn in uw `clouddrive` map in de Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="15f47-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15f47-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15f47-192">Next steps</span></span>
[<span data-ttu-id="15f47-193">Cloud-Shell Quick Start</span><span class="sxs-lookup"><span data-stu-id="15f47-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="15f47-194">
[Meer informatie over Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="15f47-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="15f47-195">
[Meer informatie over opslag labels](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="15f47-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
