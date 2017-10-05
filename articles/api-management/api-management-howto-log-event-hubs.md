---
title: Het registreren van gebeurtenissen voor Azure Event Hubs in Azure API Management | Microsoft Docs
description: Informatie over het vastleggen van gebeurtenissen in Azure Event Hubs in Azure API Management.
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
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="683fa-103">Het registreren van gebeurtenissen voor Azure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="683fa-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="683fa-104">Azure Event Hubs is een zeer schaalbare service voor inkomende gegevens die miljoenen gebeurtenissen per seconde kan opnemen, voor verwerking en analyse van de enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="683fa-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="683fa-105">Event Hubs fungeert als de 'voordeur' van een gebeurtenispijplijn en zodra gegevens zijn verzameld in een event hub, kunnen worden omgezet en opgeslagen met een realtime-analyseprovider of batchverwerking/opslagadapters.</span><span class="sxs-lookup"><span data-stu-id="683fa-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="683fa-106">Event Hubs koppelt de productie van een gebeurtenissenstroom los van het gebruik van deze gebeurtenissen, zodat de consumenten ervan toegang hebben tot de gebeurtenissen op basis van hun eigen planning.</span><span class="sxs-lookup"><span data-stu-id="683fa-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="683fa-107">Dit artikel is een aanvulling op de [Azure API Management integreren met Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video en wordt beschreven hoe u API Management-gebeurtenissen met Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="683fa-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="683fa-108">Een Azure Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="683fa-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="683fa-109">Voor het maken van nieuwe Event Hub, aanmelding bij de [klassieke Azure-portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Service Bus**->**Event Hub**->**snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="683fa-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="683fa-110">Voer een naam Event Hub, regio, selecteer een abonnement en selecteer een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="683fa-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="683fa-111">Als u nog niet eerder hebt gemaakt met een naamruimte kunt u een door een naam in de **Namespace** textbox.</span><span class="sxs-lookup"><span data-stu-id="683fa-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="683fa-112">Nadat alle eigenschappen zijn geconfigureerd, klikt u op **maken van een nieuwe Event Hub** voor het maken van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="683fa-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Event hub maken][create-event-hub]

<span data-ttu-id="683fa-114">Vervolgens gaat u naar de **configureren** tabblad voor uw nieuwe Event Hub en maak twee **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="683fa-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="683fa-115">De naam van het eerste beheerpunt **verzenden** en hieraan **verzenden** machtigingen.</span><span class="sxs-lookup"><span data-stu-id="683fa-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Verzenden van beleid][sending-policy]

<span data-ttu-id="683fa-117">De naam van de tweede waarde **ontvangen**, geeft u het **luisteren** machtigingen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="683fa-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Beleid ontvangen][receiving-policy]

<span data-ttu-id="683fa-119">Elk gedeeld toegangsbeleid kunt toepassingen voor het verzenden en ontvangen van gebeurtenissen naar en van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="683fa-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="683fa-120">Voor toegang tot de verbindingsreeksen voor dit beleid, gaat u naar de **Dashboard** tabblad van de Event Hub en klik op **verbindingsgegevens**.</span><span class="sxs-lookup"><span data-stu-id="683fa-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Verbindingsreeks][event-hub-dashboard]

