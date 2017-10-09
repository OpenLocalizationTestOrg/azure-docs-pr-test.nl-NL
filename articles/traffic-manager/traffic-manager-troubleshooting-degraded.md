---
title: status van gedegradeerd aaaTroubleshooting op Azure Traffic Manager
description: Hoe tootroubleshoot Traffic Manager-profielen wanneer deze wordt weergegeven als gedegradeerd status.
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
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a><span data-ttu-id="8b752-103">Het oplossen van problemen gedegradeerde status op Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8b752-103">Troubleshooting degraded state on Azure Traffic Manager</span></span>

<span data-ttu-id="8b752-104">Dit artikel wordt beschreven hoe een Azure Traffic Manager-profiel tootroubleshoot die wordt weergegeven een gedegradeerde status.</span><span class="sxs-lookup"><span data-stu-id="8b752-104">This article describes how tootroubleshoot an Azure Traffic Manager profile that is showing a degraded status.</span></span> <span data-ttu-id="8b752-105">Voor dit scenario kunt u een Traffic Manager-profiel wijst toosome van uw cloudapp.net gehoste services hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-105">For this scenario, consider that you have configured a Traffic Manager profile pointing toosome of your cloudapp.net hosted services.</span></span> <span data-ttu-id="8b752-106">Als Hallo status van uw Traffic Manager wordt weergegeven in een **gedegradeerd** status en vervolgens Hallo status van een of meer eindpunten mogelijk **gedegradeerd**:</span><span class="sxs-lookup"><span data-stu-id="8b752-106">If hello health of your Traffic Manager displays a **Degraded** status, then hello status of one or more endpoints may be **Degraded**:</span></span>

