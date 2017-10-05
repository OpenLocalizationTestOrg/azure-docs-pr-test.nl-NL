---
title: "Nooit gevoelige gegevens worden opgeslagen op aangepaste installatiekopieën voor Azure RemoteApp | Microsoft Docs"
description: "Meer informatie over de richtlijnen voor het opslaan van gegevens in aangepaste installatiekopieën in Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 75d5415d33324d957617426e75909a6c6c58b1f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="f292d-103">Nooit gevoelige gegevens worden opgeslagen op aangepaste installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="f292d-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f292d-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="f292d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f292d-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f292d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f292d-106">Wanneer u uw eigen toepassing in Azure RemoteApp-host, wordt de eerste stap is om een aangepaste installatiekopie te maken.</span><span class="sxs-lookup"><span data-stu-id="f292d-106">When you host your own application in Azure RemoteApp, the first step is to create a custom image.</span></span> <span data-ttu-id="f292d-107">We gebruiken die aangepaste installatiekopie maken van VM-exemplaren die uw apps aan uw gebruikers dienen.</span><span class="sxs-lookup"><span data-stu-id="f292d-107">We use that custom image to create VM instances that serve your apps to your users.</span></span> <span data-ttu-id="f292d-108">De aangepaste installatiekopie moet alleen toepassingen en nooit gevoelige gegevens die verloren gaan, zoals SQL-databases, personeelsbestanden of bestanden zoals QuickBooks bedrijfsbestanden speciale gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="f292d-108">The custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="f292d-109">Alle gevoelige gegevens moet zich bevinden extern voor Azure RemoteApp op een bestandsserver, een andere Azure-virtuele machine of in Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f292d-109">All sensitive data should reside external to Azure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="f292d-110">De afbeelding moet NET host voor de toepassing die is verbonden met de gegevensbron en worden de gegevens.</span><span class="sxs-lookup"><span data-stu-id="f292d-110">The image should just host the application that connects to the data source and presents the data.</span></span> <span data-ttu-id="f292d-111">Bekijk [vereisten voor Azure RemoteApp-installatiekopieën](remoteapp-imagereqs.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f292d-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="f292d-112">Om te begrijpen waarom moet u geen gevoelige gegevens opslaan, moet u begrijpen hoe Azure RemoteApp werkt.</span><span class="sxs-lookup"><span data-stu-id="f292d-112">To understand why you should not store sensitive data, you need to understand how Azure RemoteApp works.</span></span> <span data-ttu-id="f292d-113">Wanneer een verzameling is gemaakt of bijgewerkt, achter de schermen meerdere klonen of exemplaren van de afbeelding worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f292d-113">When a collection is created or updated, behind the scenes multiple clones or copies of the image are created.</span></span> <span data-ttu-id="f292d-114">Alle exemplaren van deze virtuele machine zijn exacte replica's van de aangepaste afbeelding. Wanneer gebruikers toepassingen starten die ze zijn verbonden met een van deze VM-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="f292d-114">All these VM instances are exact replicas of the custom image; when users launch applications they are connected to one of these VM instances.</span></span> <span data-ttu-id="f292d-115">Maar hetzelfde exemplaar kan niet worden gegarandeerd en moet niet van belang omdat ze niet-persistent.</span><span class="sxs-lookup"><span data-stu-id="f292d-115">But the same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="f292d-116">De VM-exemplaren die als host fungeert voor de toepassingen niet-persistent zijn en kunnen worden vernietigd of verwijderd op basis, bijvoorbeeld tijdens het bijwerken van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="f292d-116">The VM instances hosting the applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="f292d-117">Als de verzameling is ingericht en starten gebruikers de verbinding te maken met de virtuele machines, gebruikersgegevens is permanent en beveiligd, omdat het wordt opgeslagen op afzonderlijke opslag binnen een VHD die we noemen een [gebruikersprofielschijf (UDP)](remoteapp-upd.md), namelijk het gebruikersprofiel in c:\ gebruikers\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="f292d-117">Once the collection is provisioned and users start connecting to the VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is the user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="f292d-118">Wanneer een toepassing wordt gestart, wordt de UPD gekoppeld en beschouwd als een lokaal gebruikersprofiel door het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="f292d-118">When an application starts, the UPD is mounted and treated just like a local user profile by the operating system.</span></span> <span data-ttu-id="f292d-119">Lees meer over hoe [Azure RemoteApp slaat gebruikersgegevens en instellingen](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="f292d-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="f292d-120">Van de voorbeeldgegevens die niet zich in de afbeelding bevinden moet:</span><span class="sxs-lookup"><span data-stu-id="f292d-120">Example data that should not reside in the image:</span></span>

* <span data-ttu-id="f292d-121">Gegevens voor de gebruikers toegang krijgen tot gedeelde</span><span class="sxs-lookup"><span data-stu-id="f292d-121">Shared data for users to access</span></span>
* <span data-ttu-id="f292d-122">SQL-database of QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="f292d-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="f292d-123">Alle gegevens in D:\\</span><span class="sxs-lookup"><span data-stu-id="f292d-123">Any data in D:\\</span></span>

<span data-ttu-id="f292d-124">Van de voorbeeldgegevens die kunnen worden ondergebracht in het standaardprofiel moeten worden gekopieerd naar alle gebruikers UPD:</span><span class="sxs-lookup"><span data-stu-id="f292d-124">Example data that can reside in the default profile to be copied into every users’ UPD:</span></span>

* <span data-ttu-id="f292d-125">Configuratiebestanden per gebruiker</span><span class="sxs-lookup"><span data-stu-id="f292d-125">Configuration files per user</span></span>
* <span data-ttu-id="f292d-126">Scripts die gebruikers zouden moeten blijven behouden in hun UPD</span><span class="sxs-lookup"><span data-stu-id="f292d-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="f292d-127">Belangrijke punten:</span><span class="sxs-lookup"><span data-stu-id="f292d-127">Key points:</span></span>

* <span data-ttu-id="f292d-128">Nooit store gevoelige gegevens die op de installatiekopie verloren kunt bij het maken van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f292d-128">Never store sensitive data that can be lost on the image when creating a custom image.</span></span>
* <span data-ttu-id="f292d-129">Gevoelige gegevens moet altijd zich bevinden op een afzonderlijke bestandsserver afzonderlijke virtuele machine in Azure, in de cloud en altijd externe VM-exemplaren die als host fungeert voor uw toepassingen in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f292d-129">Sensitive data should always reside on a separate file server, separate Azure VM, on the cloud, and always external to the VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="f292d-130">Gegevens worden opgeslagen en de gebruiker zich blijft voordoen in de gebruikersprofielschijf (UDP)</span><span class="sxs-lookup"><span data-stu-id="f292d-130">User data is saved and persists in the user profile disk (UPD)</span></span>

