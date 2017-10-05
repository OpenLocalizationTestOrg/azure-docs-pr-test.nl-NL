---
title: Azure Service Fabric reverse proxy diagnostics | Microsoft Docs
description: Informatie over het bewaken en onderzoeken van aanvraag in de omgekeerde proxy worden verwerkt.
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
ms.openlocfilehash: 3bc631606afbc93d5bca94f4955fd2ef816fa9fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-request-processing-at-the-reverse-proxy"></a><span data-ttu-id="c833e-103">Controle en diagnose van aanvraagverwerking op de omgekeerde proxy</span><span class="sxs-lookup"><span data-stu-id="c833e-103">Monitor and diagnose request processing at the reverse proxy</span></span>

<span data-ttu-id="c833e-104">Beginnen met de 5.7 release van Service Fabric, zijn reverse proxy-gebeurtenissen beschikbaar voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="c833e-104">Starting with the 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="c833e-105">De gebeurtenissen zijn beschikbaar in twee kanalen, één met alleen foutgebeurtenissen met betrekking tot het mislukken van de verwerking van aanvragen bij de omgekeerde proxy en het tweede kanaal met uitgebreide gebeurtenissen met de vermeldingen voor geslaagde en mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c833e-105">The events are available in two channels, one with only error events related to request processing failure at the reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="c833e-106">Raadpleeg [reverse proxy-gebeurtenissen verzamelen](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) om in te schakelen bij het verzamelen van gebeurtenissen uit deze kanalen in lokale en Azure Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="c833e-106">Refer to [Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) to enable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="c833e-107">Problemen oplossen met Logboeken met diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="c833e-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="c833e-108">Hier volgen enkele voorbeelden over het interpreteren van de algemene fout logboeken die een kan optreden:</span><span class="sxs-lookup"><span data-stu-id="c833e-108">Here are some examples on how to interpret the common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="c833e-109">Omgekeerde proxy retourneert statuscode van antwoord 504 (time-out).</span><span class="sxs-lookup"><span data-stu-id="c833e-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="c833e-110">Een reden hiervoor kan worden veroorzaakt door de service te beantwoorden binnen de time-outperiode van aanvraag is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c833e-110">One reason could be due to the service failing to reply within the request timeout period.</span></span>
<span data-ttu-id="c833e-111">De eerste gebeurtenis onder Logboeken de details van de aanvraag is ontvangen op de omgekeerde proxy.</span><span class="sxs-lookup"><span data-stu-id="c833e-111">The first event below logs the details of the request received at the reverse proxy.</span></span> <span data-ttu-id="c833e-112">De tweede gebeurtenis geeft aan dat de aanvraag is mislukt tijdens het doorsturen naar de service, vanwege ' Interne fout ERROR_WINHTTP_TIMEOUT = "</span><span class="sxs-lookup"><span data-stu-id="c833e-112">The second event indicates that the request failed while forwarding to service, due to "internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="c833e-113">De nettolading bevat:</span><span class="sxs-lookup"><span data-stu-id="c833e-113">The payload includes:</span></span>

    *  <span data-ttu-id="c833e-114">**traceId**: deze GUID kan worden gebruikt om alle gebeurtenissen die overeenkomt met één aanvraag correleren.</span><span class="sxs-lookup"><span data-stu-id="c833e-114">**traceId**: This GUID can be used to correlate all the events corresponding to a single request.</span></span> <span data-ttu-id="c833e-115">In de onderstaande twee gebeurtenissen, de traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, wat ze deel uitmaken van dezelfde aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c833e-115">In the below two events, the traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong to the same request.</span></span>
    *  <span data-ttu-id="c833e-116">**Aanvraagurl**: de URL (Reverse proxy-URL) waarop de aanvraag is verzonden.</span><span class="sxs-lookup"><span data-stu-id="c833e-116">**requestUrl**: The URL (Reverse proxy URL) to which the request was sent.</span></span>
    *  <span data-ttu-id="c833e-117">**term**: HTTP-term.</span><span class="sxs-lookup"><span data-stu-id="c833e-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="c833e-118">**remoteAddress**: adres van client verzenden van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c833e-118">**remoteAddress**: Address of client sending the request.</span></span>
    *  <span data-ttu-id="c833e-119">**resolvedServiceUrl**: Service-eindpunt-URL waarnaar de binnenkomende aanvraag opgelost is.</span><span class="sxs-lookup"><span data-stu-id="c833e-119">**resolvedServiceUrl**: Service endpoint URL to which the incoming request was resolved.</span></span> 
    *  <span data-ttu-id="c833e-120">**errorDetails**: als u meer informatie over de fout.</span><span class="sxs-lookup"><span data-stu-id="c833e-120">**errorDetails**: Additional information about the failure.</span></span>

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
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request to service: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
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

