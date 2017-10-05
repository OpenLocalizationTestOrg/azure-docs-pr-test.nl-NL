---
title: Controleer de instellingen voor Azure Traffic Manager | Microsoft Docs
description: Dit artikel helpt u de instellingen van uw Traffic Manager controleren
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: aadff1806a7cb22347283143563467366e857569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="8bd13-103">Controleer de instellingen voor het Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8bd13-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="8bd13-104">Als u wilt testen van uw Traffic Manager-instellingen, moet u meerdere clients hebt, op verschillende locaties, van waaruit u kunt uw tests uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8bd13-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="8bd13-105">Breng vervolgens de eindpunten in uw Traffic Manager-profiel beneden één tegelijk.</span><span class="sxs-lookup"><span data-stu-id="8bd13-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="8bd13-106">De DNS-TTL-waarde laag ingesteld zodat wijzigingen die zijn doorgegeven snel (bijvoorbeeld 30 seconden).</span><span class="sxs-lookup"><span data-stu-id="8bd13-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="8bd13-107">De IP-adressen van uw Azure-cloudservices en websites in het profiel dat u wilt testen weten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span></span>
* <span data-ttu-id="8bd13-108">Gebruik hulpprogramma's waarmee u een DNS-naam omzetten in een IP-adres en weer te geven dat adres.</span><span class="sxs-lookup"><span data-stu-id="8bd13-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span></span>

<span data-ttu-id="8bd13-109">Om te zien dat de DNS-namen naar IP-adressen van de eindpunten in uw profiel omzetten dat u controleert.</span><span class="sxs-lookup"><span data-stu-id="8bd13-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span></span> <span data-ttu-id="8bd13-110">De namen moeten worden omgezet in samenhang met de verkeersrouteringsmethode gedefinieerd in de Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="8bd13-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span></span> <span data-ttu-id="8bd13-111">U kunt de hulpprogramma's zoals **nslookup** of **verdiepen** DNS-namen omzetten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span></span>

<span data-ttu-id="8bd13-112">De volgende voorbeelden kunnen u testen van uw Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="8bd13-112">The following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="8bd13-113">Traffic Manager-profiel met nslookup en ipconfig in Windows controleren</span><span class="sxs-lookup"><span data-stu-id="8bd13-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="8bd13-114">Open een opdracht of een Windows PowerShell-prompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="8bd13-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="8bd13-115">Type `ipconfig /flushdns` leegmaken van de cache van de DNS-resolver.</span><span class="sxs-lookup"><span data-stu-id="8bd13-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span></span>
3. <span data-ttu-id="8bd13-116">Typ `nslookup <your Traffic Manager domain name>`.</span><span class="sxs-lookup"><span data-stu-id="8bd13-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="8bd13-117">De volgende opdracht controleert bijvoorbeeld de naam van het domein met het voorvoegsel *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="8bd13-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="8bd13-118">Een typische resultaat ziet u de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8bd13-118">A typical result shows the following information:</span></span>

    + <span data-ttu-id="8bd13-119">De DNS-naam en IP-adres van de DNS-server om op te lossen dit Traffic Manager-domeinnaam wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8bd13-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="8bd13-120">De naam van het Traffic Manager-domein u hebt getypt op de opdrachtregel na 'nslookup' en het IP-adres waarnaar het Traffic Manager-domein wordt omgezet.</span><span class="sxs-lookup"><span data-stu-id="8bd13-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span></span> <span data-ttu-id="8bd13-121">Het tweede IP-adres is het belangrijk om te controleren.</span><span class="sxs-lookup"><span data-stu-id="8bd13-121">The second IP address is the important one to check.</span></span> <span data-ttu-id="8bd13-122">Deze moet overeenkomen met een openbare virtuele IP-adres (VIP)-adres voor een van de cloud-services of websites in het Traffic Manager-profiel dat u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="8bd13-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span></span>

## <a name="how-to-test-the-failover-traffic-routing-method"></a><span data-ttu-id="8bd13-123">De verkeersrouteringsmethode failover testen</span><span class="sxs-lookup"><span data-stu-id="8bd13-123">How to test the failover traffic routing method</span></span>

