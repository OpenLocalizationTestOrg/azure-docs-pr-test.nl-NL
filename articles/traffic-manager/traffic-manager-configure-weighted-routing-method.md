---
title: aaaConfigure gewogen round robin-verkeer met behulp van Azure Traffic Manager routeringsmethode | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooload balans vinden tussen verkeer dat gebruikmaakt van een round robin-methode in Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="600cf-103">Hallo gewogen verkeersrouteringsmethode in Traffic Manager configureren</span><span class="sxs-lookup"><span data-stu-id="600cf-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="600cf-104">Een algemene traffic routing methode patroon is tooprovide een reeks identieke eindpunten die zijn onder andere cloudservices en websites en verzenden van verkeer tooeach round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="600cf-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="600cf-105">Hallo stappen te volgen overzicht van hoe tooconfigure dit type methode voor het doorsturen van verkeer.</span><span class="sxs-lookup"><span data-stu-id="600cf-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="600cf-106">Azure Websites bieden al round robin-functionaliteit voor websites binnen een datacenter (ook wel bekend als een regio) voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="600cf-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="600cf-107">Traffic Manager kunt u toospecify round robin verkeersrouteringsmethode voor websites in verschillende datacenters.</span><span class="sxs-lookup"><span data-stu-id="600cf-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="600cf-108">verkeersrouteringsmethode hello gewogen tooconfigure</span><span class="sxs-lookup"><span data-stu-id="600cf-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="600cf-109">Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="600cf-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="600cf-110">Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="600cf-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="600cf-111">Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profielen** en klik vervolgens op Hallo profielnaam die u wilt dat tooconfigure Hallo routeringsmethode voor.</span><span class="sxs-lookup"><span data-stu-id="600cf-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="600cf-112">In Hallo **Traffic Manager-profiel** blade, Controleer of beide Hallo cloudservices en websites waartoe u tooinclude in uw configuratie aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="600cf-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="600cf-113">In Hallo **instellingen** sectie, klikt u op **configuratie**, en in Hallo **configuratie** blade voltooid zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="600cf-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="600cf-114">Voor **verkeer van de instellingen voor verkeersroutering methode**, Controleer of verkeersrouteringsmethode hello **gewogen**.</span><span class="sxs-lookup"><span data-stu-id="600cf-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="600cf-115">Als dit niet het geval is, klikt u op **gewogen** uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="600cf-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="600cf-116">Set Hallo **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:</span><span class="sxs-lookup"><span data-stu-id="600cf-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="600cf-117">Selecteer Hallo juiste **Protocol**, en geef Hallo **poort** getal.</span><span class="sxs-lookup"><span data-stu-id="600cf-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="600cf-118">Voor **pad** Typ een slash  */* .</span><span class="sxs-lookup"><span data-stu-id="600cf-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="600cf-119">toomonitor eindpunten, moet u een pad en bestandsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="600cf-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="600cf-120">Een schuine streep naar voren '/' is een geldige invoer voor Hallo relatief pad en impliceert dat Hallo-bestand is in de hoofdmap hello (standaard).</span><span class="sxs-lookup"><span data-stu-id="600cf-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="600cf-121">Bovenaan Hallo Hallo pagina, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="600cf-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="600cf-122">Hallo wijzigingen in uw configuratie als volgt testen:</span><span class="sxs-lookup"><span data-stu-id="600cf-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="600cf-123">In de zoekbalk Hallo-portal, zoeken naar Hallo Traffic Manager-profielnaam en Hallo Traffic Manager-profiel in Hallo resultaten op die Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="600cf-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="600cf-124">In Hallo **Traffic Manager** blade profiel, klikt u op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="600cf-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="600cf-125">Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="600cf-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="600cf-126">Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="600cf-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="600cf-127">In dit geval alle aanvragen worden doorgestuurd elk eindpunt round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="600cf-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="600cf-128">Als uw Traffic Manager-profiel werkt, bewerken Hallo DNS-record op de gezaghebbende DNS-server toopoint domain name toohello Traffic Manager-domeinnaam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="600cf-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Gewogen verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a><span data-ttu-id="600cf-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="600cf-130">Next steps</span></span>

- <span data-ttu-id="600cf-131">Meer informatie over [prioriteit van verkeer routeringsmethode](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="600cf-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="600cf-132">Meer informatie over [prestaties methode voor het doorsturen van verkeer](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="600cf-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="600cf-133">Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="600cf-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="600cf-134">Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="600cf-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
