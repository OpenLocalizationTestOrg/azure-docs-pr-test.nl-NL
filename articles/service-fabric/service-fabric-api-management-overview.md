---
title: Service Fabric aaaAzure met overzicht van API Management | Microsoft Docs
description: Dit artikel bevat een inleiding toousing Azure API Management als een gateway tooyour Service Fabric-toepassingen.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Service Fabric met Azure API Management-overzicht

Cloud-toepassingen moeten doorgaans een front-gateway tooprovide één punt van toegangsroutes voor gebruikers, apparaten en andere toepassingen. In de Service Fabric, een gateway worden alle stateless Services, zoals een [ASP.NET Core toepassing](service-fabric-reliable-services-communication-aspnetcore.md), of een andere service die zijn ontworpen voor inkomend verkeer, zoals [Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [IoT Hub](https://docs.microsoft.com/azure/iot-hub/), of [Azure API Management](https://docs.microsoft.com/azure/api-management/).

Dit artikel bevat een inleiding toousing Azure API Management als een gateway tooyour Service Fabric-toepassingen. API Management wordt rechtstreeks geïntegreerd met Service Fabric, zodat u toopublish API's met een groot aantal regels tooyour back-end Service Fabric routeringsservices. 

## <a name="architecture"></a>Architectuur
Een algemene Service Fabric-architectuur gebruikt een webtoepassing van één pagina waarmee HTTP-aanroepen tooback-end-services die HTTP APIs blootstellen. Hallo [aan de slag Service Fabric-voorbeeldtoepassing](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) toont een voorbeeld van deze architectuur.

In dit scenario fungeert een stateless webservice als gateway Hallo in Hallo Service Fabric-toepassing. Deze methode vereist een webservice die HTTP proxy kunt u toowrite aanvragen tooback-end-services, zoals wordt weergegeven in het volgende diagram Hallo:

![Service Fabric met Azure API Management-topologie-overzicht][sf-web-app-stateless-gateway]

Als toepassingen worden uitgebreid in complexiteit, dus Hallo gateways die een API voor allerlei back-end-services moeten aanbieden. Azure API Management is ontworpen toohandle complexe API's met regels voor het doorsturen, toegang tot beheer, snelheidsbeperking, bewaking, logboekregistratie en antwoord in cache opslaan met minimale inspanning. Azure API Management ondersteunt detectie van de Service Fabric-service, partitie-resolutie en replica selectie toointelligently route aanvragen rechtstreeks tooback-end-services in Service Fabric, dus u geen toowrite uw eigen staatloze API-gateway hebt. 

Hallo web die UI nog steeds worden geleverd via een webservice terwijl HTTP API-aanroepen worden beheerd en worden gerouteerd via Azure API Management, zoals wordt weergegeven in het volgende diagram Hallo in dit scenario:

![Service Fabric met Azure API Management-topologie-overzicht][sf-apim-web-app]

## <a name="application-scenarios"></a>Toepassingsscenario's

Services in Service Fabric mogelijk stateless of stateful en ze kunnen worden gepartitioneerd met een van drie schema's: singleton, int-64-bereik, en met de naam. Omzetting van de service-eindpunt is vereist om een specifieke partitie van een specifieke service-exemplaar te identificeren. Bij het omzetten van een eindpunt van een service, worden beide Hallo exemplaarnaam (bijvoorbeeld `fabric:/myapp/myservice`) ook specifieke partitie Hallo van Hallo-service moet worden opgegeven, behalve in geval van Hallo van singleton-partitie.

Azure API Management kan worden gebruikt met elke combinatie van stateless services, stateful services en een partitieschema.

## <a name="send-traffic-tooa-stateless-service"></a>Verkeer tooa staatloze service verzenden

In de meest eenvoudige geval hello doorgestuurd verkeer tooa staatloze service-exemplaar. tooachieve, een API Management-bewerking bevat een beleid voor binnenkomend verkeer met een Service Fabric back-end die is toegewezen tooa specifieke staatloze service-exemplaar in Hallo Service Fabric-back-end. Aanvragen verzonden toothat service verzonden tooa willekeurige replica van Hallo staatloze service-exemplaar.

#### <a name="example"></a>Voorbeeld
In Hallo volgen scenario, een Service Fabric-toepassing bevat een stateless service met de naam `fabric:/app/fooservice`, die wordt er een interne HTTP-API. Hallo-exemplaarnaam kan is bekend en vastgelegde rechtstreeks in Hallo inkomende verwerking van API Management-beleid. 

![Service Fabric met Azure API Management-topologie-overzicht][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Verkeer tooa stateful service verzenden

Vergelijkbare toohello staatloze service scenario verkeer kan worden doorgestuurd tooa stateful service-exemplaar hebben. In dit geval een API Management-bewerking bevat een beleid voor binnenkomend verkeer met een Service Fabric back-end waarmee een specifieke aanvraag tooa-partitie van een specifieke *stateful* service-exemplaar. Hallo partitie toomap elke aanvraag toois berekend via een lambda-methode met een invoer van Hallo inkomende HTTP-aanvraag, zoals een waarde in Hallo URL-pad. Hallo beleid mogelijk geconfigureerde toosend aanvragen toohello primaire replica alleen of tooa willekeurige replica voor leesbewerkingen.

#### <a name="example"></a>Voorbeeld

In de Hallo scenario te volgen, een Service Fabric-toepassing bevat een gepartitioneerde stateful service met de naam `fabric:/app/userservice` die wordt er een interne HTTP-API. Hallo-exemplaarnaam kan is bekend en vastgelegde rechtstreeks in Hallo inkomende verwerking van API Management-beleid.  

Hallo service is gepartitioneerd met Hallo Int64 partitieschema met twee partities en een sleutel die omvat `Int64.MinValue` te`Int64.MaxValue`. Hallo back-end beleid berekent een partitiesleutel binnen dat bereik door te converteren Hallo `id` waarde die is opgegeven in Hallo URL-aanvraag pad tooa 64-bits geheel getal, hoewel elk algoritme gebruikte hier toocompute Hallo partitiesleutel. 

![Service Fabric met Azure API Management-topologie-overzicht][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Verkeer verzenden toomultiple stateless services

In meer geavanceerde scenario's, kunt u een API Management-bewerking dat maps toomore dan één service-exemplaar aanvragen definiëren. In dit geval wordt bevat elke bewerking een beleid dat is toegewezen aanvragen tooa specifieke service-exemplaar op basis van waarden van Hallo inkomende HTTP-aanvraag, zoals Hallo URL-pad of de query-tekenreeks en in geval van stateful services Hallo een partitie in Hallo service-exemplaar . 

tooachieve dit een API Management bewerking bevat een beleid voor binnenkomend verkeer met een Service Fabric back-end die tooa staatloze service-exemplaar in Hallo Service Fabric back-end op basis van waarden ophalen uit Hallo inkomende HTTP-aanvraag wordt toegewezen. Aanvragen tooa service-exemplaar worden tooa willekeurige replica van de service-exemplaar Hallo verzonden.

#### <a name="example"></a>Voorbeeld

In dit voorbeeld wordt een nieuwe staatloze service-exemplaar gemaakt voor elke gebruiker van een toepassing met de naam van een dynamisch gegenereerd met behulp van de volgende formule Hallo:
 
 - `fabric:/app/users/<username>`

 Elke service een unieke naam heeft, maar Hallo niet bekend zijn vooraf omdat Hallo-services worden gemaakt in het antwoord toouser of admin invoer en dus kan niet worden hardgecodeerd in APIM beleid of routeringsregels. In plaats daarvan Hallo-naam van Hallo service toowhich toosend een aanvraag wordt gegenereerd in Hallo back-end-beleidsdefinitie van Hallo `name` waarde die is opgegeven in het pad naar Hallo URL-aanvraag. Bijvoorbeeld:

  - Een aanvraag te`/api/users/foo` gerouteerde tooservice-exemplaar`fabric:/app/users/foo`
  - Een aanvraag te`/api/users/bar` gerouteerde tooservice-exemplaar`fabric:/app/users/bar`

![Service Fabric met Azure API Management-topologie-overzicht][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Verkeer verzenden toomultiple stateful services

Vergelijkbaar toohello staatloze service-voorbeeld: een API Management opnieuw kunt toewijzen aanvragen toomore dan een **stateful** service-exemplaar, in welk geval u ook tooperform partitie naamomzetting mogelijk moet voor elke stateful service exemplaar.

tooachieve dit een API Management bewerking bevat een beleid voor binnenkomend verkeer met een Service Fabric back-end die tooa stateful service-exemplaar in Hallo Service Fabric back-end op basis van waarden ophalen uit Hallo inkomende HTTP-aanvraag wordt toegewezen. Bovendien kan toomapping aanvraag toospecific service-exemplaar, Hallo-aanvraag ook worden toegewezen tooa specifieke partitie binnen Hallo service-exemplaar en eventueel tooeither Hallo primaire replica of een willekeurige secundaire replica in Hallo-partitie.

#### <a name="example"></a>Voorbeeld

In dit voorbeeld wordt een nieuwe stateful service-exemplaar voor elke gebruiker van toepassing hello gemaakt met de naam van een dynamisch gegenereerd met behulp van de volgende formule Hallo:
 
 - `fabric:/app/users/<username>`

 Elke service een unieke naam heeft, maar Hallo niet bekend zijn vooraf omdat Hallo-services worden gemaakt in het antwoord toouser of admin invoer en dus kan niet worden hardgecodeerd in APIM beleid of routeringsregels. In plaats daarvan Hallo-naam van Hallo service toowhich toosend een aanvraag wordt gegenereerd in Hallo back-end-beleidsdefinitie van Hallo `name` opgegeven waarde Hallo URL-Aanvraagpad. Bijvoorbeeld:

  - Een aanvraag te`/api/users/foo` gerouteerde tooservice-exemplaar`fabric:/app/users/foo`
  - Een aanvraag te`/api/users/bar` gerouteerde tooservice-exemplaar`fabric:/app/users/bar`

Elk exemplaar van de service ook is gepartitioneerd met Hallo Int64 partitieschema met twee partities en een sleutel bereik die omvat `Int64.MinValue` te`Int64.MaxValue`. Hallo back-end beleid berekent een partitiesleutel binnen dat bereik door te converteren Hallo `id` waarde die is opgegeven in Hallo URL-aanvraag pad tooa 64-bits geheel getal, hoewel elk algoritme gebruikte hier toocompute Hallo partitiesleutel. 

![Service Fabric met Azure API Management-topologie-overzicht][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Volgende stappen

Ga als volgt Hallo [snelstartgids](service-fabric-api-management-quick-start.md) tooset van uw eerste Service Fabric-cluster met API Management en stroom aanvragen via de API Management tooyour services.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png