---
title: aaaUsing App-V-apps met Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toouse App-V-apps in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e2292cb2-5c89-4b2b-ab11-74dbacd07c31
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cf5c2eeee2a0ce2cf98e1cf6497dffbc6eff016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="bb0fb-103">App-V-apps gebruiken in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="bb0fb-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="bb0fb-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="bb0fb-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="bb0fb-106">U kunt App-V-toepassingen gebruiken in een Azure RemoteApp hybride verzameling waarvoor domein is vereist.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="bb0fb-107">Voordat u begint, zorg ervoor dat tooinstall Hallo App-V 5.1 client met de meest recente updates Hallo.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-107">Before you get started, make sure tooinstall hello App-V 5.1 client with hello latest updates.</span></span> <span data-ttu-id="bb0fb-108">U moet toocreate een [aangepaste installatiekopie](remoteapp-create-custom-image.md) die Hallo App-V-client bevat.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-108">You will need toocreate a [custom image](remoteapp-create-custom-image.md) that includes hello App-V client.</span></span>  

<span data-ttu-id="bb0fb-109">Het is gemakkelijk toouse uw bestaande App-V-infrastructuur met Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-109">It’s easy toouse your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="bb0fb-110">Aangezien een hybride verzameling wordt geïmplementeerd in een Azure VNET dat toegang tooyour domeincontroller heeft en Hallo VM's verbonden met het domein zijn, kunt u gebruikmaken van uw bestaande App-v-infrastructuur en implementatie methoden tooeasyily host App-V-toepassing in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-110">Since a hybrid collection is deployed into an Azure VNET that has access tooyour domain controller and hello VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods tooeasyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="bb0fb-111">Hier volgen enkele overwegingen die u moet rekening houden met op basis van App-V-implementatie die u momenteel hebt Hallo type:</span><span class="sxs-lookup"><span data-stu-id="bb0fb-111">Here are some considerations that you should be aware of based on hello type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="bb0fb-112">Configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="bb0fb-112">Configuration options</span></span> |  | <span data-ttu-id="bb0fb-113">Positief</span><span class="sxs-lookup"><span data-stu-id="bb0fb-113">Positive</span></span> | <span data-ttu-id="bb0fb-114">Negatieve</span><span class="sxs-lookup"><span data-stu-id="bb0fb-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb0fb-115">Leveringsmethode</span><span class="sxs-lookup"><span data-stu-id="bb0fb-115">Delivery method</span></span> |<span data-ttu-id="bb0fb-116">Streaming (op aanvraag)</span><span class="sxs-lookup"><span data-stu-id="bb0fb-116">Streaming (on-demand)</span></span> |<span data-ttu-id="bb0fb-117">App is altijd Hallo nieuwste en nieuwe</span><span class="sxs-lookup"><span data-stu-id="bb0fb-117">App is always hello latest and fresh</span></span> |<span data-ttu-id="bb0fb-118">Eerste wachttijd</span><span class="sxs-lookup"><span data-stu-id="bb0fb-118">First time latency</span></span> |
| <span data-ttu-id="bb0fb-119">Gekoppeld</span><span class="sxs-lookup"><span data-stu-id="bb0fb-119">Mounted</span></span> |<span data-ttu-id="bb0fb-120">Snelste; App is al aanwezig op Hallo VM</span><span class="sxs-lookup"><span data-stu-id="bb0fb-120">Fastest; app is already present on hello VM</span></span> |<span data-ttu-id="bb0fb-121">Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB)</span><span class="sxs-lookup"><span data-stu-id="bb0fb-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="bb0fb-122">App-locatie-opslag</span><span class="sxs-lookup"><span data-stu-id="bb0fb-122">App location storage</span></span> |<span data-ttu-id="bb0fb-123">Gedeelde inhoud</span><span class="sxs-lookup"><span data-stu-id="bb0fb-123">Shared content</span></span> |<span data-ttu-id="bb0fb-124">App wordt uitgevoerd in het geheugen van Azure RemoteApp-exemplaar</span><span class="sxs-lookup"><span data-stu-id="bb0fb-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="bb0fb-125">Eats geheugen en goede verbinding toostreaming (bestand) server waarop app Hallo zich bevindt</span><span class="sxs-lookup"><span data-stu-id="bb0fb-125">Eats memory and good connection toostreaming (file) server where hello app resides</span></span> |
| <span data-ttu-id="bb0fb-126">Schijf (in cache)</span><span class="sxs-lookup"><span data-stu-id="bb0fb-126">Disk (Cached)</span></span> |<span data-ttu-id="bb0fb-127">Snel kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-127">Fast execution.</span></span> <span data-ttu-id="bb0fb-128">De App is niet afhankelijk van beschikbaarheid van de inhoudsbron</span><span class="sxs-lookup"><span data-stu-id="bb0fb-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="bb0fb-129">Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB)</span><span class="sxs-lookup"><span data-stu-id="bb0fb-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="bb0fb-130">Doelen</span><span class="sxs-lookup"><span data-stu-id="bb0fb-130">Targeting</span></span> |<span data-ttu-id="bb0fb-131">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="bb0fb-131">User</span></span> |<span data-ttu-id="bb0fb-132">Volledige zelfstandige App-V-infrastructuur vereist</span><span class="sxs-lookup"><span data-stu-id="bb0fb-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="bb0fb-133">Global (computer)</span><span class="sxs-lookup"><span data-stu-id="bb0fb-133">Global (machine)</span></span> |<span data-ttu-id="bb0fb-134">Vooraf publiceren of de publicatie met als doel server</span><span class="sxs-lookup"><span data-stu-id="bb0fb-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="bb0fb-135">Moet tooupdate uw afbeelding voor Azure als u wilt dat tooupdate Hallo app (grote).</span><span class="sxs-lookup"><span data-stu-id="bb0fb-135">Need tooupdate your Azure image if you want tooupdate hello app (huge).</span></span> <span data-ttu-id="bb0fb-136">Neemt enige ruimte vrij op de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="bb0fb-137">Nadat u uw aangepaste installatiekopie en uw hybride verzameling maakt, uw toepassing publiceren, gebruikers toe te wijzen en profiteer van uw bestaande App-V-toepassingen die worden gehost in Azure RemoteApp tooany apparaat overal geleverd.</span><span class="sxs-lookup"><span data-stu-id="bb0fb-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered tooany device anywhere.</span></span>

