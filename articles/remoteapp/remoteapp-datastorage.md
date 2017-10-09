---
title: "aaaNever store gevoelige gegevens op aangepaste installatiekopieën voor Azure RemoteApp | Microsoft Docs"
description: "Informatie over Hallo richtlijnen voor het opslaan van gegevens in aangepaste installatiekopieën in Azure RemoteApp"
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
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a><span data-ttu-id="aaa0d-103">Nooit gevoelige gegevens worden opgeslagen op aangepaste installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="aaa0d-103">Never store sensitive data on custom images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="aaa0d-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="aaa0d-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="aaa0d-106">Wanneer u uw eigen toepassing in Azure RemoteApp-host, is de eerste stap Hallo toocreate een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-106">When you host your own application in Azure RemoteApp, hello first step is toocreate a custom image.</span></span> <span data-ttu-id="aaa0d-107">We gebruiken deze aangepaste installatiekopie toocreate VM-exemplaren die uw apps tooyour gebruikers dienen.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-107">We use that custom image toocreate VM instances that serve your apps tooyour users.</span></span> <span data-ttu-id="aaa0d-108">Hallo aangepaste installatiekopie moet alleen toepassingen en nooit gevoelige gegevens die verloren gaan, zoals SQL-databases, personeelsbestanden of bestanden zoals QuickBooks bedrijfsbestanden speciale gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-108">hello custom image should contain ONLY applications and never sensitive data that can be lost, such as SQL databases, personnel files, or special data files like QuickBooks company files.</span></span> <span data-ttu-id="aaa0d-109">Alle gevoelige gegevens moet zich bevinden op externe tooAzure RemoteApp op een bestandsserver, een andere Azure-virtuele machine of in Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-109">All sensitive data should reside external tooAzure RemoteApp on a file server, another Azure VM, or in SQL Azure.</span></span> <span data-ttu-id="aaa0d-110">Hallo installatiekopie moet NET host Hallo-toepassing die is verbonden gegevensbron toohello en presenteert Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-110">hello image should just host hello application that connects toohello data source and presents hello data.</span></span> <span data-ttu-id="aaa0d-111">Bekijk [vereisten voor Azure RemoteApp-installatiekopieën](remoteapp-imagereqs.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-111">Review [Requirements for Azure RemoteApp images](remoteapp-imagereqs.md) for more information.</span></span> 

<span data-ttu-id="aaa0d-112">Waarom moet u geen gevoelige gegevens opslaan toounderstand moet u de werking van Azure RemoteApp toounderstand.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-112">toounderstand why you should not store sensitive data, you need toounderstand how Azure RemoteApp works.</span></span> <span data-ttu-id="aaa0d-113">Wanneer een verzameling is gemaakt of bijgewerkt, achter de schermen Hallo worden meerdere klonen of kopieën van Hallo installatiekopie gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-113">When a collection is created or updated, behind hello scenes multiple clones or copies of hello image are created.</span></span> <span data-ttu-id="aaa0d-114">Alle exemplaren van deze virtuele machine zijn exacte kopieën van de aangepaste installatiekopie Hallo; Wanneer gebruikers toepassingen starten zijn ze verbonden tooone van deze VM-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-114">All these VM instances are exact replicas of hello custom image; when users launch applications they are connected tooone of these VM instances.</span></span> <span data-ttu-id="aaa0d-115">Maar hello hetzelfde exemplaar kan niet worden gegarandeerd en moet niet van belang omdat ze niet-persistent.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-115">But hello same instance is not guaranteed and should not matter because they are non-persistent.</span></span> <span data-ttu-id="aaa0d-116">Hallo VM-instanties hosting Hallo toepassingen zijn niet-permanente en kunnen worden vernietigd of verwijderd op basis, bijvoorbeeld tijdens het bijwerken van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-116">hello VM instances hosting hello applications are non-persistent and can be destroyed or deleted based, for example, during collection update.</span></span> 