2. <span data-ttu-id="c833e-121">Omgekeerde proxy retourneert antwoord-statuscode 404 (niet gevonden).</span><span class="sxs-lookup"><span data-stu-id="c833e-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="c833e-122">Hier volgt een voorbeeld van de gebeurtenis waarbij omgekeerde proxy 404 retourneert omdat het vinden van het overeenkomende service-eindpunt is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c833e-122">Here is an example event where reverse proxy returns 404 since it failed to find the matching service endpoint.</span></span>
    <span data-ttu-id="c833e-123">De nettolading van belang zijn hier worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="c833e-123">The payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="c833e-124">**processRequestPhase**: Hiermee geeft u de fase tijdens het verwerken van aanvraag als de fout is opgetreden, ***TryGetEndpoint*** eenledige</span><span class="sxs-lookup"><span data-stu-id="c833e-124">**processRequestPhase**: Indicates the phase during request processing when the failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="c833e-125">tijdens het ophalen van het service-eindpunt te sturen naar.</span><span class="sxs-lookup"><span data-stu-id="c833e-125">while trying to fetch the service endpoint to forward to.</span></span> 
    *  <span data-ttu-id="c833e-126">**errorDetails**: geeft een lijst van de zoekcriteria voor het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="c833e-126">**errorDetails**: Lists the endpoint search criteria.</span></span> <span data-ttu-id="c833e-127">Hier kunt u zien dat de listenerName opgegeven = **FrontEndListener** dat de replica endpoint-lijst alleen een listener met de naam bevat **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="c833e-127">Here you can see that the listenerName specified = **FrontEndListener** whereas the replica endpoint list only contains a listener with the name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward to service: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
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
    <span data-ttu-id="c833e-128">Een ander voorbeeld waarbij 404 kan worden geretourneerd door reverse proxy is niet gevonden: configuratieparameter ApplicationGateway\Http **SecureOnlyMode** is ingesteld op waar met de reverse proxy luistert op **HTTPS**echter alle van de replica-eindpunten zijn niet-beveiligde (luistert naar HTTP).</span><span class="sxs-lookup"><span data-stu-id="c833e-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set to true with the reverse proxy listening on **HTTPS**, however all of the replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="c833e-129">Reverse proxy retourneert 404 omdat er een eindpunt luistert naar HTTPS voor het doorsturen van de aanvraag kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="c833e-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS to forward the request.</span></span> <span data-ttu-id="c833e-130">Analyse van de parameters in de gebeurtenis nettolading helpt om het probleem vast te stellen:</span><span class="sxs-lookup"><span data-stu-id="c833e-130">Analyzing the parameters in the event payload helps to narrow down the issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="c833e-131">Aanvraag voor de omgekeerde proxy is mislukt met een time-outfout.</span><span class="sxs-lookup"><span data-stu-id="c833e-131">Request to the reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="c833e-132">De gebeurtenislogboeken bevatten een gebeurtenis met de ontvangen request details (hier niet weergegeven).</span><span class="sxs-lookup"><span data-stu-id="c833e-132">The event logs contain an event with the received request details (not shown here).</span></span>
    <span data-ttu-id="c833e-133">De volgende gebeurtenis ziet u dat de service met statuscode 404 reageerde en omgekeerde proxy te zetten initieert.</span><span class="sxs-lookup"><span data-stu-id="c833e-133">The next event shows that the service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request to service returned: status code = 404, status description = , Reresolving ",
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
    <span data-ttu-id="c833e-134">Wanneer alle gebeurtenissen verzamelen, ziet u een trein van gebeurtenissen met elke oplossen en voorwaarts poging.</span><span class="sxs-lookup"><span data-stu-id="c833e-134">When collecting all the events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="c833e-135">De laatste gebeurtenis in de reeks ziet u dat de aanvraagverwerking is mislukt met een time-out, samen met het aantal pogingen voor geslaagde oplossen.</span><span class="sxs-lookup"><span data-stu-id="c833e-135">The last event in the series shows the request processing has failed with a timeout, along with the number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c833e-136">Het verdient aanbeveling te houden van de uitgebreide kanaal gebeurtenisverzameling is standaard uitgeschakeld en inschakelen voor het oplossen van problemen op basis van de nodig.</span><span class="sxs-lookup"><span data-stu-id="c833e-136">It is recommended to keep the  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

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
    
    <span data-ttu-id="c833e-137">Als de verzameling is ingeschakeld voor alleen kritieke fout/gebeurtenissen, ziet u een gebeurtenis met informatie over de time-out en het aantal pogingen oplossen.</span><span class="sxs-lookup"><span data-stu-id="c833e-137">If collection is enabled for critical/error events only, you see one event with details about the timeout and the number of resolve attempts.</span></span> 
    
    <span data-ttu-id="c833e-138">Als de service een statuscode 404 terug naar de gebruiker te verzenden, moet deze vergezeld van een 'X ServiceFabric'-header.</span><span class="sxs-lookup"><span data-stu-id="c833e-138">If the service intends to send a 404 status code back to the user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="c833e-139">Nadat dit is hersteld, ziet u dat reverse proxy de statuscode terug naar de client stuurt.</span><span class="sxs-lookup"><span data-stu-id="c833e-139">After fixing this, you will see that reverse proxy forwards the status code back to the client.</span></span>  

