---
title: Overzicht van CDN aaaAzure | Microsoft Docs
description: Meer informatie over welke hello Azure inhoud Delivery Network (CDN) is en hoe toouse het toodeliver hoge bandbreedte inhoud door het in cache opslaan van blobs en statische inhoud.
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Overzicht van hello Azure Content Delivery Network (CDN)
> [!NOTE]
> Dit document wordt beschreven welke hello Azure Content Delivery Network (CDN) is, hoe het werkt en Hallo functies van elk Azure CDN-product.  Als u wilt dat deze gegevens tooskip en rechte tooa zelfstudie over het gaat toocreate een CDN-eindpunt Zie [met behulp van Azure CDN](cdn-create-new-endpoint.md).  Als u een lijst met huidige locaties van CDN-knooppunten toosee wilt, Zie [Azure CDN POP-locaties](cdn-pop-locations.md).
> 
> 

Hello Azure inhoud Delivery Network (CDN) slaat op strategisch geplaatste locaties tooprovide maximale doorvoer voor het leveren van inhoud toousers een statische webinhoud.  Hallo CDN biedt ontwikkelaars een globale oplossing voor het leveren van inhoud met hoge bandbreedte door Hallo inhoud op fysieke knooppunten over Hallo wereld cache te plaatsen. 

voordelen van het gebruik van CDN toocache website-assets Hallo Hallo zijn:

* Betere prestaties en gebruikerservaring voor eindgebruikers, vooral wanneer tooload inhoud met behulp van toepassingen waarbij meerdere retouren zijn vereist.
* Grote schaal toobetter verwerken korte hoge belasting, zoals starten gebeurtenis aan Hallo begin van een product.
* Door de gebruikersaanvragen te distribueren en de inhoud van de randservers, is minder verkeer toohello oorsprong verzonden.

## <a name="how-it-works"></a>Hoe werkt het?
![Overzicht van CDN](./media/cdn-overview/cdn-overview.png)

1. Een gebruiker (Els) gebruikt een URL met een speciale domeinnaam, zoals `<endpointname>.azureedge.net`, om een bestand (ook wel een asset genoemd) aan te vragen.  DNS routeert Hallo aanvraag toohello best presterende Point-of-Presence (POP) locatie.  Meestal is dit Hallo POP dat Zie geografisch gezien het dichtst toohello gebruiker.
2. Als Hallo randservers in Hallo POP nog geen Hallo-bestand in het cachegeheugen, aanvragen Hallo edge-server Hallo bestand vanuit de oorsprong Hallo.  Hallo oorsprong kan Azure-Web-App, Azure Cloud Service, Azure Storage-account of een openbaar toegankelijke webserver zijn.
3. Hallo oorsprong retourneert Hallo bestand toohello randserver, inclusief optionele HTTP-headers met een beschrijving van het bestand Hallo Time-to-Live (TTL).
4. Hallo edge-server in de cache opgeslagen Hallo-bestand en retourneert Hallo bestand toohello oorspronkelijke aanvrager (Alice).  Hallo-bestand blijft in de cache op de edge-server Hallo totdat Hallo TTL verloopt.  Als het Hallo-oorsprong geen TTL heeft opgegeven, is Hallo standaard-TTL zeven dagen.
5. Extra gebruikers kunnen vervolgens aanvraag Hallo hetzelfde bestand diezelfde URL gebruiken, en kan ook worden gerichte toothat hetzelfde POP.
6. Als Hallo TTL voor Hallo bestand nog niet is verlopen, retourneert Hallo edge-server Hallo-bestand uit Hallo-cache.  Dit resulteert in een snellere, responsievere gebruikerservaring.

## <a name="azure-cdn-features"></a>Functies van Azure CDN
Er zijn drie Azure CDN-producten: **Azure CDN Standard van Akamai**, **Azure CDN Standard van Verizon** en **Azure CDN Premium van Verizon**.  Hallo bevat volgende tabel Hallo-functies die beschikbaar zijn voor elk product.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Prestatiefuncties en -optimalisatie__ |
| [Dynamische siteversnelling](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dynamische siteversnelling - adaptieve afbeeldingscompressie](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Dynamische siteversnelling - vooraf ophalen van objecten](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Optimalisatie van videostreaming](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Optimalisatie van grote bestanden](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [GSLB (Global Server Load balancing)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Snel leegmaken](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Vooraf laden van assets](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Queryreeksen opslaan in cache](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| IPv4/IPv6 dual stack |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Ondersteuning voor HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Beveiliging__ |
| HTTPS-ondersteuning met CDN-eindpunt |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTPS voor aangepaste domeinen](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Ondersteuning voor aangepaste domeinnamen](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Geofilters](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Tokenverificatie](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [DDOS-beveiliging](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Analyse en rapportage__ |
| [Basisanalyse](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Geavanceerde HTTP-rapporten](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Realtime statistieken](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Realtime waarschuwingen](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Gebruiksgemak__ |
| Eenvoudige integratie met Azure-services, zoals [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) en [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Beheer via [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) of [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Aanpasbare, op regels gebaseerde engine voor contentlevering](cdn-rules-engine.md) | | |**&#x2713;** |
| Instellingen voor cache/koptekst (met behulp van [regels-engine](cdn-rules-engine.md)) | | |**&#x2713;** |
| URL-omleidings-/herschrijfbewerking (met behulp van [regels-engine](cdn-rules-engine.md)) | | |**&#x2713;** |
| Regels voor mobiele apparaten (met behulp van [regels-engine](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Verizon ondersteunt de levering van grote bestanden en media rechtstreeks via algemene webweergave.


> [!TIP]
> Is er een functie die u wilt dat toosee in Azure CDN?  [Geef ons feedback](https://feedback.azure.com/forums/169397-cdn). 
> 
> 

## <a name="next-steps"></a>Volgende stappen
tooget gestart met CDN, Zie [met behulp van Azure CDN](cdn-create-new-endpoint.md).

Als u een bestaande CDN-klant bent, kunt u nu uw CDN-eindpunten via Hallo beheren [Microsoft Azure-portal](https://portal.azure.com) of met [PowerShell](cdn-manage-powershell.md).

toosee CDN in actie Hallo, bekijk Hallo [video van onze Build 2016-sessie](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Meer informatie over hoe Azure CDN tooautomate met [.NET](cdn-app-dev-net.md) of [Node.js](cdn-app-dev-node.md).

Zie [Prijzen van CDN](https://azure.microsoft.com/pricing/details/cdn/) voor informatie over de prijzen.

