---
title: aaaOverview van verificatie en model van Azure Event Hubs | Microsoft Docs
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
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="59711-103">Verificatie en beveiliging model overzicht van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="59711-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="59711-104">Hello Azure Event Hubs beveiligingsmodel aan Hallo volgens de vereisten voldoet:</span><span class="sxs-lookup"><span data-stu-id="59711-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="59711-105">Alleen clients die geldige referenties kunnen gegevens tooan event hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="59711-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="59711-106">Een client kan een andere client niet imiteren.</span><span class="sxs-lookup"><span data-stu-id="59711-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="59711-107">Een rogue client worden verzenden van gegevens tooan event hub geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="59711-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="59711-108">Clientverificatie</span><span class="sxs-lookup"><span data-stu-id="59711-108">Client authentication</span></span>
<span data-ttu-id="59711-109">Hallo Event Hubs-beveiligingsmodel is gebaseerd op een combinatie van [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens en *gebeurtenisuitgevers*.</span><span class="sxs-lookup"><span data-stu-id="59711-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="59711-110">Een gebeurtenisuitgever definieert een virtuele-eindpunt voor een event hub.</span><span class="sxs-lookup"><span data-stu-id="59711-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="59711-111">Hallo publisher kan alleen worden gebruikt toosend berichten tooan event hub.</span><span class="sxs-lookup"><span data-stu-id="59711-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="59711-112">Het is niet mogelijk tooreceive berichten van een uitgever.</span><span class="sxs-lookup"><span data-stu-id="59711-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="59711-113">Normaal gesproken een event hub maakt gebruik van een uitgever per client.</span><span class="sxs-lookup"><span data-stu-id="59711-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="59711-114">Alle berichten die tooany met Hallo uitgevers van een event hub worden verzonden zijn in de wachtrij binnen event hub.</span><span class="sxs-lookup"><span data-stu-id="59711-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="59711-115">Uitgevers inschakelen verfijnd toegangsbeheer en beperking.</span><span class="sxs-lookup"><span data-stu-id="59711-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="59711-116">Elke client Event Hubs is een unieke token, dat geüploade toohello client is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="59711-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="59711-117">Hallo-tokens worden geproduceerd, zodat elke unieke token toegang tooa andere unieke uitgever verleent.</span><span class="sxs-lookup"><span data-stu-id="59711-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="59711-118">Een client die beschikken over een token kan alleen tooone publisher, maar er is geen andere uitgever verzenden.</span><span class="sxs-lookup"><span data-stu-id="59711-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="59711-119">Als meerdere clients delen hetzelfde token vervolgens elk van deze Hallo deelt een uitgever.</span><span class="sxs-lookup"><span data-stu-id="59711-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="59711-120">Niet aanbevolen, is maar het mogelijk tooequip apparaten met tokens die directe toegang tooan event hub verlenen.</span><span class="sxs-lookup"><span data-stu-id="59711-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="59711-121">Elk apparaat met dit token verzenden rechtstreeks in de event hub berichten.</span><span class="sxs-lookup"><span data-stu-id="59711-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="59711-122">Dergelijk apparaat geen onderwerp toothrottling worden.</span><span class="sxs-lookup"><span data-stu-id="59711-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="59711-123">Hallo-apparaat kan niet verder worden gebeurd toothat event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="59711-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="59711-124">Alle tokens zijn ondertekend met een SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="59711-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="59711-125">Normaal gesproken alle tokens zijn ondertekend met Hallo dezelfde sleutel.</span><span class="sxs-lookup"><span data-stu-id="59711-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="59711-126">Clients zich niet op de hoogte van de sleutel Hallo; Dit voorkomt dat andere clients die produceren van tokens.</span><span class="sxs-lookup"><span data-stu-id="59711-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="59711-127">Hallo SAS-sleutel maken</span><span class="sxs-lookup"><span data-stu-id="59711-127">Create hello SAS key</span></span>

<span data-ttu-id="59711-128">Bij het maken van een naamruimte Event Hubs Hallo service genereert een 256-bits SAS-sleutel met de naam **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="59711-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="59711-129">Deze sleutel verleent verzenden, luisteren en rechten toohello naamruimte wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="59711-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="59711-130">U kunt ook aanvullende sleutels maken.</span><span class="sxs-lookup"><span data-stu-id="59711-130">You can also create additional keys.</span></span> <span data-ttu-id="59711-131">Het is raadzaam het produceren van een sleutel die verleent machtigingen toohello specifieke event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="59711-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="59711-132">Hallo rest van dit onderwerp, wordt ervan uitgegaan dat u deze sleutel naam **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="59711-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="59711-133">Hallo voorbeeld te volgen, wordt er een sleutel verzenden alleen-lezen gemaakt bij het maken van Hallo event hub:</span><span class="sxs-lookup"><span data-stu-id="59711-133">hello following example creates a send-only key when creating hello event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="59711-134">Genereren van tokens</span><span class="sxs-lookup"><span data-stu-id="59711-134">Generate tokens</span></span>

<span data-ttu-id="59711-135">U kunt tokens met Hallo SAS-sleutel genereren.</span><span class="sxs-lookup"><span data-stu-id="59711-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="59711-136">U moet slechts één token per client wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="59711-136">You must produce only one token per client.</span></span> <span data-ttu-id="59711-137">Tokens kunnen vervolgens worden geproduceerd met behulp van de volgende methode Hallo.</span><span class="sxs-lookup"><span data-stu-id="59711-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="59711-138">Alle tokens worden gegenereerd met behulp van Hallo **EventHubSendKey** sleutel.</span><span class="sxs-lookup"><span data-stu-id="59711-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="59711-139">Elke token is een unieke URI toegewezen.</span><span class="sxs-lookup"><span data-stu-id="59711-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="59711-140">Wanneer u deze methode aanroept, Hallo URI moet worden opgegeven als `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="59711-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="59711-141">Voor alle tokens Hallo URI is identiek zijn, met uitzondering van Hallo `PUBLISHER_NAME`, die moeten verschillend zijn voor elk token.</span><span class="sxs-lookup"><span data-stu-id="59711-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="59711-142">In het ideale geval `PUBLISHER_NAME` vertegenwoordigt Hallo-ID van Hallo-client die de token die ontvangt.</span><span class="sxs-lookup"><span data-stu-id="59711-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="59711-143">Deze methode genereert een token met Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="59711-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="59711-144">Hallo token verlooptijd is in seconden van 1 januari 1970 opgegeven.</span><span class="sxs-lookup"><span data-stu-id="59711-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="59711-145">Hallo Hieronder volgt een voorbeeld van een token:</span><span class="sxs-lookup"><span data-stu-id="59711-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="59711-146">Normaal gesproken hebben Hallo tokens een levensduur die er ongeveer als volgt of Hallo levensduur van de client Hallo overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="59711-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="59711-147">Als Hallo client Hallo mogelijkheid tooobtain een nieuw token, kunnen tokens met een kortere levensduur kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="59711-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="59711-148">Verzenden van gegevens</span><span class="sxs-lookup"><span data-stu-id="59711-148">Sending data</span></span>
<span data-ttu-id="59711-149">Zodra het Hallo-tokens zijn gemaakt, wordt elke client ingericht met een eigen unieke token.</span><span class="sxs-lookup"><span data-stu-id="59711-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="59711-150">Wanneer Hallo-client verzendt de gegevens in een event hub, tags deze de verzendaanvraag met Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="59711-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="59711-151">een aanvaller inbreuk en stelen Hallo-token, Hallo communicatie tussen client hello en Hallo event hub tooprevent moet plaatsvinden via een versleuteld kanaal.</span><span class="sxs-lookup"><span data-stu-id="59711-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="59711-152">Beschermde clients</span><span class="sxs-lookup"><span data-stu-id="59711-152">Blacklisting clients</span></span>
<span data-ttu-id="59711-153">Als een token wordt gestolen door een aanvaller, kan de aanvaller Hallo Hallo client waarvan de token is gestolen imiteren.</span><span class="sxs-lookup"><span data-stu-id="59711-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="59711-154">Een client beleid wordt gerenderd die client onbruikbaar totdat het een nieuw token die gebruikmaakt van een andere uitgever ontvangt.</span><span class="sxs-lookup"><span data-stu-id="59711-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="59711-155">Verificatie van de back-end-toepassingen</span><span class="sxs-lookup"><span data-stu-id="59711-155">Authentication of back-end applications</span></span>

<span data-ttu-id="59711-156">een beveiligingsmodel dat vergelijkbare toohello model dat wordt gebruikt voor Service Bus-onderwerpen worden de veiligheidsmaatregelen tooauthenticate back-end-toepassingen die Hallo gegevens die worden gegenereerd door clients van Event Hubs, Event Hubs gebruiken.</span><span class="sxs-lookup"><span data-stu-id="59711-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="59711-157">Een consumergroep Event Hubs is gelijkwaardig tooa abonnement tooa Service Bus-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="59711-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="59711-158">Een client kan een consumergroep maken als Hallo aanvraag toocreate Hallo-consumergroep gaat vergezeld van een token dat verleent machtigingen voor Hallo event hub kunt beheren, of voor Hallo naamruimte toowhich Hallo event hub behoort.</span><span class="sxs-lookup"><span data-stu-id="59711-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="59711-159">Een client is toegestaan tooconsume gegevens uit een consumergroep als Hallo ontvangt met de aanvraag vergezeld gaat van een token dat verleent rechten op consumergroep ontvangen, hello event hub, of Hallo naamruimte toowhich Hallo event hub behoort.</span><span class="sxs-lookup"><span data-stu-id="59711-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="59711-160">Hallo huidige versie van Service Bus biedt SAS regels geen ondersteuning voor afzonderlijke abonnementen.</span><span class="sxs-lookup"><span data-stu-id="59711-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="59711-161">Hallo die dezelfde voor Event Hubs consumer-groepen geldt.</span><span class="sxs-lookup"><span data-stu-id="59711-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="59711-162">SAS-ondersteuning wordt toegevoegd voor beide functies in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="59711-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="59711-163">Hallo geen SAS-verificatie voor afzonderlijke consumer-groepen, kunt u SAS sleutels toosecure alle consumergroepen met een gemeenschappelijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="59711-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="59711-164">Deze aanpak kunt een toepassing tooconsume-gegevens uit een aantal Hallo consumer-groepen van een event hub.</span><span class="sxs-lookup"><span data-stu-id="59711-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59711-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="59711-165">Next steps</span></span>
<span data-ttu-id="59711-166">toolearn meer informatie over Event Hubs, gaat u naar de volgende onderwerpen Hallo:</span><span class="sxs-lookup"><span data-stu-id="59711-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="59711-167">[Event Hubs-overzicht]</span><span class="sxs-lookup"><span data-stu-id="59711-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="59711-168">[Overzicht van handtekeningen voor gedeelde toegang]</span><span class="sxs-lookup"><span data-stu-id="59711-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="59711-169">[Voorbeeldtoepassingen die gebruikmaken van Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="59711-169">[Sample applications that use Event Hubs]</span></span>

[Event Hubs-overzicht]: event-hubs-what-is-event-hubs.md
[Voorbeeldtoepassingen die gebruikmaken van Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Overzicht van handtekeningen voor gedeelde toegang]: ../service-bus-messaging/service-bus-sas.md

