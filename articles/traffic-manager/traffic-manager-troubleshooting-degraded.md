---
title: Het oplossen van problemen gedegradeerd status op Azure Traffic Manager
description: Problemen met Traffic Manager-profielen wanneer deze wordt weergegeven als de status gedegradeerd.
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: b1d00fb84695d2289f37647f55a7c56cf28c8c96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="8176e-103">Het oplossen van problemen gedegradeerde status op Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8176e-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="8176e-104">In dit artikel wordt beschreven hoe een Azure Traffic Manager-profiel dat wordt weergegeven een gedegradeerde status oplossen.</span><span class="sxs-lookup"><span data-stu-id="8176e-104">This article describes how to troubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="8176e-105">Voor dit scenario kunt u een Traffic Manager-profiel die verwijst naar een deel van uw cloudapp.net gehoste services hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8176e-105">For this scenario, consider that you have configured a Traffic Manager profile pointing to some of your cloudapp.net hosted services.</span></span> <span data-ttu-id="8176e-106">Als de status van uw Traffic Manager wordt weergegeven in een **gedegradeerd** status en vervolgens de status van een of meer eindpunten mogelijk **gedegradeerd**:</span><span class="sxs-lookup"><span data-stu-id="8176e-106">If the health of your Traffic Manager displays a **Degraded** status, then the status of one or more endpoints may be **Degraded**:</span></span>

