---
title: aaaSizing-informatie voor een VNET in Azure RemoteApp | Microsoft Docs
description: Meer informatie over vereisten voor Hallo IP-adressen voor Azure RemoteApp uitgevoerd met een VNET
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
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="6bf1e-103">Informatie voor een VNET in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="6bf1e-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6bf1e-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="6bf1e-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="6bf1e-106">Wanneer u Azure RemoteApp gebruiken met een virtueel netwerk (VNET), gebruikt RemoteApp IP-adressen binnen het Hallo-subnet.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="6bf1e-107">Op basis van Hallo schaal van uw RemoteApp-service, moet u tooensure dat uw subnet voldoende IP-adressen beschikbaar voor RemoteApp-virtuele machines heeft.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="6bf1e-108">Terwijl deze richtlijn niet perfect gezien hoe RemoteApp dynamisch draait en draait op virtuele machines binnen een verzameling, kunt u uw subnetbereik schatten.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="6bf1e-109">Dit is vooral belangrijk als zodra een RemoteApp-service wordt geplaatst in een VNET, u Hallo subnetgrootte kan niet vergroten zonder RemoteApp worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="6bf1e-110">U hebt voor elke RemoteApp-verzameling die u toorun op de maximale capaciteit wilt, 100 IP-adressen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="6bf1e-111">Als er een RemoteApp-verzameling in hello standaard-plan en toohave Hallo maximaal 500 gebruikers gewenste, moet u bijvoorbeeld 100 IP-adressen voor deze verzameling hebt.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="6bf1e-112">Op dezelfde manier moet u 100 IP-adressen voor een RemoteApp-verzameling in hello basisniveau met 800 gebruikers.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="6bf1e-113">Als u van plan bent toohave minder gebruikers (minder dan de maximale Hallo), kunt u de benodigde per verzameling van Hallo IP-adressen beperken.</span><span class="sxs-lookup"><span data-stu-id="6bf1e-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="6bf1e-114">vereiste minimale subnet Hallo is 30 IP-adressen (/ 27).</span><span class="sxs-lookup"><span data-stu-id="6bf1e-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="6bf1e-115">Bekijk Hallo informatie toomake of dat uw VNET is geconfigureerd volgens en propertly werken:</span><span class="sxs-lookup"><span data-stu-id="6bf1e-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="6bf1e-116">Migreren van een persoonlijke VNET tooan Azure VNET</span><span class="sxs-lookup"><span data-stu-id="6bf1e-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="6bf1e-117">Hello Azure VNET toouse met Azure RemoteApp valideren</span><span class="sxs-lookup"><span data-stu-id="6bf1e-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

