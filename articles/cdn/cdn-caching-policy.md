---
title: aaaManage Azure CDN cachebeleid in Azure Media Services | Microsoft Docs
description: Meer informatie over hoe toomanage Azure CDN cachebeleid in Azure Media Services.
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Azure CDN cachebeleid in Azure Media Services beheren
Azure Media Services biedt dat HTTP gebaseerde adaptief streamen en progressief downloaden. HTTP op basis van streaming is zeer schaalbaar met voordelen van het opslaan in cache in proxy en CDN lagen, evenals het caching aan clientzijde. Streaming-eindpunten bevat algemene streaming mogelijkheden en configuratie voor cache-HTTP-headers. Streaming-eindpunten ingesteld HTTP-Cache-Control: maximumleeftijd en -Expires-koppen. U kunt meer informatie ophalen voor HTTP-headers cache van [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Standaard opslaan in cache headers
Standaard is voor streaming-eindpunten 3 dagen cache headers voor op aanvraag streamen gegevens (echte media fragmenten/segmenten) en manifest(playlist) toepassen. Streaming-eindpunten toepassing 3 dagen cache headers voor gegevens (echte media fragmenten/segmenten) en 2 seconden in de cache-header voor manifest(playlist) aanvragen voor live streamen. Wanneer live programma tooon aanvraag (live archiveren wordt) toepassen op aanvraag streamen cache headers.

## <a name="azure-cdn-integration"></a>Integratie van Azure CDN
Azure Media Services biedt [CDN geïntegreerd](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) voor streaming-eindpunten. Cache-control van headers past in Hallo dezelfde manier zoals streaming eindpunten tooCDN ingeschakeld streaming-eindpunten. Azure CDN gebruikt intern streaming-eindpunt geconfigureerd cache waarden toodefine Hallo levensduur Hallo objecten in cache opgeslagen en gebruikt ook deze waarde tooset Hallo levering cache headers. Wanneer de streaming-eindpunten met behulp van CDN ingeschakeld is het tooset kleine cachewaarden niet aanbevolen. Kleine waarden in te stellen Hallo prestaties verminderen, en verlagen Hallo voordeel van het CDN. Het is niet toegestaan tooset cache headers kleiner is dan 600 seconden voor CDN ingeschakeld streaming-eindpunten.

> [!IMPORTANT]
>Azure Media Services is volledig geïntegreerd met Azure CDN. U kunt alle Hallo beschikbaar Azure CDN-providers (Akamai en Verizon) tooyour streaming-eindpunt met inbegrip van CDN Standard en Premium-producten te integreren met één klik. Zie voor meer informatie dit [aankondiging](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Kosten van de gegevens van streaming-eindpunt tooCDN alleen opgehaald uitgeschakeld als hello CDN is ingeschakeld in plaats van streaming-eindpunt API's of met behulp van Azure-beheerportal streaming-eindpunt sectie. Handmatige integratie of maken van een CDN-eindpunt met CDN-API's of portal sectie rechtstreeks wordt niet uitschakelen voor Hallo gegevens kosten.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Cache-headers configureren met Azure Media Services
U kunt Azure Management portal of Azure Media Services-API's tooconfigure cache headerwaarden gebruiken.

1. tooconfigure cache kopteksten met management portal Raadpleeg te[hoe tooManage Streaming-eindpunten](../media-services/media-services-portal-manage-streaming-endpoints.md) sectie configureren Hallo Streaming-eindpunt.
2. Azure Media Services REST-API [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. Azure Media Services .NET SDK [StreamingEndpointCacheControl eigenschappen](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Voorkeursvolgorde cache-configuratie
1. Azure Media Services geconfigureerd cachewaarde overschrijft de standaardwaarde.
2. Als er geen handmatige configuratie, geldt de standaardwaarden.
3. 2 seconden cache headers geldt toolive streaming manifest(playlist) ongeacht de configuratie van Azure Media of Azure Storage en onderdrukken deze waarde is standaard niet beschikbaar.