![status van gedegradeerd endpoint](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

<span data-ttu-id="8b752-108">Als Hallo status van uw Traffic Manager wordt weergegeven in een **inactief** status en vervolgens beide eindpunten mogelijk **uitgeschakelde**:</span><span class="sxs-lookup"><span data-stu-id="8b752-108">If hello health of your Traffic Manager displays an **Inactive** status, then both end points may be **Disabled**:</span></span>

![Inactieve Traffic Manager-status](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a><span data-ttu-id="8b752-110">Understanding Traffic Manager-tests</span><span class="sxs-lookup"><span data-stu-id="8b752-110">Understanding Traffic Manager probes</span></span>

* <span data-ttu-id="8b752-111">Traffic Manager overweegt een eindpunt toobe ONLINE alleen wanneer Hallo test een HTTP 200-respons ontvangt back vanaf Hallo test pad.</span><span class="sxs-lookup"><span data-stu-id="8b752-111">Traffic Manager considers an endpoint toobe ONLINE only when hello probe receives an HTTP 200 response back from hello probe path.</span></span> <span data-ttu-id="8b752-112">Een ander niet-200-antwoord is een fout.</span><span class="sxs-lookup"><span data-stu-id="8b752-112">Any other non-200 response is a failure.</span></span>
* <span data-ttu-id="8b752-113">Een omleiding 30 x mislukt, zelfs als Hallo omgeleid URL retourneert een 200.</span><span class="sxs-lookup"><span data-stu-id="8b752-113">A 30x redirect fails, even if hello redirected URL returns a 200.</span></span>
* <span data-ttu-id="8b752-114">Voor HTTPs-tests worden certificaatfouten genegeerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-114">For HTTPs probes, certificate errors are ignored.</span></span>
* <span data-ttu-id="8b752-115">de daadwerkelijke inhoud Hallo van Hallo test pad maakt niet uit als een 200 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-115">hello actual content of hello probe path doesn't matter, as long as a 200 is returned.</span></span> <span data-ttu-id="8b752-116">Scannen van de like voor statische inhoud van een URL-toosome ' / favicon.ico ' is een algemene methode.</span><span class="sxs-lookup"><span data-stu-id="8b752-116">Probing a URL toosome static content like "/favicon.ico" is a common technique.</span></span> <span data-ttu-id="8b752-117">Dynamische inhoud, zoals Hallo ASP-pagina's mogelijk niet altijd retourneren, 200, zelfs wanneer de toepassing hello in orde is.</span><span class="sxs-lookup"><span data-stu-id="8b752-117">Dynamic content, like hello ASP pages, may not always return 200, even when hello application is healthy.</span></span>
* <span data-ttu-id="8b752-118">Een aanbevolen procedure is tooset Hallo test pad toosomething met voldoende toodetermine logica die site Hallo omhoog of omlaag is.</span><span class="sxs-lookup"><span data-stu-id="8b752-118">A best practice is tooset hello Probe path toosomething that has enough logic toodetermine that hello site is up or down.</span></span> <span data-ttu-id="8b752-119">In Hallo vorige voorbeeld door in te stellen hello pad too"/favicon.ico", kunt u alleen die w3wp.exe testen reageert.</span><span class="sxs-lookup"><span data-stu-id="8b752-119">In hello previous example, by setting hello path too"/favicon.ico", you are only testing that w3wp.exe is responding.</span></span> <span data-ttu-id="8b752-120">Deze test niet geeft aan dat uw webtoepassing in orde.</span><span class="sxs-lookup"><span data-stu-id="8b752-120">This probe may not indicate that your web application is healthy.</span></span> <span data-ttu-id="8b752-121">Een betere optie zou worden tooset een tooa pad iets zoals ' / Probe.aspx ' die logica toodetermine Hallo status van Hallo site heeft.</span><span class="sxs-lookup"><span data-stu-id="8b752-121">A better option would be tooset a path tooa something such as "/Probe.aspx" that has logic toodetermine hello health of hello site.</span></span> <span data-ttu-id="8b752-122">Bijvoorbeeld, kunt u prestaties tellers tooCPU gebruik of meting Hallo aantal mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="8b752-122">For example, you could use performance counters tooCPU utilization or measure hello number of failed requests.</span></span> <span data-ttu-id="8b752-123">Of u kan proberen tooaccess databaseresources of sessie status toomake of webtoepassing Hallo werkt.</span><span class="sxs-lookup"><span data-stu-id="8b752-123">Or you could attempt tooaccess database resources or session state toomake sure that hello web application is working.</span></span>
* <span data-ttu-id="8b752-124">Als alle eindpunten in een profiel zijn gedegradeerd, klikt u vervolgens alle eindpunten in Traffic Manager wordt beschouwd als goed en routes verkeer tooall eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8b752-124">If all endpoints in a profile are degraded, then Traffic Manager treats all endpoints as healthy and routes traffic tooall endpoints.</span></span> <span data-ttu-id="8b752-125">Dit gedrag zorgt ervoor dat problemen met Hallo probing mechanisme niet in een volledige onderbreking van uw service resulteren.</span><span class="sxs-lookup"><span data-stu-id="8b752-125">This behavior ensures that problems with hello probing mechanism do not result in a complete outage of your service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8b752-126">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="8b752-126">Troubleshooting</span></span>

<span data-ttu-id="8b752-127">tootroubleshoot een test-fout, moet u een hulpprogramma waarmee Hallo HTTP-statuscode geretourneerd uit Hallo WebTest-URL.</span><span class="sxs-lookup"><span data-stu-id="8b752-127">tootroubleshoot a probe failure, you need a tool that shows hello HTTP status code return from hello probe URL.</span></span> <span data-ttu-id="8b752-128">Er zijn veel hulpprogramma's beschikbaar die u onbewerkte HTTP-antwoord Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="8b752-128">There are many tools available that show you hello raw HTTP response.</span></span>

* [<span data-ttu-id="8b752-129">Fiddler</span><span class="sxs-lookup"><span data-stu-id="8b752-129">Fiddler</span></span>](http://www.telerik.com/fiddler)
* [<span data-ttu-id="8b752-130">cURL</span><span class="sxs-lookup"><span data-stu-id="8b752-130">curl</span></span>](https://curl.haxx.se/)
* [<span data-ttu-id="8b752-131">wget</span><span class="sxs-lookup"><span data-stu-id="8b752-131">wget</span></span>](http://gnuwin32.sourceforge.net/packages/wget.htm)

<span data-ttu-id="8b752-132">U kunt ook Hallo netwerk tabblad Hallo F12 foutopsporing extra in Internet Explorer tooview Hallo HTTP-antwoorden.</span><span class="sxs-lookup"><span data-stu-id="8b752-132">Also, you can use hello Network tab of hello F12 Debugging Tools in Internet Explorer tooview hello HTTP responses.</span></span>

<span data-ttu-id="8b752-133">In dit voorbeeld willen we toosee Hallo reactie van de WebTest-URL: http://watestsdp2008r2.cloudapp.net:80/test.</span><span class="sxs-lookup"><span data-stu-id="8b752-133">For this example we want toosee hello response from our probe URL: http://watestsdp2008r2.cloudapp.net:80/Probe.</span></span> <span data-ttu-id="8b752-134">Hallo volgende PowerShell-voorbeeld illustreert Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="8b752-134">hello following PowerShell example illustrates hello problem.</span></span>

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

<span data-ttu-id="8b752-135">Voorbeelduitvoer:</span><span class="sxs-lookup"><span data-stu-id="8b752-135">Example output:</span></span>

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

<span data-ttu-id="8b752-136">U ziet dat er een omleidingsantwoord ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8b752-136">Notice that we received a redirect response.</span></span> <span data-ttu-id="8b752-137">Zoals eerder gezegd, een StatusCode dan wordt 200 als een fout geïnterpreteerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-137">As stated previously, any StatusCode other than 200 is considered a failure.</span></span> <span data-ttu-id="8b752-138">Traffic Manager wijzigingen Hallo eindpunt status tooOffline.</span><span class="sxs-lookup"><span data-stu-id="8b752-138">Traffic Manager changes hello endpoint status tooOffline.</span></span> <span data-ttu-id="8b752-139">tooresolve hello probleem selectievakje Hallo website configuratie tooensure die de juiste StatusCode Hallo vanaf Hallo test pad kan worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-139">tooresolve hello problem, check hello website configuration tooensure that hello proper StatusCode can be returned from hello probe path.</span></span> <span data-ttu-id="8b752-140">Configureer opnieuw Hallo Traffic Manager-test toopoint tooa pad waarmee een 200 wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="8b752-140">Reconfigure hello Traffic Manager probe toopoint tooa path that returns a 200.</span></span>

<span data-ttu-id="8b752-141">Als uw test Hallo HTTPS-protocol gebruikt, moet u mogelijk toodisable certificaat tooavoid SSL/TLS-fouten tijdens uw test controleren.</span><span class="sxs-lookup"><span data-stu-id="8b752-141">If your probe is using hello HTTPS protocol, you may need toodisable certificate checking tooavoid SSL/TLS errors during your test.</span></span> <span data-ttu-id="8b752-142">Hallo uitschakelen volgende PowerShell-instructies validatie van het servercertificaat voor de huidige PowerShell-sessie Hallo:</span><span class="sxs-lookup"><span data-stu-id="8b752-142">hello following PowerShell statements disable certificate validation for hello current PowerShell session:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8b752-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b752-143">Next Steps</span></span>

[<span data-ttu-id="8b752-144">Over verkeersrouteringsmethoden voor Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8b752-144">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="8b752-145">Wat is het Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8b752-145">What is Traffic Manager</span></span>](traffic-manager-overview.md)

[<span data-ttu-id="8b752-146">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="8b752-146">Cloud Services</span></span>](http://go.microsoft.com/fwlink/?LinkId=314074)

[<span data-ttu-id="8b752-147">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="8b752-147">Azure Web Apps</span></span>](https://azure.microsoft.com/documentation/services/app-service/web/)

[<span data-ttu-id="8b752-148">Bewerkingen op Traffic Manager (REST API-referentiemateriaal)</span><span class="sxs-lookup"><span data-stu-id="8b752-148">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

<span data-ttu-id="8b752-149">[Azure Traffic Manager-Cmdlets][1]</span><span class="sxs-lookup"><span data-stu-id="8b752-149">[Azure Traffic Manager Cmdlets][1]</span></span>

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
