---
title: Informatie voor een VNET in Azure RemoteApp | Microsoft Docs
description: Meer informatie over de vereisten voor IP-adressen voor Azure RemoteApp uitgevoerd met een VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="10199-103">Informatie voor een VNET in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="10199-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="10199-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="10199-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="10199-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="10199-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="10199-106">Wanneer u Azure RemoteApp gebruiken met een virtueel netwerk (VNET), gebruikt RemoteApp IP-adressen binnen het subnet.</span><span class="sxs-lookup"><span data-stu-id="10199-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="10199-107">Op basis van de schaal van uw RemoteApp-service, moet u ervoor zorgen dat uw subnet voldoende IP-adressen beschikbaar voor RemoteApp-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="10199-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="10199-108">Terwijl deze richtlijn niet perfect gezien hoe RemoteApp dynamisch draait en draait op virtuele machines binnen een verzameling, kunt u uw subnetbereik schatten.</span><span class="sxs-lookup"><span data-stu-id="10199-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="10199-109">Dit is vooral belangrijk als zodra een RemoteApp-service wordt geplaatst in een VNET, u kan niet groter subnet zonder RemoteApp worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="10199-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="10199-110">U hebt voor elke RemoteApp-verzameling die u wilt uitvoeren op de maximale capaciteit, 100 IP-adressen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="10199-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="10199-111">Als u een RemoteApp-verzameling in de standaard-plan hebt en u wilt dat het maximumaantal 500 gebruikers, moet u bijvoorbeeld 100 IP-adressen voor deze verzameling hebt.</span><span class="sxs-lookup"><span data-stu-id="10199-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="10199-112">Daarnaast moet u 100 IP-adressen voor een RemoteApp-collectie in het basis-plan met 800 gebruikers.</span><span class="sxs-lookup"><span data-stu-id="10199-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="10199-113">Als u van plan bent om minder gebruikers (kleiner dan het maximum), kunt u de IP-adressen per verzameling nodig verkleinen.</span><span class="sxs-lookup"><span data-stu-id="10199-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="10199-114">De vereiste minimale subnet is 30 IP-adressen (/ 27).</span><span class="sxs-lookup"><span data-stu-id="10199-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="10199-115">Het uitchecken van de volgende informatie om te controleren of uw VNET is geconfigureerd en werkt propertly:</span><span class="sxs-lookup"><span data-stu-id="10199-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="10199-116">Migreren van een persoonlijke VNET naar een Azure-VNET</span><span class="sxs-lookup"><span data-stu-id="10199-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="10199-117">Valideren van het Azure VNET gebruiken met Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="10199-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

