---
title: Overzicht van Azure Event Hubs-verificatie en beveiliging model | Microsoft Docs
description: Verificatie en beveiliging model overzicht van Event Hubs.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="b5de1-103">Verificatie en beveiliging model overzicht van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b5de1-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="b5de1-104">Het beveiligingsmodel van Azure Event Hubs voldoet aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="b5de1-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="b5de1-105">Alleen clients die geldige referenties kunnen gegevens verzenden naar een event hub.</span><span class="sxs-lookup"><span data-stu-id="b5de1-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="b5de1-106">Een client kan een andere client niet imiteren.</span><span class="sxs-lookup"><span data-stu-id="b5de1-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="b5de1-107">Een rogue client worden verzenden van gegevens naar een event hub geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="b5de1-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="b5de1-108">Clientverificatie</span><span class="sxs-lookup"><span data-stu-id="b5de1-108">Client authentication</span></span>
<span data-ttu-id="b5de1-109">Het beveiligingsmodel van Event Hubs is gebaseerd op een combinatie van [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens en *gebeurtenisuitgevers*.</span><span class="sxs-lookup"><span data-stu-id="b5de1-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="b5de1-110">Een gebeurtenisuitgever definieert een virtuele-eindpunt voor een event hub.</span><span class="sxs-lookup"><span data-stu-id="b5de1-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="b5de1-111">De uitgever kan alleen worden gebruikt om berichten te verzenden naar een event hub.</span><span class="sxs-lookup"><span data-stu-id="b5de1-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="b5de1-112">Het is niet mogelijk om berichten te ontvangen van een uitgever.</span><span class="sxs-lookup"><span data-stu-id="b5de1-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="b5de1-113">Normaal gesproken een event hub maakt gebruik van een uitgever per client.</span><span class="sxs-lookup"><span data-stu-id="b5de1-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="b5de1-114">Alle berichten die worden verzonden naar een van de uitgevers van een event hub zijn in de wachtrij binnen event hub.</span><span class="sxs-lookup"><span data-stu-id="b5de1-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="b5de1-115">Uitgevers inschakelen verfijnd toegangsbeheer en beperking.</span><span class="sxs-lookup"><span data-stu-id="b5de1-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="b5de1-116">Elke client Event Hubs is een unieke token, dat is geüpload naar de client toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="b5de1-117">De tokens worden geproduceerd, zodat elke unieke token toegang tot een andere unieke uitgever verleent.</span><span class="sxs-lookup"><span data-stu-id="b5de1-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="b5de1-118">Een client die beschikken over een token kan alleen verzenden naar een publisher, maar er is geen andere uitgever.</span><span class="sxs-lookup"><span data-stu-id="b5de1-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="b5de1-119">Als meerdere clients hetzelfde token delen, deelt elk van deze uitgever.</span><span class="sxs-lookup"><span data-stu-id="b5de1-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="b5de1-120">Hoewel niet aanbevolen, is het mogelijk zowel apparaten met tokens die directe toegang tot een event hub verlenen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="b5de1-121">Elk apparaat met dit token verzenden rechtstreeks in de event hub berichten.</span><span class="sxs-lookup"><span data-stu-id="b5de1-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="b5de1-122">Een apparaat kan niet worden onderworpen aan beperking.</span><span class="sxs-lookup"><span data-stu-id="b5de1-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="b5de1-123">Het apparaat kan niet verder worden gebeurd verzenden naar deze event hub.</span><span class="sxs-lookup"><span data-stu-id="b5de1-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="b5de1-124">Alle tokens zijn ondertekend met een SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b5de1-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="b5de1-125">Normaal gesproken zijn alle tokens ondertekend met dezelfde sleutel.</span><span class="sxs-lookup"><span data-stu-id="b5de1-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="b5de1-126">Clients zich niet op de hoogte van de sleutel; Dit voorkomt dat andere clients die produceren van tokens.</span><span class="sxs-lookup"><span data-stu-id="b5de1-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="b5de1-127">De SAS-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="b5de1-127">Create the SAS key</span></span>

<span data-ttu-id="b5de1-128">Bij het maken van een naamruimte Event Hubs, de service een 256-bits SAS-sleutel met de naam genereert **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="b5de1-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="b5de1-129">Deze sleutel verleent verzenden, luisteren en beheer van rechten aan de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="b5de1-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="b5de1-130">U kunt ook aanvullende sleutels maken.</span><span class="sxs-lookup"><span data-stu-id="b5de1-130">You can also create additional keys.</span></span> <span data-ttu-id="b5de1-131">Het is raadzaam het produceren van een sleutel dat verleent machtigingen aan de specifieke event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="b5de1-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="b5de1-132">Voor de rest van dit onderwerp wordt ervan uitgegaan dat u deze sleutel naam **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="b5de1-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="b5de1-133">Het volgende voorbeeld wordt een sleutel verzenden alleen-lezen bij het maken van de event hub:</span><span class="sxs-lookup"><span data-stu-id="b5de1-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="b5de1-134">Genereren van tokens</span><span class="sxs-lookup"><span data-stu-id="b5de1-134">Generate tokens</span></span>

<span data-ttu-id="b5de1-135">U kunt met behulp van de SAS-sleutel tokens genereren.</span><span class="sxs-lookup"><span data-stu-id="b5de1-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="b5de1-136">U moet slechts één token per client wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b5de1-136">You must produce only one token per client.</span></span> <span data-ttu-id="b5de1-137">Tokens kunnen vervolgens worden geproduceerd met behulp van de volgende methode.</span><span class="sxs-lookup"><span data-stu-id="b5de1-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="b5de1-138">Alle tokens worden gegenereerd met de **EventHubSendKey** sleutel.</span><span class="sxs-lookup"><span data-stu-id="b5de1-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="b5de1-139">Elke token is een unieke URI toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="b5de1-140">Wanneer u deze methode aanroept, de URI moet worden opgegeven als `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="b5de1-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="b5de1-141">Voor alle tokens de URI is identiek zijn, met uitzondering van `PUBLISHER_NAME`, die moeten verschillend zijn voor elk token.</span><span class="sxs-lookup"><span data-stu-id="b5de1-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="b5de1-142">In het ideale geval `PUBLISHER_NAME` vertegenwoordigt de ID van de client die de token die ontvangt.</span><span class="sxs-lookup"><span data-stu-id="b5de1-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="b5de1-143">Deze methode genereert een token met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="b5de1-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="b5de1-144">De verlooptijd van de token is opgegeven in seconden van 1 januari 1970.</span><span class="sxs-lookup"><span data-stu-id="b5de1-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="b5de1-145">Hier volgt een voorbeeld van een token:</span><span class="sxs-lookup"><span data-stu-id="b5de1-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="b5de1-146">Normaal gesproken hebben tokens een levensduur die er ongeveer als volgt of hoger is dan de levensduur van de client.</span><span class="sxs-lookup"><span data-stu-id="b5de1-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="b5de1-147">Als de client de mogelijkheid een nieuw token te verkrijgen heeft, kunnen tokens met een kortere levensduur kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5de1-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="b5de1-148">Verzenden van gegevens</span><span class="sxs-lookup"><span data-stu-id="b5de1-148">Sending data</span></span>
<span data-ttu-id="b5de1-149">Zodra de tokens zijn gemaakt, wordt elke client ingericht met een eigen unieke token.</span><span class="sxs-lookup"><span data-stu-id="b5de1-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="b5de1-150">Als de client verzendt de gegevens in een event hub, tags deze de verzendaanvraag met het token.</span><span class="sxs-lookup"><span data-stu-id="b5de1-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="b5de1-151">Om te voorkomen dat een aanvaller inbreuk en stelen van het token, moet de communicatie tussen de client en de event hub plaatsvinden via een versleuteld kanaal.</span><span class="sxs-lookup"><span data-stu-id="b5de1-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="b5de1-152">Beschermde clients</span><span class="sxs-lookup"><span data-stu-id="b5de1-152">Blacklisting clients</span></span>
<span data-ttu-id="b5de1-153">Als een token wordt gestolen door een aanvaller, kan de aanvaller zich voordoen als de client waarvan de token is gestolen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="b5de1-154">Een client beleid wordt gerenderd die client onbruikbaar totdat het een nieuw token die gebruikmaakt van een andere uitgever ontvangt.</span><span class="sxs-lookup"><span data-stu-id="b5de1-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="b5de1-155">Verificatie van de back-end-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b5de1-155">Authentication of back-end applications</span></span>

<span data-ttu-id="b5de1-156">Event Hubs maakt gebruik van een beveiligingsmodel die vergelijkbaar is met het model dat wordt gebruikt voor Service Bus-onderwerpen voor de authenticatie van back-end-toepassingen die de gegevens die worden gegenereerd door de Event Hubs-clients gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5de1-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="b5de1-157">Een consumergroep Event Hubs is gelijk aan een abonnement op een Service Bus-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b5de1-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="b5de1-158">Een client kan een consumergroep maken als de aanvraag voor het maken van de consumergroep gaat vergezeld van een token dat verleent machtigingen voor de event hub, of voor de naamruimte waartoe de event hub behoort beheren.</span><span class="sxs-lookup"><span data-stu-id="b5de1-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="b5de1-159">Een client is toegestaan om gegevens uit een consumergroep gebruiken als de aanvraag ontvangen gaat vergezeld van een token dat verleent rechten ontvangen op consumergroep, de event hub of de naamruimte waartoe de event hub behoort.</span><span class="sxs-lookup"><span data-stu-id="b5de1-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="b5de1-160">De huidige versie van Service Bus biedt SAS regels geen ondersteuning voor afzonderlijke abonnementen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="b5de1-161">Hetzelfde geldt voor Event Hubs consumer-groepen.</span><span class="sxs-lookup"><span data-stu-id="b5de1-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="b5de1-162">SAS-ondersteuning wordt in de toekomst voor beide functies worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b5de1-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="b5de1-163">In het ontbreken van SAS-verificatie voor afzonderlijke consumergroepen kunt u SAS-sleutels gebruiken voor het beveiligen van alle consumergroepen met een gemeenschappelijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="b5de1-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="b5de1-164">Deze aanpak kunt een toepassing gegevens uit een van de consumergroepen van een event hub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b5de1-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5de1-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5de1-165">Next steps</span></span>
<span data-ttu-id="b5de1-166">Voor meer informatie over Event Hubs, gaat u naar de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="b5de1-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="b5de1-167">[Event Hubs-overzicht]</span><span class="sxs-lookup"><span data-stu-id="b5de1-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="b5de1-168">[Overzicht van handtekeningen voor gedeelde toegang]</span><span class="sxs-lookup"><span data-stu-id="b5de1-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="b5de1-169">[Voorbeeldtoepassingen die gebruikmaken van Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="b5de1-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="b5de1-170">[Event Hubs-overzicht]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="b5de1-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="b5de1-171">[Voorbeeldtoepassingen die gebruikmaken van Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="b5de1-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="b5de1-172">[Overzicht van handtekeningen voor gedeelde toegang]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="b5de1-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