<span data-ttu-id="683fa-122">De **verzenden** verbindingsreeks wordt gebruikt bij het vastleggen van gebeurtenissen, en de **ontvangen** verbindingsreeks wordt gebruikt bij het downloaden van gebeurtenissen van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="683fa-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Verbindingsreeks][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="683fa-124">Maken van een API Management-logboek</span><span class="sxs-lookup"><span data-stu-id="683fa-124">Create an API Management logger</span></span>
<span data-ttu-id="683fa-125">Nu dat u een Event Hub hebt, de volgende stap is voor het configureren van een [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in uw API Management-service zodat deze gebeurtenissen in de Event Hub vastleggen kan.</span><span class="sxs-lookup"><span data-stu-id="683fa-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="683fa-126">API Management voorkomen zijn geconfigureerd met behulp van de [API Management REST API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="683fa-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="683fa-127">Controleer voordat u de REST-API voor het eerst gebruikt, de [vereisten](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) en zorg ervoor dat er [toegang tot de REST-API ingeschakeld](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="683fa-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="683fa-128">Controleer een HTTP PUT-aanvraag van de volgende URL-sjabloon voor het maken van een logboek.</span><span class="sxs-lookup"><span data-stu-id="683fa-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="683fa-129">Vervang `{your service}` met de naam van uw API Management-service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="683fa-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="683fa-130">Vervang `{new logger name}` met de gewenste naam voor uw nieuwe berichtenlogboek.</span><span class="sxs-lookup"><span data-stu-id="683fa-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="683fa-131">U verwijst bij het configureren van deze naam de [logboek voor eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) beleid</span><span class="sxs-lookup"><span data-stu-id="683fa-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="683fa-132">De volgende headers toevoegen aan de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="683fa-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="683fa-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="683fa-133">Content-Type : application/json</span></span>
* <span data-ttu-id="683fa-134">Autorisatie: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="683fa-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="683fa-135">Voor instructies voor het genereren van de `SharedAccessSignature` Zie [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="683fa-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="683fa-136">Geef de hoofdtekst van de aanvraag van de volgende sjabloon.</span><span class="sxs-lookup"><span data-stu-id="683fa-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="683fa-137">`type`moet worden ingesteld op `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="683fa-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="683fa-138">`description`biedt een optionele beschrijving van het logboek en tekenreekslengte van nul kan zijn, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="683fa-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="683fa-139">`credentials`bevat de `name` en `connectionString` van uw Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="683fa-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="683fa-140">Wanneer u de aanvraag als een statuscode van is gemaakt door het logboek `201 Created` wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="683fa-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="683fa-141">Zie voor andere mogelijke retourcodes en hun redenen [maken van een logboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="683fa-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="683fa-142">Om te zien hoe andere bewerkingen zoals lijst, bijwerken en verwijderen, Zie de [berichtenlogboek](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entiteit documentatie.</span><span class="sxs-lookup"><span data-stu-id="683fa-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="683fa-143">Logboek-eventhubs-beleid configureren</span><span class="sxs-lookup"><span data-stu-id="683fa-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="683fa-144">Zodra uw berichtenlogboek in API Management is geconfigureerd, kunt u uw logboek-eventhubs-beleid voor de gewenste gebeurtenissen logboekregistratie configureren.</span><span class="sxs-lookup"><span data-stu-id="683fa-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="683fa-145">Het logboek voor eventhubs-beleid kan worden gebruikt in de sectie binnenkomende beleid of de beleidssectie voor uitgaande.</span><span class="sxs-lookup"><span data-stu-id="683fa-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="683fa-146">Voor het configureren van beleidsregels voor aanmelding bij de [Azure-portal](https://portal.azure.com), navigeer naar uw API Management-service en klik op **publicatieportal** voor toegang tot de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="683fa-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Publicatieportal][publisher-portal]

<span data-ttu-id="683fa-148">Klik op **beleid** in het menu API Management aan de linkerkant, selecteer de gewenste product en de API en op **beleid toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="683fa-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="683fa-149">In dit voorbeeld wordt een beleid voor toevoegt de **Echo-API** in de **onbeperkt** product.</span><span class="sxs-lookup"><span data-stu-id="683fa-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Beleid toevoegen][add-policy]

<span data-ttu-id="683fa-151">Plaats de cursor in de `inbound` beleidssectie en klik op de **logboek EventHub** beleid invoegen de `log-to-eventhub` beleidssjabloon-instructie.</span><span class="sxs-lookup"><span data-stu-id="683fa-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Beleidseditor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="683fa-153">Vervang `logger-id` met de naam van het API Management-logboek die u in de vorige stap hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="683fa-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="683fa-154">U kunt een expressie die een tekenreeks retourneert als de waarde voor de `log-to-eventhub` element.</span><span class="sxs-lookup"><span data-stu-id="683fa-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="683fa-155">In dit voorbeeld wordt een tekenreeks met de datum en tijd, servicenaam, aanvraag-id, aanvraag IP-adres en de naam van bewerking geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="683fa-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="683fa-156">Klik op **opslaan** de bijgewerkte beleidsconfiguratie opslaan.</span><span class="sxs-lookup"><span data-stu-id="683fa-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="683fa-157">Het beleid actief is en worden gebeurtenissen vastgelegd op de aangewezen Event Hub zodra deze is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="683fa-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="683fa-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="683fa-158">Next steps</span></span>
* <span data-ttu-id="683fa-159">Meer informatie over Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="683fa-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="683fa-160">Aan de slag met Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="683fa-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="683fa-161">Berichten ontvangen met EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="683fa-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="683fa-162">Programmeerhandleiding voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="683fa-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="683fa-163">Meer informatie over de integratie van API Management en Event Hubs</span><span class="sxs-lookup"><span data-stu-id="683fa-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="683fa-164">Entiteitsverwijzing berichtenlogboek</span><span class="sxs-lookup"><span data-stu-id="683fa-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="683fa-165">documentatie voor logboek-eventhub-beleid</span><span class="sxs-lookup"><span data-stu-id="683fa-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="683fa-166">Uw API's met Azure API Management, Event Hubs en Runscope bewaken</span><span class="sxs-lookup"><span data-stu-id="683fa-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="683fa-167">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="683fa-167">Watch a video walkthrough</span></span>
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
