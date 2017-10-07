---
title: Service Fabric aaaAzure reverse proxy diagnostics | Microsoft Docs
description: Meer informatie over hoe toomonitor en onderzoeken van aanvraagverwerking op Hallo omgekeerde proxy.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Controle en diagnose van aanvraagverwerking op Hallo omgekeerde proxy

Vanaf Hallo 5.7-versie van Service Fabric, zijn reverse proxy-gebeurtenissen beschikbaar voor de verzameling. Hallo gebeurtenissen zijn beschikbaar in twee kanalen een met alleen foutgebeurtenissen gerelateerd toorequest verwerkingsfout op Hallo omgekeerde proxy en het tweede kanaal met uitgebreide gebeurtenissen met de vermeldingen voor geslaagde en mislukte aanvragen.

Raadpleeg te[reverse proxy-gebeurtenissen verzamelen](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable en gebeurtenissen verzamelen van deze kanalen in lokale en Azure Service Fabric-clusters.

## <a name="troubleshoot-using-diagnostics-logs"></a>Problemen oplossen met Logboeken met diagnostische gegevens
Hier volgen enkele voorbeelden van hoe toointerpret Hallo algemene fout logboeken dat een kan optreden:

1. Omgekeerde proxy retourneert statuscode van antwoord 504 (time-out).

    Een reden kan zijn vanwege toohello service mislukken tooreply binnen Hallo aanvraag time-outperiode.
Hallo eerste onderstaande gebeurtenislogboeken Hallo-details van Hallo-aanvraag ontvangen op Hallo omgekeerde proxy. Hallo tweede gebeurtenis geeft aan dat Hallo aanvraag is mislukt tijdens het doorsturen van tooservice, behoren te ' Interne fout ERROR_WINHTTP_TIMEOUT = " 

    Hallo nettolading bevat:

    *  **traceId**: deze GUID kan worden gebruikt toocorrelate alle Hallo gebeurtenissen tooa één aanvraag overeenkomt. Hallo in Hallo lager dan twee gebeurtenissen traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, wat ze horen toohello dezelfde aanvraag.
    *  **Aanvraagurl**: Hallo URL (Reverse proxy-URL) toowhich Hallo-aanvraag is verzonden.
    *  **term**: HTTP-term.
    *  **remoteAddress**: adres van client Hallo-aanvraag wordt verzonden.
    *  **resolvedServiceUrl**: Service-eindpunt-URL toowhich Hallo binnenkomende aanvraag is opgelost. 
    *  **errorDetails**: meer informatie over Hallo-fout.

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. Omgekeerde proxy retourneert antwoord-statuscode 404 (niet gevonden). 
    
    Hier volgt een voorbeeld van de gebeurtenis waarbij omgekeerde proxy 404 retourneert omdat deze toofind Hallo die overeenkomt met de service-eindpunt is mislukt.
    Hallo nettolading van belang zijn hier worden gebruikt:
    *  **processRequestPhase**: Hiermee wordt aangegeven Hallo fase tijdens het verwerken van aanvraag wanneer Hallo-fout is opgetreden, ***TryGetEndpoint*** eenledige tijdens de poging toofetch Hallo service-eindpunt tooforward aan. 
    *  **errorDetails**: geeft een lijst van Hallo eindpunt zoekcriteria voldoen. Hier ziet u dat Hallo listenerName opgegeven = **FrontEndListener** dat Hallo replica eindpuntlijst alleen een listener met de naam van de Hallo bevat **OldListener**.
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    Een ander voorbeeld waarbij 404 kan worden geretourneerd door reverse proxy is niet gevonden: configuratieparameter ApplicationGateway\Http **SecureOnlyMode** tootrue is ingesteld met de reverse proxy Hallo luistert op **HTTPS**, alle Hallo replica eindpunten zijn echter niet-beveiligde (luistert naar HTTP).
    Reverse proxy retourneert 404 omdat het een eindpunt luistert naar HTTPS tooforward Hallo-aanvraag niet is gevonden. Hallo-parameters in de nettolading Hallo analyseren helpt toonarrow omlaag Hallo probleem:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Aanvraag toohello omgekeerde proxy is mislukt met een time-outfout. 
    Hallo-gebeurtenislogboeken bevatten een gebeurtenis met Hallo ontvangen aanvraaggegevens (hier niet weergegeven).
    de volgende gebeurtenis Hallo ziet u dat Hallo-service met statuscode 404 reageerde en omgekeerde proxy te zetten initieert. 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    Wanneer alle Hallo-gebeurtenissen verzamelen, ziet u een trein van gebeurtenissen met elke oplossen en voorwaarts poging.
    laatste gebeurtenis in de reeks Hallo Hallo toont Hallo aanvraagverwerking is mislukt met een time-out, samen met de Hallo aantal geslaagde los pogingen.
    
    > [!NOTE]
    > Het wordt aanbevolen tookeep Hallo uitgebreide kanaal gebeurtenissen verzamelen is standaard uitgeschakeld en inschakelen voor het oplossen van problemen op basis van de nodig.

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    Als de verzameling is ingeschakeld voor alleen kritieke fout/gebeurtenissen, ziet u een gebeurtenis met informatie over Hallo time-out en het aantal pogingen dat los Hallo. 
    
    Als service Hallo toosend een 404 status code back toohello gebruiker, moet deze vergezeld van een 'X ServiceFabric'-header. Nadat dit is hersteld, ziet u dat de omgekeerde proxy forwards Hallo status code back toohello client.  

4. Gevallen wanneer Hallo-client de verbinding Hallo-aanvraag verbroken heeft.

    Hallo hieronder gebeurtenis wordt vastgelegd als omgekeerde proxy is Hallo antwoord tooclient doorsturen, maar Hallo-client de verbinding verbreekt:

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> Verwerking van gebeurtenissen gerelateerde toowebsocket aanvragen worden momenteel niet geregistreerd. Dit wordt in de volgende release Hallo toegevoegd.

## <a name="next-steps"></a>Volgende stappen
* [Gebeurtenis-aggregatie en verzameling op basis van Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) voor het inschakelen van logboekverzameling in Azure-clusters.
* tooview Service Fabric-gebeurtenissen in Visual Studio, Zie [bewaken en onderzoeken van lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Raadpleeg te[omgekeerde proxy tooconnect toosecure services configureren](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) voor Azure Resource Manager-sjabloon voorbeelden tooconfigure beveiligde omgekeerde proxy met Hallo andere service-certificaatopties voor validatie.
* Lees [Service Fabric omgekeerde proxy](service-fabric-reverseproxy.md) toolearn meer.