1. <span data-ttu-id="8bd13-124">Laat alle eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="8bd13-125">Met behulp van één client, DNS-omzetting voor de domeinnaam van uw bedrijf met nslookup of een vergelijkbaar hulpprogramma aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8bd13-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="8bd13-126">Zorg ervoor dat het omgezette IP-adres overeenkomt met het primaire eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8bd13-126">Ensure that the resolved IP address matches the primary endpoint.</span></span>
4. <span data-ttu-id="8bd13-127">Buiten uw primaire eindpunt of verwijderen van het controle-bestand, zodat die Traffic Manager denkt dat de toepassing niet actief is.</span><span class="sxs-lookup"><span data-stu-id="8bd13-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span></span>
5. <span data-ttu-id="8bd13-128">Wacht tot de DNS-Time-to-Live (TTL) van Traffic Manager-profiel plus nog twee minuten zijn verstreken.</span><span class="sxs-lookup"><span data-stu-id="8bd13-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="8bd13-129">Bijvoorbeeld, als uw DNS-TTL is 300 seconden (5 minuten), moet u wachten zeven minuten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="8bd13-130">Uw DNS-client cache en aanvraag DNS-omzetting met nslookup leegmaken.</span><span class="sxs-lookup"><span data-stu-id="8bd13-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="8bd13-131">In Windows kunt u uw DNS-cache met de opdracht ipconfig/flushdns leegmaken.</span><span class="sxs-lookup"><span data-stu-id="8bd13-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="8bd13-132">Zorg ervoor dat het omgezette IP-adres overeenkomt met uw secundaire eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8bd13-132">Ensure that the resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="8bd13-133">Herhaal dit proces, op zijn beurt omlaag elk eindpunt te brengen.</span><span class="sxs-lookup"><span data-stu-id="8bd13-133">Repeat the process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="8bd13-134">Controleer of dat de DNS-server het IP-adres van het volgende eindpunt in de lijst retourneert.</span><span class="sxs-lookup"><span data-stu-id="8bd13-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span></span> <span data-ttu-id="8bd13-135">Wanneer alle eindpunten niet beschikbaar zijn, moet u het IP-adres van het primaire eindpunt opnieuw verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="8bd13-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span></span>

## <a name="how-to-test-the-weighted-traffic-routing-method"></a><span data-ttu-id="8bd13-136">De gewogen verkeersrouteringsmethode testen</span><span class="sxs-lookup"><span data-stu-id="8bd13-136">How to test the weighted traffic routing method</span></span>

1. <span data-ttu-id="8bd13-137">Laat alle eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="8bd13-138">Met behulp van één client, DNS-omzetting voor de domeinnaam van uw bedrijf met nslookup of een vergelijkbaar hulpprogramma aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8bd13-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="8bd13-139">Zorg ervoor dat het omgezette IP-adres overeenkomt met een van de eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8bd13-139">Ensure that the resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="8bd13-140">Uw DNS-client-cache leegmaken en Herhaal stappen 2 en 3 voor elk eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8bd13-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="8bd13-141">Hier ziet u verschillende IP-adressen voor elk van uw eindpunten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8bd13-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-to-test-the-performance-traffic-routing-method"></a><span data-ttu-id="8bd13-142">Het testen van de verkeersrouteringsmethode voor prestaties</span><span class="sxs-lookup"><span data-stu-id="8bd13-142">How to test the performance traffic routing method</span></span>

<span data-ttu-id="8bd13-143">Als u wilt testen effectief prestaties verkeersrouteringsmethode, moet u de clients zich in verschillende onderdelen van de hele wereld hebben.</span><span class="sxs-lookup"><span data-stu-id="8bd13-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span></span> <span data-ttu-id="8bd13-144">U kunt clients in verschillende Azure-regio's die kunnen worden gebruikt voor het testen van uw services maken.</span><span class="sxs-lookup"><span data-stu-id="8bd13-144">You can create clients in different Azure regions that can be used to test your services.</span></span> <span data-ttu-id="8bd13-145">Als u een wereldwijd netwerk hebt, kunt u op afstand op clients in andere onderdelen van de hele wereld aanmelden en uw tests van daaruit uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8bd13-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span></span>

<span data-ttu-id="8bd13-146">U kunt ook er zijn gratis, webgebaseerde DNS-zoekopdracht en kennis van de services die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="8bd13-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="8bd13-147">Sommige van deze hulpprogramma's bieden u de mogelijkheid om te controleren van de DNS-naamomzetting vanaf verschillende locaties over de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="8bd13-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span></span> <span data-ttu-id="8bd13-148">Voer een zoekopdracht op 'DNS-zoekopdracht' voor voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8bd13-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="8bd13-149">De services van derden zoals Gomez of Keynote kunnen worden gebruikt om te bevestigen dat de profielen van uw verkeer distribueert zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="8bd13-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd13-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bd13-150">Next steps</span></span>

* [<span data-ttu-id="8bd13-151">Over verkeersrouteringsmethoden voor Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8bd13-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="8bd13-152">Prestatieoverwegingen voor Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8bd13-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="8bd13-153">Problemen met Traffic Manager in gedegradeerde status oplossen</span><span class="sxs-lookup"><span data-stu-id="8bd13-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
