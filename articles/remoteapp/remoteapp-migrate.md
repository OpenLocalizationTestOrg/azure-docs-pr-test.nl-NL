---
title: de gebruikersgegevens aaaMigrate van Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toomigrate uw gebruikersgegevens in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="e12ed-103">Hoe toomigrate gegevens naar en van Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e12ed-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e12ed-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="e12ed-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e12ed-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e12ed-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e12ed-106">Kunt u veel verschillende hulpprogramma's en methoden tootransfer [gebruikersgegevens](remoteapp-upd.md) naar en van Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e12ed-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="e12ed-107">Hier volgen een aantal methoden:</span><span class="sxs-lookup"><span data-stu-id="e12ed-107">Here are a few methods:</span></span>

* <span data-ttu-id="e12ed-108">Kopiëren en plakken met behulp van het gedeelde Klembord</span><span class="sxs-lookup"><span data-stu-id="e12ed-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="e12ed-109">Kopiëren van bestanden en gegevens tooa bestandsserver</span><span class="sxs-lookup"><span data-stu-id="e12ed-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="e12ed-110">Kopiëren van bestanden tooOneDrive voor bedrijven via een browser</span><span class="sxs-lookup"><span data-stu-id="e12ed-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="e12ed-111">Bestanden kopiëren met omleiding</span><span class="sxs-lookup"><span data-stu-id="e12ed-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="e12ed-112">U kunt Hallo OneDrive niet inschakelen voor synchronisatie-agents, bedrijfs- of - ze [worden niet ondersteund](remoteapp-onedrive.md) in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e12ed-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="e12ed-113">Kopiëren en plakken in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="e12ed-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="e12ed-114">Kopiëren en plakken met de Hallo Klembord is ingeschakeld in RemoteApp-implementaties [standaard](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="e12ed-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="e12ed-115">Hiermee kunnen gebruikers bestanden kopiëren tussen hun lokale PC's en RemoteApp-apps.</span><span class="sxs-lookup"><span data-stu-id="e12ed-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="e12ed-116">Vaak via normale Hallo van het gebruik van apps in RemoteApp-hebben gebruikers opgeslagen bestanden tootheir UPDs - verplaatsen van gegevens buiten RemoteApp is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="e12ed-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="e12ed-117">[Verkenner als een app publiceren](remoteapp-publish.md) in een RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="e12ed-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="e12ed-118">(Houd er rekening mee dat dit kan een beheertaak.)</span><span class="sxs-lookup"><span data-stu-id="e12ed-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="e12ed-119">Directe uw gebruikers toolaunch Hallo Verkenner-app die u hebt gepubliceerd en toouse die bestanden toocopy en plakken zowel naar hun UPD en van deze.</span><span class="sxs-lookup"><span data-stu-id="e12ed-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="e12ed-120">Uploaden van bestanden en gegevens tooa bestandsserver door standaardnetwerk bestand kopiëren</span><span class="sxs-lookup"><span data-stu-id="e12ed-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="e12ed-121">Vaak organisaties gebruiken om servers toostore algemene bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="e12ed-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="e12ed-122">Als u Hallo server-naam of locatie weet, kunnen uw gebruikers Hallo lokale netwerk voor Hallo server bladeren en kopieert u hun bestanden, worden er veel zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="e12ed-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="e12ed-123">U zult opnieuw wilt toopublish Verkenner tooRemoteApp en vervolgens te delen met uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e12ed-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="e12ed-124">Hallo-bestandsserver moet op Hallo routeerbaar netwerk met RemoteApp is geïmplementeerd in.</span><span class="sxs-lookup"><span data-stu-id="e12ed-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="e12ed-125">Kopiëren van bestanden tooOneDrive voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="e12ed-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="e12ed-126">Hoewel u Hallo OneDrive voor bedrijven-synchronisatie-agent in RemoteApp niet inschakelen, kunt u nog steeds bestanden kopiëren vanaf uw tooOneDrive UPD voor bedrijven via een browser.</span><span class="sxs-lookup"><span data-stu-id="e12ed-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="e12ed-127">Verkenner tooRemoteApp publiceren en vervolgens instrueren dat gebruikers tooaccess Hallo bestanden via de app.</span><span class="sxs-lookup"><span data-stu-id="e12ed-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="e12ed-128">Het is eenvoudigste tootransfer bestanden als ze worden gecomprimeerd, zodat gebruikers een ZIP-bestand waarin alle Hallo bestanden toomove tooOneDrive voor bedrijven moeten maken.</span><span class="sxs-lookup"><span data-stu-id="e12ed-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="e12ed-129">Vraag gebruikers toogo toohello Office 365-portal en gaat u tooOneDrive en Hallo ZIP-bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="e12ed-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="e12ed-130">Kopiëren van bestanden met behulp van stationsomleiding</span><span class="sxs-lookup"><span data-stu-id="e12ed-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="e12ed-131">Als u hebt ingeschakeld [station omleiding](remoteapp-redirection.md), u hebt al een toegewezen station gemaakt voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e12ed-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="e12ed-132">In dit geval ze kunnen hun bestanden op Hallo omgeleid station zip en slaat u deze tootheir lokale PC.</span><span class="sxs-lookup"><span data-stu-id="e12ed-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="e12ed-133">Hoe kunnen beheerders gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="e12ed-133">How administrators can export data</span></span>

<span data-ttu-id="e12ed-134">Beheert voor Azure RemoteApp alle gebruikersprofielschijven (UPD exporteren kunt) voor alle collecties binnen een abonnement tooAzure opslag met Azure PowerShell-cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="e12ed-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="e12ed-135">Er is geen mogelijkheid tooselect afzonderlijke UPD van.</span><span class="sxs-lookup"><span data-stu-id="e12ed-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="e12ed-136">Wanneer Hallo PowerShell-opdracht wordt uitgevoerd, wordt elke gebruiker schijf een 50gb in grootte van de vaste schijf en geëxporteerde tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="e12ed-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="e12ed-137">Kosten van Azure storage, onmiddellijk worden voor deze opslag.</span><span class="sxs-lookup"><span data-stu-id="e12ed-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="e12ed-138">Wanneer u deze opdracht uitvoert ervoor te zorgen zijn er geen sessies anders Hallo exporteren mislukt.</span><span class="sxs-lookup"><span data-stu-id="e12ed-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="e12ed-139">UPD de voor lid van domein Azure RemoteApp-implementaties kan alleen opnieuw in een RDS-implementatie worden gebruikt, niet van het domein gekoppelde implementaties kunnen niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e12ed-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="e12ed-140">Als deze schijven worden gebruikt in een RDS-implementatie raden wij aan toouse onze [geautomatiseerde scripts](https://github.com/arcadiahlyy/aramigration) die wordt exporteren, converteren en Hallo van UPD importeren in een RDS-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e12ed-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

