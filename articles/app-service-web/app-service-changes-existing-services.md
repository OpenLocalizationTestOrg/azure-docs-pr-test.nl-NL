---
title: aaaAzure App Service en de invloed ervan op bestaande Azure services
description: Legt uit hoe Hallo nieuwe Azure App Service en de functies gevolgen voor bestaande services in Azure.
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure App Service en bestaande Azure-services
In dit artikel bevat een overzicht van Hallo wijzigingen tooexisting Azure-services als onderdeel van Hallo wijziging toobring samen verschillende Azure-services in [Azure App Service](https://azure.microsoft.com/services/app-service/), een nieuwe geïntegreerde aanbieding.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Overzicht
[Azure App Service](https://azure.microsoft.com/services/app-service/) is een nieuwe en unieke cloudservice waarmee ontwikkelaars toocreate web- en mobiele apps voor elk platform en elk apparaat. App Service is dat een geïntegreerde oplossing ontworpen toostreamline herhaald codering functies, integreren met enterprise- en SaaS-systemen en bedrijfsprocessen te automatiseren en te voldoen aan uw behoeften voor beveiliging, betrouwbaarheid en schaalbaarheid.

App Service samenbrengt Hallo volgende op bestaande Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), en [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) gecombineerd in één service, terwijl krachtige nieuwe mogelijkheden toevoegen.  App Service kunt u toohost Hallo volgende app-typen:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

Hallo volgende tabel wordt uitgelegd hoe bestaande Azure services tooApp-Service en Hallo typen Apps die beschikbaar zijn binnen deze worden toegewezen.

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
<td align="left"><li>App Service is voor Azure Websites strikt beperkt toochanging Hallo naam Websites tooWeb Apps.
<p><li>Uw bestaande exemplaren van Websites zijn nu Web-Apps in App Service.</p>
<p><li>U kunt toegang tot uw bestaande websites via Hallo <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, waarbij vindt u alle bestaande sites onder <em>Web-Apps</em>.</p>
<p><li><em>Web-Hosting plannen</em> is nu <em>App Service-Plan</em>. Een <em>App Service-Plan</em> elk type app van App Service, zoals Web-, mobiele, logische of API-apps kunnen hosten.</p>
<p><li>Azure App Service Web Apps is in het algemeen beschikbaarheid.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Meer informatie over Web-Apps</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Services</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services toobe beschikbaar als zelfstandige service blijven en blijven volledig wordt ondersteund.</p>
<p><li>Mobiele Apps is een app in App Service, die kan worden geïntegreerd Hallo-functionaliteit van Mobile Services en meer.</p>
<p><li>Het is te eenvoudig<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migreren van Mobile Services tooMobile Apps</a>.</p>
<p><li>Als onderdeel van App Service ophalen Mobile Apps nieuwe mogelijkheden buiten Mobile Services, zoals integratie met on-premises en SaaS-systemen, sleuven, WebJobs en beter schalingsopties voor fasering.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Meer informatie over Mobile Apps</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API-apps</td>
<td align="left">
<p><li>API-Apps is een nieuw type app in App Service waarmee u eenvoudig bouwen en API's in de cloud hello gebruiken.</p>
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
<li><p>BizTalk Services toobe beschikbaar als zelfstandige service blijven en blijven volledig wordt ondersteund.</p>
<li><p>Alle Hallo-mogelijkheden van BizTalk Services zijn geïntegreerd in App Service API-Apps inschakelen gebruikers tooperform integratie van bedrijfstoepassingen en B2B integratiescenario's met een van de app-typen Hallo in App Service.</p>
<li><p>Met Logic Apps kunt u nu gebruik van een visuele ontwerp ervaring toocreate werkstromen bedrijfsprocessen automatiseren.</p></td>
</tr>
</tbody>
</table>

toolearn meer, gaat u naar [App Service-documentatie](https://azure.microsoft.com/documentation/services/app-service/).