<span data-ttu-id="aaa0d-117">Zodra de Hallo verzameling is ingericht en starten gebruikers de verbindende toohello VM's, gebruikersgegevens is permanent en beveiligd, omdat het wordt opgeslagen op afzonderlijke opslag binnen een VHD die we noemen een [gebruikersprofielschijf (UDP)](remoteapp-upd.md), namelijk Hallo gebruikersprofiel in c:\users\<userprofile >.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-117">Once hello collection is provisioned and users start connecting toohello VMs, user data is persistent and protected because it is saved on separate storage within a VHD that we call a [user profile disk (UPD)](remoteapp-upd.md), which is hello user profile in c:\users\<userprofile>.</span></span> <span data-ttu-id="aaa0d-118">Wanneer een toepassing wordt gestart, wordt de Hallo UPD gekoppeld en de behandeld net als een lokaal gebruikersprofiel door Hallo-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-118">When an application starts, hello UPD is mounted and treated just like a local user profile by hello operating system.</span></span> <span data-ttu-id="aaa0d-119">Lees meer over hoe [Azure RemoteApp slaat gebruikersgegevens en instellingen](remoteapp-upd.md).</span><span class="sxs-lookup"><span data-stu-id="aaa0d-119">Read more about how [Azure RemoteApp saves user data and settings](remoteapp-upd.md).</span></span>

<span data-ttu-id="aaa0d-120">Van de voorbeeldgegevens die niet zich in de installatiekopie van het Hallo bevinden moet:</span><span class="sxs-lookup"><span data-stu-id="aaa0d-120">Example data that should not reside in hello image:</span></span>

* <span data-ttu-id="aaa0d-121">Gedeelde gegevensbron voor gebruikers tooaccess</span><span class="sxs-lookup"><span data-stu-id="aaa0d-121">Shared data for users tooaccess</span></span>
* <span data-ttu-id="aaa0d-122">SQL-database of QuickBooks DB</span><span class="sxs-lookup"><span data-stu-id="aaa0d-122">SQL DB or QuickBooks DB</span></span>
* <span data-ttu-id="aaa0d-123">Alle gegevens in D:\\</span><span class="sxs-lookup"><span data-stu-id="aaa0d-123">Any data in D:\\</span></span>

<span data-ttu-id="aaa0d-124">Van de voorbeeldgegevens die kunnen worden ondergebracht in Hallo standaard profiel toobe gekopieerd naar alle gebruikers UPD:</span><span class="sxs-lookup"><span data-stu-id="aaa0d-124">Example data that can reside in hello default profile toobe copied into every users’ UPD:</span></span>

* <span data-ttu-id="aaa0d-125">Configuratiebestanden per gebruiker</span><span class="sxs-lookup"><span data-stu-id="aaa0d-125">Configuration files per user</span></span>
* <span data-ttu-id="aaa0d-126">Scripts die gebruikers zouden moeten blijven behouden in hun UPD</span><span class="sxs-lookup"><span data-stu-id="aaa0d-126">Scripts that users would need preserved in their UPD</span></span>

<span data-ttu-id="aaa0d-127">Belangrijke punten:</span><span class="sxs-lookup"><span data-stu-id="aaa0d-127">Key points:</span></span>

* <span data-ttu-id="aaa0d-128">Sla nooit gevoelige gegevens die gaan op Hallo installatiekopie verloren kunnen bij het maken van een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-128">Never store sensitive data that can be lost on hello image when creating a custom image.</span></span>
* <span data-ttu-id="aaa0d-129">Gevoelige gegevens moet altijd zich bevinden op een afzonderlijke bestandsserver, afzonderlijke virtuele machine in Azure, op Hallo cloud en altijd externe toohello VM-exemplaren die als host fungeert voor uw toepassingen in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="aaa0d-129">Sensitive data should always reside on a separate file server, separate Azure VM, on hello cloud, and always external toohello VM instances hosting your applications within Azure RemoteApp.</span></span> 
* <span data-ttu-id="aaa0d-130">Gegevens worden opgeslagen en de gebruiker zich blijft voordoen in Hallo gebruikersprofielschijf (UDP)</span><span class="sxs-lookup"><span data-stu-id="aaa0d-130">User data is saved and persists in hello user profile disk (UPD)</span></span>

