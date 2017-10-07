---
title: aaaHow toolog gebeurtenissen tooAzure Event Hubs in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="35105-103">Hoe toolog gebeurtenissen tooAzure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="35105-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="35105-104">Azure Event Hubs is een uiterst schaalbare inkomend gegevensservice die miljoenen gebeurtenissen per seconde opnemen kan, zodat u kunt verwerken en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="35105-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="35105-105">Event Hubs fungeert als Hallo 'voordeur' van een gebeurtenispijplijn en zodra gegevens zijn verzameld in een event hub, kunnen worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters.</span><span class="sxs-lookup"><span data-stu-id="35105-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="35105-106">Event Hubs worden losgekoppeld Hallo productie van een stream van gebeurtenissen van Hallo gebruik van deze gebeurtenissen, zodat gebeurtenisconsumers Hallo gebeurtenissen op basis van hun eigen planning kunnen openen.</span><span class="sxs-lookup"><span data-stu-id="35105-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="35105-107">Dit artikel is een aanvullende toohello [Azure API Management integreren met Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video en beschrijft hoe toolog API Management-gebeurtenissen met Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="35105-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="35105-108">Een Azure Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="35105-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="35105-109">een nieuwe Event Hub, aanmelden toohello toocreate [klassieke Azure-portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Service Bus**  -> **Event Hub**->**snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="35105-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="35105-110">Voer een naam Event Hub, regio, selecteer een abonnement en selecteer een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="35105-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="35105-111">Als u nog niet eerder hebt gemaakt met een naamruimte kunt u een door een naam te typen in Hallo **Namespace** textbox.</span><span class="sxs-lookup"><span data-stu-id="35105-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="35105-112">Nadat alle eigenschappen zijn geconfigureerd, klikt u op **maken van een nieuwe Event Hub** toocreate Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="35105-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Event hub maken][create-event-hub]

<span data-ttu-id="35105-114">Vervolgens gaat u toohello **configureren** tabblad voor uw nieuwe Event Hub en maak twee **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="35105-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="35105-115">Naam Hallo eerste **verzenden** en hieraan **verzenden** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="35105-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Verzenden van beleid][sending-policy]

<span data-ttu-id="35105-117">Naam Hallo tweede **ontvangen**, geeft u het **luisteren** machtigingen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="35105-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Beleid ontvangen][receiving-policy]

<span data-ttu-id="35105-119">Elk gedeeld toegangsbeleid kunt toepassingen toosend en tooand gebeurtenissen ontvangen van Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="35105-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="35105-120">tooaccess Hallo-verbindingsreeksen voor deze beleidsregels Navigeer toohello **Dashboard** tabblad Hallo Event Hub en klik op **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="35105-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Verbindingsreeks][event-hub-dashboard]

