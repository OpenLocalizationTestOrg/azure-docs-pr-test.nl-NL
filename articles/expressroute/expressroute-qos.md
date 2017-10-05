---
title: QoS-vereisten voor ExpressRoute | Microsoft Docs
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
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="9c783-103">QoS-vereisten voor ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9c783-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="9c783-104">Skype voor Bedrijven heeft verschillende workloads die allemaal een andere QoS-behandeling vereisen.</span><span class="sxs-lookup"><span data-stu-id="9c783-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="9c783-105">Als u via ExpressRoute voice-services wilt gaan gebruiken, moet u voldoen aan de vereisten die hieronder worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="9c783-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="9c783-106">QoS-vereisten zijn alleen van toepassing op de Microsoft-peering.</span><span class="sxs-lookup"><span data-stu-id="9c783-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="9c783-107">De DSCP-waarden in uw netwerkverkeer dat is ontvangen op Openbare Azure-peering en Persoonlijke Azure-peering wordt ingesteld op 0.</span><span class="sxs-lookup"><span data-stu-id="9c783-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="9c783-108">De volgende tabel bevat een lijst van DSCP-markeringen die worden gebruikt door Skype voor Bedrijven.</span><span class="sxs-lookup"><span data-stu-id="9c783-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="9c783-109">Raadpleeg [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) (QoS voor Skype voor Bedrijven beheren) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9c783-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="9c783-110">**Verkeersklasse**</span><span class="sxs-lookup"><span data-stu-id="9c783-110">**Traffic Class**</span></span> | <span data-ttu-id="9c783-111">**Behandeling (DSCP-markering)**</span><span class="sxs-lookup"><span data-stu-id="9c783-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="9c783-112">**Workloads voor Skype voor Bedrijven**</span><span class="sxs-lookup"><span data-stu-id="9c783-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9c783-113">**Spraak**</span><span class="sxs-lookup"><span data-stu-id="9c783-113">**Voice**</span></span> |<span data-ttu-id="9c783-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="9c783-114">EF (46)</span></span> |<span data-ttu-id="9c783-115">Skype / Lync voice</span><span class="sxs-lookup"><span data-stu-id="9c783-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="9c783-116">**Interactief**</span><span class="sxs-lookup"><span data-stu-id="9c783-116">**Interactive**</span></span> |<span data-ttu-id="9c783-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="9c783-117">AF41 (34)</span></span> |<span data-ttu-id="9c783-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="9c783-118">Video, VBSS</span></span> |
| <span data-ttu-id="9c783-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="9c783-119">AF21 (18)</span></span> |<span data-ttu-id="9c783-120">Apps delen</span><span class="sxs-lookup"><span data-stu-id="9c783-120">App sharing</span></span> | |
| <span data-ttu-id="9c783-121">**Standaard**</span><span class="sxs-lookup"><span data-stu-id="9c783-121">**Default**</span></span> |<span data-ttu-id="9c783-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="9c783-122">AF11 (10)</span></span> |<span data-ttu-id="9c783-123">Bestandsoverdracht</span><span class="sxs-lookup"><span data-stu-id="9c783-123">File transfer</span></span> |
| <span data-ttu-id="9c783-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="9c783-124">CS0 (0)</span></span> |<span data-ttu-id="9c783-125">Overige</span><span class="sxs-lookup"><span data-stu-id="9c783-125">Anything else</span></span> | |

* <span data-ttu-id="9c783-126">U moet de workloads classificeren en de juiste DSCP-waarden markeren.</span><span class="sxs-lookup"><span data-stu-id="9c783-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="9c783-127">Volg [deze](https://technet.microsoft.com/library/gg405409.aspx) richtlijnen over het instellen van DSCP-markeringen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="9c783-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="9c783-128">U moet meerdere QoS-wachtrijen in uw netwerk configureren en ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="9c783-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="9c783-129">Voice moet een zelfstandige klasse zijn en de EF-behandeling ontvangen die is opgegeven in RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="9c783-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="9c783-130">U kunt het wachtrijmechanisme, het congestiedetectiebeleid en de bandbreedtetoewijzing per verkeersklasse bepalen.</span><span class="sxs-lookup"><span data-stu-id="9c783-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="9c783-131">De DSCP-markering voor workloads voor Skype voor Bedrijven moet echter behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="9c783-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="9c783-132">Als u DSCP-markeringen gebruikt die niet worden weergegeven, bijvoorbeeld AF31 (26), moet u deze DSCP-waarde wijzigen in 0 voordat u het pakket naar Microsoft verzendt.</span><span class="sxs-lookup"><span data-stu-id="9c783-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="9c783-133">Microsoft verzendt alleen pakketten die zijn gemarkeerd met de DSCP-waarde die wordt weergegeven in de bovenstaande tabel.</span><span class="sxs-lookup"><span data-stu-id="9c783-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9c783-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9c783-134">Next steps</span></span>
* <span data-ttu-id="9c783-135">Raadpleeg de vereisten voor [Routering](expressroute-routing.md) en [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="9c783-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="9c783-136">Klik op de volgende koppelingen als u uw ExpressRoute-verbinding wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="9c783-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="9c783-137">Een ExpressRoute-circuit maken</span><span class="sxs-lookup"><span data-stu-id="9c783-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="9c783-138">Routering configureren</span><span class="sxs-lookup"><span data-stu-id="9c783-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="9c783-139">Een VNet koppelen aan een ExpressRoute-circuit</span><span class="sxs-lookup"><span data-stu-id="9c783-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

