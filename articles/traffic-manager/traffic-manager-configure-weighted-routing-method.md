---
title: Routeringsmethode voor gewogen round robin-verkeer met behulp van Azure Traffic Manager configureren | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe u taken te verdelen voor verkeer met een round robin-methode in Traffic Manager
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
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="d04b8-103">De gewogen verkeersrouteringsmethode in Traffic Manager configureren</span><span class="sxs-lookup"><span data-stu-id="d04b8-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="d04b8-104">Een patroon algemene traffic routing methode is het bieden van een reeks identieke eindpunten, waaronder cloudservices en websites, en verkeer worden verzonden naar elk round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="d04b8-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="d04b8-105">De volgende stappen geven een overzicht van het configureren van dit type verkeersrouteringsmethode.</span><span class="sxs-lookup"><span data-stu-id="d04b8-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="d04b8-106">Azure Websites bieden al round robin-functionaliteit voor websites binnen een datacenter (ook wel bekend als een regio) voor taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="d04b8-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="d04b8-107">Traffic Manager kunt u de routeringsmethode voor round robin-verkeer voor websites opgeven in verschillende datacenters.</span><span class="sxs-lookup"><span data-stu-id="d04b8-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="d04b8-108">De gewogen verkeersrouteringsmethode configureren</span><span class="sxs-lookup"><span data-stu-id="d04b8-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="d04b8-109">Meld u vanuit een browser aan bij [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d04b8-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="d04b8-110">Als u nog geen account hebt, kunt u zich registreren voor een [gratis proefversie van één maand](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="d04b8-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="d04b8-111">Zoek in de portal zoekbalk, op de **Traffic Manager-profielen** en klik vervolgens op de naam van het profiel dat u wilt de routeringsmethode voor configureren.</span><span class="sxs-lookup"><span data-stu-id="d04b8-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="d04b8-112">In de **Traffic Manager-profiel** blade, Controleer of de cloudservices en de websites die u wilt opnemen in uw configuratie aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="d04b8-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="d04b8-113">In de **instellingen** sectie, klikt u op **configuratie**, en in de **configuratie** blade voltooid zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="d04b8-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="d04b8-114">Voor **verkeer van de instellingen voor verkeersroutering methode**, Controleer of de verkeersrouteringsmethode **gewogen**.</span><span class="sxs-lookup"><span data-stu-id="d04b8-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="d04b8-115">Als dit niet het geval is, klikt u op **gewogen** uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d04b8-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="d04b8-116">Stel de **monitor eindpuntinstellingen** identiek voor alle elk eindpunt binnen dit profiel als volgt:</span><span class="sxs-lookup"><span data-stu-id="d04b8-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="d04b8-117">Selecteer de relevante **Protocol**, en geef de **poort** getal.</span><span class="sxs-lookup"><span data-stu-id="d04b8-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="d04b8-118">Voor **pad** Typ een slash  */* .</span><span class="sxs-lookup"><span data-stu-id="d04b8-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="d04b8-119">U moet een pad en bestandsnaam opgeven voor het bewaken van eindpunten.</span><span class="sxs-lookup"><span data-stu-id="d04b8-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="d04b8-120">Een schuine streep naar voren '/' is een geldige invoer voor het relatieve pad en impliceert dat het bestand zich in de hoofdmap (standaard).</span><span class="sxs-lookup"><span data-stu-id="d04b8-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="d04b8-121">Klik boven aan de pagina op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d04b8-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="d04b8-122">De wijzigingen in uw configuratie als volgt testen:</span><span class="sxs-lookup"><span data-stu-id="d04b8-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="d04b8-123">In de portal zoekbalk, zoek de naam van het Traffic Manager-profiel en klik op het Traffic Manager-profiel in de resultaten die de weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d04b8-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="d04b8-124">In de **Traffic Manager** blade profiel, klikt u op **overzicht**.</span><span class="sxs-lookup"><span data-stu-id="d04b8-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="d04b8-125">De **Traffic Manager-profiel** blade bevat de DNS-naam van de zojuist gemaakte Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="d04b8-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="d04b8-126">Dit kan worden gebruikt door clients (bijvoorbeeld door te navigeren naar het met een webbrowser) te verkrijgen gerouteerd naar het juiste eindpunt als bepaald door het type routering.</span><span class="sxs-lookup"><span data-stu-id="d04b8-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="d04b8-127">In dit geval alle aanvragen worden doorgestuurd elk eindpunt round-robin toewijst.</span><span class="sxs-lookup"><span data-stu-id="d04b8-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="d04b8-128">Zodra uw Traffic Manager-profiel werkt, bewerkt u de DNS-record op de gezaghebbende DNS-server de naam van uw bedrijf domein verwijzen naar de naam van het Traffic Manager-domein.</span><span class="sxs-lookup"><span data-stu-id="d04b8-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Gewogen verkeersrouteringsmethode met Traffic Manager configureren][1]

## <a name="next-steps"></a><span data-ttu-id="d04b8-130">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d04b8-130">Next steps</span></span>

- <span data-ttu-id="d04b8-131">Meer informatie over [prioriteit van verkeer routeringsmethode](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d04b8-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="d04b8-132">Meer informatie over [prestaties methode voor het doorsturen van verkeer](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d04b8-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="d04b8-133">Meer informatie over [routeringsmethode voor geografische](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="d04b8-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="d04b8-134">Meer informatie over hoe [Traffic Manager-instellingen testen](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="d04b8-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
