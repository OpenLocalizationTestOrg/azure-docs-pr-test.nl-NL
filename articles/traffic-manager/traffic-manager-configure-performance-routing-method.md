---
title: aaaConfigure prestaties verkeer routeringsmethode met Azure Traffic Manager | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooconfigure Traffic Manager tooroute toohello eindpunt verkeer met de laagste latentie
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a><span data-ttu-id="f3cdc-103">Hallo verkeersrouteringsmethode voor prestaties configureren</span><span class="sxs-lookup"><span data-stu-id="f3cdc-103">Configure hello performance traffic routing method</span></span>

<span data-ttu-id="f3cdc-104">Hallo verkeersrouteringsmethode prestaties kunt u toodirect verkeer toohello eindpunt met de laagste latentie Hallo van Hallo clientnetwerk.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-104">hello Performance traffic routing method allows you toodirect traffic toohello endpoint with hello lowest latency from hello client's network.</span></span> <span data-ttu-id="f3cdc-105">Hallo-datacenter met de laagste latentie Hallo is doorgaans Hallo dichtstbijzijnde in geografische afstand.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-105">Typically, hello datacenter with hello lowest latency is hello closest in geographic distance.</span></span> <span data-ttu-id="f3cdc-106">Deze methode voor het doorsturen van verkeer kan geen account voor realtime-wijzigingen in de netwerkconfiguratie of laden.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="tooconfigure-performance-routing-method"></a><span data-ttu-id="f3cdc-107">routeringsmethode voor prestaties tooconfigure</span><span class="sxs-lookup"><span data-stu-id="f3cdc-107">tooconfigure performance routing method</span></span>

1. <span data-ttu-id="f3cdc-108">Aanmelden via een browser toohello [Azure-portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-108">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f3cdc-109">Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="f3cdc-110">Zoek in de zoekbalk Hallo-portal, op Hallo **Traffic Manager-profielen** en klik vervolgens op Hallo profielnaam die u wilt dat tooconfigure Hallo routeringsmethode voor.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-110">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="f3cdc-111">In Hallo **Traffic Manager-profiel** blade, Controleer of beide Hallo cloudservices en websites waartoe u tooinclude in uw configuratie aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-111">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="f3cdc-112">In Hallo **instellingen** sectie, klikt u op **configuratie**, en in Hallo **configuratie** blade voltooid zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="f3cdc-112">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="f3cdc-113">Voor **verkeer van de instellingen voor verkeersroutering methode**, voor **routeringsmethode** Selecteer **prestaties**.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="f3cdc-114">Set Hallo **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:</span><span class="sxs-lookup"><span data-stu-id="f3cdc-114">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="f3cdc-115">Selecteer Hallo juiste **Protocol**, en geef Hallo **poort** getal.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-115">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="f3cdc-116">Voor **pad** Typ een slash  */* .</span><span class="sxs-lookup"><span data-stu-id="f3cdc-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="f3cdc-117">toomonitor eindpunten, moet u een pad en bestandsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-117">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="f3cdc-118">Een schuine streep naar voren '/' is een geldige invoer voor Hallo relatief pad en impliceert dat Hallo-bestand is in de hoofdmap hello (standaard).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-118">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="f3cdc-119">Bovenaan Hallo Hallo pagina, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-119">At hello top of hello page, click **Save**.</span></span>
5.  <span data-ttu-id="f3cdc-120">Hallo wijzigingen in uw configuratie als volgt testen:</span><span class="sxs-lookup"><span data-stu-id="f3cdc-120">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="f3cdc-121">In de zoekbalk Hallo-portal, zoeken naar Hallo Traffic Manager-profielnaam en Hallo Traffic Manager-profiel in Hallo resultaten op die Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-121">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="f3cdc-122">In Hallo **Traffic Manager** blade profiel, klikt u op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-122">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="f3cdc-123">Hallo **Traffic Manager-profiel** blade Hallo DNS-naam van de zojuist gemaakte Traffic Manager-profiel wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-123">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="f3cdc-124">Dit kan worden gebruikt door alle clients (bijvoorbeeld door te gaan met een webbrowser tooit) tooget gerouteerd toohello eindpunt rechts zoals wordt bepaald door de routeringstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-124">This can be used by any clients (for example, by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="f3cdc-125">In dit geval worden alle aanvragen gerouteerde toohello eindpunt met de laagste latentie Hallo van Hallo clientnetwerk.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-125">In this case all requests are routed toohello endpoint with hello lowest latency from hello client's network.</span></span>
6. <span data-ttu-id="f3cdc-126">Als uw Traffic Manager-profiel werkt, bewerken Hallo DNS-record op de gezaghebbende DNS-server toopoint domain name toohello Traffic Manager-domeinnaam van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="f3cdc-126">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Prestaties verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a><span data-ttu-id="f3cdc-128">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f3cdc-128">Next steps</span></span>

- <span data-ttu-id="f3cdc-129">Meer informatie over [verkeersrouteringsmethode gewogen](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="f3cdc-130">Meer informatie over [routeringsmethode voor prioriteit](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="f3cdc-131">Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="f3cdc-132">Meer informatie over hoe te[Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="f3cdc-132">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png