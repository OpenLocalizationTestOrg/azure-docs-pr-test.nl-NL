---
title: overzicht van de aaaRedirect voor Azure Application Gateway | Microsoft Docs
description: Meer informatie over mogelijkheden voor het omleiden van Hallo in Azure Application Gateway
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Overzicht van Application Gateway-omleiding

Een veelvoorkomend scenario voor veel webtoepassingen is toosupport automatische HTTP tooHTTPS omleiding tooensure die alle communicatie tussen de toepassing en haar gebruikers vindt plaats via een versleutelde pad. Klanten hebben in de afgelopen Hallo, technieken zoals het maken van een toegewezen back-endpool met als enige doel is ontvangen op http-tooHTTPS tooredirect-aanvragen worden gebruikt.  Toepassingsgateway ondersteunt nu de mogelijkheid tooredirect verkeer op Hallo Application Gateway. Dit vereenvoudigt de configuratie van toepassing, optimaliseert de Hallo Resourcegebruik en nieuwe scenario's voor omleiding omleiding van globale en op basis van een pad inclusief ondersteunt. Ondersteuning voor toepassingen Gateway omleiding is niet beperkt tooHTTP -> alleen HTTPS-omleiding. Dit is een algemene omleiding mechanisme, waardoor de omleiding van verkeer dat op één listener tooanother listener voor Application Gateway wordt ontvangen. Het ondersteunt ook omleiding tooan externe site ook. Ondersteuning voor toepassingen Gateway omleiding biedt Hallo volgende mogelijkheden:

1. Globale omleiding vanaf één listener tooanother listener op Hallo Gateway. Hierdoor kunnen HTTP-omleiding tooHTTPS op een site.
2. Omleiding op basis van het pad. Deze manier van omleiding kan HTTP-omleiding tooHTTPS alleen op een specifieke site gebied, zoals een winkelwagen winkelwagen gebied aangeduid met/mandje / *.
3. Omleiden tooexternal site.

![omleiden](./media/application-gateway-redirect-overview/redirect.png)

Met deze wijziging klanten moet een nieuw omleiding configuration-object waarmee de doel-listener Hallo toocreate of externe site toowhich omleiding gewenst is. Hallo, configuratie-element ondersteunt ook opties tooenable Hallo URI-pad en query-tekenreeks toohello omgeleid URL in te voegen. Klanten kunnen ook voor kiezen of omleiding een tijdelijke (HTTP-statuscode 302) of een permanente omleiding (HTTP-statuscode 301 is). Wanneer deze configuratie omleiding gemaakt is aangesloten toohello bron listener via een nieuwe regel. Wanneer u een eenvoudige regel, Hallo omleidings-configuratie is gekoppeld aan een bron-listener en is een globale omleiding. Wanneer een regel op basis van het pad wordt gebruikt, wordt Hallo omleidings-configuratie is gedefinieerd in het overzicht van Hallo URL-pad en daarom is alleen van toepassing toohello specifiek padgebied van een site.

### <a name="next-steps"></a>Volgende stappen

[URL-omleiding op een toepassingsgateway configureren](application-gateway-configure-redirect-powershell.md)
