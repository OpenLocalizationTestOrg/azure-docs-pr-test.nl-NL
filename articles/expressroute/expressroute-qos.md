---
title: aaaQoS vereisten voor ExpressRoute | Microsoft Docs
description: Deze pagina bevat gedetailleerde vereisten voor het configureren en beheren van de QoS voor ExpressRoute-circuits.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="fe061-103">QoS-vereisten voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fe061-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="fe061-104">Skype voor Bedrijven heeft verschillende workloads die allemaal een andere QoS-behandeling vereisen.</span><span class="sxs-lookup"><span data-stu-id="fe061-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="fe061-105">Als u van plan tooconsume voice-services via ExpressRoute bent, moet u voldoen toohello vereisten die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fe061-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="fe061-106">QoS-vereisten toohello Microsoft-peering alleen van toepassing.</span><span class="sxs-lookup"><span data-stu-id="fe061-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="fe061-107">Hallo DSCP-waarden in het netwerkverkeer dat is ontvangen op openbare Azure-peering en persoonlijke Azure-peering worden too0 opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="fe061-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="fe061-108">Hallo bevat volgende tabel een lijst van DSCP-markeringen gebruikt door Skype voor bedrijven.</span><span class="sxs-lookup"><span data-stu-id="fe061-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="fe061-109">Raadpleeg te[QoS voor Skype voor bedrijven beheren](https://technet.microsoft.com/library/gg405409.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fe061-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="fe061-110">**Verkeersklasse**</span><span class="sxs-lookup"><span data-stu-id="fe061-110">**Traffic Class**</span></span> | <span data-ttu-id="fe061-111">**Behandeling (DSCP-markering)**</span><span class="sxs-lookup"><span data-stu-id="fe061-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="fe061-112">**Workloads voor Skype voor Bedrijven**</span><span class="sxs-lookup"><span data-stu-id="fe061-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe061-113">**Spraak**</span><span class="sxs-lookup"><span data-stu-id="fe061-113">**Voice**</span></span> |<span data-ttu-id="fe061-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="fe061-114">EF (46)</span></span> |<span data-ttu-id="fe061-115">Skype / Lync voice</span><span class="sxs-lookup"><span data-stu-id="fe061-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="fe061-116">**Interactief**</span><span class="sxs-lookup"><span data-stu-id="fe061-116">**Interactive**</span></span> |<span data-ttu-id="fe061-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="fe061-117">AF41 (34)</span></span> |<span data-ttu-id="fe061-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="fe061-118">Video, VBSS</span></span> |
| <span data-ttu-id="fe061-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="fe061-119">AF21 (18)</span></span> |<span data-ttu-id="fe061-120">Apps delen</span><span class="sxs-lookup"><span data-stu-id="fe061-120">App sharing</span></span> | |
| <span data-ttu-id="fe061-121">**Standaard**</span><span class="sxs-lookup"><span data-stu-id="fe061-121">**Default**</span></span> |<span data-ttu-id="fe061-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="fe061-122">AF11 (10)</span></span> |<span data-ttu-id="fe061-123">Bestandsoverdracht</span><span class="sxs-lookup"><span data-stu-id="fe061-123">File transfer</span></span> |
| <span data-ttu-id="fe061-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="fe061-124">CS0 (0)</span></span> |<span data-ttu-id="fe061-125">Overige</span><span class="sxs-lookup"><span data-stu-id="fe061-125">Anything else</span></span> | |

* <span data-ttu-id="fe061-126">U moet Hallo workloads classificeren en Hallo juiste DSCP-waarden markeren.</span><span class="sxs-lookup"><span data-stu-id="fe061-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="fe061-127">Volg de richtlijnen voor Hallo [hier](https://technet.microsoft.com/library/gg405409.aspx) over het tooset DSCP-markeringen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="fe061-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="fe061-128">U moet meerdere QoS-wachtrijen in uw netwerk configureren en ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="fe061-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="fe061-129">Voice moet een zelfstandige klasse en krijg Hallo EF-behandeling opgegeven in RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="fe061-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="fe061-130">U kunt Hallo queuing mechanisme, congestiedetectiebeleid en de bandbreedtetoewijzing per verkeersklasse bepalen.</span><span class="sxs-lookup"><span data-stu-id="fe061-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="fe061-131">Maar hello DSCP-markering voor Skype voor bedrijven-werkbelastingen moet worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="fe061-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="fe061-132">Als u DSCP-markeringen die niet wordt weergegeven, bijvoorbeeld AF31 (26), moet u deze DSCP-waarde too0 herschrijven voordat Hallo pakket tooMicrosoft worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="fe061-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="fe061-133">Microsoft verzendt alleen pakketten die zijn gemarkeerd met Hallo DSCP-waarde wordt weergegeven in Hallo bovenstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="fe061-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fe061-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe061-134">Next steps</span></span>
* <span data-ttu-id="fe061-135">Raadpleeg de vereisten voor toohello [routering](expressroute-routing.md) en [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="fe061-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="fe061-136">Zie de volgende Hallo koppelingen tooconfigure uw ExpressRoute-verbinding.</span><span class="sxs-lookup"><span data-stu-id="fe061-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="fe061-137">Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="fe061-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="fe061-138">Routering configureren</span><span class="sxs-lookup"><span data-stu-id="fe061-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="fe061-139">Koppelen van een VNet tooan ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="fe061-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

