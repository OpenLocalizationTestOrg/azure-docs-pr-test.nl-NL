---
title: Met behulp van App-V-apps met Azure RemoteApp | Microsoft Docs
description: Informatie over het gebruik van App-V-apps in Azure RemoteApp.
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
ms.openlocfilehash: e55bb8db83c04025c46b383a9ebbef4399178116
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-app-v-apps-in-azure-remoteapp"></a><span data-ttu-id="37af3-103">App-V-apps gebruiken in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="37af3-103">Using App-V apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="37af3-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="37af3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="37af3-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="37af3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="37af3-106">U kunt App-V-toepassingen gebruiken in een Azure RemoteApp hybride verzameling waarvoor domein is vereist.</span><span class="sxs-lookup"><span data-stu-id="37af3-106">You can use App-V applications in a Azure RemoteApp hybrid collection, which requires domain join.</span></span>

<span data-ttu-id="37af3-107">Voordat u begint, zorg ervoor dat de App-V 5.1-client installeren met de meest recente updates.</span><span class="sxs-lookup"><span data-stu-id="37af3-107">Before you get started, make sure to install the App-V 5.1 client with the latest updates.</span></span> <span data-ttu-id="37af3-108">U moet maken een [aangepaste installatiekopie](remoteapp-create-custom-image.md) die de App-V-client bevat.</span><span class="sxs-lookup"><span data-stu-id="37af3-108">You will need to create a [custom image](remoteapp-create-custom-image.md) that includes the App-V client.</span></span>  

<span data-ttu-id="37af3-109">Het is gemakkelijk het gebruik van uw bestaande App-V-infrastructuur met Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="37af3-109">It’s easy to use your existing App-V infrastructure with Azure RemoteApp.</span></span> <span data-ttu-id="37af3-110">Aangezien een hybride verzameling wordt geïmplementeerd in een Azure VNET dat toegang tot uw domeincontroller heeft en de virtuele machines verbonden met het domein worden, kunt u gebruikmaken van uw bestaande App-v-infrastructuur- en implementatiemethodes easyily host App-V-toepassing in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="37af3-110">Since a hybrid collection is deployed into an Azure VNET that has access to your domain controller and the VMs are domain joined, you can leverage your existing App-v infrastructure and deployment methods to easyily host App-V application in Azure RemoteApp.</span></span> <span data-ttu-id="37af3-111">Hier volgen enkele overwegingen die u moet rekening houden met op basis van het type App-V-implementatie die u momenteel hebt:</span><span class="sxs-lookup"><span data-stu-id="37af3-111">Here are some considerations that you should be aware of based on the type of App-V deployment you currently have:</span></span>

| <span data-ttu-id="37af3-112">Configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="37af3-112">Configuration options</span></span> |  | <span data-ttu-id="37af3-113">Positief</span><span class="sxs-lookup"><span data-stu-id="37af3-113">Positive</span></span> | <span data-ttu-id="37af3-114">Negatieve</span><span class="sxs-lookup"><span data-stu-id="37af3-114">Negative</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="37af3-115">Leveringsmethode</span><span class="sxs-lookup"><span data-stu-id="37af3-115">Delivery method</span></span> |<span data-ttu-id="37af3-116">Streaming (op aanvraag)</span><span class="sxs-lookup"><span data-stu-id="37af3-116">Streaming (on-demand)</span></span> |<span data-ttu-id="37af3-117">App is altijd de meest recente en nieuwe</span><span class="sxs-lookup"><span data-stu-id="37af3-117">App is always the latest and fresh</span></span> |<span data-ttu-id="37af3-118">Eerste wachttijd</span><span class="sxs-lookup"><span data-stu-id="37af3-118">First time latency</span></span> |
| <span data-ttu-id="37af3-119">Gekoppeld</span><span class="sxs-lookup"><span data-stu-id="37af3-119">Mounted</span></span> |<span data-ttu-id="37af3-120">Snelste; App is al aanwezig op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="37af3-120">Fastest; app is already present on the VM</span></span> |<span data-ttu-id="37af3-121">Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB)</span><span class="sxs-lookup"><span data-stu-id="37af3-121">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="37af3-122">App-locatie-opslag</span><span class="sxs-lookup"><span data-stu-id="37af3-122">App location storage</span></span> |<span data-ttu-id="37af3-123">Gedeelde inhoud</span><span class="sxs-lookup"><span data-stu-id="37af3-123">Shared content</span></span> |<span data-ttu-id="37af3-124">App wordt uitgevoerd in het geheugen van Azure RemoteApp-exemplaar</span><span class="sxs-lookup"><span data-stu-id="37af3-124">App runs in memory of Azure RemoteApp instance</span></span> |<span data-ttu-id="37af3-125">Eats geheugen en goede verbinding met streaming (bestandsserver) waarin de app zich bevindt</span><span class="sxs-lookup"><span data-stu-id="37af3-125">Eats memory and good connection to streaming (file) server where the app resides</span></span> |
| <span data-ttu-id="37af3-126">Schijf (in cache)</span><span class="sxs-lookup"><span data-stu-id="37af3-126">Disk (Cached)</span></span> |<span data-ttu-id="37af3-127">Snel kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37af3-127">Fast execution.</span></span> <span data-ttu-id="37af3-128">De App is niet afhankelijk van beschikbaarheid van de inhoudsbron</span><span class="sxs-lookup"><span data-stu-id="37af3-128">App not dependent on availability of Content Source</span></span> |<span data-ttu-id="37af3-129">Gegevensophoping - inneemt installatiekopie ruimte (maximaal 127 GB)</span><span class="sxs-lookup"><span data-stu-id="37af3-129">Bloat - takes up image space (127 GB limit)</span></span> | |
| <span data-ttu-id="37af3-130">Doelen</span><span class="sxs-lookup"><span data-stu-id="37af3-130">Targeting</span></span> |<span data-ttu-id="37af3-131">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="37af3-131">User</span></span> |<span data-ttu-id="37af3-132">Volledige zelfstandige App-V-infrastructuur vereist</span><span class="sxs-lookup"><span data-stu-id="37af3-132">Requires full standalone App-V infrastructure</span></span> | |
| <span data-ttu-id="37af3-133">Global (computer)</span><span class="sxs-lookup"><span data-stu-id="37af3-133">Global (machine)</span></span> |<span data-ttu-id="37af3-134">Vooraf publiceren of de publicatie met als doel server</span><span class="sxs-lookup"><span data-stu-id="37af3-134">Pre-publish or target using Publishing server</span></span> |<span data-ttu-id="37af3-135">Moet uw Azure-installatiekopie bijwerken als u wilt bijwerken van de app (grote).</span><span class="sxs-lookup"><span data-stu-id="37af3-135">Need to update your Azure image if you want to update the app (huge).</span></span> <span data-ttu-id="37af3-136">Neemt enige ruimte vrij op de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="37af3-136">Takes up some space on image.</span></span> | |

 <span data-ttu-id="37af3-137">Nadat u uw aangepaste installatiekopie en uw hybride verzameling maakt, uw toepassing publiceren, gebruikers toe te wijzen en profiteer van uw bestaande App-V-toepassingen die worden gehost in Azure RemoteApp geleverd aan elk apparaat een willekeurige plaats.</span><span class="sxs-lookup"><span data-stu-id="37af3-137">After you create your custom image and your hybrid collection, publish your application, assign users and enjoy your existing App-V applications hosted in Azure RemoteApp delivered to any device anywhere.</span></span>

