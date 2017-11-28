---
title: API's met Azure API Management, Event Hubs en Runscope aaaMonitor | Microsoft Docs
description: Voorbeeld van een toepassing demonstreren Hallo logboek-eventhub-beleid door het maken van verbinding Azure API Management, Azure Event Hubs en Runscope voor HTTP-logboekregistratie en controle
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
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="c04f3-103">Uw API's met Azure API Management, Event Hubs en Runscope bewaken</span><span class="sxs-lookup"><span data-stu-id="c04f3-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="c04f3-104">Hallo [API Management-service](api-management-key-concepts.md) biedt veel mogelijkheden tooenhance Hallo verwerking van HTTP-aanvragen dat is verzonden tooyour HTTP-API.</span><span class="sxs-lookup"><span data-stu-id="c04f3-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="c04f3-105">Hallo echter bestaan Hallo aanvragen en antwoorden zijn tijdelijke.</span><span class="sxs-lookup"><span data-stu-id="c04f3-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="c04f3-106">Hallo-aanvraag wordt gedaan en wordt gebruikt door Hallo API Management-service tooyour end-API.</span><span class="sxs-lookup"><span data-stu-id="c04f3-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="c04f3-107">Hallo-aanvraag wordt verwerkt door uw API en een antwoord terug via toohello API consumer loopt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="c04f3-108">Hallo API Management-service houdt een aantal belangrijke statistische gegevens over Hallo API's voor weergave in Hallo Publisher portaldashboard, maar naast, details Hallo zijn verdwenen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="c04f3-109">Met behulp van Hallo [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [beleid](api-management-howto-policies.md) in Hallo API Management-service verzendt u details van de aanvraag en -antwoord tooan hello [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="c04f3-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="c04f3-110">Er zijn diverse redenen waarom u kunt toogenerate gebeurtenissen van HTTP-berichten worden verzonden tooyour API's.</span><span class="sxs-lookup"><span data-stu-id="c04f3-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="c04f3-111">Voorbeelden zijn audittrail van updates, gebruiksanalyse, uitzondering waarschuwingen en 3e integraties van derden.</span><span class="sxs-lookup"><span data-stu-id="c04f3-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="c04f3-112">In dit artikel laat zien hoe toocapture Hallo gehele HTTP-aanvraag en antwoord-bericht verzenden tooan Event Hub en vervolgens relay-bericht tooa van derden service waarmee HTTP-logboekregistratie en controle van services.</span><span class="sxs-lookup"><span data-stu-id="c04f3-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="c04f3-113">Waarom verzenden van API Management-Service?</span><span class="sxs-lookup"><span data-stu-id="c04f3-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="c04f3-114">Het is mogelijk toowrite HTTP middleware waarmee kunt aansluiten op een HTTP-API frameworks toocapture HTTP-aanvragen en antwoorden en ze in logboekregistratie en controle van systemen feed.</span><span class="sxs-lookup"><span data-stu-id="c04f3-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="c04f3-115">Hallo neerwaartse toothis aanpak is Hallo HTTP middleware moet toobe geïntegreerd in Hallo-end-API en platform Hallo Hallo API moet overeenkomen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="c04f3-116">Als er meerdere API's moet elk criterium Hallo middleware implementeren.</span><span class="sxs-lookup"><span data-stu-id="c04f3-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="c04f3-117">Er zijn vaak redenen waarom de back-end voor API's kan niet worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="c04f3-118">Met behulp van hello Azure API Management-service toointegrate met infrastructuur voor logboekregistratie biedt een gecentraliseerd en platformonafhankelijk-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c04f3-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="c04f3-119">Het is ook schaalbare gedeeltelijk vanwege toohello [geo-replicatie](api-management-howto-deploy-multi-region.md) mogelijkheden van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="c04f3-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="c04f3-120">Waarom Azure Event Hub tooan verzenden?</span><span class="sxs-lookup"><span data-stu-id="c04f3-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="c04f3-121">Het is een redelijke tooask, waarom maakt u een beleid dat specifiek tooAzure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="c04f3-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="c04f3-122">Er zijn verschillende plaatsen waar mogelijk wil toolog mijn aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="c04f3-123">Waarom niet gewoon verzenden Hallo-aanvragen rechtstreeks toohello eindbestemming?</span><span class="sxs-lookup"><span data-stu-id="c04f3-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="c04f3-124">Dit is een optie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-124">That is an option.</span></span> <span data-ttu-id="c04f3-125">Wanneer u logboekregistratie van aanvragen van een API management-service, is het echter noodzakelijk tooconsider hoe berichtregistratie heeft invloed op prestaties Hallo Hallo API.</span><span class="sxs-lookup"><span data-stu-id="c04f3-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="c04f3-126">Geleidelijke toename in belasting kunnen worden verwerkt door het verhogen van de beschikbare exemplaren van de onderdelen van het systeem of door gebruik te maken van geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="c04f3-127">Korte pieken in het verkeer kunnen echter leiden tot aanvragen toobe aanzienlijk vertraagd als aanvragen toologging infrastructuur tooslow belast wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c04f3-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="c04f3-128">Hello Azure Event Hubs is ontworpen tooingress grote hoeveelheden gegevens, met capaciteit voor het omgaan met een veel hoger aantal gebeurtenissen dan Hallo aantal HTTP-aanvragen proces voor de meeste API's.</span><span class="sxs-lookup"><span data-stu-id="c04f3-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="c04f3-129">Hallo Event Hub fungeert als een soort geavanceerde buffer tussen uw API management-service en Hallo infrastructuur die wordt opgeslagen en Hallo-berichten verwerken.</span><span class="sxs-lookup"><span data-stu-id="c04f3-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="c04f3-130">Dit zorgt ervoor dat de prestaties van uw API niet vanwege toohello logboekregistratie infrastructuur afnemen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="c04f3-131">Wanneer gegevens Hallo is verstreken tooan Event Hub worden bewaard en wordt gewacht op Event Hub consumenten tooprocess deze.</span><span class="sxs-lookup"><span data-stu-id="c04f3-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="c04f3-132">Hallo Event Hub niets uit hoe deze worden verwerkt, het is net belangrijk ervoor te zorgen dat het Hallo-bericht met succes worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="c04f3-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="c04f3-133">Event Hubs hebben Hallo mogelijkheid toostream gebeurtenissen toomultiple consumer-groepen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="c04f3-134">Hiermee worden gebeurtenissen toobe verwerkt door andere systemen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="c04f3-135">Hierdoor kunnen veel integratiescenario's ondersteunen toevoeging vertragingen zonder op te plaatsen Hallo verwerken van de API-aanvraag Hallo binnen Hallo API Management-service wanneer slechts één gebeurtenis toobe gegenereerd moet.</span><span class="sxs-lookup"><span data-stu-id="c04f3-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="c04f3-136">Een beleid toosend toepassing/HTTP-berichten</span><span class="sxs-lookup"><span data-stu-id="c04f3-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="c04f3-137">Een Event Hub accepteert gebeurtenisgegevens worden opgeslagen als een eenvoudige tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c04f3-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="c04f3-138">Hallo-inhoud van de reeks zijn volledig tooyou.</span><span class="sxs-lookup"><span data-stu-id="c04f3-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="c04f3-139">toobe kunnen toopackage-up maken van een HTTP-aanvraag en uit tooEvent Hubs tooformat Hallo tekenreeks met de aanvraag of antwoord informatie Hallo moet verzenden.</span><span class="sxs-lookup"><span data-stu-id="c04f3-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="c04f3-140">In dit scenario, als er een bestaande opmaak die kan opnieuw worden gebruikt, vervolgens wordt mogelijk geen toowrite ons eigen bij het parseren van code.</span><span class="sxs-lookup"><span data-stu-id="c04f3-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="c04f3-141">In eerste instantie als ik beschouwd met behulp van Hallo [HAR](http://www.softwareishard.com/blog/har-12-spec/) voor het verzenden van HTTP-aanvragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="c04f3-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="c04f3-142">Deze indeling is echter wel geoptimaliseerd voor het opslaan van een reeks van HTTP-aanvragen in een JSON op basis van indeling.</span><span class="sxs-lookup"><span data-stu-id="c04f3-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="c04f3-143">Het bevat een aantal verplichte elementen die onnodige complexiteit voor Hallo scenario Hallo HTTP-bericht om door te geven via de kabel Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="c04f3-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="c04f3-144">Een alternatief is toouse hello `application/http` mediatype zoals beschreven in Hallo HTTP-specificatie [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="c04f3-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="c04f3-145">Dit mediatype gebruikt Hallo exact dezelfde notatie is gebruikte tooactually verzenden HTTP-berichten via de kabel hello, maar de volledige Hallo-bericht in de Hallo hoofdtekst van een andere HTTP-aanvraag kan worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c04f3-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="c04f3-146">In ons geval gaan NET we toouse Hallo instantie als onze bericht toosend tooEvent Hubs.</span><span class="sxs-lookup"><span data-stu-id="c04f3-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="c04f3-147">Gemakkelijk, is er een parser dat voorkomt in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotheken die kunnen parseren deze indeling en deze converteren naar Hallo systeemeigen `HttpRequestMessage` en `HttpResponseMessage` objecten.</span><span class="sxs-lookup"><span data-stu-id="c04f3-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="c04f3-148">toobe kunnen toocreate dit bericht moeten we tootake profiteren van C# [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="c04f3-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="c04f3-149">Hier volgt Hallo-beleid waarmee een HTTP-aanvraag bericht tooAzure Event Hubs wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="c04f3-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="c04f3-150">De declaratie van het beleid</span><span class="sxs-lookup"><span data-stu-id="c04f3-150">Policy declaration</span></span>
<span data-ttu-id="c04f3-151">Er enkele bepaalde zaken opgemerkt over dit beleidsexpressie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="c04f3-152">Hallo-logboek voor eventhub beleid heeft een kenmerk met de naam van logboek-id die verwijst toohello-naam van het logboek dat binnen Hallo API Management-service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="c04f3-153">meer informatie over hoe toosetup een Event Hub berichtenlogboek in Hallo API Management-service kan worden gevonden in Hallo document Hallo [hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="c04f3-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="c04f3-154">Hallo tweede kenmerk is een optionele parameter zodat Event Hubs welke partitie toostore Hallo-bericht in.</span><span class="sxs-lookup"><span data-stu-id="c04f3-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="c04f3-155">Event Hubs partities tooenable schaalbaarheid gebruiken en een minimum van twee vereisen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="c04f3-156">Hallo besteld aflevering van berichten is alleen binnen een partitie gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="c04f3-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="c04f3-157">Als we Event Hub niet in welke partitie tooplace Hallo-bericht opdragen doen, wordt een round robin algoritme toodistribute Hallo belasting gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="c04f3-158">Echter, die mogelijk enkele van onze berichten toobe volgorde worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="c04f3-159">Partities</span><span class="sxs-lookup"><span data-stu-id="c04f3-159">Partitions</span></span>
<span data-ttu-id="c04f3-160">tooensure onze berichten worden tooconsumers op volgorde geleverd en te profiteren van Hallo load distributie mogelijkheid van partities, ik heb gekozen toosend HTTP-aanvraag berichten tooone en HTTP-antwoord berichten tooa tweede partitie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="c04f3-161">Dit zorgt ervoor dat een gelijkmatige verdeling en wij kunnen garanderen dat alle aanvragen worden gebruikt in volgorde en alle antwoorden in volgorde worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="c04f3-162">Het is mogelijk een antwoord toobe geconsumeerd voor het bijbehorende Hallo-aanvraag, maar omdat die niet is een probleem zoals we hebben een ander mechanisme voor het correleren tooresponses vraagt en we weten dat aanvragen altijd voordat antwoorden afkomstig zijn.</span><span class="sxs-lookup"><span data-stu-id="c04f3-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="c04f3-163">HTTP-nettoladingen</span><span class="sxs-lookup"><span data-stu-id="c04f3-163">HTTP payloads</span></span>
<span data-ttu-id="c04f3-164">Na het bouwen van Hallo `requestLine` we toosee controleren als aanvraagtekst Hallo moet worden afgekapt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="c04f3-165">Hallo aanvraagtekst is afgekapt tooonly 1024.</span><span class="sxs-lookup"><span data-stu-id="c04f3-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="c04f3-166">Dit kan worden verhoogd, afzonderlijke Event Hub berichten zijn echter beperkt too256KB, dus is het waarschijnlijk dat bepaalde HTTP-bericht wordt niet in een enkel bericht passen instanties.</span><span class="sxs-lookup"><span data-stu-id="c04f3-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="c04f3-167">Bij het uitvoeren van logboekregistratie en analyse een aanzienlijke hoeveelheid gegevens kunnen worden afgeleid van NET Hallo HTTP-aanvraagregel en -koppen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="c04f3-168">Ook veel API-aanvragen alleen kleine instanties retourneren en dus Hallo verlies van informatie waarde door af te kappen grote organisaties is vrij minimale vergelijking toohello vermindering van overdracht, verwerking en opslag van kosten tookeep alle inhoud.</span><span class="sxs-lookup"><span data-stu-id="c04f3-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="c04f3-169">Een definitieve opmerking over het verwerken van Hallo-instantie is moeten we toopass `true` toohello als<string>()-methode omdat we bij het lezen van de inhoud van hello, maar is ook wilt Hallo-end-API toobe kunnen tooread Hallo hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="c04f3-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="c04f3-170">Door door te geven waar toothis methode hebben we Hallo hoofdtekst toobe gebufferd zodat deze een tweede keer kan worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="c04f3-171">Dit is belangrijk toobe op de hoogte van hebt u een API die geen zeer grote bestanden worden geüpload of lange polling gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="c04f3-172">In deze gevallen zou worden aanbevolen tooavoid Hallo hoofdtekst helemaal lezen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="c04f3-173">HTTP-headers</span><span class="sxs-lookup"><span data-stu-id="c04f3-173">HTTP headers</span></span>
<span data-ttu-id="c04f3-174">HTTP-Headers kunnen eenvoudig worden overgedragen via in Hallo berichtindeling in een eenvoudige sleutel/waarde-paar-indeling.</span><span class="sxs-lookup"><span data-stu-id="c04f3-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="c04f3-175">We hebben ervoor gekozen toostrip uit bepaalde beveiligings-tijdgevoelige velden, tooavoid onnodig lekken referentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="c04f3-176">Het lijkt onwaarschijnlijk dat API-sleutels en andere referenties zou worden gebruikt voor andere doeleinden analytics.</span><span class="sxs-lookup"><span data-stu-id="c04f3-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="c04f3-177">Als we toodo analyse op Hallo gebruiker en Hallo bepaald product wilt ze gebruiken en we die kan verkrijgen van Hallo `context` object en toohello bericht toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="c04f3-178">De metagegevens van het bericht</span><span class="sxs-lookup"><span data-stu-id="c04f3-178">Message Metadata</span></span>
<span data-ttu-id="c04f3-179">Wanneer u Hallo volledige bericht toosend toohello event hub, Hallo eerste regel is niet deel uit van Hallo `application/http` bericht.</span><span class="sxs-lookup"><span data-stu-id="c04f3-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="c04f3-180">de eerste regel Hallo is aanvullende metagegevens die bestaan uit of het Hallo-bericht een aanvraag of antwoord-bericht is en een bericht-id die gebruikt toocorrelate is tooresponses aanvragen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="c04f3-181">Hallo-bericht-id is gemaakt met behulp van een ander beleid dat op dit lijkt:</span><span class="sxs-lookup"><span data-stu-id="c04f3-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="c04f3-182">Er kan Hallo-aanvraagbericht dat in een variabele tot Hallo antwoord is geretourneerd en vervolgens gewoon Hallo-aanvraag en -antwoord als een enkel bericht verzonden opgeslagen gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="c04f3-183">Hallo echter door Hallo-aanvraag en -antwoord onafhankelijk verzenden en het gebruik van een bericht-id toocorrelate twee, er iets meer flexibiliteit bij het Hallo-berichtgrootte, Hallo mogelijkheid tootake profiteren van meerdere partities ophalen terwijl de volgorde van berichten en Hallo behouden blijven aanvraag wordt weergegeven in het dashboard van onze logboekregistratie sneller.</span><span class="sxs-lookup"><span data-stu-id="c04f3-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="c04f3-184">Ook kan er een aantal scenario's waarbij toohello event hub, mogelijk vanwege tooa aanvraag fatale fout in Hallo API Management-service, nooit door een geldig antwoord wordt verzonden, maar we kunnen je wordt nog een record van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c04f3-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="c04f3-185">Hallo beleid toosend Hallo antwoord HTTP-bericht vergelijkbaar toohello aanvraag eruitziet en dus Hallo voltooien beleidsconfiguratie uitziet:</span><span class="sxs-lookup"><span data-stu-id="c04f3-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="c04f3-186">Hallo `set-variable` beleid maakt een waarde die toegankelijk is voor beide Hallo `log-to-eventhub` beleid in Hallo `<inbound>` sectie en Hallo `<outbound>` sectie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="c04f3-187">Ontvangen van gebeurtenissen van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c04f3-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="c04f3-188">Gebeurtenissen van Azure Event Hub worden ontvangen met Hallo [AMQP-protocol](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="c04f3-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="c04f3-189">Hallo Microsoft Service Bus-team aangebracht client bibliotheken beschikbaar toomake Hallo gebeurtenissen gemakkelijker verbruikt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="c04f3-190">Er zijn twee verschillende benaderingen ondersteund, een wordt een *directe Consumer* , en andere Hallo Hallo `EventProcessorHost` klasse.</span><span class="sxs-lookup"><span data-stu-id="c04f3-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="c04f3-191">Voorbeelden van deze twee methoden kunnen u vinden in Hallo [Event Hubs-programmeergids](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c04f3-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="c04f3-192">Hallo verkorte versie van Hallo verschillen is, `Direct Consumer` , hebt u volledige controle en Hallo `EventProcessorHost` biedt een aantal Loodgieterswerk Hallo voor u maar kunt u bepaalde veronderstellingen over hoe u deze gebeurtenissen worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c04f3-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="c04f3-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c04f3-193">EventProcessorHost</span></span>
<span data-ttu-id="c04f3-194">In dit voorbeeld gebruiken we Hallo `EventProcessorHost` voor eenvoud, maar deze kan niet Hallo beste keuze voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="c04f3-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="c04f3-195">`EventProcessorHost`Hallo harde werk waarbij wordt gecontroleerd of er geen tooworry over threading problemen binnen een bepaalde gebeurtenis processor-klasse.</span><span class="sxs-lookup"><span data-stu-id="c04f3-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="c04f3-196">In ons scenario zijn er echter gewoon Hallo tooanother berichtindeling converteren en doorgeeft langs tooanother service met behulp van een async-methode.</span><span class="sxs-lookup"><span data-stu-id="c04f3-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="c04f3-197">Er is niet nodig voor het bijwerken van de gedeelde status en daarom geen risico bestaat dat threading problemen.</span><span class="sxs-lookup"><span data-stu-id="c04f3-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="c04f3-198">Voor de meeste scenario `EventProcessorHost` is waarschijnlijk de beste keuze Hallo en het is gewoon eenvoudiger Hallo-optie.</span><span class="sxs-lookup"><span data-stu-id="c04f3-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="c04f3-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="c04f3-199">IEventProcessor</span></span>
<span data-ttu-id="c04f3-200">Hallo centrale concept bij gebruik van `EventProcessorHost` toocreate is een een implementatie van Hallo `IEventProcessor` interface waarin Hallo methode `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="c04f3-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="c04f3-201">Hallo essentie van deze methode wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="c04f3-201">hello essence of that method is shown here:</span></span>

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

<span data-ttu-id="c04f3-202">Een lijst met EventData objecten worden doorgegeven aan de methode Hallo en we doorlopen die lijst.</span><span class="sxs-lookup"><span data-stu-id="c04f3-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="c04f3-203">Hallo bytes van elke methode worden geparseerd naar een object HttpMessage en dat object tooan exemplaar van IHttpMessageProcessor wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="c04f3-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="c04f3-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="c04f3-204">HttpMessage</span></span>
<span data-ttu-id="c04f3-205">Hallo `HttpMessage` -exemplaar bevat drie soorten gegevens:</span><span class="sxs-lookup"><span data-stu-id="c04f3-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="c04f3-206">Hallo `HttpMessage` -exemplaar bevat een `MessageId` GUID waarmee we tooconnect Hallo HTTP-aanvraag toohello bijbehorende HTTP-antwoord en een Booleaanse waarde die aangeeft of het Hallo-object bevat een exemplaar van een HttpRequestMessage en HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="c04f3-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="c04f3-207">Met behulp van de ingebouwde HTTP-klassen uit Hallo `System.Net.Http`, ik tootake kunnen profiteren van Hallo is `application/http` bij het parseren van code die is opgenomen in `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="c04f3-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="c04f3-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="c04f3-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="c04f3-209">Hallo `HttpMessage` exemplaar wordt vervolgens doorgestuurd tooimplementation van `IHttpMessageProcessor` die ik heb gemaakt toodecouple Hallo ontvangen en interpretatie van Hallo-gebeurtenis uit Azure Event Hub en Hallo daadwerkelijke verwerking van deze interface is.</span><span class="sxs-lookup"><span data-stu-id="c04f3-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="c04f3-210">Doorsturen Hallo HTTP-bericht</span><span class="sxs-lookup"><span data-stu-id="c04f3-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="c04f3-211">Voor dit voorbeeld ik besloten zou zijn interessante toopush Hallo HTTP-aanvraag via te[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="c04f3-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="c04f3-212">Runscope is een service in de cloud die is gespecialiseerd in HTTP-foutopsporing, logboekregistratie en controle.</span><span class="sxs-lookup"><span data-stu-id="c04f3-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="c04f3-213">Ze hebben een gratis laag, dus is het eenvoudig tootry en kunt u ons toosee Hallo HTTP-aanvragen in realtime stromend door onze API Management-service.</span><span class="sxs-lookup"><span data-stu-id="c04f3-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="c04f3-214">Hallo `IHttpMessageProcessor` implementatie uitziet,</span><span class="sxs-lookup"><span data-stu-id="c04f3-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="c04f3-215">Ik was tootake kunnen profiteren van een [bestaande-clientbibliotheek voor Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) kunt dan eenvoudig toopush `HttpRequestMessage` en `HttpResponseMessage` up bij hun service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="c04f3-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="c04f3-216">In volgorde Hallo tooaccess Runscope API moet u een account en een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="c04f3-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="c04f3-217">Instructies voor het ophalen van een API-sleutel kunnen worden gevonden in Hallo [toepassingen maken tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="c04f3-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="c04f3-218">Compleet codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="c04f3-218">Complete sample</span></span>
<span data-ttu-id="c04f3-219">Hallo [broncode](https://github.com/darrelmiller/ApimEventProcessor) en tests voor Hallo voorbeeld op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c04f3-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="c04f3-220">U moet een [API Management-Service](api-management-get-started.md), [een verbonden Event Hub](api-management-howto-log-event-hubs.md), en een [Opslagaccount](../storage/common/storage-create-storage-account.md) toorun Hallo voorbeeld voor uzelf.</span><span class="sxs-lookup"><span data-stu-id="c04f3-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="c04f3-221">Hallo voorbeeld is alleen een eenvoudige consoletoepassing die luistert naar gebeurtenissen die afkomstig zijn van de Event Hub, converteert u deze in een `HttpRequestMessage` en `HttpResponseMessage` objecten en stuurt ze door op toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="c04f3-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="c04f3-222">In Hallo animatie te volgen, ziet u een aanvraag wordt tooan API in Hallo Portal voor ontwikkelaars Hallo Console toepassing waarin Hallo-bericht wordt ontvangen, verwerkt en doorgestuurd en vervolgens Hallo aanvraag en -antwoord weergegeven in de Hallo Runscope verkeer Inspector.</span><span class="sxs-lookup"><span data-stu-id="c04f3-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Demonstratie van de aanvraag doorgestuurd tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="c04f3-224">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="c04f3-224">Summary</span></span>
<span data-ttu-id="c04f3-225">Azure API Management-service biedt een ideaal plaats toocapture Hallo HTTP-verkeer op reis tooand van uw API's.</span><span class="sxs-lookup"><span data-stu-id="c04f3-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="c04f3-226">Azure Event Hubs is een zeer schaalbaar, voordelige oplossing voor het vastleggen van dat verkeer en die deze naar secundaire verwerkingssystemen voor logboekregistratie, bewaken en andere geavanceerde analyses.</span><span class="sxs-lookup"><span data-stu-id="c04f3-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="c04f3-227">Verbinding maken met too3rd partij verkeer bewaken Runscope is een eenvoudige als een paar dozijn regels code.</span><span class="sxs-lookup"><span data-stu-id="c04f3-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c04f3-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c04f3-228">Next steps</span></span>
* <span data-ttu-id="c04f3-229">Meer informatie over Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c04f3-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="c04f3-230">Aan de slag met Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c04f3-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="c04f3-231">Berichten ontvangen met EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c04f3-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="c04f3-232">Programmeerhandleiding voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c04f3-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="c04f3-233">Meer informatie over de integratie van API Management en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="c04f3-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="c04f3-234">Hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c04f3-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="c04f3-235">Entiteitsverwijzing berichtenlogboek</span><span class="sxs-lookup"><span data-stu-id="c04f3-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="c04f3-236">documentatie voor logboek-eventhub-beleid</span><span class="sxs-lookup"><span data-stu-id="c04f3-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
