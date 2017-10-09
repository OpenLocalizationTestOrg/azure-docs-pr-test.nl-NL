---
title: een bedrijf Internet domein tooa Traffic Manager-domeinnaam aaaPoint | Microsoft Docs
description: In dit artikel helpt u uw bedrijf domain name tooa Traffic Manager-domeinnaam wijst.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="aad8d-103">Wijs een bedrijf Internet domein tooan Azure Traffic Manager-domein</span><span class="sxs-lookup"><span data-stu-id="aad8d-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="aad8d-104">Wanneer u een Traffic Manager-profiel maakt, wijst Azure automatisch een DNS-naam toe voor dat profiel.</span><span class="sxs-lookup"><span data-stu-id="aad8d-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="aad8d-105">toouse een naam van uw DNS-zone, een DNS CNAME-record maken die wijst toohello domeinnaam van uw Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="aad8d-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="aad8d-106">U vindt Hallo Traffic Manager-domeinnaam in Hallo **algemene** sectie op de configuratiepagina Hallo Hallo Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="aad8d-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="aad8d-107">Bijvoorbeeld: toopoint naam www.contoso.com toohello contoso.trafficmanager.net van Traffic Manager-DNS-naam, maakt u Hallo DNS-resourcerecord te volgen:</span><span class="sxs-lookup"><span data-stu-id="aad8d-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="aad8d-108">Alle aanvragen te*www.contoso.com* te worden doorgestuurd*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="aad8d-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aad8d-109">U een tweede niveau domein, zoals kan niet verwijzen *contoso.com*, toohello Traffic Manager-domein.</span><span class="sxs-lookup"><span data-stu-id="aad8d-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="aad8d-110">DNS-protocolstandaarden staan geen CNAME-records toe voor domeinnamen van het tweede niveau.</span><span class="sxs-lookup"><span data-stu-id="aad8d-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aad8d-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aad8d-111">Next steps</span></span>

* [<span data-ttu-id="aad8d-112">Methoden voor het doorsturen van Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="aad8d-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="aad8d-113">Traffic Manager - Een profiel uitschakelen, inschakelen of verwijderen</span><span class="sxs-lookup"><span data-stu-id="aad8d-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="aad8d-114">Traffic Manager - Een eindpunt in- of uitschakelen</span><span class="sxs-lookup"><span data-stu-id="aad8d-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
