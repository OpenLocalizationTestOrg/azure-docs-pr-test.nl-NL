---
title: overzicht van de Media Services-Streaming-eindpunt aaaAzure | Microsoft Docs
description: In dit onderwerp geeft een overzicht van Azure Media Services streaming-eindpunten.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Streaming-eindpunten-overzicht 

##<a name="overview"></a>Overzicht

In Microsoft Azure Media Services (AMS), een **Streaming-eindpunt** vertegenwoordigt een streaming-service die inhoud rechtstreeks tooa player clienttoepassing of tooa inhoud Delivery Network (CDN) voor verdere distributie kunt leveren. Media Services biedt ook naadloze integratie van Azure CDN. Hallo uitgaande stroom van een service StreamingEndpoint mag een live stream, video op aanvraag of progressief downloaden van de activa in uw Media Services-account. Elke Azure Media Services-account bevat standaard StreamingEndpoint. Aanvullende streaming-eindpunten kunnen worden gemaakt onder Hallo-account. Er zijn twee versies van streaming-eindpunten, 1.0 en 2.0. Vanaf januari 10 2017, bevatten nieuwe accounts AMS versie 2.0 **standaard** StreamingEndpoint. Aanvullende streaming-eindpunten dat u toothis account toevoegt, worden ook versie 2.0. Deze wijziging heeft geen invloed op bestaande accounts Hallo; bestaande streaming-eindpunten versie 1.0 zijn en mag de bijgewerkte tooversion 2.0. Met deze wijziging zal er wijzigingen in gedrag, facturering en functie (Zie voor meer informatie, Hallo **Streaming typen en versies** sectie hieronder).

