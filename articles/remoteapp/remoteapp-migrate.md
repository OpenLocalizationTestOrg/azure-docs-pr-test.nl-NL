---
title: Gegevens migreren van Azure RemoteApp | Microsoft Docs
description: Informatie over het migreren van uw gebruikersgegevens in Azure RemoteApp.
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
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="de89e-103">Het migreren van gegevens naar en van Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="de89e-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="de89e-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="de89e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="de89e-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="de89e-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="de89e-106">U kunt veel verschillende hulpprogramma's en -methoden gebruiken om over te dragen [gebruikersgegevens](remoteapp-upd.md) naar en van Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="de89e-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="de89e-107">Hier volgen een aantal methoden:</span><span class="sxs-lookup"><span data-stu-id="de89e-107">Here are a few methods:</span></span>

* <span data-ttu-id="de89e-108">Kopiëren en plakken met behulp van het gedeelde Klembord</span><span class="sxs-lookup"><span data-stu-id="de89e-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="de89e-109">Kopiëren van bestanden en gegevens op een bestandsserver</span><span class="sxs-lookup"><span data-stu-id="de89e-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="de89e-110">Bestanden kopiëren naar OneDrive voor bedrijven via een browser</span><span class="sxs-lookup"><span data-stu-id="de89e-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="de89e-111">Bestanden kopiëren met omleiding</span><span class="sxs-lookup"><span data-stu-id="de89e-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="de89e-112">U kunt de OneDrive niet inschakelen voor synchronisatie-agents, bedrijfs- of - ze [worden niet ondersteund](remoteapp-onedrive.md) in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="de89e-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="de89e-113">Kopiëren en plakken in Windows Verkenner</span><span class="sxs-lookup"><span data-stu-id="de89e-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="de89e-114">Kopiëren en plakken met behulp van het Klembord is ingeschakeld in RemoteApp-implementaties [standaard](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="de89e-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="de89e-115">Hiermee kunnen gebruikers bestanden kopiëren tussen hun lokale PC's en RemoteApp-apps.</span><span class="sxs-lookup"><span data-stu-id="de89e-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="de89e-116">Vaak in de normale loop van het gebruik van apps in RemoteApp-hebben gebruikers opgeslagen bestanden in hun UPDs - verplaatsen van gegevens buiten RemoteApp is eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="de89e-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="de89e-117">[Verkenner als een app publiceren](remoteapp-publish.md) in een RemoteApp-verzameling.</span><span class="sxs-lookup"><span data-stu-id="de89e-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="de89e-118">(Houd er rekening mee dat dit kan een beheertaak.)</span><span class="sxs-lookup"><span data-stu-id="de89e-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="de89e-119">Uw gebruikers Start de Verkenner-app die u hebt gepubliceerd en gebruikt deze om te kopiëren en plakken van bestanden in hun UPD zowel buiten het rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="de89e-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="de89e-120">Uploaden van bestanden en gegevens op een bestandsserver met behulp van standaard netwerk bestand kopiëren</span><span class="sxs-lookup"><span data-stu-id="de89e-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="de89e-121">Bestandsservers vaak organisaties gebruiken voor het opslaan van algemene gegevens.</span><span class="sxs-lookup"><span data-stu-id="de89e-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="de89e-122">Als u de servernaam of locatie, kunnen uw gebruikers het lokale netwerk voor de server te bladeren en kopieert u hun bestanden, worden er veel zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="de89e-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="de89e-123">Opnieuw moet u Windows Verkenner naar gepubliceerd RemoteApp en vervolgens te delen met uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="de89e-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="de89e-124">De bestandsserver moet op het routeerbaar netwerk die RemoteApp is geïmplementeerd in.</span><span class="sxs-lookup"><span data-stu-id="de89e-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="de89e-125">Bestanden kopiëren naar OneDrive voor bedrijven</span><span class="sxs-lookup"><span data-stu-id="de89e-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="de89e-126">Hoewel u de OneDrive voor bedrijven-synchronisatie-agent in RemoteApp niet inschakelen, kunt u nog steeds bestanden kopiëren vanaf uw UPD naar OneDrive voor bedrijven via een browser.</span><span class="sxs-lookup"><span data-stu-id="de89e-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="de89e-127">Windows Verkenner naar RemoteApp publiceren en vervolgens instrueren dat gebruikers toegang krijgen tot de bestanden via die app.</span><span class="sxs-lookup"><span data-stu-id="de89e-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="de89e-128">Het gemakkelijkst voor overdracht van bestanden als ze zijn gecomprimeerd, zodat gebruikers een ZIP-bestand met alle bestanden verplaatsen naar OneDrive voor bedrijven moeten maken.</span><span class="sxs-lookup"><span data-stu-id="de89e-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="de89e-129">Gebruikers vragen om gaat u naar de Office 365-portal en gaat u naar OneDrive en upload het ZIP-bestand.</span><span class="sxs-lookup"><span data-stu-id="de89e-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="de89e-130">Kopiëren van bestanden met behulp van stationsomleiding</span><span class="sxs-lookup"><span data-stu-id="de89e-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="de89e-131">Als u hebt ingeschakeld [station omleiding](remoteapp-redirection.md), u hebt al een toegewezen station gemaakt voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="de89e-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="de89e-132">In dit geval kunnen ze hun bestanden op de omgeleide schijf zip en slaat u deze op hun lokale PC.</span><span class="sxs-lookup"><span data-stu-id="de89e-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="de89e-133">Hoe kunnen beheerders gegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="de89e-133">How administrators can export data</span></span>

<span data-ttu-id="de89e-134">Hiermee worden beheerd voor Azure RemoteApp alle gebruikersprofielschijven (UPD exporteren kunt) voor alle collecties binnen een abonnement op Azure Storage met Azure PowerShell-cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="de89e-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="de89e-135">Er is geen mogelijkheid om afzonderlijke UPD selecteren.</span><span class="sxs-lookup"><span data-stu-id="de89e-135">There is no ability to select individual UPD's.</span></span>  <span data-ttu-id="de89e-136">Wanneer de PowerShell-opdracht wordt uitgevoerd, wordt elke schijf van de gebruiker is een 50gb in grootte van de vaste schijf en worden geëxporteerd naar Azure storage.</span><span class="sxs-lookup"><span data-stu-id="de89e-136">When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.</span></span>  <span data-ttu-id="de89e-137">Kosten van Azure storage, onmiddellijk worden voor deze opslag.</span><span class="sxs-lookup"><span data-stu-id="de89e-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="de89e-138">Wanneer u deze opdracht uitvoert ervoor te zorgen zijn er geen sessies anders het exporteren mislukt.</span><span class="sxs-lookup"><span data-stu-id="de89e-138">When running this command ensure there are no sessions otherwise the export will fail.</span></span>

<span data-ttu-id="de89e-139">UPD de voor lid van domein Azure RemoteApp-implementaties kan alleen opnieuw in een RDS-implementatie worden gebruikt, niet van het domein gekoppelde implementaties kunnen niet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de89e-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="de89e-140">Als u deze schijven worden gebruikt in een RDS-implementatie is het raadzaam om te gebruiken onze [geautomatiseerde scripts](https://github.com/arcadiahlyy/aramigration) die wordt exporteren, converteren en importeren van de UPD in een RDS-implementatie.</span><span class="sxs-lookup"><span data-stu-id="de89e-140">If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.</span></span>

