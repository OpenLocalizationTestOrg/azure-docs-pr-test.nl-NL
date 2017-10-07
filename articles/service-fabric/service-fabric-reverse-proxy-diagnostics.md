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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="34ec6-103">Controle en diagnose van aanvraagverwerking op Hallo omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="34ec6-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="34ec6-104">Vanaf Hallo 5.7-versie van Service Fabric, zijn reverse proxy-gebeurtenissen beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="34ec6-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="34ec6-105">Hallo gebeurtenissen zijn beschikbaar in twee kanalen een met alleen foutgebeurtenissen gerelateerd toorequest verwerkingsfout op Hallo omgekeerde proxy en het tweede kanaal met uitgebreide gebeurtenissen met de vermeldingen voor geslaagde en mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="34ec6-106">Raadpleeg te[reverse proxy-gebeurtenissen verzamelen](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable en gebeurtenissen verzamelen van deze kanalen in lokale en Azure Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="34ec6-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="34ec6-107">Problemen oplossen met Logboeken met diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="34ec6-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="34ec6-108">Hier volgen enkele voorbeelden van hoe toointerpret Hallo algemene fout logboeken dat een kan optreden:</span><span class="sxs-lookup"><span data-stu-id="34ec6-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="34ec6-109">Omgekeerde proxy retourneert statuscode van antwoord 504 (time-out).</span><span class="sxs-lookup"><span data-stu-id="34ec6-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="34ec6-110">Een reden kan zijn vanwege toohello service mislukken tooreply binnen Hallo aanvraag time-outperiode.</span><span class="sxs-lookup"><span data-stu-id="34ec6-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="34ec6-111">Hallo eerste onderstaande gebeurtenislogboeken Hallo-details van Hallo-aanvraag ontvangen op Hallo omgekeerde proxy.</span><span class="sxs-lookup"><span data-stu-id="34ec6-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="34ec6-112">Hallo tweede gebeurtenis geeft aan dat Hallo aanvraag is mislukt tijdens het doorsturen van tooservice, behoren te ' Interne fout ERROR_WINHTTP_TIMEOUT = "</span><span class="sxs-lookup"><span data-stu-id="34ec6-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="34ec6-113">Hallo nettolading bevat:</span><span class="sxs-lookup"><span data-stu-id="34ec6-113">hello payload includes:</span></span>

    *  <span data-ttu-id="34ec6-114">**traceId**: deze GUID kan worden gebruikt toocorrelate alle Hallo gebeurtenissen tooa één aanvraag overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="34ec6-115">Hallo in Hallo lager dan twee gebeurtenissen traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, wat ze horen toohello dezelfde aanvraag.</span><span class="sxs-lookup"><span data-stu-id="34ec6-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="34ec6-116">**Aanvraagurl**: Hallo URL (Reverse proxy-URL) toowhich Hallo-aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="34ec6-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="34ec6-117">**term**: HTTP-term.</span><span class="sxs-lookup"><span data-stu-id="34ec6-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="34ec6-118">**remoteAddress**: adres van client Hallo-aanvraag wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="34ec6-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="34ec6-119">**resolvedServiceUrl**: Service-eindpunt-URL toowhich Hallo binnenkomende aanvraag is opgelost.</span><span class="sxs-lookup"><span data-stu-id="34ec6-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="34ec6-120">**errorDetails**: meer informatie over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="34ec6-120">**errorDetails**: Additional information about hello failure.</span></span>

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

2. <span data-ttu-id="34ec6-121">Omgekeerde proxy retourneert antwoord-statuscode 404 (niet gevonden).</span><span class="sxs-lookup"><span data-stu-id="34ec6-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="34ec6-122">Hier volgt een voorbeeld van de gebeurtenis waarbij omgekeerde proxy 404 retourneert omdat deze toofind Hallo die overeenkomt met de service-eindpunt is mislukt.</span><span class="sxs-lookup"><span data-stu-id="34ec6-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="34ec6-123">Hallo nettolading van belang zijn hier worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="34ec6-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="34ec6-124">**processRequestPhase**: Hiermee wordt aangegeven Hallo fase tijdens het verwerken van aanvraag wanneer Hallo-fout is opgetreden, ***TryGetEndpoint*** eenledige</span><span class="sxs-lookup"><span data-stu-id="34ec6-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="34ec6-125">tijdens de poging toofetch Hallo service-eindpunt tooforward aan.</span><span class="sxs-lookup"><span data-stu-id="34ec6-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="34ec6-126">**errorDetails**: geeft een lijst van Hallo eindpunt zoekcriteria voldoen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="34ec6-127">Hier ziet u dat Hallo listenerName opgegeven = **FrontEndListener** dat Hallo replica eindpuntlijst alleen een listener met de naam van de Hallo bevat **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="34ec6-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
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
    <span data-ttu-id="34ec6-128">Een ander voorbeeld waarbij 404 kan worden geretourneerd door reverse proxy is niet gevonden: configuratieparameter ApplicationGateway\Http **SecureOnlyMode** tootrue is ingesteld met de reverse proxy Hallo luistert op **HTTPS**, alle Hallo replica eindpunten zijn echter niet-beveiligde (luistert naar HTTP).</span><span class="sxs-lookup"><span data-stu-id="34ec6-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="34ec6-129">Reverse proxy retourneert 404 omdat het een eindpunt luistert naar HTTPS tooforward Hallo-aanvraag niet is gevonden.</span><span class="sxs-lookup"><span data-stu-id="34ec6-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="34ec6-130">Hallo-parameters in de nettolading Hallo analyseren helpt toonarrow omlaag Hallo probleem:</span><span class="sxs-lookup"><span data-stu-id="34ec6-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="34ec6-131">Aanvraag toohello omgekeerde proxy is mislukt met een time-outfout.</span><span class="sxs-lookup"><span data-stu-id="34ec6-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="34ec6-132">Hallo-gebeurtenislogboeken bevatten een gebeurtenis met Hallo ontvangen aanvraaggegevens (hier niet weergegeven).</span><span class="sxs-lookup"><span data-stu-id="34ec6-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="34ec6-133">de volgende gebeurtenis Hallo ziet u dat Hallo-service met statuscode 404 reageerde en omgekeerde proxy te zetten initieert.</span><span class="sxs-lookup"><span data-stu-id="34ec6-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

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
    <span data-ttu-id="34ec6-134">Wanneer alle Hallo-gebeurtenissen verzamelen, ziet u een trein van gebeurtenissen met elke oplossen en voorwaarts poging.</span><span class="sxs-lookup"><span data-stu-id="34ec6-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="34ec6-135">laatste gebeurtenis in de reeks Hallo Hallo toont Hallo aanvraagverwerking is mislukt met een time-out, samen met de Hallo aantal geslaagde los pogingen.</span><span class="sxs-lookup"><span data-stu-id="34ec6-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="34ec6-136">Het wordt aanbevolen tookeep Hallo uitgebreide kanaal gebeurtenissen verzamelen is standaard uitgeschakeld en inschakelen voor het oplossen van problemen op basis van de nodig.</span><span class="sxs-lookup"><span data-stu-id="34ec6-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

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
    
    <span data-ttu-id="34ec6-137">Als de verzameling is ingeschakeld voor alleen kritieke fout/gebeurtenissen, ziet u een gebeurtenis met informatie over Hallo time-out en het aantal pogingen dat los Hallo.</span><span class="sxs-lookup"><span data-stu-id="34ec6-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="34ec6-138">Als service Hallo toosend een 404 status code back toohello gebruiker, moet deze vergezeld van een 'X ServiceFabric'-header.</span><span class="sxs-lookup"><span data-stu-id="34ec6-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="34ec6-139">Nadat dit is hersteld, ziet u dat de omgekeerde proxy forwards Hallo status code back toohello client.</span><span class="sxs-lookup"><span data-stu-id="34ec6-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="34ec6-140">Gevallen wanneer Hallo-client de verbinding Hallo-aanvraag verbroken heeft.</span><span class="sxs-lookup"><span data-stu-id="34ec6-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="34ec6-141">Hallo hieronder gebeurtenis wordt vastgelegd als omgekeerde proxy is Hallo antwoord tooclient doorsturen, maar Hallo-client de verbinding verbreekt:</span><span class="sxs-lookup"><span data-stu-id="34ec6-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

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
> <span data-ttu-id="34ec6-142">Verwerking van gebeurtenissen gerelateerde toowebsocket aanvragen worden momenteel niet geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="34ec6-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="34ec6-143">Dit wordt in de volgende release Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="34ec6-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34ec6-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34ec6-144">Next steps</span></span>
* <span data-ttu-id="34ec6-145">[Gebeurtenis-aggregatie en verzameling op basis van Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) voor het inschakelen van logboekverzameling in Azure-clusters.</span><span class="sxs-lookup"><span data-stu-id="34ec6-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="34ec6-146">tooview Service Fabric-gebeurtenissen in Visual Studio, Zie [bewaken en onderzoeken van lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="34ec6-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="34ec6-147">Raadpleeg te[omgekeerde proxy tooconnect toosecure services configureren](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) voor Azure Resource Manager-sjabloon voorbeelden tooconfigure beveiligde omgekeerde proxy met Hallo andere service-certificaatopties voor validatie.</span><span class="sxs-lookup"><span data-stu-id="34ec6-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="34ec6-148">Lees [Service Fabric omgekeerde proxy](service-fabric-reverseproxy.md) toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="34ec6-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
