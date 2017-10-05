---
title: API's met Azure API Management, Event Hubs en Runscope bewaken | Microsoft Docs
description: Voorbeeld van een toepassing demonstreren van het logboek voor eventhub-beleid door het verbindende Azure API Management, Azure Event Hubs en Runscope voor HTTP-logboekregistratie en controle
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="62df4-103">Uw API's met Azure API Management, Event Hubs en Runscope bewaken</span><span class="sxs-lookup"><span data-stu-id="62df4-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="62df4-104">De [API Management-service](api-management-key-concepts.md) biedt veel mogelijkheden voor het verbeteren van de verwerking van HTTP-aanvragen verzonden naar uw HTTP-API.</span><span class="sxs-lookup"><span data-stu-id="62df4-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="62df4-105">Het bestaan van de aanvragen en antwoorden zijn echter tijdelijke.</span><span class="sxs-lookup"><span data-stu-id="62df4-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="62df4-106">De aanvraag wordt gedaan en wordt via de API Management-service naar uw back-end API gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62df4-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="62df4-107">De aanvraag wordt verwerkt door uw API en een antwoord doorloopt aan de verbruiker API.</span><span class="sxs-lookup"><span data-stu-id="62df4-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="62df4-108">API Management-service houdt een aantal belangrijke statistieken over de API voor weergave in het dashboard van de uitgever-portal, maar ook buiten dat de gegevens verwijderd zijn.</span><span class="sxs-lookup"><span data-stu-id="62df4-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="62df4-109">Met behulp van de [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [beleid](api-management-howto-policies.md) in API Management-service verzendt u details van de aanvraag en de reactie op een [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="62df4-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="62df4-110">Er zijn diverse redenen waarom u mogelijk gebeurtenissen wilt van HTTP-berichten worden verzonden naar uw API's.</span><span class="sxs-lookup"><span data-stu-id="62df4-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="62df4-111">Voorbeelden zijn audittrail van updates, gebruiksanalyse, uitzondering waarschuwingen en 3e integraties van derden.</span><span class="sxs-lookup"><span data-stu-id="62df4-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="62df4-112">In dit artikel laat zien hoe het gehele HTTP-aanvraag en -antwoord bericht vastleggen, verzenden naar een Event Hub en vervolgens relay-bericht naar een service waarmee HTTP-logboekregistratie en controle van de services van derden.</span><span class="sxs-lookup"><span data-stu-id="62df4-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="62df4-113">Waarom verzenden van API Management-Service?</span><span class="sxs-lookup"><span data-stu-id="62df4-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="62df4-114">Het is mogelijk HTTP-middleware waarmee HTTP-API-frameworks vastleggen HTTP-aanvragen en antwoorden en ze in logboekregistratie en controle van systemen feed kunt aansluiten schrijven.</span><span class="sxs-lookup"><span data-stu-id="62df4-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="62df4-115">Het nadeel hiervan is de HTTP-middleware moet worden geïntegreerd in de back-end API en moet overeenkomen met het platform van de API.</span><span class="sxs-lookup"><span data-stu-id="62df4-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="62df4-116">Als er meerdere API's moet elk criterium de middleware implementeren.</span><span class="sxs-lookup"><span data-stu-id="62df4-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="62df4-117">Er zijn vaak redenen waarom de back-end voor API's kan niet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="62df4-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="62df4-118">De Azure API Management-service gebruikt om te integreren met infrastructuur voor logboekregistratie biedt een gecentraliseerd en platformonafhankelijk-oplossing.</span><span class="sxs-lookup"><span data-stu-id="62df4-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="62df4-119">Het is ook schaalbare gedeeltelijk indienen bij de [geo-replicatie](api-management-howto-deploy-multi-region.md) mogelijkheden van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="62df4-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="62df4-120">Waarom verzenden naar een Azure Event Hub?</span><span class="sxs-lookup"><span data-stu-id="62df4-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="62df4-121">Het is een redelijk te vragen, waarom maakt u een beleid dat specifiek is voor Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="62df4-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="62df4-122">Er zijn verschillende plaatsen waar mogelijk wil mijn aanvragen moeten worden geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="62df4-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="62df4-123">Alleen verzenden waarom niet de aanvragen rechtstreeks naar de uiteindelijke bestemming?</span><span class="sxs-lookup"><span data-stu-id="62df4-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="62df4-124">Dit is een optie.</span><span class="sxs-lookup"><span data-stu-id="62df4-124">That is an option.</span></span> <span data-ttu-id="62df4-125">Wanneer u logboekregistratie van aanvragen van een API management-service, is het echter nodig zijn om te overwegen hoe berichtregistratie invloed op de prestaties van de API.</span><span class="sxs-lookup"><span data-stu-id="62df4-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="62df4-126">Geleidelijke toename in belasting kunnen worden verwerkt door het verhogen van de beschikbare exemplaren van de onderdelen van het systeem of door gebruik te maken van geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="62df4-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="62df4-127">Korte pieken in het verkeer kunnen echter leiden tot aanvragen als aanvragen voor de infrastructuur voor logboekregistratie van beginnen met het vertragen belast aanzienlijk vertraagd.</span><span class="sxs-lookup"><span data-stu-id="62df4-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="62df4-128">De Azure Event Hubs is ontworpen voor grote hoeveelheden gegevens, inkomend met capaciteit voor het omgaan met een veel hoger aantal gebeurtenissen dan het aantal HTTP-verwerken voor de meeste API's aanvragen.</span><span class="sxs-lookup"><span data-stu-id="62df4-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="62df4-129">De Event Hub fungeert als een soort geavanceerde buffer tussen uw API management-service en de infrastructuur die wordt opgeslagen en de berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="62df4-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="62df4-130">Dit zorgt ervoor dat de prestaties van uw API niet als gevolg van de infrastructuur voor logboekregistratie afnemen.</span><span class="sxs-lookup"><span data-stu-id="62df4-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="62df4-131">Nadat de gegevens is doorgegeven naar een Event Hub, deze wordt bewaard en wordt gewacht op Event Hub consumenten verwerken.</span><span class="sxs-lookup"><span data-stu-id="62df4-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="62df4-132">De Event Hub niets uit hoe deze worden verwerkt, het is net belangrijk ervoor te zorgen dat het bericht met succes worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="62df4-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="62df4-133">Event Hubs kunnen de stroom gebeurtenissen aan meerdere consumergroepen.</span><span class="sxs-lookup"><span data-stu-id="62df4-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="62df4-134">Hiermee worden gebeurtenissen worden verwerkt door andere systemen.</span><span class="sxs-lookup"><span data-stu-id="62df4-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="62df4-135">Hierdoor kunnen veel integratiescenario's ondersteunen zonder te plaatsen vertragingen bij het toevoegen van de verwerking van de API-aanvraag in de API Management-service als slechts één gebeurtenis moet worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="62df4-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="62df4-136">Een beleid voor het verzenden van de toepassing/HTTP-berichten</span><span class="sxs-lookup"><span data-stu-id="62df4-136">A policy to send application/http messages</span></span>
<span data-ttu-id="62df4-137">Een Event Hub accepteert gebeurtenisgegevens worden opgeslagen als een eenvoudige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="62df4-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="62df4-138">De inhoud van de reeks zijn volledig bepaalt zelf.</span><span class="sxs-lookup"><span data-stu-id="62df4-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="62df4-139">Om te kunnen verpakken in een HTTP-aanvraag en dit uit te verzenden naar Event Hubs moet de tekenreeks met de aanvraag of antwoord informatie.</span><span class="sxs-lookup"><span data-stu-id="62df4-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="62df4-140">In dit soort situaties, als er een bestaande opmaak kan opnieuw worden gebruikt en we kunnen geen ons eigen bij het parseren van code schrijven.</span><span class="sxs-lookup"><span data-stu-id="62df4-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="62df4-141">In eerste instantie als ik beschouwd met behulp van de [HAR](http://www.softwareishard.com/blog/har-12-spec/) voor het verzenden van HTTP-aanvragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="62df4-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="62df4-142">Deze indeling is echter wel geoptimaliseerd voor het opslaan van een reeks van HTTP-aanvragen in een JSON op basis van indeling.</span><span class="sxs-lookup"><span data-stu-id="62df4-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="62df4-143">Het bevat een aantal verplichte elementen die onnodige complexiteit voor het scenario van het HTTP-bericht wordt doorgegeven via de kabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="62df4-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="62df4-144">Een alternatief is om te gebruiken de `application/http` mediatype zoals beschreven in de HTTP-specificatie [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="62df4-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="62df4-145">Dit mediumtype exact dezelfde indeling die wordt gebruikt voor het daadwerkelijk HTTP-berichten verzenden via de kabel gebruikt, maar het volledige bericht kan worden geplaatst in de hoofdtekst van een andere HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62df4-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="62df4-146">In ons geval gaan we net gebruiken de hoofdtekst als ons bericht te verzenden naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="62df4-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="62df4-147">Gemakkelijk, is er een parser dat voorkomt in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotheken die u kunnen deze indeling parseren en te converteren naar het native `HttpRequestMessage` en `HttpResponseMessage` objecten.</span><span class="sxs-lookup"><span data-stu-id="62df4-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="62df4-148">Om te kunnen maken van dit bericht moeten we om te profiteren van C# [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="62df4-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="62df4-149">Hier wordt het beleid dat u een HTTP-bericht naar Azure Event Hubs verzendt.</span><span class="sxs-lookup"><span data-stu-id="62df4-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="62df4-150">De declaratie van het beleid</span><span class="sxs-lookup"><span data-stu-id="62df4-150">Policy declaration</span></span>
<span data-ttu-id="62df4-151">Er enkele bepaalde zaken opgemerkt over dit beleidsexpressie.</span><span class="sxs-lookup"><span data-stu-id="62df4-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="62df4-152">Het logboek voor eventhub-beleid heeft een kenmerk met de naam van logboek-id die verwijst naar de naam van het logboek dat is gemaakt in de API Management-service.</span><span class="sxs-lookup"><span data-stu-id="62df4-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="62df4-153">De details van het instellen van een Event Hub-logboek in de API Management-service vindt u in het document [vastleggen van gebeurtenissen voor Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="62df4-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="62df4-154">Het tweede kenmerk is een optionele parameter zodat Event Hubs die partitie voor het opslaan van het bericht in.</span><span class="sxs-lookup"><span data-stu-id="62df4-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="62df4-155">Event Hubs partities gebruiken voor schaalbaarheid en ten minste twee nodig hebben.</span><span class="sxs-lookup"><span data-stu-id="62df4-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="62df4-156">De levering van berichten is alleen binnen een partitie gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="62df4-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="62df4-157">Als we niet het Event Hub in welke partitie opdragen doen te plaatsen van het bericht, die een round robin-algoritme wordt gebruikt voor de verdelen.</span><span class="sxs-lookup"><span data-stu-id="62df4-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="62df4-158">Echter, die mogelijk enkele van onze berichten volgorde worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="62df4-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="62df4-159">Partities</span><span class="sxs-lookup"><span data-stu-id="62df4-159">Partitions</span></span>
<span data-ttu-id="62df4-160">Ik heb gekozen onze berichten naar gebruikers in volgorde worden geleverd en te profiteren van de load-distributie-functionaliteit van partities te garanderen, HTTP-aanvraagberichten verzenden naar één partitie en HTTP-antwoordberichten naar een tweede partitie.</span><span class="sxs-lookup"><span data-stu-id="62df4-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="62df4-161">Dit zorgt ervoor dat een gelijkmatige verdeling en wij kunnen garanderen dat alle aanvragen worden gebruikt in volgorde en alle antwoorden in volgorde worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62df4-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="62df4-162">Is het mogelijk een reactie op voordat de bijbehorende aanvraag worden verbruikt, maar omdat die niet is een probleem zoals we hebben een ander mechanisme voor het correleren van aanvragen te antwoorden en we weten dat aanvragen altijd voordat antwoorden afkomstig zijn.</span><span class="sxs-lookup"><span data-stu-id="62df4-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="62df4-163">HTTP-nettoladingen</span><span class="sxs-lookup"><span data-stu-id="62df4-163">HTTP payloads</span></span>
<span data-ttu-id="62df4-164">Na het gebouw de `requestLine` gecontroleerd om te zien als de hoofdtekst van de aanvraag moet worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="62df4-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="62df4-165">De aanvraagtekst is afgekapt tot enige 1024.</span><span class="sxs-lookup"><span data-stu-id="62df4-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="62df4-166">Dit kan worden verhoogd, maar afzonderlijke Event Hub berichten beperkt tot 256KB zijn, dus is het waarschijnlijk dat bepaalde HTTP-bericht wordt niet in een enkel bericht passen instanties.</span><span class="sxs-lookup"><span data-stu-id="62df4-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="62df4-167">Bij het uitvoeren van logboekregistratie en analyse kan een aanzienlijke hoeveelheid gegevens worden afgeleid van alleen de regel voor HTTP-aanvraag en -koppen.</span><span class="sxs-lookup"><span data-stu-id="62df4-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="62df4-168">Ook veel API-aanvragen alleen kleine instanties retourneren en dus het verlies van informatie waarde door af te kappen grote instanties vrij minimale in vergelijking met de beperking van overdracht, verwerking en kosten voor opslag te houden van alle inhoud.</span><span class="sxs-lookup"><span data-stu-id="62df4-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="62df4-169">Een afsluitende opmerking over het verwerken van de hoofdtekst is dat we moet doorgeven `true` naar de As<string>()-methode omdat we bij het lezen van de inhoud van de instantie, maar is ook wilt dat de back-end API om te kunnen worden gelezen van de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="62df4-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="62df4-170">Door door te geven waar deze methode we ervoor zorgen dat de hoofdtekst van de buffer worden opgeslagen zodat deze een tweede keer kan worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="62df4-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="62df4-171">Dit is belangrijk te weten als er een API die geen zeer grote bestanden worden geüpload of lange polling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="62df4-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="62df4-172">In deze gevallen zou worden aanbevolen om te voorkomen dat de hoofdtekst helemaal lezen.</span><span class="sxs-lookup"><span data-stu-id="62df4-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="62df4-173">HTTP-headers</span><span class="sxs-lookup"><span data-stu-id="62df4-173">HTTP headers</span></span>
<span data-ttu-id="62df4-174">HTTP-Headers kunnen eenvoudig worden overgedragen via in de berichtindeling in een eenvoudige sleutel/waarde-paar-indeling.</span><span class="sxs-lookup"><span data-stu-id="62df4-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="62df4-175">We hebben ervoor gekozen het verwijderen van bepaalde beveiliging gevoelige velden, om te voorkomen dat onnodig lekken referentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="62df4-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="62df4-176">Het lijkt onwaarschijnlijk dat API-sleutels en andere referenties zou worden gebruikt voor andere doeleinden analytics.</span><span class="sxs-lookup"><span data-stu-id="62df4-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="62df4-177">Als we willen analyse van de gebruiker en het product ze gebruiken en we kan ophalen die van de `context` object en voeg die toe aan het bericht.</span><span class="sxs-lookup"><span data-stu-id="62df4-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="62df4-178">De metagegevens van het bericht</span><span class="sxs-lookup"><span data-stu-id="62df4-178">Message Metadata</span></span>
<span data-ttu-id="62df4-179">Wanneer u het volledige bericht te verzenden naar de event hub, de eerste regel is niet daadwerkelijk deel uit van de `application/http` bericht.</span><span class="sxs-lookup"><span data-stu-id="62df4-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="62df4-180">De eerste regel zijn aanvullende metagegevens die bestaan uit of het bericht is een aanvraag of antwoordbericht en een bericht-id die wordt gebruikt voor aanvragen voor reacties correleren.</span><span class="sxs-lookup"><span data-stu-id="62df4-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="62df4-181">De bericht-id is gemaakt met behulp van een ander beleid dat op dit lijkt:</span><span class="sxs-lookup"><span data-stu-id="62df4-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="62df4-182">Er kan het aanvraagbericht gemaakt, die in een variabele opgeslagen totdat het antwoord is geretourneerd en gewoon verzend de aanvraag en -antwoord als één bericht.</span><span class="sxs-lookup"><span data-stu-id="62df4-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="62df4-183">Echter, krijgen we verzenden onafhankelijk van de aanvraag en -antwoord en een bericht-id correlaties zichtbaar maken tussen de twee, iets meer flexibiliteit in de berichtgrootte, de mogelijkheid om te profiteren van meerdere partities terwijl het onderhouden van de volgorde van berichten en het verzoek wordt weergegeven in onze logboekregistratie dashboard sneller.</span><span class="sxs-lookup"><span data-stu-id="62df4-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="62df4-184">Ook kan er een aantal scenario's waarbij een geldig antwoord wordt nooit verzonden naar de event hub, mogelijk vanwege een onherstelbare aanvraag-fout in de API Management-service, maar er wordt nog een record van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="62df4-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="62df4-185">Het beleid voor het verzenden van het HTTP-antwoordbericht lijkt erg op de aanvraag en dus de volledige beleidsconfiguratie ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="62df4-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="62df4-186">De `set-variable` beleid maakt een waarde die toegankelijk is voor zowel de `log-to-eventhub` beleid in de `<inbound>` sectie en de `<outbound>` sectie.</span><span class="sxs-lookup"><span data-stu-id="62df4-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="62df4-187">Ontvangen van gebeurtenissen van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62df4-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="62df4-188">Gebeurtenissen van Azure Event Hub worden ontvangen met behulp van de [AMQP-protocol](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="62df4-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="62df4-189">Het Microsoft Service Bus-team aangebracht client bibliotheken beschikbaar om de verbruikende gebeurtenissen te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="62df4-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="62df4-190">Er zijn twee verschillende benaderingen ondersteund, een wordt een *directe Consumer* en de andere maakt gebruik van de `EventProcessorHost` klasse.</span><span class="sxs-lookup"><span data-stu-id="62df4-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="62df4-191">Voorbeelden van deze twee methoden kunnen u vinden in de [Event Hubs-programmeergids](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="62df4-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="62df4-192">Er is de beknopte versie van de verschillen, `Direct Consumer` hebt u volledige controle en de `EventProcessorHost` biedt u enkele van de Loodgieterswerk voor u maar kunt u bepaalde veronderstellingen over hoe u deze gebeurtenissen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="62df4-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="62df4-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="62df4-193">EventProcessorHost</span></span>
<span data-ttu-id="62df4-194">In dit voorbeeld gebruiken we de `EventProcessorHost` voor eenvoud, maar het kan niet de beste keuze voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="62df4-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="62df4-195">`EventProcessorHost`de vaste werkt waarbij wordt gecontroleerd of er problemen binnen een bepaalde gebeurtenis Processorklasse threading bang geen.</span><span class="sxs-lookup"><span data-stu-id="62df4-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="62df4-196">In ons scenario zijn we echter gewoon het bericht converteren naar een andere indeling en deze samen met een andere service door middel van een async-methode wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="62df4-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="62df4-197">Er is niet nodig voor het bijwerken van de gedeelde status en daarom geen risico bestaat dat threading problemen.</span><span class="sxs-lookup"><span data-stu-id="62df4-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="62df4-198">Voor de meeste scenario `EventProcessorHost` is waarschijnlijk de beste keuze en het is gewoon de gemakkelijker optie.</span><span class="sxs-lookup"><span data-stu-id="62df4-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="62df4-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="62df4-199">IEventProcessor</span></span>
<span data-ttu-id="62df4-200">Het centrale concept bij gebruik van `EventProcessorHost` is het maken van een implementatie van de `IEventProcessor` interface de methode bevat `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="62df4-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="62df4-201">De essentie van deze methode wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="62df4-201">The essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="62df4-202">Een lijst met EventData objecten worden doorgegeven aan de methode en we doorlopen die lijst.</span><span class="sxs-lookup"><span data-stu-id="62df4-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="62df4-203">Het aantal bytes van elke methode worden geparseerd naar een object HttpMessage en dat object wordt doorgegeven aan een exemplaar van IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="62df4-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="62df4-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="62df4-204">HttpMessage</span></span>
<span data-ttu-id="62df4-205">De `HttpMessage` -exemplaar bevat drie soorten gegevens:</span><span class="sxs-lookup"><span data-stu-id="62df4-205">The `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="62df4-206">De `HttpMessage` -exemplaar bevat een `MessageId` GUID die kan worden uitgevoerd op de verbinding met de HTTP-aanvragen in het bijbehorende HTTP-antwoord en een Boolean die aangeeft of het object een exemplaar van een HttpRequestMessage en HttpResponseMessage bevat.</span><span class="sxs-lookup"><span data-stu-id="62df4-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="62df4-207">Met behulp van de ingebouwde in HTTP-klassen uit `System.Net.Http`, kon ik om te profiteren van de `application/http` bij het parseren van code die is opgenomen in `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="62df4-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="62df4-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="62df4-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="62df4-209">De `HttpMessage` exemplaar wordt vervolgens doorgestuurd naar de implementatie van `IHttpMessageProcessor` die ik gemaakt voor het loskoppelen van de ontvangen en de interpretatie van de gebeurtenis van Azure Event Hub en de daadwerkelijke verwerking van deze interface is.</span><span class="sxs-lookup"><span data-stu-id="62df4-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="62df4-210">Het HTTP-bericht doorsturen</span><span class="sxs-lookup"><span data-stu-id="62df4-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="62df4-211">Voor dit voorbeeld ik besloten deze zou van belang zijn voor de HTTP-aanvraag via push naar [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="62df4-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="62df4-212">Runscope is een service in de cloud die is gespecialiseerd in HTTP-foutopsporing, logboekregistratie en controle.</span><span class="sxs-lookup"><span data-stu-id="62df4-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="62df4-213">Ze hebben een gratis laag, zodat het gemakkelijk om te proberen en kunt u ons om te zien van de HTTP-aanvragen in realtime stromend door onze API Management-service.</span><span class="sxs-lookup"><span data-stu-id="62df4-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="62df4-214">De `IHttpMessageProcessor` implementatie uitziet,</span><span class="sxs-lookup"><span data-stu-id="62df4-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="62df4-215">Ik heb om te profiteren van een [bestaande-clientbibliotheek voor Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) waarmee u gemakkelijk te pushen `HttpRequestMessage` en `HttpResponseMessage` up bij hun service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="62df4-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="62df4-216">Om te kunnen krijgen tot de API Runscope moet u een account en een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="62df4-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="62df4-217">Instructies voor het ophalen van een API-sleutel kunnen worden gevonden in de [toepassingen maken voor toegang tot Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="62df4-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="62df4-218">Compleet codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="62df4-218">Complete sample</span></span>
<span data-ttu-id="62df4-219">De [broncode](https://github.com/darrelmiller/ApimEventProcessor) en tests voor het voorbeeld op GitHub.</span><span class="sxs-lookup"><span data-stu-id="62df4-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="62df4-220">U moet een [API Management-Service](api-management-get-started.md), [een verbonden Event Hub](api-management-howto-log-event-hubs.md), en een [Opslagaccount](../storage/common/storage-create-storage-account.md) om uit te voeren van het voorbeeld voor uzelf.</span><span class="sxs-lookup"><span data-stu-id="62df4-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="62df4-221">Het voorbeeld is alleen een eenvoudige consoletoepassing die luistert naar gebeurtenissen die afkomstig zijn van de Event Hub, converteert u deze in een `HttpRequestMessage` en `HttpResponseMessage` objecten en stuurt deze door u aan bij de Runscope-API.</span><span class="sxs-lookup"><span data-stu-id="62df4-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="62df4-222">In de volgende animatie afbeelding ziet u een aanvraag wordt aan een API in de Portal voor ontwikkelaars de consoletoepassing met het bericht wordt ontvangen, verwerkt en doorgestuurd en vervolgens de aanvraag en antwoord weergegeven in de inspector Runscope verkeer.</span><span class="sxs-lookup"><span data-stu-id="62df4-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Demonstratie van de aanvraag doorgestuurd naar Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="62df4-224">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="62df4-224">Summary</span></span>
<span data-ttu-id="62df4-225">Azure API Management-service biedt een ideaal plaats voor het vastleggen van de HTTP-verkeer op reis naar en van uw API's.</span><span class="sxs-lookup"><span data-stu-id="62df4-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="62df4-226">Azure Event Hubs is een zeer schaalbaar, voordelige oplossing voor het vastleggen van dat verkeer en die deze naar secundaire verwerkingssystemen voor logboekregistratie, bewaken en andere geavanceerde analyses.</span><span class="sxs-lookup"><span data-stu-id="62df4-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="62df4-227">Verbinding maken met 3e partij verkeer bewaken Runscope is een eenvoudige als een paar dozijn regels code.</span><span class="sxs-lookup"><span data-stu-id="62df4-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62df4-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62df4-228">Next steps</span></span>
* <span data-ttu-id="62df4-229">Meer informatie over Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62df4-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="62df4-230">Aan de slag met Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62df4-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="62df4-231">Berichten ontvangen met EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="62df4-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="62df4-232">Programmeerhandleiding voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62df4-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="62df4-233">Meer informatie over de integratie van API Management en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="62df4-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="62df4-234">Het registreren van gebeurtenissen voor Azure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="62df4-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="62df4-235">Entiteitsverwijzing berichtenlogboek</span><span class="sxs-lookup"><span data-stu-id="62df4-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="62df4-236">documentatie voor logboek-eventhub-beleid</span><span class="sxs-lookup"><span data-stu-id="62df4-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