Bovendien vanaf Hallo 2.15 versie (uitgebracht in januari 2017), Azure Media Services toegevoegd Hallo eigenschappen toohello Streaming-eindpunt entiteit te volgen: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Zie voor een gedetailleerd overzicht van deze eigenschappen [dit](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Wanneer u een Azure Media Services-account standaard standaard streaming-eindpunt voor u op Hallo gemaakt is maakt **gestopt** status. U kunt Hallo standaardstreaming-eindpunt niet verwijderen. Afhankelijk van hello Azure CDN beschikbaarheid in regio Hallo gericht, standaard een nieuw gemaakt standaard streaming-eindpunt bevat ook 'StandardVerizon' CDN provider-integratie. 

>[!NOTE]
>Integratie van Azure CDN kan worden uitgeschakeld voordat u begint Hallo streaming-eindpunt.

In dit onderwerp geeft een overzicht van de belangrijkste Hallo-functies die worden geleverd door het streaming-eindpunten.

## <a name="streaming-types-and-versions"></a>Streaming-typen en versies

### <a name="standardpremium-types-version-20"></a>Standaard/Premium typen (versie 2.0)

Vanaf Hallo januari 2017 versie van Media Services kunt u twee streaming typen hebben: **standaard** en **Premium**. Deze typen uitmaken deel van Hallo Streaming-eindpunt versie '2.0'.

Type|Beschrijving
---|---
**Standard**|Dit is de standaardoptie Hallo die voor de meeste Hallo Hallo scenario's.<br/>Met deze optie u vaste/beperkt SLA worden opgehaald; het eerste 15 dagen na het starten van Hallo streaming-eindpunt is gratis.<br/>Als u meer dan één streaming-eindpunten maken, alleen is hello eerst een gratis voor Hallo eerste 15 dagen Hallo anderen kosten in rekening gebracht worden zodra ze worden gestart. <br/>Houd er rekening mee dat gratis proefversie alleen van toepassing is toonewly media services-accounts en standaardstreaming-eindpunt gemaakt. Bestaande streaming-eindpunten en bovendien gemaakte streaming-eindpunten niet gratis proefversie bevat periode, zelfs als ze zijn bijgewerkt tooversion 2.0 of ze zijn gemaakt als versie 2.0.
**Premium**|Deze optie is geschikt voor professionals scenario's waarvoor hogere schaal of het besturingselement.<br/>Variabele SLA die is gebaseerd op premium streaming-eenheid (SU) capaciteit hebt aangeschaft, speciale streaming-eindpunten bevinden zich in een geïsoleerde omgeving en niet van invloed zijn voor bronnen.

Voor meer informatie gedetailleerde, Zie Hallo **vergelijken Streaming typen** volgende sectie.

### <a name="classic-type-version-10"></a>Klassieke type (versie 1.0)

Voor gebruikers die AMS accounts voorafgaande toohello januari 10 2017 release gemaakt, die u hebt een **klassieke** type van een streaming-eindpunt. Dit type maakt deel uit van Hallo streaming-eindpunt, versie "1.0".

Als uw **versie "1.0"** streaming-eindpunt is > = 1 premium streaming-eenheden (SU), deze worden premium streaming-eindpunt en bieden alle AMS-functies (net als Hallo **standaard/Premium** type) zonder aanvullende configuratiestappen.

>[!NOTE]
>**Klassieke** streaming-eindpunten (versie "1.0" en 0 SU), biedt beperkte onderdelen en een SLA niet opgenomen. Het verdient aanbeveling toomigrate te**standaard** typt u een betere ervaring en toouse functies zoals dynamische pakketten of versleuteling en andere functies die worden geleverd met Hallo tooget **standaard** type. toomigrate toohello **standaard** typt, gaat u toohello [Azure-portal](https://portal.azure.com/) en selecteer **Opt-in tooStandard**. Zie voor meer informatie over de migratie Hallo [migratie](#migration-between-types) sectie.
>
>Houd er rekening mee dat deze bewerking kan niet worden teruggedraaid en gevolgen voor de prijscategorie heeft.
>
 
## <a name="comparing-streaming-types"></a>Streaming typen vergelijken

### <a name="versions"></a>Versies

|Type|StreamingEndpointVersion|ScaleUnits|CDN|Facturering|SLA| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Klassiek|1.0|0|N.v.t.|Gratis|N.v.t.|
|Standard streaming-eindpunt|2.0|0|Ja|Betaald|Ja|
|Premium streamingeenheden|1.0|>0|Ja|Betaald|Ja|
|Premium streamingeenheden|2.0|>0|Ja|Betaald|Ja|

### <a name="features"></a>Functies

Functie|Standard|Premium
---|---|---
Eerste 15 dagen gratis| Ja |Nee
Doorvoer |Up too600 Mbps wanneer Azure CDN wordt niet gebruikt. Kan worden geschaald met CDN.|200 Mbps per streaming-eenheid (SU). Kan worden geschaald met CDN.
SLA | 99.9|99,9 (200 Mbps per SU).
CDN|Azure CDN van derden CDN of er is geen CDN.|Azure CDN van derden CDN of er is geen CDN.
Facturering is verdeeld.| Dagelijks|Dagelijks
Dynamische versleuteling|Ja|Ja
Dynamische verpakking|Ja|Ja
Schalen|Automatisch wordt geschaald up toohello gericht doorvoer.|Aanvullende streaming-eenheden
IP-filtering/G20/aangepast host|Ja|Ja
Progressief downloaden|Ja|Ja
Aanbevolen gebruik |Aanbevolen Hallo overgrote deel uitmaken van het streaming-scenario's.|Het gebruik van Professional.<br/>Als u denkt dat wellicht u behoeften buiten standaard. Contact met ons opnemen (amsstreaming op microsoft.com) als u verwacht de grootte van een gelijktijdige doelgroep groter is dan 50.000 viewers dat.


## <a name="migration-between-types"></a>Migratie tussen typen

Van | te| Actie
---|---|---
Klassiek|Standard|Nodig tooopt in
Klassiek|Premium| Schaal (extra streaming-eenheden)
Standaard/Premium|Klassiek|Niet beschikbaar (als streaming endpoint versie 1.0 is. Het toochange tooclassic bij het instellen van scaleunits is toegestaan te "0")
Standard (met/zonder CDN)|Premium met Hallo dezelfde configuraties|Toegestaan in Hallo **gestart** status. (via Azure portal)
Premium (met/zonder CDN)|Standaard Hello dezelfde configuraties|Toegestaan in Hallo **gestart** status (via Azure portal)
Standard (met/zonder CDN)|Premium met andere configuratie|Toegestaan in Hallo **gestopt** status (via Azure portal). Niet toegestaan in Hallo actief is.
Premium (met/zonder CDN)|Standard met andere configuratie|Toegestaan in Hallo **gestopt** status (via Azure portal). Niet toegestaan in Hallo actief is.
Versie 1.0 met SU > = 1 met CDN|Standaard/Premium met geen CDN|Toegestaan in Hallo **gestopt** status. Niet toegestaan in Hallo **gestart** status.
Versie 1.0 met SU > = 1 met CDN|Standard met/zonder CDN|Toegestaan in Hallo **gestopt** status. Niet toegestaan in Hallo **gestart** status. Versie 1.0 van het CDN zal worden verwijderd en nieuwe gemaakt en gestart.
Versie 1.0 met SU > = 1 met CDN|Premium met/zonder CDN|Toegestaan in Hallo **gestopt** status. Niet toegestaan in Hallo **gestart** status. Klassieke CDN worden verwijderd en nieuwe één gemaakt en gestart.

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

