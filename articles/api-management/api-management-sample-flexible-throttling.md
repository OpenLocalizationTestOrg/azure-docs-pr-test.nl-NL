---
title: aaaAdvanced aanvraagbeperking met Azure API Management
description: Meer informatie over hoe toocreate en flexibele quota's en -beleid met Azure API Management snelheidsbeperking toe te passen.
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Geavanceerde aanvraagbeperking met Azure API Management
De binnenkomende aanvragen kunnen toothrottle is een belangrijke rol van Azure API Management. API Management kunnen door beheren Hallo snelheid van aanvragen of Hallo totale aanvragen/gegevens overgebracht, API-providers tooprotect hun-API's van misbruik en waarde maken voor de verschillende lagen voor API-product.

## <a name="product-based-throttling"></a>Op basis van product-beperking
toodate, Hallo snelheid beperking mogelijkheden zijn beperkt toobeing binnen het bereik van tooa bepaald Product abonnement (in wezen een sleutel), gedefinieerd in Hallo publicatieportal van API Management. Dit is handig voor het Hallo-provider tooapply API-limieten op Hallo-ontwikkelaars die zich hebben geregistreerd toouse hun API, echter dat niet helpt, bijvoorbeeld in afzonderlijke eindgebruikers Hallo API beperking. Het is mogelijk dat voor één gebruiker van Hallo ontwikkelaarshandleiding toepassing tooconsume Hallo gehele quota en vervolgens verhinderen andere Hallo developer-klanten kunnen toouse Hallo-toepassing. Enkele klanten een groot aantal aanvragen genereren kunnen kunnen ook toegang toooccasional gebruikers te beperken.

## <a name="custom-key-based-throttling"></a>Aangepaste sleutel op basis van beperking
Hallo nieuwe [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -beleid biedt u een aanzienlijk meer flexibele oplossing tootraffic-besturingselement. Dit nieuwe beleid kunt u toodefine expressies tooidentify Hallo sleutels die gebruikt tootrack verkeer gebruik worden. Hallo die dit werkt wordt geïllustreerd hoe u easiest met een voorbeeld. 

## <a name="ip-address-throttling"></a>Beperking van IP-adres
Hallo volgende beleid beperkt één client IP-adres tooonly 10 aanroepen elke minuut, met een totaal van 1.000.000 aanroepen en 10.000 kilobytes van bandbreedte per maand. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Als alle clients op Internet Hallo een uniek IP-adres gebruikt, dit wordt mogelijk een effectieve manier voor het beperken van gebruiksgegevens door de gebruiker. Het is echter wel waarschijnlijk dat meerdere gebruikers delen één openbaar IP-adres vanwege toothem toegang tot Hallo Internet via een NAT-apparaat wordt. Ondanks dit voor de API's waarmee niet-geverifieerde toegang Hallo `IpAddress` mogelijk de beste optie Hallo.

## <a name="user-identity-throttling"></a>Gebruiker identity-beperking
Als een eindgebruiker is geverifieerd, wordt een bandbreedteregeling sleutel kan worden gegenereerd op basis van informatie die een unieke identificatie van een die gebruiker.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

In dit voorbeeld we extraheren Hallo autorisatie-header, te converteren`JWT` object en onderwerp Hallo van Hallo token tooidentify Hallo gebruiker gebruiken als Hallo snelheidsbeperking-sleutel. Als de identiteit van de gebruiker Hallo is opgeslagen in Hallo `JWT` als een van de Hallo andere claims vervolgens dat de waarde kan worden gebruikt in plaats daarvan.

## <a name="combined-policies"></a>Gecombineerde beleid
Hoewel Hallo nieuwe beperking beleidsregels meer controle dan Hallo bestaande beleidsregels voor bandbreedteregeling bieden, is er nog steeds waarde combinatie van beide mogelijkheden. Beperkingen door abonnement productcode ([aanroepfrequentie per abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) en [gebruiksquotum per abonnement instellen](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is een uitstekende manier op tooenable monetizing van een API in rekening gebracht op basis van gebruik niveaus. Hallo betere resultaten gedetailleerde controle over wordt kunnen toothrottle door de gebruiker is een aanvulling en voorkomt dat gedrag van een gebruiker Hallo-ervaring van een andere beïnvloeden. 

## <a name="client-driven-throttling"></a>Client aangestuurd beperking
Als Hallo beperking sleutel is gedefinieerd met behulp van een [beleidsexpressie](https://msdn.microsoft.com/library/azure/dn910913.aspx), dan is het Hallo-API-provider die is kiezen hoe Hallo beperking ligt binnen het bereik. Een ontwikkelaar mogelijk wilt echter toocontrol hoe ze beoordelen beperken hun eigen klanten. Dit kan worden ingeschakeld door Hallo API provider door de introductie van een aangepaste header tooallow Hallo ontwikkelaar client toepassing toocommunicate Hallo sleutel toohello API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Hierdoor kunnen Hallo ontwikkelaarshandleiding client toepassing toochoose hoe ze willen toocreate Hallo snelheidsbeperking sleutel. Met een beetje draaien kan een ontwikkelaar client hun eigen niveaus tarief maken door sets met sleutels toousers toewijzen en roteren Hallo sleutelgebruik.

## <a name="summary"></a>Samenvatting
Azure API Management biedt snelheid en beperking tooboth aanhalingsteken beveiligen en waarde tooyour API-service toevoegen. Hallo nieuwe beperking beleidsregels met aangepaste bereik regels kunt dat u meer controle over deze beleidsregels tooenable geslaagde uw klanten toobuild nog beter toepassingen. Hallo-voorbeelden in dit artikel worden Hallo gebruik van dit nieuwe beleid door productie snelheidsbeperking-sleutels met client-IP-adressen, gebruikers-id en waarden van de client gegenereerd. Er zijn echter veel andere onderdelen van het Hallo-bericht die kunnen worden gebruikt zoals gebruikersagent, fragmenten voor URL-pad, de grootte van het bericht.

## <a name="next-steps"></a>Volgende stappen
Geef ons uw feedback in Hallo Disqus-thread voor dit onderwerp. Het normaal zou zijn goede toohear over andere mogelijke sleutelwaarden die logische keuze in uw scenario's zijn.

## <a name="watch-a-video-overview-of-these-policies"></a>Bekijk een video-overzicht van deze beleidsregels
Voor meer informatie over Hallo [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) en [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) beleidsregels die in dit artikel, neem Hallo volgende video bekijken.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