![status van gedegradeerd endpoint](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="8176e-108">Als de status van uw Traffic Manager wordt weergegeven in een **inactief** status en vervolgens beide eindpunten mogelijk **uitgeschakelde**:</span><span class="sxs-lookup"><span data-stu-id="8176e-108">If the health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Inactieve Traffic Manager-status](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="8176e-110">Understanding Traffic Manager-tests</span><span class="sxs-lookup"><span data-stu-id="8176e-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="8176e-111">Traffic Manager overweegt een eindpunt worden ONLINE alleen wanneer de test een HTTP 200-respons van het pad van de test ontvangt.</span><span class="sxs-lookup"><span data-stu-id="8176e-111">Traffic Manager considers an endpoint to be ONLINE only when the probe receives an HTTP 200 response back from the probe path.</span></span> <span data-ttu-id="8176e-112">Een ander niet-200-antwoord is een fout.</span><span class="sxs-lookup"><span data-stu-id="8176e-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="8176e-113">Een omleiding 30 x mislukt, zelfs als de omgeleide URL een 200 retourneert.</span><span class="sxs-lookup"><span data-stu-id="8176e-113">A 30x redirect fails, even if the redirected URL returns a 200.</span></span>
* <span data-ttu-id="8176e-114">Voor HTTPs-tests worden certificaatfouten genegeerd.</span><span class="sxs-lookup"><span data-stu-id="8176e-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="8176e-115">De daadwerkelijke inhoud van het pad van de test maakt niet uit als een 200 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8176e-115">The actual content of the probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="8176e-116">Scannen van een URL naar een aantal statische inhoud, zoals ' / favicon.ico ' is een algemene methode.</span><span class="sxs-lookup"><span data-stu-id="8176e-116">Probing a URL to some static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="8176e-117">Dynamische inhoud, zoals de ASP-pagina's mogelijk niet altijd retourneren, 200, zelfs wanneer de toepassing in orde is.</span><span class="sxs-lookup"><span data-stu-id="8176e-117">Dynamic content, like the ASP pages, may not always return 200, even when the application is healthy.</span></span>
* <span data-ttu-id="8176e-118">Er is een best practice naar het pad van de test ingesteld op iets wat onvoldoende logica om te bepalen heeft dat de site omhoog of omlaag is.</span><span class="sxs-lookup"><span data-stu-id="8176e-118">A best practice is to set the Probe path to something that has enough logic to determine that the site is up or down.</span></span> <span data-ttu-id="8176e-119">In het vorige voorbeeld, door het pad in te stellen op ' / favicon.ico ', u alleen bent testen die w3wp.exe reageert.</span><span class="sxs-lookup"><span data-stu-id="8176e-119">In the previous example, by setting the path to "/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="8176e-120">Deze test niet geeft aan dat uw webtoepassing in orde.</span><span class="sxs-lookup"><span data-stu-id="8176e-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="8176e-121">Een betere optie zou zijn, zoals een pad op een iets instellen ' / Probe.aspx ' die logica voor het bepalen van de status van de site is.</span><span class="sxs-lookup"><span data-stu-id="8176e-121">A better option would be to set a path to a something such as "/Probe.aspx" that has logic to determine the health of the site.</span></span> <span data-ttu-id="8176e-122">U kunt bijvoorbeeld prestatiemeteritems voor CPU-gebruik gebruiken of het aantal mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8176e-122">For example, you could use performance counters to CPU utilization or measure the number of failed requests.</span></span> <span data-ttu-id="8176e-123">Of u toegang tot bronnen van de database of sessiestatus om ervoor te zorgen dat de webtoepassing werkt kan proberen.</span><span class="sxs-lookup"><span data-stu-id="8176e-123">Or you could attempt to access database resources or session state to make sure that the web application is working.</span></span>
* <span data-ttu-id="8176e-124">Als alle eindpunten in een profiel zijn gedegradeerd, behandelt Traffic Manager alle eindpunten als goed en routes verkeer naar alle eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8176e-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic to all endpoints.</span></span> <span data-ttu-id="8176e-125">Dit gedrag zorgt ervoor dat problemen met het mechanisme voor zoek niet in een volledige onderbreking van uw service resulteren.</span><span class="sxs-lookup"><span data-stu-id="8176e-125">This behavior ensures that problems with the probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8176e-126">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8176e-126">Troubleshooting</span></span>

<span data-ttu-id="8176e-127">Voor het oplossen van een test-fout, moet u een hulpprogramma waarmee de HTTP-statuscode geretourneerd van de test-URL.</span><span class="sxs-lookup"><span data-stu-id="8176e-127">To troubleshoot a probe failure, you need a tool that shows the HTTP status code return from the probe URL.</span></span> <span data-ttu-id="8176e-128">Er zijn veel hulpprogramma's beschikbaar die u de onbewerkte HTTP-antwoord tonen.</span><span class="sxs-lookup"><span data-stu-id="8176e-128">There are many tools available that show you the raw HTTP response.</span></span>

* [<span data-ttu-id="8176e-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="8176e-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="8176e-130">cURL</span><span class="sxs-lookup"><span data-stu-id="8176e-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="8176e-131">wget</span><span class="sxs-lookup"><span data-stu-id="8176e-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="8176e-132">Bovendien kunt u het tabblad netwerk van de F12-foutopsporing hulpprogramma's in Internet Explorer om de HTTP-antwoorden weer te geven.</span><span class="sxs-lookup"><span data-stu-id="8176e-132">Also, you can use the Network tab of the F12 Debugging Tools in Internet Explorer to view the HTTP responses.</span></span>

<span data-ttu-id="8176e-133">In dit voorbeeld willen we zien van het antwoord van de WebTest-URL: http://watestsdp2008r2.cloudapp.net:80/test.</span><span class="sxs-lookup"><span data-stu-id="8176e-133">For this example we want to see the response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="8176e-134">De volgende PowerShell-voorbeeld ziet u het probleem.</span><span class="sxs-lookup"><span data-stu-id="8176e-134">The following PowerShell example illustrates the problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="8176e-135">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="8176e-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="8176e-136">U ziet dat er een omleidingsantwoord ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8176e-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="8176e-137">Zoals eerder gezegd, een StatusCode dan wordt 200 als een fout geïnterpreteerd.</span><span class="sxs-lookup"><span data-stu-id="8176e-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="8176e-138">Traffic Manager verandert de Eindpuntstatus op Offline.</span><span class="sxs-lookup"><span data-stu-id="8176e-138">Traffic Manager changes the endpoint status to Offline.</span></span> <span data-ttu-id="8176e-139">Controleer de websiteconfiguratie om ervoor te zorgen dat de juiste StatusCode kan worden geretourneerd van het pad van de test het probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="8176e-139">To resolve the problem, check the website configuration to ensure that the proper StatusCode can be returned from the probe path.</span></span> <span data-ttu-id="8176e-140">Configureer opnieuw de Traffic Manager-test om te verwijzen naar een pad op dat een 200 retourneert.</span><span class="sxs-lookup"><span data-stu-id="8176e-140">Reconfigure the Traffic Manager probe to point to a path that returns a 200.</span></span>

<span data-ttu-id="8176e-141">Als uw test het HTTPS-protocol wordt gebruikt, moet u wellicht controleren SSL/TLS om fouten te voorkomen tijdens uw test certificaat uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="8176e-141">If your probe is using the HTTPS protocol, you may need to disable certificate checking to avoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="8176e-142">De volgende PowerShell-instructies uitschakelen validatie van het servercertificaat voor de huidige PowerShell-sessie:</span><span class="sxs-lookup"><span data-stu-id="8176e-142">The following PowerShell statements disable certificate validation for the current PowerShell session:</span></span>

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a><span data-ttu-id="8176e-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8176e-143">Next Steps</span></span>

[<span data-ttu-id="8176e-144">Over verkeersrouteringsmethoden voor Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8176e-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="8176e-145">Wat is het Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8176e-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="8176e-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="8176e-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="8176e-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="8176e-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="8176e-148">Bewerkingen op Traffic Manager (REST API-referentiemateriaal)</span><span class="sxs-lookup"><span data-stu-id="8176e-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="8176e-149">[Azure Traffic Manager-Cmdlets][1]</span><span class="sxs-lookup"><span data-stu-id="8176e-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
