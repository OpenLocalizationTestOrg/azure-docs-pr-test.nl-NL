---
title: Azure App Service en de invloed ervan op bestaande Azure services
description: Legt uit hoe de nieuwe Azure App Service en de bijbehorende functies invloed zijn op bestaande services in Azure.
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure App Service en bestaande Azure-services
In dit artikel bevat een overzicht van de wijzigingen in bestaande Azure services als onderdeel van de verschillende Azure-services in samengebracht [Azure App Service](https://azure.microsoft.com/services/app-service/), een nieuwe geïntegreerde aanbieding.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Overzicht
[Azure App Service](https://azure.microsoft.com/services/app-service/) is een nieuwe en unieke cloudservice waarmee ontwikkelaars kunnen maken van web- en mobiele apps voor elk platform en elk apparaat. App Service is een geïntegreerde oplossing die is ontworpen om te stroomlijnen herhaalde codering functies, integreren met enterprise- en SaaS-systemen en bedrijfsprocessen te automatiseren en te voldoen aan uw behoeften voor beveiliging, betrouwbaarheid en schaalbaarheid.

App Service verenigt de volgende bestaande Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), en [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) gecombineerd in één service, tijdens het toevoegen van krachtige nieuwe mogelijkheden.  App Service kunt u voor het hosten van de volgende typen Apps:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

De volgende tabel wordt uitgelegd hoe bestaande Azure-services zijn toegewezen aan de App Service en de beschikbaar binnen het app-typen.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Bestaande Azure-Service</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">Wat is er gewijzigd</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Azure Websites</td>
<td align="left">Web Apps</td>
<td align="left"><li>App Service is strikt beperkt is tot het wijzigen van de naam van de Websites in Web-Apps voor Azure Websites.
<p><li>Uw bestaande exemplaren van Websites zijn nu Web-Apps in App Service.</p>
<p><li>U kunt toegang tot uw bestaande websites via de <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, waarbij vindt u alle bestaande sites onder <em>Web-Apps</em>.</p>
<p><li><em>Web-Hosting plannen</em> is nu <em>App Service-Plan</em>. Een <em>App Service-Plan</em> elk type app van App Service, zoals Web-, mobiele, logische of API-apps kunnen hosten.</p>
<p><li>Azure App Service Web Apps is in het algemeen beschikbaarheid.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Meer informatie over Web-Apps</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Services</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services blijven beschikbaar als zelfstandige service en blijven volledig wordt ondersteund.</p>
<p><li>Mobiele Apps is een app in App Service, die kan worden geïntegreerd in de functionaliteit van Mobile Services en meer.</p>
<p><li>Het is gemakkelijk te <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">van Mobile Services migreren naar Mobile Apps</a>.</p>
<p><li>Als onderdeel van App Service ophalen Mobile Apps nieuwe mogelijkheden buiten Mobile Services, zoals integratie met on-premises en SaaS-systemen, sleuven, WebJobs en beter schalingsopties voor fasering.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Meer informatie over Mobile Apps</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API-apps</td>
<td align="left">
<p><li>API-Apps is een nieuw type app in App Service waarmee u gemakkelijk maken en gebruiken van API's in de cloud.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Meer informatie over API-Apps</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Logic Apps is een nieuw type app in App Service waarmee u eenvoudig bedrijfsprocessen automatiseren.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Meer informatie over Logic Apps</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Azure BizTalk Services</td>
<td align="left">BizTalk API Apps</td>
<td align="left">
<li><p>BizTalk Services kunnen blijven beschikbaar als zelfstandige service en blijven volledig wordt ondersteund.</p>
<li><p>De mogelijkheden van BizTalk Services zijn geïntegreerd in App Service als zodat gebruikers voor het uitvoeren van de integratie van bedrijfstoepassingen en B2B integratiescenario's met een van de app-typen in App Service API-Apps.</p>
<li><p>Met Logic Apps kunt u nu werkstromen maken met een visuele ontwerp bedrijfsprocessen automatiseren.</p></td>
</tr>
</tbody>
</table>

Voor meer informatie gaat u naar [App Service-documentatie](https://azure.microsoft.com/documentation/services/app-service/).