4. <span data-ttu-id="c833e-140">Gevallen wanneer de client heeft verbinding met de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c833e-140">Cases when the client has disconnected the request.</span></span>

    <span data-ttu-id="c833e-141">De onderstaande gebeurtenis wordt geregistreerd wanneer het antwoord op de client is doorsturen van omgekeerde proxy, maar de client de verbinding verbreekt:</span><span class="sxs-lookup"><span data-stu-id="c833e-141">The below event is recorded when reverse proxy is forwarding the response to client but the client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable to send response to client: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
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
> <span data-ttu-id="c833e-142">Gebeurtenissen met betrekking tot de verwerking van de websocket-aanvraag worden momenteel niet geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="c833e-142">Events related to websocket request processing are not currently logged.</span></span> <span data-ttu-id="c833e-143">Dit wordt toegevoegd in de volgende release.</span><span class="sxs-lookup"><span data-stu-id="c833e-143">This will be added in the next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c833e-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c833e-144">Next steps</span></span>
* <span data-ttu-id="c833e-145">[Gebeurtenis-aggregatie en verzameling op basis van Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) voor het inschakelen van logboekverzameling in Azure-clusters.</span><span class="sxs-lookup"><span data-stu-id="c833e-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="c833e-146">Zie voor meer informatie over het bekijken van Service Fabric-gebeurtenissen in Visual Studio [bewaken en onderzoeken van lokaal](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="c833e-146">To view Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="c833e-147">Raadpleeg [configureren omgekeerde proxy voor het verbinding maken met veilige services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) voor Azure Resource Manager voorbeelden van de sjabloon voor het configureren van secure reverse proxy gebruikt met het certificaat voor verschillende validatieopties voor.</span><span class="sxs-lookup"><span data-stu-id="c833e-147">Refer to [Configure reverse proxy to connect to secure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples to configure secure reverse proxy with the different service certificate validation options.</span></span>
* <span data-ttu-id="c833e-148">Lees [Service Fabric omgekeerde proxy](service-fabric-reverseproxy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c833e-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) to learn more.</span></span>
