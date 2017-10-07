---
title: aaaHTTP/2-ondersteuning in Azure CDN | Microsoft Docs
description: Meer informatie over ondersteuning voor HTTP/2- en CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>HTTP-/ 2-ondersteuning in Azure CDN

HTTP/2 is een grote revisie tooHTTP/1.1\. Het biedt sneller webprestaties, verminderde reactietijd, en verbeterde gebruikerservaring, terwijl Hallo bekend HTTP-methoden, statuscodes en semantiek behouden blijven. Hoewel HTTP/2 ontworpen toowork met HTTP en HTTPS, ondersteunen veel client webbrowsers alleen HTTP/2 via TLS.

###<a name="http2-benefits"></a>Voordelen van de HTTP-/ 2

Hallo voordelen van HTTP-/ 2:

*   **Multiplex en gelijktijdigheid**

    HTTP 1.1 meerdere waardoor meerdere aanvragen van de resource is vereist voor meerdere TCP-verbindingen en elke verbinding heeft prestatieoverhead gekoppeld. HTTP/2 kunt meerdere resources toobe aangevraagd op een enkele TCP-verbinding.

*   **Headercompressie**

    Door het comprimeren van Hallo HTTP-headers voor aangeboden bronnen tijd op de kabel Hallo aanzienlijk verminderd.

*   **Stroom-afhankelijkheden**

    Afhankelijkheden van de stroom kunnen Hallo client tooindicate toohello server welke resources prioriteit hebben.


##<a name="http2-browser-support"></a>Ondersteuning voor HTTP/2-Browser

Alle belangrijke browsers Hallo hebt HTTP/2-ondersteuning in versies van hun huidige geïmplementeerd. Niet-ondersteunde browsers wordt automatisch terugval tooHTTP/1.1.

|Browser|Minimale versie|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>HTTP-/ 2-ondersteuning in Azure CDN inschakelen

HTTP-/ 2-ondersteuning is momenteel actief is voor **Azure CDN van Akamai** en **Azure CDN van Verizon** profielen. Er is geen verdere actie vereist van klanten.

##<a name="next-steps"></a>Volgende stappen

toosee hello voordelen van het HTTP/2 in actie, Zie [deze demo van Akamai](https://http2.akamai.com/demo).

toolearn meer informatie over HTTP/2, gaat u naar Hallo resources te volgen:

*   [HTTP-/ 2-specificatie startpagina](https://http2.github.io/)
*   [Officiële HTTP/2 Veelgestelde vragen](https://http2.github.io/faq/)
*   [Akamai HTTP/2-gegevens](https://http2.akamai.com/)

toolearn meer informatie over de beschikbare functies van Azure CDN, Zie Hallo [overzicht van Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).