<span data-ttu-id="35105-122">Hallo **verzenden** verbindingsreeks wordt gebruikt bij het vastleggen van gebeurtenissen, en Hallo **ontvangen** verbindingsreeks wordt gebruikt bij het downloaden van gebeurtenissen van Hallo Event Hub.</span><span class="sxs-lookup"><span data-stu-id="35105-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Verbindingsreeks][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="35105-124">Maken van een API Management-logboek</span><span class="sxs-lookup"><span data-stu-id="35105-124">Create an API Management logger</span></span>
<span data-ttu-id="35105-125">Nu dat u een Event Hub hebt, de volgende stap Hallo tooconfigure is een [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in uw API Management-service zodat deze zich gebeurtenissen toohello Event Hub aanmelden kan.</span><span class="sxs-lookup"><span data-stu-id="35105-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="35105-126">API Management voorkomen zijn geconfigureerd met Hallo [API Management REST API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="35105-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="35105-127">Controleer voordat u Hallo REST-API voor Hallo eerst gebruikt, Hallo [vereisten](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) en zorg ervoor dat er [toegang toohello REST-API ingeschakeld](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="35105-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="35105-128">toocreate een logboek maken een HTTP PUT-aanvraag met Hallo URL sjabloon te volgen.</span><span class="sxs-lookup"><span data-stu-id="35105-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="35105-129">Vervang `{your service}` met Hallo-naam van uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="35105-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="35105-130">Vervang `{new logger name}` met Hallo gewenste naam voor uw nieuwe berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="35105-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="35105-131">U verwijst bij het configureren van Hallo deze naam [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) beleid</span><span class="sxs-lookup"><span data-stu-id="35105-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="35105-132">Hallo na headers toohello aanvraag toevoegen.</span><span class="sxs-lookup"><span data-stu-id="35105-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="35105-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="35105-133">Content-Type : application/json</span></span>
* <span data-ttu-id="35105-134">Autorisatie: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="35105-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="35105-135">Voor instructies voor het genereren van Hallo `SharedAccessSignature` Zie [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="35105-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="35105-136">Hallo aanvraagtekst met behulp van de volgende sjabloon Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="35105-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="35105-137">`type`te moet worden ingesteld`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="35105-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="35105-138">`description`biedt een optionele beschrijving van Hallo berichtenlogboek en tekenreekslengte van nul kan zijn, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="35105-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="35105-139">`credentials`Hallo bevat `name` en `connectionString` van uw Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="35105-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="35105-140">Wanneer u indienen hello, als Hallo berichtenlogboek statuscode is gemaakt `201 Created` wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="35105-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="35105-141">Zie voor andere mogelijke retourcodes en hun redenen [maken van een logboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="35105-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="35105-142">andere bewerkingen toosee hoe uitvoeren, zoals de lijst, bijwerken en verwijderen, Zie Hallo [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entiteit documentatie.</span><span class="sxs-lookup"><span data-stu-id="35105-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="35105-143">Logboek-eventhubs-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="35105-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="35105-144">Nadat uw berichtenlogboek in API Management is geconfigureerd, kunt u uw logboek-eventhubs-beleid toolog Hallo gewenst gebeurtenissen configureren.</span><span class="sxs-lookup"><span data-stu-id="35105-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="35105-145">Hallo logboek-eventhubs-beleid kan worden gebruikt in beide Hallo binnenkomende of beleidssectie Hallo uitgaande beleid.</span><span class="sxs-lookup"><span data-stu-id="35105-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="35105-146">beleid voor tooconfigure aanmelden toohello [Azure-portal](https://portal.azure.com), gaat u tooyour API Management-service en klik op **publicatieportal** tooaccess Hallo publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="35105-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Publicatieportal][publisher-portal]

<span data-ttu-id="35105-148">Klik op **beleid** Selecteer de gewenste product Hallo en API Hallo API Management-menu op Hallo links, en klik op **beleid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="35105-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="35105-149">In dit voorbeeld wordt bij het toevoegen van een beleid toohello **Echo-API** in Hallo **onbeperkt** product.</span><span class="sxs-lookup"><span data-stu-id="35105-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Beleid toevoegen][add-policy]

<span data-ttu-id="35105-151">Plaats de cursor in Hallo `inbound` beleid sectie en klikt u op Hallo **logboek tooEventHub** beleid tooinsert hello `log-to-eventhub` beleidssjabloon-instructie.</span><span class="sxs-lookup"><span data-stu-id="35105-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Beleidseditor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="35105-153">Vervang `logger-id` met de naam van Hallo API Management berichtenlogboek die u hebt geconfigureerd in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="35105-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="35105-154">U kunt een expressie die een tekenreeks als waarde voor Hallo Hallo retourneert `log-to-eventhub` element.</span><span class="sxs-lookup"><span data-stu-id="35105-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="35105-155">In dit voorbeeld is een tekenreeks met Hallo datum en tijd, servicenaam, aanvraag-id, aanvraag IP-adres en naam van de bewerking wordt vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="35105-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="35105-156">Klik op **opslaan** toosave Hallo beleidsconfiguratie bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="35105-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="35105-157">Zodra deze is opgeslagen Hallo beleid actief is en gebeurtenissen worden vastgelegd toohello aangewezen Event Hub.</span><span class="sxs-lookup"><span data-stu-id="35105-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35105-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="35105-158">Next steps</span></span>
* <span data-ttu-id="35105-159">Meer informatie over Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="35105-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="35105-160">Aan de slag met Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="35105-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="35105-161">Berichten ontvangen met EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="35105-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="35105-162">Programmeerhandleiding voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="35105-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="35105-163">Meer informatie over de integratie van API Management en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="35105-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="35105-164">Entiteitsverwijzing berichtenlogboek</span><span class="sxs-lookup"><span data-stu-id="35105-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="35105-165">documentatie voor logboek-eventhub-beleid</span><span class="sxs-lookup"><span data-stu-id="35105-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="35105-166">Uw API's met Azure API Management, Event Hubs en Runscope bewaken</span><span class="sxs-lookup"><span data-stu-id="35105-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="35105-167">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="35105-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
