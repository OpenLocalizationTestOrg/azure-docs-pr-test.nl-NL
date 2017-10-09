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
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Het oplossen van problemen gedegradeerde status op Azure Traffic Manager

Dit artikel wordt beschreven hoe een Azure Traffic Manager-profiel tootroubleshoot die wordt weergegeven een gedegradeerde status. Voor dit scenario kunt u een Traffic Manager-profiel wijst toosome van uw cloudapp.net gehoste services hebt geconfigureerd. Als Hallo status van uw Traffic Manager wordt weergegeven in een **gedegradeerd** status en vervolgens Hallo status van een of meer eindpunten mogelijk **gedegradeerd**:

![status van gedegradeerd endpoint](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Als Hallo status van uw Traffic Manager wordt weergegeven in een **inactief** status en vervolgens beide eindpunten mogelijk **uitgeschakelde**:

![Inactieve Traffic Manager-status](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Understanding Traffic Manager-tests

* Traffic Manager overweegt een eindpunt toobe ONLINE alleen wanneer Hallo test een HTTP 200-respons ontvangt back vanaf Hallo test pad. Een ander niet-200-antwoord is een fout.
* Een omleiding 30 x mislukt, zelfs als Hallo omgeleid URL retourneert een 200.
* Voor HTTPs-tests worden certificaatfouten genegeerd.
* de daadwerkelijke inhoud Hallo van Hallo test pad maakt niet uit als een 200 wordt geretourneerd. Scannen van de like voor statische inhoud van een URL-toosome ' / favicon.ico ' is een algemene methode. Dynamische inhoud, zoals Hallo ASP-pagina's mogelijk niet altijd retourneren, 200, zelfs wanneer de toepassing hello in orde is.
* Een aanbevolen procedure is tooset Hallo test pad toosomething met voldoende toodetermine logica die site Hallo omhoog of omlaag is. In Hallo vorige voorbeeld door in te stellen hello pad too"/favicon.ico", kunt u alleen die w3wp.exe testen reageert. Deze test niet geeft aan dat uw webtoepassing in orde. Een betere optie zou worden tooset een tooa pad iets zoals ' / Probe.aspx ' die logica toodetermine Hallo status van Hallo site heeft. Bijvoorbeeld, kunt u prestaties tellers tooCPU gebruik of meting Hallo aantal mislukte aanvragen. Of u kan proberen tooaccess databaseresources of sessie status toomake of webtoepassing Hallo werkt.
* Als alle eindpunten in een profiel zijn gedegradeerd, klikt u vervolgens alle eindpunten in Traffic Manager wordt beschouwd als goed en routes verkeer tooall eindpunten. Dit gedrag zorgt ervoor dat problemen met Hallo probing mechanisme niet in een volledige onderbreking van uw service resulteren.

## <a name="troubleshooting"></a>Problemen oplossen

tootroubleshoot een test-fout, moet u een hulpprogramma waarmee Hallo HTTP-statuscode geretourneerd uit Hallo WebTest-URL. Er zijn veel hulpprogramma's beschikbaar die u onbewerkte HTTP-antwoord Hallo weergeven.

* [Fiddler](http://www.telerik.com/fiddler)
* [cURL](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

U kunt ook Hallo netwerk tabblad Hallo F12 foutopsporing extra in Internet Explorer tooview Hallo HTTP-antwoorden.

In dit voorbeeld willen we toosee Hallo reactie van de WebTest-URL: http://watestsdp2008r2.cloudapp.net:80/test. Hallo volgende PowerShell-voorbeeld illustreert Hallo probleem.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Voorbeelduitvoer:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

U ziet dat er een omleidingsantwoord ontvangen. Zoals eerder gezegd, een StatusCode dan wordt 200 als een fout geïnterpreteerd. Traffic Manager wijzigingen Hallo eindpunt status tooOffline. tooresolve hello probleem selectievakje Hallo website configuratie tooensure die de juiste StatusCode Hallo vanaf Hallo test pad kan worden geretourneerd. Configureer opnieuw Hallo Traffic Manager-test toopoint tooa pad waarmee een 200 wordt geretourneerd.

Als uw test Hallo HTTPS-protocol gebruikt, moet u mogelijk toodisable certificaat tooavoid SSL/TLS-fouten tijdens uw test controleren. Hallo uitschakelen volgende PowerShell-instructies validatie van het servercertificaat voor de huidige PowerShell-sessie Hallo:

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

## <a name="next-steps"></a>Volgende stappen

[Over verkeersrouteringsmethoden voor Traffic Manager](traffic-manager-routing-methods.md)

[Wat is het Traffic Manager](traffic-manager-overview.md)

[Cloud Services](http://go.microsoft.com/fwlink/?LinkId=314074)

[Azure Web Apps](https://azure.microsoft.com/documentation/services/app-service/web/)

[Bewerkingen op Traffic Manager (REST API-referentiemateriaal)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Azure Traffic Manager-Cmdlets][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
